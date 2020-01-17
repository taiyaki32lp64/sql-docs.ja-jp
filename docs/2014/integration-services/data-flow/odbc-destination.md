---
title: ODBC 入力先 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcdest.f1
ms.assetid: bffa63e0-c737-4b54-b4ea-495a400ffcf8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9de91ba98533e82fbf63376ed6d9c56ad73a000c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771028"
---
# <a name="odbc-destination"></a>ODBC 入力先
  ODBC 入力先は、ODBC でサポートされているデータベース テーブルにデータを一括で読み込みます。 ODBC 入力先は ODBC 接続マネージャーを使用してデータ ソースに接続します。  
  
 ODBC 入力先には、入力列と入力先データ ソースの列との間のマッピングが含まれています。 入力列をすべての入力先列にマップする必要はありませんが、入力先列のプロパティによっては、入力先列にマップされる入力列がない場合、エラーが発生することがあります。 たとえば、入力先列で NULL 値が許容されていない場合は、入力列をその列にマップする必要があります。 また、さまざまな種類の列をマッピングできますが、入力データと入力先の列の型との間に互換性がない場合は、実行時にエラーが発生します。 エラー動作設定に応じて、エラーが無視されるか、エラーが発生するか、エラー出力に行が送信されます。  
  
 ODBC 入力先には、1 つの標準出力と 1 つのエラー出力があります。  
  
##  <a name="BKMK_odbcdestination_loadoptions"></a> 読み込みオプション  
 ODBC 入力先先は、2 つのアクセス読み込みモジュールのうちどちらかを使用できます。 [ODBC ソース エディター &#40;[接続マネージャー] ページ&#41;](../odbc-source-editor-connection-manager-page.md)。 次の 2 つのモードがあります。  
  
-   **バッチ**: このモードでは、ODBC 入力先は、把握した ODBC プロバイダーの機能に基づいて、最も効率的な挿入方法を使用します。 最新の ODBC プロバイダーの場合、これは、パラメーターを設定した INSERT ステートメントを準備し、行方向の配列パラメーター バインドを使用する方法です (このとき、配列のサイズは **BatchSize** プロパティによって制御します)。 **[バッチ]** を選択したが、この方法がプロバイダーでサポートされていない場合、ODBC 入力先は自動的に **[行ごと]** モードに切り替わります。  
  
-   **行ごと**: このモードでは、ODBC 入力先はパラメーターを設定した INSERT ステートメントを準備し、**SQL の Execute** を使用して一度に 1 行ずつ行を挿入します。  
  
## <a name="error-handling"></a>エラー処理  
 ODBC 入力先にはエラー出力があります。 コンポーネントのエラー出力には、次の出力列があります。  
  
-   **エラー コード**: 現在のエラーに対応する数字です。 エラーの一覧については、ソース データベースのドキュメントを参照してください。 SSIS エラー コードの一覧については、「SSIS のエラー コードおよびメッセージ リファレンス」を参照してください。  
  
-   **エラー列**: (変換エラーの) エラーの原因となるソース列。  
  
-   標準出力データ列。  
  
 ODBC 入力先は、エラー動作の設定に応じて、抽出処理中に発生したエラー (データ変換、切り捨て) をエラー出力に返します。 詳細については、「[CDC ソース エディター &#40;[エラー出力] ページ&#41;](../odbc-source-editor-error-output-page.md)」を参照してください。  
  
## <a name="parallelism"></a>並列処理  
 並列実行できる ODBC 入力先コンポーネントの数に制限はありません。これは、同一テーブル上にある場合または異なるテーブル上にある場合、同一コンピューター上で実行する場合または異なるコンピューター上で実行する場合のいずれにも該当します (ただし、通常のグローバルなセッション制限を除きます)。  
  
 ただし、使用する ODBC プロバイダーの制限によって、プロバイダーを介するコンカレント接続数が制限される場合があります。 これらの制限によって、ODBC 入力先で使用できる並列インスタンス数のサポートが制限されます。 SSIS プロバイダーは、使用される ODBC プロバイダーの制限を把握し、SSIS パッケージを作成する際に考慮する必要があります。  
  
 また、同一テーブルへの同時読み込みの場合、標準のレコード ロックのためにパフォーマンスが低下することがある点についても理解しておく必要があります。 これは、読み込まれているデータとテーブルの編成によって異なります。  
  
## <a name="troubleshooting-the-odbc-destination"></a>ODBC 入力先のトラブルシューティング  
 ODBC 入力元による外部データ プロバイダーの呼び出しをログに記録できます。 このログ機能を使用すると、ODBC 入力先による外部データ ソースへのデータ保存に関するトラブルシューティングを行うことができます。 ODBC 入力先による外部データ プロバイダーの呼び出しをログに記録するには、ODBC ドライバー マネージャーによるトレースを有効にします。 詳細については、「 *ODBC で ODBC トレースを生成する方法 (データ ソース管理者向け)* 」 の Microsoft のドキュメントを参照してください。  
  
## <a name="configuring-the-odbc-destination"></a>ODBC 入力先の構成  
 ODBC 入力先は、プログラムによって、または SSIS デザイナーを使用して構成できます。  
  
 詳細については、次のいずれかのトピックを参照してください。  
  
-   [ODBC 変換先エディター &#40;[接続マネージャー] ページ&#41;](../odbc-destination-editor-connection-manager-page.md)  
  
-   [ODBC 変換先エディター &#40;[マッピング] ページ&#41;](../odbc-destination-editor-mappings-page.md)  
  
-   [ODBC 変換先エディター &#40;[エラー出力] ページ&#41;](../odbc-destination-editor-error-output-page.md)  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが表示されます。  
  
 **[詳細エディター]** ダイアログ ボックスを開くには、次の操作を実行します。  
  
-   **プロジェクトの** [データ フロー] [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 画面で、ODBC 入力先を右クリックし、 **[詳細エディターの表示]** をクリックします。  
  
 [詳細エディター] ダイアログ ボックスで設定できるプロパティの詳細については、「 [ODBC 入力先のカスタム プロパティ](odbc-destination-custom-properties.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [ODBC 変換先エディター &#40;[エラー出力] ページ&#41;](../odbc-destination-editor-error-output-page.md)  
  
-   [ODBC 変換先エディター &#40;[マッピング] ページ&#41;](../odbc-destination-editor-mappings-page.md)  
  
-   [ODBC 変換先エディター &#40;[接続マネージャー] ページ&#41;](../odbc-destination-editor-connection-manager-page.md)  
  
-   [ODBC 入力先を使用したデータ読み込み](odbc-destination.md)  
  
-   [ODBC 入力先のカスタム プロパティ](odbc-destination-custom-properties.md)  
  
  
