---
title: PDO クラス |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c77b68d-0649-44af-96fa-586cbb319f5f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b016d850286daf0c2cda9604302d78faa6cc6ae1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936284"
---
# <a name="pdo-class"></a>PDO クラス
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO クラスには、PHP アプリケーションが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続できるようにするメソッドが含まれています。  
  
## <a name="syntax"></a>構文  
  
```  
  
PDO {}  
```  
  
## <a name="remarks"></a>Remarks  
PDO クラスには次のメソッドが含まれています。  
  
[PDO::__construct](../../connect/php/pdo-construct.md)  

[PDO::beginTransaction](../../connect/php/pdo-begintransaction.md)  
  
[PDO::commit](../../connect/php/pdo-commit.md)  
  
[PDO::errorCode](../../connect/php/pdo-errorcode.md)  
  
[PDO::errorInfo](../../connect/php/pdo-errorinfo.md)  
  
[PDO::exec](../../connect/php/pdo-exec.md)  
  
[PDO::getAttribute](../../connect/php/pdo-getattribute.md)  
  
[PDO::getAvailableDrivers](../../connect/php/pdo-getavailabledrivers.md)  
  
[PDO::lastInsertId](../../connect/php/pdo-lastinsertid.md)  
  
[PDO::prepare](../../connect/php/pdo-prepare.md)  
  
[PDO::query](../../connect/php/pdo-query.md)  
  
[PDO::quote](../../connect/php/pdo-quote.md)  
  
[PDO::rollback](../../connect/php/pdo-rollback.md)  
  
[PDO::setAttribute](../../connect/php/pdo-setattribute.md)  
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="see-also"></a>参照  
[PDO_SQLSRV ドライバー リファレンス](../../connect/php/pdo-sqlsrv-driver-reference.md)

[Microsoft SQL Server 用 Drivers for PHP の概要](../../connect/php/overview-of-the-php-sql-driver.md)

[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server の概要](../../connect/php/getting-started-with-the-php-sql-driver.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
