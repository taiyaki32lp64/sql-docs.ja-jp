---
title: 'PDO:: errorInfo |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9d5481d5-13bc-4388-b3aa-78676c0fc709
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fe0f0cc2ec15fcdb871f290f03565482a8477995
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936268"
---
# <a name="pdoerrorinfo"></a>PDO::errorInfo
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

データベース ハンドルの最新の操作のエラーの詳細情報を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
array PDO::errorInfo();  
```  
  
## <a name="return-value"></a>戻り値  
データベース ハンドルの最新の操作に関するエラー情報の配列。 配列は、次のフィールドで構成されます。  
  
-   SQLSTATE エラー コード。  
  
-   ドライバー固有のエラー コード。  
  
-   ドライバー固有のエラー メッセージ。  
  
エラーがない場合、または SQLSTATE が設定されていない場合、ドライバー固有のフィールドは NULL になります。  
  
## <a name="remarks"></a>Remarks  
PDO::errorInfo は、データベースで直接実行された操作のエラー情報だけを取得します。 PDO::prepare または PDO::query を使用して PDOStatement インスタンスを作成する場合は、PDOStatement::errorInfo を使用します。  
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
この例では、列の名前が間違っており (`City` ではなく `Cityx`)、エラーが発生します。そのエラーは報告されます。  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
echo "\n";  
print_r ($conn->errorInfo());  
?>  
```  
  
## <a name="see-also"></a>参照  
[PDO クラス](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
