---
title: バッチ操作の実行 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1a576d95-7da6-4b7b-8b32-59e5b4d354c4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a77816598e7c8e3f0589f71cb5c02e40e0e17317
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027926"
---
# <a name="performing-batch-operations"></a>バッチ操作の実行
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに対する更新処理が複数回にわたって発生する際のパフォーマンスを向上させるため、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] には、複数の更新処理を 1 回の作業単位として送信する機能が備わっています。この機能は、"バッチ" と呼ばれることもあります。  
  
 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)、[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)、および [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスはすべて、バッチ更新を送信するために使用できます。 [addBatch](../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md) メソッドは、コマンドを追加するために使用します。 [clearBatch](../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md) メソッドは、コマンドのリストをクリアするために使用します。 [executeBatch](../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md) メソッドは、すべてのコマンドを送信して処理するために使用します。 バッチの一部として実行できるのは、単純に更新数を返すデータ操作言語 (DML) ステートメントおよびデータ定義言語 (DDL) ステートメントだけです。  
  
 executeBatch メソッドは、各コマンドの更新数に対応する **int** 値の配列を返します。 いずれかのコマンドが失敗した場合は、BatchUpdateException がスローされます。そのため、BatchUpdateException クラスの getUpdateCounts メソッドを使用して、更新数の配列を取得する必要があります。 いずれかのコマンドが失敗した場合、JDBC ドライバーでは残りのコマンドの処理は続行されます。 ただし、コマンドに構文エラーがある場合は、バッチ内のステートメントが失敗します。  
  
> [!NOTE]  
>  更新数を使用する必要がない場合は、最初に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に対して SET NOCOUNT ON ステートメントを発行できます。 これによりネットワーク トラフィックが減少し、アプリケーションのパフォーマンスがさらに強化されます。  
  
 例として、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] サンプル データベースで次のテーブルを作成します。  
  
```sql
CREATE TABLE TestTable   
   (Col1 int IDENTITY,   
    Col2 varchar(50),   
    Col3 int);  
```  
  
 次の例は、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] サンプル データベースに対して開いている接続を関数に渡し、実行するステートメントを作成するために addBatch メソッドを使用し、バッチをデータベースに送信するために executeBatch メソッドを呼び出します。  
  
```java
public static void executeBatchUpdate(Connection con) {  
   try {  
      Statement stmt = con.createStatement();  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('X', 100)");  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('Y', 200)");  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('Z', 300)");  
      int[] updateCounts = stmt.executeBatch();  
      stmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>参照  
 [JDBC ドライバーでのステートメントの使用](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
