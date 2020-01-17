---
title: 'PDO:: beginTransaction |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4d5db438-9df7-4d22-9907-3ddc63bd2220
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 739565ae633140cef7d0df6531b6adfd6389d1e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993305"
---
# <a name="pdobegintransaction"></a>PDO::beginTransaction
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

自動コミット モードをオフにしてトランザクションを開始します。  
  
## <a name="syntax"></a>構文  
  
```  
  
bool PDO::beginTransaction();  
```  
  
## <a name="return-value"></a>戻り値  
メソッドの呼び出しに成功した場合は true、それ以外の場合は false。  
  
## <a name="remarks"></a>Remarks  
PDO::beginTransaction で開始されたトランザクションは、[PDO::commit](../../connect/php/pdo-commit.md) または [PDO::rollback](../../connect/php/pdo-rollback.md) が呼び出されたときに終了します。  
  
PDO::beginTransaction は PDO::ATTR_AUTOCOMMIT の値によって影響を受けず、PDO::ATTR_AUTOCOMMIT の値に影響を与えません。  
  
前の PDO::beginTransaction が PDO::rollback または PDO::commit で終了する前に PDO::beginTransaction を呼び出すことはできません。  
  
このメソッドが失敗した場合、接続は自動コミット モードに戻ります。  
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
次の例では、「Test」という名前のデータベースと「Table1」という名前のテーブルを使用します。 トランザクションを開始し、コマンドを発行して 2 つの行を追加し、1 つの行を削除します。 コマンドはデーダースに送信され、トランザクションは `PDO::commit`で明示的に終了します。  
  
```  
<?php  
   $conn = new PDO( "sqlsrv:server=(local); Database = Test", "", "");  
   $conn->beginTransaction();  
   $ret = $conn->exec("insert into Table1(col1, col2) values('a', 'b') ");  
   $ret = $conn->exec("insert into Table1(col1, col2) values('a', 'c') ");  
   $ret = $conn->exec("delete from Table1 where col1 = 'a' and col2 = 'b'");  
   $conn->commit();  
   // $conn->rollback();  
   echo $ret;  
?>  
```  
  
## <a name="see-also"></a>参照  
[PDO クラス](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
