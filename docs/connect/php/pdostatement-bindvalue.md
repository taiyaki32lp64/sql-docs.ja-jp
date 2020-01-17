---
title: 'PDOStatement:: bindValue |Microsoft Docs'
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 13bc4ece-420e-4887-8809-bf0705ddf126
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 89126d696f7210132adb5ef10ec557604ebc543f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993124"
---
# <a name="pdostatementbindvalue"></a>PDOStatement::bindValue
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQL ステートメントで名前付きまたは疑問符プレースホルダーに値をバインドします。  
  
## <a name="syntax"></a>構文  
  
```  
  
bool PDOStatement::bindValue($parameter, $value[, $data_type]);  
```  
  
#### <a name="parameters"></a>パラメーター  
$*parameter*: (混合) パラメーター識別子。 名前付きプレースホルダーを使用するステートメントの場合、パラメーター名 (:name) を使用します。 疑問符構文を使用する準備されたステートメントの場合、これはパラメーターの 1 から始まるインデックスになります。
  
$*value*: パラメーターにバインドする (複合) 値。  
  
$*data_type*: PDO::PARAM_* 定数で表される省略可能な (整数) データ型。 既定は PDO::PARAM_STR です。  
  
## <a name="return-value"></a>戻り値  
成功した場合は TRUE、それ以外の場合は FALSE です。  
  
## <a name="remarks"></a>Remarks  
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
この例は、$contact の値をバインドした後に、値を変更してもクエリで渡される値が変更されないことを示しています。  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
$contact = "Sales Agent";  
$stmt = $conn->prepare("select * from Person.ContactType where name = ?");  
$stmt->bindValue(1, $contact);  
$contact = "Owner";  
$stmt->execute();  
  
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {  
   print "$row[Name]\n\n";  
}  
  
$stmt = null;  
$contact = "Sales Agent";  
$stmt = $conn->prepare("select * from Person.ContactType where name = :contact");  
$stmt->bindValue(':contact', $contact);  
$contact = "Owner";  
$stmt->execute();  
  
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {  
   print "$row[Name]\n\n";  
}  
?>  
```

> [!NOTE]
> 値を [10 進数列または数値列](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)にバインドするときは、有効桁数と精度を保持するために、入力として文字列を使用することをお勧めします。これは、PHP には[浮動小数点数](https://php.net/manual/en/language.types.float.php)の有効桁数に制限があるためです。 値が[整数](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)の範囲外にある場合は特に、同じことが bigint 列にも適用されます。

## <a name="example"></a>例  
このコード サンプルでは、入力パラメーターとして 10 進数値をバインドする方法を示しています。  

```
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  

// Assume TestTable exists with a decimal field 
$input = 9223372036854.80000;
$stmt = $conn->prepare("INSERT INTO TestTable (DecimalCol) VALUES (?)");
// by default it is PDO::PARAM_STR, rounding of a large input value may
// occur if PDO::PARAM_INT is specified
$stmt->bindValue(1, $input, PDO::PARAM_STR);
$stmt->execute();
```
  
## <a name="see-also"></a>参照  
[PDOStatement クラス](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
