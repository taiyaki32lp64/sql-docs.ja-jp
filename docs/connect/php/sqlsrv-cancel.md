---
title: sqlsrv_cancel |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_cancel
apitype: NA
helpviewer_keywords:
- sqlsrv_cancel
- API Reference, sqlsrv_cancel
ms.assetid: 75798c9b-f711-445d-9b8f-ba4d405ca50a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f109a264d394a47164966e602b264f0fcd337e12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935843"
---
# <a name="sqlsrvcancel"></a>sqlsrv_cancel
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

ステートメントをキャンセルします。 これは、保留中のステートメントの結果を破棄することを意味します。 この関数が呼び出されると、ステートメントを再実行することができます (ステートメントが [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) を使用して準備された場合)。 ステートメントに関連付けられているすべての結果が消費されている場合、この関数を呼び出す必要はありません。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqlsrv_cancel( resource $stmt)  
```  
  
#### <a name="parameters"></a>パラメーター  
*$stmt*: 取り消されるステートメントです。  
  
## <a name="return-value"></a>戻り値  
ブール値: 操作が成功した場合は **true** です。 それ以外の場合は、 **false**です。  
  
## <a name="example"></a>例  
次の例では、 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースを使用してクエリを実行し、変数 *$salesTotal* が、指定した値に達するまで結果を消費してカウントします。 残りのクエリ結果は破棄されます。 この例では、ローカル コンピューターに SQL Server および AdventureWorks データベースがインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
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
  
/* Prepare and execute the query. */  
$tsql = "SELECT OrderQty, UnitPrice FROM Sales.SalesOrderDetail";  
$stmt = sqlsrv_prepare( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in statement preparation.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
if( sqlsrv_execute( $stmt ) === false)  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Initialize tracking variables. */  
$salesTotal = 0;  
$count = 0;  
  
/* Count and display the number of sales that produce revenue  
of $100,000. */  
while( ($row = sqlsrv_fetch_array( $stmt)) && $salesTotal <=100000)  
{  
     $qty = $row[0];  
     $price = $row[1];  
     $salesTotal += ( $price * $qty);  
     $count++;  
}  
echo "$count sales accounted for the first $$salesTotal in revenue.\n";  
  
/* Cancel the pending results. The statement can be reused. */  
sqlsrv_cancel( $stmt);  
?>  
```  
  
## <a name="comments"></a>コメント  
[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) と [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) の組み合わせを使用して準備され実行されたステートメントは、**sqlsrv_cancel** を呼び出した後、**sqlsrv_execute** を使用して再実行することができます。 [sqlsrv_query](../../connect/php/sqlsrv-query.md) を使用して実行されたステートメントは、**sqlsrv_cancel** の呼び出し後に再実行することはできません。  
  
## <a name="see-also"></a>参照  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)

[サーバーへの接続](../../connect/php/connecting-to-the-server.md)

[データの取得](../../connect/php/retrieving-data.md)

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)

[sqlsrv_free_stmt](../../connect/php/sqlsrv-free-stmt.md)

  
