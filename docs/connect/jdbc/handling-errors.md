---
title: エラーの処理 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6277b3ecf0160078fa47bc79994d31f64519d9b7
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028031"
---
# <a name="handling-errors"></a>エラーの処理
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] の使用時に発生するデータベース エラー状態はすべて、[SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) クラスの例外として Java アプリケーションに返されます。 SQLServerException クラスの次のメソッドは、java.sql.SQLException および java.lang.Throwable から継承されます。これらのメソッドを使用して、発生した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラーに関する特定の情報を返すことができます。  
  
-   `getSQLState()` は、例外の標準的な X/Open または SQL99 状態コードを返します。
  
-   `getErrorCode()` は、具体的なデータベース エラー番号を返します。
  
-   `getMessage()` は、例外の全文を返します。 エラー メッセージ テキストは問題について説明します。そして、オブジェクト名のような情報のプレースホルダーを含むことがよくあります。こうしたプレースホルダーは、エラー メッセージが表示されるとき、その中に挿入されます。
  
-   `getNextException()` は、返す例外オブジェクトが他にない場合、次の `SQLServerException` オブジェクトまたは null を返します。

-   `getSQLServerError()`SQL Server から`SQLServerError`受信した例外に関する詳細情報を格納しているオブジェクトを返します。 サーバーエラーが発生しなかった場合、このメソッドは null を返します。

`SQLServerError`クラスの次のメソッドは、サーバーから生成されたエラーに関する追加情報を取得するために使用できます。

-   `SQLServerError.getErrorMessage()`サーバーから受信したエラーメッセージを返します。

-   `SQLServerError.getErrorNumber()`エラーの種類を識別する数値を返します。

-   `SQLServerError.getErrorState()`エラー、警告、または "データが見つかりません" メッセージを表す SQL Server から数値エラーコードを返します。

-   `SQLServerError.getErrorSeverity()`受信したエラーの重大度レベルを返します。

-   `SQLServerError.getServerName()`エラーを生成した SQL Server のインスタンスを実行しているコンピューターの名前を返します。

-   `SQLServerError.getProcedureName()`エラーを生成したストアドプロシージャまたはリモートプロシージャコール (RPC) の名前を返します。

-   `SQLServerError.getLineNumber()`Transact-sql コマンドバッチまたはストアドプロシージャ内の、エラーを生成した行番号を返します。
  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] サンプル データベースに対して開いている接続が関数に渡され、FROM 句のない不適切な SQL ステートメントが作成されます。 次に、ステートメントが実行され、SQL 例外が処理されます。  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>参照  
 [JDBC ドライバーに関する問題の診断](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
