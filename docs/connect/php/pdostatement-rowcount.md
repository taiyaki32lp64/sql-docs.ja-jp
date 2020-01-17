---
title: 'PDOStatement:: rowCount |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0569f26a-2376-4c20-8813-bd3c87d0ae9f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a9f6f7045c0729dad4fbb7d2875a645d370a1a5e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935991"
---
# <a name="pdostatementrowcount"></a>PDOStatement::rowCount
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

最後のステートメントでは、追加、削除、または変更された行数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
int PDOStatement::rowCount ();  
```  
  
## <a name="return-value"></a>戻り値  
追加、削除、または変更された行数。  
  
## <a name="remarks"></a>Remarks  
関連付けられた PDOStatement によって実行された最後の SQL ステートメントは SELECT ステートメントだったので、PDO::CURSOR_FWDONLY カーソルは -1 を返します。 PDO::CURSOR_SCROLLABLE カーソルは、結果セットの行数を返します。  
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
この例では、rowCount の 2 つの使用方法を示します。 1 つ目の rowCount は、テーブルに追加された行数を返します。 2 つ目の rowCount は、スクロール可能なカーソルを指定するときに、結果セットの行数を返すことができることを示します。  
  
```  
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$col1 = 'a';  
$col2 = 'b';  
  
$query = "insert into Table2(col1, col2) values(?, ?)";  
$stmt = $conn->prepare( $query );  
$stmt->execute( array( $col1, $col2 ) );  
print $stmt->rowCount();  
  
echo "\n\n";  
  
$con = null;  
$database = "AdventureWorks";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));  
$stmt->execute();  
print $stmt->rowCount();  
?>  
```  
  
## <a name="see-also"></a>参照  
[PDOStatement クラス](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
