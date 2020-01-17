---
title: sqlsrv_configure |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_configure
apitype: NA
helpviewer_keywords:
- sqlsrv_configure
- API Reference, sqlsrv_configure
ms.assetid: 9393f975-a4ef-4c50-b4dd-14892fc55cc9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b98533dcc1589e07bc8ae37562bf6734077a78f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935805"
---
# <a name="sqlsrvconfigure"></a>sqlsrv_configure
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

エラー処理とログ記録のオプションの設定を変更します。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqlsrv_configure( string $setting, mixed $value )  
```  
  
#### <a name="parameters"></a>パラメーター  
*$setting*: 構成する設定の名前です。 設定の一覧については、次の表を参照してください。  
  
*$value*: *$setting* パラメーターで指定された設定に適用する値です。 このパラメーターに指定できる値は、指定されている設定によって異なります。 次の表に、考えられる組み合わせを示します。  
  
|設定|$value パラメーターに使用可能な値 (かっこ内と同等の整数)|既定値|  
|-----------|------------------------------------------------------------------------------|-----------------|  
|ClientBufferMaxKBSize<sup>1</sup>|PHP メモリの上限に達するまでの負以外の数値。<br /><br />ゼロおよび負の数値は許可できません。|10240 KB|  
|LogSeverity<sup>2</sup>|SQLSRV_LOG_SEVERITY_ALL (-1)<br /><br />SQLSRV_LOG_SEVERITY_ERROR (1)<br /><br />SQLSRV_LOG_SEVERITY_NOTICE (4)<br /><br />SQLSRV_LOG_SEVERITY_WARNING (2)|SQLSRV_LOG_SEVERITY_ERROR (1)|  
|LogSubsystems<sup>2</sup>|SQLSRV_LOG_SYSTEM_ALL (-1)<br /><br />SQLSRV_LOG_SYSTEM_CONN (2)<br /><br />SQLSRV_LOG_SYSTEM_INIT (1)<br /><br />SQLSRV_LOG_SYSTEM_OFF (0)<br /><br />SQLSRV_LOG_SYSTEM_STMT (4)<br /><br />SQLSRV_LOG_SYSTEM_UTIL (8)|SQLSRV_LOG_SYSTEM_OFF (0)|  
|WarningsReturnAsErrors<sup>3</sup>|**true** (1) または **false** (0)|**true** (1)|  
  
## <a name="return-value"></a>戻り値  
サポートされていない設定または値を使用して **sqlsrv_configure** 関数を呼び出すと、この関数は **false**を返します。 それ以外の場合は、 **true**を返します。  
  
## <a name="remarks"></a>Remarks  
(1) クライアント側クエリの詳細については、「[カーソルの種類 &#40;SQLSRV ドライバー&#41;](../../connect/php/cursor-types-sqlsrv-driver.md)」を参照してください。  
  
(2) ログ記録アクティビティの詳細については、「[アクティビティのログ記録](../../connect/php/logging-activity.md)」を参照してください。  
  
(3) エラーの設定および警告の処理の詳細については、「[方法: SQLSRV ドライバーを使用してエラーおよび警告処理を構成する](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)

[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md) 
  
