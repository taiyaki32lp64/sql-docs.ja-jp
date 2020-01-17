---
title: 'PDOStatement:: Cloセキュリティー + |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8997ab61-e948-4d54-8d32-fc080d55525c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: caf214fa7055bb0e8000f52f5db43c4f76e48e1b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993102"
---
# <a name="pdostatementclosecursor"></a>PDOStatement::closeCursor
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

カーソルを閉じて、もう一度実行するステートメントを有効にします。  
  
## <a name="syntax"></a>構文  
  
```  
  
bool PDOStatement::closeCursor();  
```  
  
## <a name="return-value"></a>戻り値  
成功した場合は true、それ以外の場合は false です。  
  
## <a name="remarks"></a>Remarks  
MultipleActiveResultSets 接続オプションが false に設定されている場合に、closeCursor は有効になります。  MultipleActiveResultSets 接続オプションの詳細については、「[方法: 複数のアクティブな結果セット (MARS) を無効にする](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)」を参照してください。  
  
closeCursor を呼び出す代わりに、ステートメント ハンドルを null に設定するだけでも同じことができます。  
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets' => false ) );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
$stmt2 = $conn->prepare('SELECT * FROM HumanResources.Department');  
  
$stmt->execute();  
  
$result = $stmt->fetch();  
print_r($result);  
  
$stmt->closeCursor();  
  
$stmt2->execute();  
$result = $stmt2->fetch();  
print_r($result);  
?>  
```  
  
## <a name="see-also"></a>参照  
[PDOStatement クラス](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
