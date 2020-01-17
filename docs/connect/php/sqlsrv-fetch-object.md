---
title: sqlsrv_fetch_object |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_fetch_object
apitype: NA
helpviewer_keywords:
- sqlsrv_fetch_object
- API Reference, sqlsrv_fetch_object
- retrieving data, as an object
ms.assetid: 4ce2df2c-083a-4a4d-a1e2-e866e63707d5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 36c0ae99e38da83e3d534423b8a09ba9e198ce3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992740"
---
# <a name="sqlsrvfetchobject"></a>sqlsrv_fetch_object
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PHP オブジェクトとしてデータの次の行を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqlsrv_fetch_object( resource $stmt [, string $className [, array $ctorParams[, row[, ]offset]]])  
```  
  
#### <a name="parameters"></a>パラメーター  
*$stmt*: 実行されたステートメントに対応するステートメント リソースです。  
  
*$className* [省略可能]: インスタンス化するクラスの名前を指定する文字列。 *$className* パラメーターの値が指定されていない場合、PHP **stdClass** のインスタンスがインスタンス化されます。  
  
*$ctorParams* [省略可能]: *$className* パラメーターで指定されたクラスのコンストラクターに渡される値を含む配列。 指定したクラスのコンストラクターがパラメーター値を受け取る場合、 *$ctorParams* object **sqlsrv_fetch_object**パラメーターを使用する必要があります。  
  
*row* [省略可能]: 次の値のいずれかで、スクロール可能なカーソルを使用して結果セットにアクセスする行を指定します。 (*row* が指定されている場合、 *$className* と *$ctorParams* に null を指定しなければならない場合でも、 *$className* と *$ctorParams* を明示的に指定する必要があります。)  
  
-   SQLSRV_SCROLL_NEXT  
  
-   SQLSRV_SCROLL_PRIOR  
  
-   SQLSRV_SCROLL_FIRST  
  
-   SQLSRV_SCROLL_LAST  
  
-   SQLSRV_SCROLL_ABSOLUTE  
  
-   SQLSRV_SCROLL_RELATIVE  
  
これらの値の詳細については、「 [カーソルの種類を指定し、行を選択する](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)」を参照してください。  
  
*offset* [省略可能]: SQLSRV_SCROLL_ABSOLUTE と SQLSRV_SCROLL_RELATIVE と共に使用し、取得する行を指定します。 結果セットの最初のレコードは 0 です。  
  
## <a name="return-value"></a>戻り値  
結果セットのフィールド名に対応するプロパティを持つ PHP オブジェクト。 プロパティ値には、対応する結果セットのフィールド値が入力されます。 省略可能な *$className* パラメーターで指定されたクラスが存在しないか、指定されたステートメントにアクティブな結果セットが存在しない場合、 **false** が返されます。 取得する行がなくなった場合、 **null** が返されます。  
  
返されたオブジェクトの値のデータ型は既定の PHP データ型になります。 既定の PHP データ型の詳細については、「 [Default PHP Data Types](../../connect/php/default-php-data-types.md)」を参照してください。  
  
## <a name="remarks"></a>Remarks  
クラス名が省略可能な *$className* パラメーターで指定される場合、このクラス型のオブジェクトはインスタンス化されます。 名前が結果セットのフィールド名に一致するプロパティがクラスにある場合、対応する結果セット値がプロパティに適用されます。 結果セットのフィールド名がクラス プロパティに一致しない場合、結果セットのフィールド名を持つプロパティがオブジェクトに追加され、結果セットの値がプロパティに適用されます。  
  
次の規則は、 *$className* パラメーターと共にクラスを指定したときに適用されます。  
  
-   一致では、大文字と小文字が区別されます。 たとえば、「CustomerId」というプロパティ名は「CustomerID」というフィールド名に一致しません。 この場合、CustomerID プロパティはオブジェクトに追加され、CustomerID フィールドの値は CustomerID プロパティに与えられます。  
  
-   一致は、アクセス修飾子に関係なく行われます。 たとえば、指定されたクラスに、名前が結果セットのフィールド名と一致するプライベート プロパティがある場合、結果セットのフィールドからの値がプロパティに適用されます。  
  
-   クラス プロパティのデータ型は無視されます。 結果セットの「CustomerID」フィールドが文字列で、クラスの「CustomerID」プロパティが整数の場合、結果セットからの文字列値が「CustomerID」プロパティに書き込まれます。  
  
-   指定したクラスが存在しない場合、関数は **false** を返し、エラーをエラー コレクションに追加します。 エラーの取得については、「 [sqlsrv_errors](../../connect/php/sqlsrv-errors.md)」を参照してください。  
  
名前のないフィールドが返された場合、 **sqlsrv_fetch_object** はフィールド値を破棄し、警告を発行します。 たとえば、データベース テーブルに値を挿入し、サーバーが生成したプライマリ キーを取得する、この Transact-SQL ステートメントがあります。  
  
<pre>INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()</pre>  
  
このクエリで返される結果が **sqlsrv_fetch_object**で取得される場合、 `SELECT SCOPE_IDENTITY()` で返される値は破棄され、警告が発行されます。 これを回避するために、Transact-SQL ステートメントに返されたフィールドの名前を指定できます。 次は、Transact-SQL に列名を指定する方法の 1 つです。  
  
`SELECT SCOPE_IDENTITY() AS PictureID`  
  
## <a name="example"></a>例  
次の例では、結果セットの各行を PHP オブジェクトとして取得します。 この例では、SQL Server と [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースはローカル コンピューターにインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
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
if( $stmt === false )  
{  
     echo "Error in query preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve each row as a PHP object and display the results.*/  
while( $obj = sqlsrv_fetch_object( $stmt))  
{  
      echo $obj->LastName.", ".$obj->FirstName."\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>例  
次の例では、スクリプトに定義されている *Product* クラスのインスタンスとして結果セットの各行が取得されます。 この例では、指定納期 *DueDate* で在庫数 *StockQty* が指定値より少ない製品の情報が AdventureWorks データベースの *Purchasing.PurchaseOrderDetail* テーブルと *Production.Product* テーブルから取得されます。 この例では、 **sqlsrv_fetch_object**の呼び出しにクラスを指定したときに適用される規則の一部が強調表示されています。  
  
-   *$product* 変数は *Product* クラスのインスタンスです。「Product」が *$className* パラメーターで指定され、 *Product* クラスが存在するからです。  
  
-   既存の *name* プロパティが一致しないため、 *Name* プロパティが *$product* インスタンスに追加されます。  
  
-   一致するプロパティがないため、 *Color* プロパティが *$product* インスタンスに追加されます。  
  
-   プライベート プロパティ *UnitPrice* に *UnitPrice* フィールドの値が入力されます。  
  
この例では、ローカル コンピューターに SQL Server および [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) データベースがインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
```  
<?php  
/* Define the Product class. */  
class Product  
{  
     /* Constructor */  
     public function Product($ID)  
     {  
          $this->objID = $ID;  
     }  
     public $objID;  
     public $name;  
     public $StockedQty;  
     public $SafetyStockLevel;  
     private $UnitPrice;  
     function getPrice()  
     {  
          return $this->UnitPrice;  
     }  
}  
  
/* Connect to the local server using Windows Authentication, and  
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
$tsql = "SELECT Name,  
                SafetyStockLevel,  
                StockedQty,  
                UnitPrice,  
                Color  
         FROM Purchasing.PurchaseOrderDetail AS pdo  
         JOIN Production.Product AS p  
         ON pdo.ProductID = p.ProductID  
         WHERE pdo.StockedQty < ?  
         AND pdo.DueDate= ?";  
  
/* Set the parameter values. */  
$params = array(3, '2002-01-29');  
  
/* Execute the query. */  
$stmt = sqlsrv_query( $conn, $tsql, $params);  
if ( $stmt )  
{  
     echo "Statement executed.\n";  
}   
else   
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Iterate through the result set, printing a row of data upon each  
 iteration. Note the following:  
     1) $product is an instance of the Product class.  
     2) The $ctorParams parameter is required in the call to  
        sqlsrv_fetch_object, because the Product class constructor is  
        explicity defined and requires parameter values.  
     3) The "Name" property is added to the $product instance because  
        the existing "name" property does not match.  
     4) The "Color" property is added to the $product instance  
        because there is no matching property.  
     5) The private property "UnitPrice" is populated with the value  
        of the "UnitPrice" field.*/  
$i=0; //Used as the $objID in the Product class constructor.  
while( $product = sqlsrv_fetch_object( $stmt, "Product", array($i)))  
{  
     echo "Object ID: ".$product->objID."\n";  
     echo "Product Name: ".$product->Name."\n";  
     echo "Stocked Qty: ".$product->StockedQty."\n";  
     echo "Safety Stock Level: ".$product->SafetyStockLevel."\n";  
     echo "Product Color: ".$product->Color."\n";  
     echo "Unit Price: ".$product->getPrice()."\n";  
     echo "-----------------\n";  
     $i++;  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
既存の **sqlsrv_fetch_object** 関数は常に [Default PHP Data Types](../../connect/php/default-php-data-types.md)パラメーターを使用する必要があります。 PHP データ型を指定する方法については、「 [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md)」を参照してください。  
  
名前のないフィールドが返された場合、 **sqlsrv_fetch_object** はフィールド値を破棄し、警告を発行します。 たとえば、データベース テーブルに値を挿入し、サーバーが生成したプライマリ キーを取得する、この Transact-SQL ステートメントがあります。  
  
<pre>INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()</pre>  
  
このクエリで返される結果が **sqlsrv_fetch_object**で取得される場合、 `SELECT SCOPE_IDENTITY()` で返される値は破棄され、警告が発行されます。 これを回避するために、Transact-SQL ステートメントに返されたフィールドの名前を指定できます。 次は、Transact-SQL に列名を指定する方法の 1 つです。  
  
`SELECT SCOPE_IDENTITY() AS PictureID`  
  
## <a name="see-also"></a>参照  
[データの取得](../../connect/php/retrieving-data.md)  

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)  

[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  
  
