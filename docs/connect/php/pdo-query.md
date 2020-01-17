---
title: 'PDO:: query |Microsoft Docs'
ms.custom: ''
ms.date: 08/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f6f5e6d4-8ca9-4f06-89ed-de65ad3952a2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb7131e96277ea05b43f30923dcc64c5be602696
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936208"
---
# <a name="pdoquery"></a>PDO::query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQL クエリを実行し、PDOStatement オブジェクトとして結果セットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
PDOStatement PDO::query ($statement[, $fetch_style);  
```  
  
#### <a name="parameters"></a>パラメーター  
*$statement*: 実行する SQL ステートメント。  
  
*$fetch_style*: クエリを実行する手順 (省略可能)。 詳細については、「解説」を参照してください。PDO::query の  $*fetch_style* は、PDO::fetch の $*fetch_style* でオーバーライドできます。  
  
## <a name="return-value"></a>戻り値  
呼び出しに成功すると、PDO::query は PDOStatement オブジェクトを返します。 呼び出しに失敗すると、PDO::ATTR_ERRMODE の設定に応じて PDO::query は PDOException オブジェクトをスローするか、false を返します。  
  
## <a name="exceptions"></a>例外  
PDOException。  
  
## <a name="remarks"></a>Remarks  
PDO::query を使用して実行されたクエリは、PDO::SQLSRV_ATTR_DIRECT_QUERY の設定に応じて、準備したステートメントを実行するか、直接実行されます。 詳細については、「 [Direct Statement Execution and Prepared Statement Execution in the PDO_SQLSRV Driver](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)」 (PDO_SQLSRV ドライバーでの直接ステートメント実行と準備されたステートメントの実行) を参照してください。  
  
また、PDO::SQLSRV_ATTR_QUERY_TIMEOUT は、PDO::exec の動作にも影響があります。詳細については、「[PDO::setAttribute](../../connect/php/pdo-setattribute.md)」を参照してください。  
  
$*fetch_style* には、次のオプションを指定できます。  
  
|style|[説明]|  
|---------|---------------|  
|PDO::FETCH_COLUMN, *num*|指定された列内のデータを照会します。 テーブルの最初の列は 0 です。|  
|PDO::FETCH_CLASS, '*classname*', array( *arglist* )|クラスのインスタンスを作成し、列名をクラスのプロパティに割り当てます。 クラス コンストラクターに 1 つ以上のパラメーターを指定できる場合、 *arglist*を渡すこともできます。|  
|PDO:: FETCH_CLASS, '*classname*'|既存のクラスのプロパティに列名を割り当てます。|  
  
PDOStatement::closeCursor を呼び出して、PDOStatement オブジェクトに関連付けられたデータベース リソースを解放してから、もう一度 PDO::query を呼び出します。  
  
PDOStatement オブジェクトを閉じるには、オブジェクトを null に設定します。  
  
結果セット内のすべてのデータがフェッチされていない場合でも、次の PDO::query の呼び出しは失敗しません。  
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
この例では、いくつかのクエリを使用します。  
  
```  
<?php  
$database = "AdventureWorks";  
$conn = new PDO( "sqlsrv:server=(local) ; Database = $database", "", "");  
$conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
$conn->setAttribute( PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 1 );  
  
$query = 'select * from Person.ContactType';  
  
// simple query  
$stmt = $conn->query( $query );  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print_r( $row['Name'] ."\n" );  
}  
  
echo "\n........ query for a column ............\n";  
  
// query for one column  
$stmt = $conn->query( $query, PDO::FETCH_COLUMN, 1 );  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query with a new class ............\n";  
$query = 'select * from HumanResources.Department order by GroupName';  
// query with a class  
class cc {  
   function __construct( $arg ) {  
      echo "$arg";  
   }  
  
   function __toString() {  
      return $this->DepartmentID . "; " . $this->Name . "; " . $this->GroupName;  
   }  
}  
  
$stmt = $conn->query( $query, PDO::FETCH_CLASS, 'cc', array( "arg1 " ));  
  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query into an existing class ............\n";  
$c_obj = new cc( '' );  
$stmt = $conn->query( $query, PDO::FETCH_INTO, $c_obj );  
while ( $stmt->fetch() ){  
   echo "$c_obj\n";  
}  
  
$stmt = null;  
?>  
```

## <a name="example"></a>例
このコード例では、[sql_variant](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql) 型のテーブルを作成し、挿入されたデータをフェッチする方法を示しています。

```
<?php
$server = 'serverName';
$dbName = 'databaseName';
$uid = 'yourUserName';
$pwd = 'yourPassword';

$conn = new PDO("sqlsrv:server=$server; database = $dbName", $uid, $pwd);
$conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  

try {
    $tableName = 'testTable';
    $query = "CREATE TABLE $tableName ([c1_int] sql_variant, [c2_varchar] sql_variant)";

    $stmt = $conn->query($query);
    unset($stmt);

    $query = "INSERT INTO [$tableName] (c1_int, c2_varchar) VALUES (1, 'test_data')";
    $stmt = $conn->query($query);
    unset($stmt);

    $query = "SELECT * FROM $tableName";
    $stmt = $conn->query($query);

    $result = $stmt->fetch(PDO::FETCH_ASSOC);
    print_r($result);
    
    unset($stmt);
    unset($conn);
} catch (Exception $e) {
    echo $e->getMessage();
}
?>
```

予想される出力は次のようになります。

```
Array
(
    [c1_int] => 1
    [c2_varchar] => test_data
)
```

## <a name="see-also"></a>参照  
[PDO クラス](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
