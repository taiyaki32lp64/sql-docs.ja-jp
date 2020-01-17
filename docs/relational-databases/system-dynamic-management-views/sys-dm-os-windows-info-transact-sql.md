---
title: sys.dm_os_windows_info (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_windows_info
- dm_os_windows_info_TSQL
- sys.dm_os_windows_info
- sys.dm_os_windows_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_windows_info dynamic management view
ms.assetid: adc81283-fdc2-46c0-bb48-abe82bbf2459
author: stevestein
ms.author: sstein
ms.openlocfilehash: d25713ba8fb298ce465910eae786befb710961d7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899592"
---
# <a name="sysdmoswindowsinfo-transact-sql"></a>sys.dm_os_windows_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Windows オペレーティング システムのバージョン情報を示す 1 行のデータを返します。  
  
  Windows で実行されている SQL Server にのみ適用されます。 Linux などの非 Windows ホストで実行されている SQL Server のような情報を表示する使用[sys.dm_os_host_info &#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)します。 
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**windows_release**|**nvarchar (256)**|Windows では、リリース番号を返します。 値と説明の一覧は、次を参照してください。[オペレーティング システムのバージョン (Windows)](/windows/desktop/SysInfo/operating-system-version)します。 NULL 値は許容されません。|  
|**windows_service_pack_level**|**nvarchar (256)**| Windows では、サービス パック番号を返します。 NULL 値は許容されません。 |  
|**windows_sku**|**int**|Windows、Windows 在庫管理単位 (SKU) ID を返します SKU Id と説明の一覧は、次を参照してください。 [GetProductInfo 関数](https://msdn.microsoft.com/library/ms724358.aspx)します。 Null 値は。 |  
|**os_language_version**|**int**| Windows では、オペレーティング システムの Windows ロケール識別子 (LCID) を返します。 LCID 値と説明の一覧は、次を参照してください。 [Microsoft によるロケール Id 割り当て](https://go.microsoft.com/fwlink/?LinkId=208080)します。 NULL 値は許容されません。|  
  
  
## <a name="permissions"></a>アクセス許可  
Sys.dm_os_windows_info に対する SELECT 権限は、既定では、public ロールに付与されます。 失効させた場合、サーバーに対する VIEW SERVER STATE 権限が必要です。  

## <a name="limitations-and-restrictions"></a>制限事項と制約事項
Linux などの非 Windows ホストで実行されている SQL の情報を表示する使用[sys.dm_os_host_info &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)します。 
  
## <a name="examples"></a>使用例  
 次の例は、すべての列を返します、 **sys.dm_os_windows_info**ビュー。  
  
```  
SELECT windows_release, windows_service_pack_level, windows_sku, os_language_version  
FROM sys.dm_os_windows_info;  
```  
  
 次に結果セットの例を示します。  
  
 `windows_release  windows_service_pack_level   windows_sku   os_language_version`  
  
 `---------------  ---------------------------  ------------  -------------------`  
  
 `6.0              Service Pack 2                4            1033`  
  
## <a name="see-also"></a>参照  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_host_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)  
  
  

