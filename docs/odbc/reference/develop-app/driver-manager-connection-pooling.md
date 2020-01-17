---
title: ドライバー マネージャーの接続プール |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- pooled connections [ODBC]
- connecting to driver [ODBC], connection pooling
- connecting to data source [ODBC], connection pooling
ms.assetid: ee95ffdb-5aa1-49a3-beb2-7695b27c3df9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 92aab28274d3709047e46c55192b437449e252ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047013"
---
# <a name="driver-manager-connection-pooling"></a>ドライバー マネージャーの接続プール
接続プールが使用するたびに再確立されている必要がない接続プールからの接続を使用するアプリケーションを有効にします。 接続が作成され、プール内に配置されている、アプリケーションは、完全な接続プロセスを実行せず、その接続を再利用できます。  
  
 プールされた接続を使用すると、アプリケーションへの接続に関連するオーバーヘッドを保存できるために大幅なパフォーマンスの向上が発生することができます。 ネットワーク経由で接続する中間層アプリケーションや接続し、切断しても、インターネット アプリケーションなどを繰り返し行うアプリケーションの特に重要なことができます。  
  
 パフォーマンスの向上だけでなく、接続プールのアーキテクチャは、環境と関連付けられている 1 つのプロセスで複数のコンポーネントで使用される接続を使用できます。 これは、相互を意識することがなく同じプロセス内でスタンドアロンのコンポーネントを相互作用できることを意味します。 接続プール内の接続は、複数のコンポーネントで繰り返し使用できます。  
  
> [!NOTE]
>  接続プールは、ODBC 2、ODBC アプリケーションで使用できます。*x*動作では、アプリケーションを呼び出している限り*SQLSetEnvAttr*します。 アプリケーションがデータベースまたは変更するなど、データベースのコンテキストを変更する SQL ステートメントを実行する必要がありますされません接続プールを使用する場合、 \<*データベース名*>、データによって使用されるカタログを変更します。ソース。  


 ODBC ドライバーは完全スレッド セーフである必要があり、接続が接続プールをサポートするためにスレッド アフィニティを必要ありません。 つまり、ドライバーが、いつでも任意のスレッドで呼び出しを処理することが、別のスレッドで、接続を使用して、3 番目のスレッドで切断する 1 つのスレッドで接続できます。  
  
 ドライバー マネージャーによって、接続プールが維持されます。 アプリケーションを呼び出すとき、プールからの接続が描画される**SQLConnect**または**SQLDriverConnect**アプリケーションを呼び出すときに、プールに返される**SQLDisconnect**. 要求されたリソースの割り当てに基づいて、動的にプールのサイズが大きくなります。 非アクティブ タイムアウトに基づいてを縮小します。接続が一定期間 (それが使用されていない接続で) 非アクティブは、プールから削除されます。 プールのサイズは、メモリの制約と、サーバー上の制限によってのみ制限されます。  
  
 ドライバー マネージャーは、渡された引数に従って、プール内の特定の接続を使用する必要があるかどうかを決定します**SQLConnect**または**SQLDriverConnect**、および接続属性に従って。接続が割り当てられた後に設定します。  
  
 ドライバー マネージャーは、接続をプールは、接続が接続を渡す前に引き続き機能しているかを判別できるその必要があります。 それ以外の場合、ドライバー マネージャーを保持での配布対象アプリケーションへの接続を配信不能、一時的なネットワーク障害が発生するたびにします。 ODBC 3 で新しい接続属性が定義されて *.x*:SQL_ATTR_CONNECTION_DEAD します。 これは SQL_CD_TRUE または SQL_CD_FALSE のいずれかを返す読み取り専用の接続属性です。 SQL_CD_TRUE 値では、接続が失われたこと、SQL_CD_FALSE 値により、接続がまだアクティブであるが、一方を意味します。 (以前のバージョンの ODBC に準拠したドライバーは、この属性をサポートできますも)。  
  
 ドライバーでは、このオプションを効率的に実装する必要があります。 または接続プールのパフォーマンスが品質が低下します。 具体的には、この接続属性を取得する呼び出しでは、サーバーへのラウンド トリップが発生する必要があります。 代わりに、ドライバーは、接続の最後の既知の状態を返すだけする必要があります。 サーバーへの最後のトリップが失敗した場合は消滅して最後のトリップが成功した場合にいない配信不能の接続です。  
  
## <a name="remarks"></a>コメント  
 接続が失われました (SQL_ATTR_CONNECTION_DEAD を使用して報告されます)、ODBC ドライバー マネージャーは、ドライバーで SQLDisconnect を呼び出すことによってその接続が破棄されます。 新しい接続要求がプールで使用可能な接続が見つかりません。 最終的に、ドライバー マネージャーことは、新しい接続をプールが空であると仮定します。  
  
 接続プールを使用するには、アプリケーションは、次の手順を実行します。  
  
1.  により、接続プールを呼び出して**SQLSetEnvAttr** SQL_CP_ONE_PER_DRIVER または SQL_CP_ONE_PER_HENV SQL_ATTR_CONNECTION_POOLING 環境属性を設定します。 アプリケーションを有効にする接続プールは共有環境を割り当てる前に、この呼び出しを実行する必要があります。 呼び出しで環境ハンドル**SQLSetEnvAttr** SQL_ATTR_CONNECTION_POOLING プロセス レベルの属性は、null に設定する必要があります。 属性が SQL_CP_ONE_PER_DRIVER に設定されている場合は、ドライバーごとに 1 つの接続プールがサポートされています。 アプリケーションは、ドライバーの多くといくつかの環境で動作する場合がありますより効率的な少なく比較する必要。 SQL_CP_ONE_PER_HENV、1 つの接続プールに設定が各環境をサポート場合します。 アプリケーションは、多くの環境およびいくつかのドライバーで動作する場合がありますより効率的な少なく比較する必要。 SQL_CP_OFF SQL_ATTR_CONNECTION_POOLING に設定して、接続プールを無効になっています。  
  
2.  呼び出すことによって、環境を割り当てる**SQLAllocHandle**で、 *HandleType*を SQL_HANDLE_ENV 引数を設定します。 接続プールが有効になっているために、この呼び出しによって割り当てられた環境は暗黙の共有環境になります。 使用する環境が決定されないまで、ただし**SQLAllocHandle**で、 *HandleType* sql_handle_dbc としてがこの環境で呼び出されます。  
  
3.  呼び出して接続を割り当てる**SQLAllocHandle**で*InputHandle* sql_handle_dbc としてに設定し、 *InputHandle*に割り当てられた環境ハンドルに設定接続がプールされます。 ドライバー マネージャーは、アプリケーションによって設定された環境属性に一致する既存の環境を検索しようとします。 このような環境が存在しない場合 1 つと、作成されます (ドライバー マネージャーによって保持される) 1 の参照カウントします。 一致する共有環境が見つかった場合は、環境は、アプリケーションに返され、参照カウントがインクリメントされます。 (使用する実際の接続をドライバー マネージャーによってまでを判断できない**SQLConnect**または**SQLDriverConnect**が呼び出されます)。  
  
4.  呼び出し**SQLConnect**または**SQLDriverConnect**接続を作成します。 ドライバー マネージャーへの呼び出しで、接続オプションを使用して**SQLConnect** (またはへの呼び出しで接続キーワード**SQLDriverConnect**) への接続の割り当て後に、接続属性の設定プールの接続を使用する必要がありますを決定します。  
  
    > [!NOTE]  
    >  要求された接続が照合されているプールされた接続する方法については、SQL_ATTR_CP_MATCH 環境属性によって決まります。 詳細については、次を参照してください。 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)します。  
  
     接続プールを使用する ODBC アプリケーションで呼び出す必要があります[CoInitializeEx](https://go.microsoft.com/fwlink/?LinkID=116307)アプリケーションの初期化中に、 [CoUninitialize](https://go.microsoft.com/fwlink/?LinkId=116310)アプリケーションの終了します。  
  
5.  呼び出し**SQLDisconnect**接続を完了します。 接続では、接続プールに返され、再利用できるようになります。  
  
 詳細については、次を参照してください。 [、Microsoft Data Access Components のプーリング](https://go.microsoft.com/fwlink/?LinkId=120776)します。  
  
## <a name="connection-pooling-considerations"></a>接続プールの考慮事項  
 SQL コマンドを使用して、次の操作 (ではなくの ODBC API を使用) のいずれかを実行の接続の状態に影響を与えるし、接続プールがアクティブなときに予期しない問題が発生することができます。  
  
-   接続を開き、既定のデータベースを変更します。  
  
-   SET ステートメントを使用して、構成可能なオプション (SET ROWCOUNT、ANSI_、IMPLICIT_TRANSACTIONS、実行プラン、統計、TEXTSIZE、および DATEFORMAT を含む) を変更します。  
  
-   一時テーブルとストアド プロシージャを作成します。  
  
 ODBC API の外部でこれらのアクションのいずれかが実行される場合、接続を使用する次のユーザーは以前の設定、テーブル、またはプロシージャを自動的に継承します。  
  
> [!NOTE]  
>  接続状態にある特定の設定を望んでいません。 常に、アプリケーションで接続状態を設定し、アプリケーションが使用されていない接続プール設定を削除することを確認する必要があります。  
  
## <a name="driver-aware-connection-pooling"></a>ドライバー対応接続プール  
 以降 Windows 8 では、ODBC ドライバーできます接続プールでより効率的に使用します。 詳細については、次を参照してください。[ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)します。  
  
## <a name="see-also"></a>参照  
 [データ ソースまたはドライバー](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft データ アクセス コンポーネントでのプール](https://go.microsoft.com/fwlink/?LinkId=120776)
