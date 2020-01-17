---
title: sqlsrv_get_config |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_get_config
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_get_config
- sqlsrv_get_config
ms.assetid: ce2befc2-af98-45bb-8d41-60f1674dccfc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f94c20c8aa6cf603c6588586e072813682b2ce68
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992703"
---
# <a name="sqlsrvgetconfig"></a>sqlsrv_get_config
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

指定された構成設定の現在の値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqlsrv_get_config( string $setting )  
```  
  
#### <a name="parameters"></a>パラメーター  
*$setting*: 値を返す構成設定。 構成可能な設定の一覧については、「 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md)」を参照してください。  
  
## <a name="return-value"></a>戻り値  
*$setting* パラメーターで指定された設定の値。 無効な設定を指定した場合は、 **false** が返されて、エラーがエラー コレクションに追加されます。  
  
## <a name="remarks"></a>Remarks  
**false** が **sqlsrv_get_config** によって返された場合は、[sqlsrv_errors](../../connect/php/sqlsrv-errors.md) を呼び出して、エラーが発生したかどうか、または **false** が *$setting* パラメーターで指定した設定の値かどうかを、判定する必要があります。  
  
## <a name="see-also"></a>参照  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  

[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)  

[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)  
  
