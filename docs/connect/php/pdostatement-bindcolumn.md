---
title: 'PDOStatement:: bindColumn |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bbdcea53-d23d-4769-89a0-95c7cf4d5390
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4b159e57f6f2335e894490f7e34d159bd95b2b6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993134"
---
# <a name="pdostatementbindcolumn"></a>PDOStatement::bindColumn
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

結果セット内の列に変数をバインドします。  
  
## <a name="syntax"></a>構文  
  
```  
  
bool PDOStatement::bindColumn($column, &$param[, $type[, $maxLen[, $driverdata ]]] );  
```  
  
#### <a name="parameters"></a>パラメーター  
$*column*: 結果セットの列 (1 から始まるインデックス) の (混合の) 番号または列の名前。  
  
&$*param*: 列をバインドする PHP 変数の (混合の) 名前。  
  
$*type*: (省略可能) PDO::PARAM_* 定数で表されたパラメーターのデータ型。  
  
$*maxLen*: (省略可能) 整数。Microsoft Drivers for PHP for SQL Server では使用されません。  
  
$*driverdata*: (省略可能) ドライバーに対する混合パラメーター。 たとえば、PDO::SQLSRV_ENCODING_UTF8 と指定すると、UTF-8 でエンコードされた文字列として列を変数にバインドできます。  
  
## <a name="return-value"></a>戻り値  
成功した場合は TRUE、それ以外の場合は FALSE。  
  
## <a name="remarks"></a>Remarks  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
次の例では、結果セット内の列に変数をバインドする方法を示します。  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "SELECT Title, FirstName, EmailAddress FROM Person.Contact where LastName = 'Estes'";  
$stmt = $conn->prepare($query);  
$stmt->execute();  
  
$stmt->bindColumn('EmailAddress', $email);  
while ( $row = $stmt->fetch( PDO::FETCH_BOUND ) ){  
   echo "$email\n";  
}  
?>  
```  
  
## <a name="see-also"></a>参照  
[PDOStatement クラス](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
