---
title: sys.dm_os_host_info (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 02/10/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_os_host_info
- sys.dm_os_host_info_TSQL
- dm_os_host_info
- dm_os_host_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_host_info dynamic management view
ms.assetid: 9bb6ef86-957b-4ca1-ad20-ca2f8460a86d
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 052402d3a394e8da3e08828992127d3cd89b95ea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900158"
---
# <a name="sysdmoshostinfo-transact-sql"></a>sys.dm_os_host_info (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

オペレーティング システムのバージョン情報を表示する 1 つの行を返します。  
  
|列名 |データ型 |説明 |  
|-----------------|---------------|-----------------|  
|**host_platform** |**nvarchar (256)** |オペレーティング システムの種類:Windows または Linux |
|**host_distribution** |**nvarchar (256)** |オペレーティング システムの説明です。 |
|**host_release**|**nvarchar (256)**|[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows オペレーティング システムのリリース (バージョン番号)。 値と説明の一覧は、次を参照してください。[オペレーティング システムのバージョン (Windows)](/windows/desktop/SysInfo/operating-system-version)します。 <br> Linux の場合は、空の文字列を返します。 |  
|**host_service_pack_level**|**nvarchar (256)**|Windows オペレーティング システムの Service Pack のレベル。 <br> Linux の場合は、空の文字列を返します。 |  
|**host_sku**|**int**|Windows 在庫商品識別番号 (SKU) ID。 SKU Id と説明の一覧は、次を参照してください。 [GetProductInfo 関数](https://msdn.microsoft.com/library/ms724358.aspx)します。 NULL 値が許可されます。 <br> Linux の場合は、NULL を返します。 |  
|**os_language_version**|**int**|オペレーティング システムの Windows ロケール識別子 (LCID)。 LCID 値と説明の一覧は、次を参照してください。 [Microsoft によるロケール Id 割り当て](https://go.microsoft.com/fwlink/?LinkId=208080)します。 null にすることはできません。|  

## <a name="remarks"></a>コメント  
このビューに似ています[sys.dm_os_windows_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)、Windows および Linux を区別する列を追加します。
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
`SELECT`に対する権限`sys.dm_os_host_info`に付与されます、`public`既定ロール。 失効させた場合、以下の必要があります`VIEW SERVER STATE`サーバーに対する権限。   
 
> [!CAUTION]
>  以降のバージョンで[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]CTP 1.3、[!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)]バージョン 17 で必要な`SELECT`に対する権限`sys.dm_os_host_info`に接続するために[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]します。 場合`SELECT`から権限を取り消す`public`を持つログインだけ`VIEW SERVER STATE`アクセス許可は、最新バージョンの SSMS で接続できます。 (などの他のツール`sqlcmd.exe`しなくても接続できます`SELECT`に対する権限`sys.dm_os_host_info`)。

  
## <a name="examples"></a>使用例  
 次の例は、すべての列を返します、 **sys.dm_os_host_info**ビュー。  
  
```  
SELECT host_platform, host_distribution, host_release, 
    host_service_pack_level, host_sku, os_language_version  
FROM sys.dm_os_host_info;  
```  

結果セットでは、Windows のサンプルを次に示します。
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Windows   |Windows Server 2012 R2 Standard    |6.3    |   |7  |1033 |  

結果セットを Linux 上のサンプルを次に示します。
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Linux |Ubuntu |16.04  |   |NULL   |1033 |  

  
## <a name="see-also"></a>参照  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_windows_info (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)  
 

