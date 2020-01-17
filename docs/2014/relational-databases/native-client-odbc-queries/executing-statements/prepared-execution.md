---
title: 準備の実行 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- deferred statement preparation
- prepared execution [ODBC]
- SQLPrepare function
- ODBC applications, statements
- SQLExecute function
- statements [ODBC], prepared execution
ms.assetid: f3a9d32b-6cd7-4f0c-b38d-c8ccc4ee40c3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01982222ba5a18086aeadbbec776cba222f0e235
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207049"
---
# <a name="prepared-execution"></a>準備実行
  ODBC API では、準備実行とは、[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを繰り返し実行する際に関連して生じる解析やコンパイルのオーバーヘッドを削減する方法と定義されています。 アプリケーションでは SQL ステートメントを保持する文字列を構築してから、そのステートメントを 2 段階に分けて実行します。 呼び出す[SQLPrepare 関数](https://go.microsoft.com/fwlink/?LinkId=59360)ステートメントが解析され、コンパイルして実行プランに 1 回、[!INCLUDE[ssDE](../../../includes/ssde-md.md)]します。 呼び出して**SQLExecute**準備された実行プランの実行のたびにします。 この方法では、各実行にかかる解析とコンパイルのオーバーヘッドが抑制されます。 準備実行は、通常、同一のパラメーター化された SQL ステートメントを繰り返し実行するアプリケーションで使用されます。  
  
 ほとんどのデータベースでは、直接実行されるステートメントが実行のたびにコンパイルされるのに対し、準備実行されるステートメントは 1 回だけコンパイルされるので、準備実行は主に 4、5 回以上実行されるステートメントの場合は直接実行よりも高速になります。 準備実行では、SQL ステートメントが実行されるたびに、ドライバーはステートメント全体ではなく、実行プランの識別子とパラメーター値だけをデータ ソースに送信できるので、ネットワーク トラフィックも削減できます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] パフォーマンスの差異を検出して、実行プランを再利用するアルゴリズムが強化されたダイレクトおよび準備された実行が少なくなります**SQLExecDirect**します。 そのため、直接実行されるステートメントでも、準備実行のパフォーマンス上の利点の一部を利用できるようになります。 詳細については、次を参照してください。[を直接実行](direct-execution.md)します。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、準備実行がネイティブにサポートされます。 実行プランが上に構築された**SQLPrepare**し、後で実行すると実行に**SQLExecute**が呼び出されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]一時ストアド プロシージャを構築する必要はありません**SQLPrepare**、内のシステム テーブルに余分なオーバーヘッドがない**tempdb**します。  
  
 パフォーマンス上の理由から、まで、ステートメントの準備が遅延**SQLExecute**と呼びますか、メタプロパティ操作 (など[SQLDescribeCol](../../native-client-odbc-api/sqldescribecol.md)または[SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md)ODBC の) が実行されます。 これは既定の動作です。 準備されているステートメントのエラーは、ステートメントまたはメタプロパティ操作が実行されるまでわかりません。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバー固有のステートメント属性の SQL_SOPT_SS_DEFER_PREPARE を SQL_DP_OFF に設定することで、この既定の動作を無効にできます。  
  
 場合に遅延を準備する、いずれかの呼び出し**SQLDescribeCol**または**SQLDescribeParam**呼び出す前に**SQLExecute**サーバーに余分なラウンド トリップが生成されます。 **SQLDescribeCol**ドライバーは、クエリから WHERE 句を削除し、クエリによって返される最初の結果セット内の列の説明を取得する SET FMTONLY ON を使用して、サーバーに送信します。 **SQLDescribeParam**ドライバーは、式またはクエリ内のすべてのパラメーター マーカーによって参照される列の説明を取得するサーバーを呼び出します。 この方法には、サブクエリのパラメーターを解決することができないなど、いくつか制限事項もあります。  
  
 使用、余分な**SQLPrepare**で、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]以前のバージョンの SQL Server に接続されている場合は特に Native Client ODBC ドライバーによりパフォーマンスが低下します。 準備実行は、1 回しか実行されないステートメントには使用しないでください。 準備実行では、クライアントからサーバーへのネットワーク上のやり取りを余分に実行する必要があるため、ステートメントを 1 回しか実行しない場合は直接実行よりも時間がかかります。 以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、準備実行で一時ストアド プロシージャの生成も行います。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、準備されたステートメントを使用して一時オブジェクトを作成することはできません。  
  
 使用されるいくつかの以前の ODBC アプリケーション**SQLPrepare**いつ[SQLBindParameter](../../native-client-odbc-api/sqlbindparameter.md)が使用されました。 **SQLBindParameter**の使用が必要としない**SQLPrepare**で使える**SQLExecDirect**します。 たとえば、使用して**SQLExecDirect**で**SQLBindParameter**リターン コードを取得または出力が 1 回しか実行するストアド プロシージャからパラメーターを。 使用しないでください**SQLPrepare**で**SQLBindParameter**しない限り、同じステートメントが複数回実行します。  
  
## <a name="see-also"></a>参照  
 [ステートメントを実行する&#40;ODBC&#41;](executing-statements-odbc.md)  
  
  
