---
title: 結果の処理 (ODBC) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], about result sets
- SQLRowCount function
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- COMPUTE clause
- result sets [ODBC]
- COMPUTE BY clause
ms.assetid: 61a8db19-6571-47dd-84e8-fcc97cb60b45
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cb490ab23d146dc8131c16e22b0d63f07b79d482
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207042"
---
# <a name="processing-results-odbc"></a>結果の処理 (ODBC)
  アプリケーションで SQL ステートメントが実行されると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では結果として生成されるすべてのデータを 1 つ以上の結果セットとして返します。 結果セットとは、クエリの条件に一致する行と列の集まりです。 SELECT ステートメント、カタログ関数、および一部のストアド プロシージャでは、アプリケーションで使用できる結果セットが表形式で生成されます。 実行される SQL ステートメントがストアド プロシージャ、複数のコマンドを含むバッチ、またはキーワードを含む SELECT ステートメントの場合、処理対象の結果セットが複数生成されます。  
  
 ODBC カタログ関数では、データを取得することもできます。 たとえば、 [SQLColumns](../native-client-odbc-api/sqlcolumns.md)データ ソース内の列に関するデータを取得します。 これらの結果セットには、0 行以上の行を含めることができます。  
  
 GRANT や REVOKE など、結果セットが返されない SQL ステートメントもあります。 これらのステートメントの戻り値のコードから**SQLExecute**または**SQLExecDirect**は通常、ステートメントの唯一の目印が成功しました。  
  
 INSERT ステートメント、UPDATE ステートメント、および DELETE ステートメントからは、変更によって処理された行数だけを含む結果セットが返されます。 この数は、アプリケーションがあるときに使用できる呼び出しを行っては[SQLRowCount](../native-client-odbc-api/sqlrowcount.md)します。 ODBC 3。*x*アプリケーションには、いずれかの呼び出しが必要があります**SQLRowCount**結果を取得するには設定または[SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md)を取り消してください。 使用して、各変更ステートメントの結果セットを処理する必要があります、バッチまたはストアド プロシージャの複数の INSERT、UPDATE、または DELETE ステートメントを含む、アプリケーションの実行時に**SQLRowCount** を使用して取り消すまたは**SQLMoreResults**します。 バッチやストアド プロシージャに SET NOCOUNT ON ステートメントを含めることで、これらの数をキャンセルできます。  
  
 Transact-SQL には、NOCOUNT ステートメントが含まれています。 SQL Server では、ステートメントによって影響を受ける行のカウントは返されません NOCOUNT オプションに設定されている場合と**SQLRowCount** 0 を返します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのバージョン、ドライバー固有の紹介[SQLGetStmtAttr](../native-client-odbc-api/sqlgetstmtattr.md)オプションとして SQL_SOPT_SS_NOCOUNT_STATUS、NOCOUNT オプションがオンかオフかどうかを報告します。 いつでも**SQLRowCount**返します 0 の場合、アプリケーションで SQL_SOPT_SS_NOCOUNT_STATUS をテストする必要があります。 SQL_NC_ON が返されますかどうか、値が 0 から**SQLRowCount**のみ SQL Server では、行の数が返されないことを示します。 SQL_NC_OFF が返された場合、NOCOUNT がオフであることと、値の 0 から**SQLRowCount**ステートメントがすべての行に影響しないことを示します。 アプリケーションがの値を表示する必要がありますいない**SQLRowCount** SQL_SOPT_SS_NOCOUNT_STATUS が SQL_NC_OFF の場合。 大きなバッチやストアド プロシージャには、複数の SET NOCOUNT ステートメントが含まれていることがあるので、プログラマは SQL_SOPT_SS_NOCOUNT_STATUS が一定であると想定することはできません。 オプションは、毎回テスト必要があります**SQLRowCount** 0 を返します。  
  
 他のいくつかの Transact-SQL ステートメントは、結果セットではなく、メッセージにデータを含めて返します。 ときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、これらのメッセージを受信、sql_success_with_info をアプリケーションに情報メッセージが使用できることを通知できるようにします。 アプリケーションを呼び出して**SQLGetDiagRec**をこれらのメッセージを取得します。 このように機能する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを次に示します。  
  
-   DBCC  
  
-   SET SHOWPLAN (以前のバージョンの SQL Server で使用可能)  
  
-   SET STATISTICS  
  
-   PRINT  
  
-   RAISERROR  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、raiserror で重大度レベル 11 以上の SQL_ERROR を返します。 RAISERROR の重大度が 19 以上の場合は、接続も削除されます。  
  
 アプリケーションでは、SQL ステートメントから返される結果セットを処理するために次の処理を行います。  
  
-   結果セットの特性を判断します。  
  
-   プログラム変数に列をバインドします。  
  
-   1 つの値、値の行全体、または値の複数の行を取得します。  
  
-   さらに結果セットが存在するかどうかを確認するテストを行い、存在する場合は、新しい結果セットの特性を判断する処理まで戻って、それ以降をループ処理します。  
  
 データ ソースから行を取得し、取得した行をアプリケーションに返す処理をフェッチと呼びます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [結果セットの特性の決定&#40;ODBC&#41;](determining-the-characteristics-of-a-result-set-odbc.md)  
  
-   [ストレージの割り当て](assigning-storage.md)  
  
-   [結果データのフェッチ](fetching-result-data.md)  
  
-   [データ型のマッピング&#40;ODBC&#41;](mapping-data-types-odbc.md)  
  
-   [データ型の使用方法](data-type-usage.md)  
  
-   [文字データの自動変換](autotranslation-of-character-data.md)  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [結果の操作方法に関するトピックを処理&#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)  
  
  
