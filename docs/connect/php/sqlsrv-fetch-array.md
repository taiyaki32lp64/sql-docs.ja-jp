---
title: sqlsrv_fetch_array |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_fetch_array
apitype: NA
helpviewer_keywords:
- sqlsrv_fetch_array
- retrieving data, as an array
- API Reference, sqlsrv_fetch_array
ms.assetid: 69270b9e-0791-42f4-856d-412da39dea63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02b4311348ebbd52e5e8382048449072c84d2e46
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015035"
---
# <a name="sqlsrvfetcharray"></a>sqlsrv_fetch_array
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

次のデータ行を数値インデックス配列、連想配列、またはその両方として取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqlsrv_fetch_array( resource $stmt[, int $fetchType [, row[, ]offset]])  
```  
  
#### <a name="parameters"></a>パラメーター  
*$stmt*: 実行されたステートメントに対応するステートメント リソースです。  
  
*$fetchType* [省略可能]: 定義済みの定数。 このパラメーターには、次の表に示すいずれかの値を指定できます。  
  
|[値]|[説明]|  
|---------|---------------|  
|SQLSRV_FETCH_NUMERIC|次のデータ行は数値の配列として返されます。|  
|SQLSRV_FETCH_ASSOC|次のデータ行は連想配列として返されます。 配列キーは、結果セットの列名です。|  
|SQLSRV_FETCH_BOTH|次のデータ行は数値配列と連想配列の両方として返されます。 これが既定値です。|  
  
*row* [省略可能]: バージョン 1.1 で追加されました。 次の値のいずれかで、スクロール可能なカーソルを使用して結果セットにアクセスする行を指定します (*row* を指定するときは、既定値を指定した場合でも、*fetchtype* を明示的に指定する必要があります。)  
  
-   SQLSRV_SCROLL_NEXT  
-   SQLSRV_SCROLL_PRIOR  
-   SQLSRV_SCROLL_FIRST  
-   SQLSRV_SCROLL_LAST  
-   SQLSRV_SCROLL_ABSOLUTE  
-   SQLSRV_SCROLL_RELATIVE  
  
これらの値の詳細については、「 [カーソルの種類を指定し、行を選択する](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)」を参照してください。 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 1.1 に、スクロール可能なカーソルのサポートが追加されました。  
  
*offset* [省略可能]: SQLSRV_SCROLL_ABSOLUTE と SQLSRV_SCROLL_RELATIVE と共に使用し、取得する行を指定します。 結果セットの最初のレコードは 0 です。  
  
## <a name="return-value"></a>戻り値  
データ行が取得された場合は、 **配列** が返されます。 取得する行がなくなった場合、 **null** が返されます。 エラーが発生した場合は、 **false** が返されます。  
  
*$fetchType* パラメーターの値に基づき、返される **配列** は数値インデックス **配列**、連想 **配列**、またはその両方になる可能性があります。 既定では、数値キーと連想キーの両方の **配列** が返されます。 返される配列の値のデータ型は、既定の PHP データ型になります。 既定の PHP データ型の詳細については、「 [Default PHP Data Types](../../connect/php/default-php-data-types.md)」を参照してください。  
  
## <a name="remarks"></a>Remarks  
名前のない列が返された場合、配列要素の連想キーは空の文字列 ("") になります。 たとえば、データベース テーブルに値を挿入し、サーバーが生成したプライマリ キーを取得する、この Transact-SQL ステートメントがあります。  
  
```
INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()
```
  
このステートメントの `SELECT SCOPE_IDENTITY()` 部分によって返される結果セットが連想配列として取得される場合、返される列には名前がないので、返される値のキーは空の文字列 ("") になります。 これを回避するには、結果を数値配列として取得するか、または返される列の名前を Transact-SQL ステートメントに指定します。 次は、Transact-SQL に列名を指定する方法の 1 つです。  
  
```
SELECT SCOPE_IDENTITY() AS PictureID
```
  
結果セットに名前のない複数の列が含まれている場合は、名前のない最後の列の値が、空の文字列 ("") キーに割り当てられます。  
  
## <a name="example"></a>例  
次の例では、結果セットの各行を連想 **配列**として取得します。 この例では、SQL Server と [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースはローカル コンピューターにインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
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
  
/* Set up and execute the query. */  
$tsql = "SELECT FirstName, LastName  
         FROM Person.Contact  
         WHERE LastName='Alan'";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false)  
{  
     echo "Error in query preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve each row as an associative array and display the results.*/  
while( $row = sqlsrv_fetch_array( $stmt, SQLSRV_FETCH_ASSOC))  
{  
      echo $row['LastName'].", ".$row['FirstName']."\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>例  
次の例では、結果セットの各行を数値インデックス配列として取得します。  
  
この例では、指定日で在庫数 (*StockQty*) が指定値より少ない製品の情報を AdventureWorks データベースの *Purchasing.PurchaseOrderDetail* テーブルから取得します。  
  
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
  
/* Define the query. */  
$tsql = "SELECT ProductID,  
                UnitPrice,  
                StockedQty   
         FROM Purchasing.PurchaseOrderDetail  
         WHERE StockedQty < 3   
         AND DueDate='2002-01-29'";  
  
/* Execute the query. */  
$stmt = sqlsrv_query( $conn, $tsql);  
if ( $stmt )  
{  
     echo "Statement executed.\n";  
}   
else   
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Iterate through the result set printing a row of data upon each  
iteration.*/  
while( $row = sqlsrv_fetch_array( $stmt, SQLSRV_FETCH_NUMERIC))  
{  
     echo "ProdID: ".$row[0]."\n";  
     echo "UnitPrice: ".$row[1]."\n";  
     echo "StockedQty: ".$row[2]."\n";  
     echo "-----------------\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
**sqlsrv_fetch_array** 関数は、常に [Default PHP Data Types](../../connect/php/default-php-data-types.md) パラメーターに基づいてデータを返します。 PHP データ型を指定する方法については、「 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)」を参照してください。  
  
名前のないフィールドが取得された場合、配列要素の連想キーは空の文字列 ("") になります。 詳細については、「 [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)

[データの取得](../../connect/php/retrieving-data.md)

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)

[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md)
  
