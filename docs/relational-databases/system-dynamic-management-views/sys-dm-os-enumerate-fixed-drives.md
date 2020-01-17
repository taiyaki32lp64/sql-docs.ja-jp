---
title: dm_os_enumerate_fixed_drives (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/18/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_enumerate_fixed_drives
- sys.dm_os_enumerate_fixed_drives_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_enumerate_fixed_drives dynamic management view
ms.assetid: 2e27489e-cf69-4a89-9036-77723ac3de66
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fa5834c14bfb1fafe3123c28a60359d64d059dfc
ms.sourcegitcommit: c4875c097e3aae1b76233777d15e0a0ec8e0d681
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71342517"
---
# <a name="sysdm_os_enumerate_fixed_drives-transact-sql"></a>dm_os_enumerate_fixed_drives (Transact-sql)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

SQL Server 2019 で導入されました。

`C:\` のようなドライブ文字にマウントされているボリュームを列挙します。

|列名|データ型|[説明]|
|-----------------|---------------|-----------------|  
|`fixed_drive_path`|`nvarchar(512)`|ボリュームへのパス (`C:\`など)。|  
|`drive_type`|`int`|ドライブの種類のコード。 [`GetDriveTypeW` 関数](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew)を参照してください。|
|`drive_type_desc`|`nvarchar(512)`|ドライブの種類の説明。 [`GetDriveTypeW` 関数](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew)を参照してください。|
|`free_space_in_bytes`|`bigint`|ディスクの空き領域 (バイト単位)。|

## <a name="permissions"></a>アクセス許可

ユーザーは、サーバーに対して `VIEW SERVER STATE` の権限を持っている必要があります。

## <a name="see-also"></a>参照  

 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [I/O 関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
