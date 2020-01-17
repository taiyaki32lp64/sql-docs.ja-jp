---
title: '方法: パラメーター化クエリを実行する |Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data
- parameterized queries
ms.assetid: dc7d0ede-a9b6-4ce2-977e-4d1e7ec2131c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7e406d64bd8c56b467c9b331eb4aef132dc0cc67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993500"
---
# <a name="how-to-perform-parameterized-queries"></a>方法: パラメーター化クエリを実行する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このトピックでは、 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] を使用してパラメーター化クエリを実行する方法を説明し、実例を示します。  
  
パラメーター化クエリを実行する手順は、次の 4 つのステップにまとめることができます。  
  
1.  実行するクエリである Transact-SQL の文字列にパラメーターのプレースホルダーとして疑問符 (?) を配置します。  
  
2.  Transact-SQL クエリ内のプレースホルダーに対応する PHP 変数を初期化または更新します。  
  
3.  ステップ 2 の PHP 変数を使用して、Transact-SQL 文字列内のパラメーター プレースホルダーに対応するパラメーター値の配列を作成または更新します。 配列内のパラメーター値は、それらを表すためのプレースホルダーと同じ順序である必要があります。
  
4.  クエリを実行します。  
  
    -   SQLSRV ドライバーを使用している場合は、 [sqlsrv_query](../../connect/php/sqlsrv-query.md) または [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md)を使用します。  
  
    -   PDO_SQLSRV ドライバーを使用している場合は、[PDO::prepare](../../connect/php/pdo-prepare.md) および [PDOStatement::execute](../../connect/php/pdostatement-execute.md) でクエリを実行します。 コードの例については、 [PDO::prepare](../../connect/php/pdo-prepare.md) および [PDOStatement::execute](../../connect/php/pdostatement-execute.md) のトピックを参照してください。  
  
以降では、SQLSRV ドライバーを使用するパラメーター化クエリについて説明します。  
  
> [!NOTE]  
> パラメーターは、 **sqlsrv_prepare**を使用します。 つまり、 **sqlsrv_prepare** を使用してパラメーター化クエリを準備し、パラメーター配列内の値を更新した場合、更新された値はクエリの次の実行時に使用されます。 詳細については、このトピックの 2 番目の例を参照してください。  
  
## <a name="example"></a>例  
次の例では、AdventureWorks データベースの *Production.ProductInventory* テーブルで指定した製品 ID の数量を更新します。 数量と製品 ID は、UPDATE クエリのパラメーターです。  
  
次の例では、データベースにクエリを発行して数量が正しく更新されたことを確認しています。 製品 ID は、SELECT クエリのパラメーターです。  
  
この例では、ローカル コンピューターに SQL Server および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースがインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Define the Transact-SQL query.  
Use question marks as parameter placeholders. */  
$tsql1 = "UPDATE Production.ProductInventory   
          SET Quantity = ?   
          WHERE ProductID = ?";  
  
/* Initialize $qty and $productId */  
$qty = 10; $productId = 709;  
  
/* Execute the statement with the specified parameter values. */  
$stmt1 = sqlsrv_query( $conn, $tsql1, array($qty, $productId));  
if( $stmt1 === false )  
{  
     echo "Statement 1 could not be executed.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free statement resources. */  
sqlsrv_free_stmt( $stmt1);  
  
/* Now verify the updated quantity.  
Use a question mark as parameter placeholder. */  
$tsql2 = "SELECT Quantity   
          FROM Production.ProductInventory  
          WHERE ProductID = ?";  
  
/* Execute the statement with the specified parameter value.  
Display the returned data if no errors occur. */  
$stmt2 = sqlsrv_query( $conn, $tsql2, array($productId));  
if( $stmt2 === false )  
{  
     echo "Statement 2 could not be executed.\n";  
     die( print_r(sqlsrv_errors(), true));  
}  
else  
{  
     $qty = sqlsrv_fetch_array( $stmt2);  
     echo "There are $qty[0] of product $productId in inventory.\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_close( $conn);  
?>  
```  
  
前の例では、 **sqlsrv_query** 関数を使用してクエリを実行しています。 この関数は、ステートメントの準備と実行の両方を行うため、1 回限りのクエリを実行するのに便利です。 異なるパラメーター値でクエリを再実行するには、**sqlsrv_prepare**/**sqlsrv_execute** の組み合わせが最善です。 異なるパラメーター値でクエリを再実行する例については、次の例を参照してください。  
  
## <a name="example"></a>例  
次の例では、 **sqlsrv_prepare** 関数を使用するときに変数を暗黙的にバインドする方法を示します。 この例では、複数の注文を *Sales.SalesOrderDetail* テーブルに挿入します。 **sqlsrv_prepare** を呼び出すと、 *$params* 配列がステートメント ( *$stmt*) にバインドされます。 テーブルに新しい注文を挿入する各クエリを実行する前に、 *$params* 配列が注文の詳細に対応する新しい値で更新されます。 後続のクエリ実行では、新しいパラメーター値が使用されます。  
  
この例では、ローカル コンピューターに SQL Server および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースがインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "INSERT INTO Sales.SalesOrderDetail (SalesOrderID,   
                                             OrderQty,   
                                             ProductID,   
                                             SpecialOfferID,   
                                             UnitPrice)  
         VALUES (?, ?, ?, ?, ?)";  
  
/* Each sub array here will be a parameter array for a query.  
The values in each sub array are, in order, SalesOrderID, OrderQty,  
 ProductID, SpecialOfferID, UnitPrice. */  
$parameters = array( array(43659, 8, 711, 1, 20.19),  
                     array(43660, 6, 762, 1, 419.46),  
                     array(43661, 4, 741, 1, 818.70)  
                    );  
  
/* Initialize parameter values. */  
$orderId = 0;  
$qty = 0;  
$prodId = 0;  
$specialOfferId = 0;  
$price = 0.0;  
  
/* Prepare the statement. $params is implicitly bound to $stmt. */  
$stmt = sqlsrv_prepare( $conn, $tsql, array( &$orderId,  
                                             &$qty,  
                                             &$prodId,  
                                             &$specialOfferId,  
                                             &$price));  
if( $stmt === false )  
{  
     echo "Statement could not be prepared.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Execute a statement for each set of params in $parameters.  
Because $params is bound to $stmt, as the values are changed, the  
new values are used in the subsequent execution. */  
foreach( $parameters as $params)  
{  
     list($orderId, $qty, $prodId, $specialOfferId, $price) = $params;  
     if( sqlsrv_execute($stmt) === false )  
     {  
          echo "Statement could not be executed.\n";  
          die( print_r( sqlsrv_errors(), true));  
     }  
     else  
     {  
          /* Verify that the row was successfully inserted. */  
          echo "Rows affected: ".sqlsrv_rows_affected( $stmt )."\n";  
     }  
}  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>参照  
[データ型の変換](../../connect/php/converting-data-types.md)

[Microsoft Drivers for PHP for SQL Server のセキュリティに関する考慮事項](../../connect/php/security-considerations-for-php-sql-driver.md)

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)

[sqlsrv_rows_affected](../../connect/php/sqlsrv-rows-affected.md)  
  
