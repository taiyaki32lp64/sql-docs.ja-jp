---
title: 'PDO:: Getget-help Drivers |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: eab561e6-1229-401a-9482-008c23f9a4e6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 632663b813db9a8b9a5b425c717613c24fa58ad5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993260"
---
# <a name="pdogetavailabledrivers"></a>PDO::getAvailableDrivers
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PHP のインストールで PDO ドライバーの配列を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
array PDO::getAvailableDrivers ();  
```  
  
## <a name="return-value"></a>戻り値  
PDO ドライバーの一覧が格納された配列。  
  
## <a name="remarks"></a>Remarks  
PDO ドライバーの名前は、PDO インスタンスを作成するときに PDO::__construct で使用されます。  
  
PHP ドライバーで実行する場合、PDO::getAvailableDrivers は必要ありません。 このメソッドの詳細については、PHP ドキュメントを参照してください。  
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
  
```  
<?php  
print_r(PDO::getAvailableDrivers());  
?>  
```  
  
## <a name="see-also"></a>参照  
[PDO クラス](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
