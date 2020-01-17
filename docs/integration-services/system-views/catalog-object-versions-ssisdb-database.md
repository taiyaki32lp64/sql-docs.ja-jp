---
title: catalog.object_versions (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 2fd8c020-1c77-4702-8e6b-efa6a348daab
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7dac194c0ceb54eeb716b9cf5ec676e7fe120d8f
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296515"
---
# <a name="catalogobject_versions-ssisdb-database"></a>catalog.object_versions (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのオブジェクトのバージョンを示します。 このリリースでは、プロジェクトのバージョンのみがこのビューでサポートされます。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|object_version_lsn|**bigint**|オブジェクト バージョンの一意識別子 (ID)。 この番号は、シーケンシャルを保証するものではありません。|  
|object_id|**bigint**|オブジェクトの一意の ID。|  
|object_type|**smallint**|オブジェクトの種類。 プロジェクトには、値 `20` が表示されます。|  
|object_name|**sysname(nvarchar(128))**|オブジェクトの名前。|  
|description|**nvarchar(1024)**|プロジェクトの説明。|  
|created_by|**nvarchar(128)**|オブジェクトをカタログに追加したユーザーの名前。|  
|created_time|**datetimeoffset**|オブジェクトがカタログに追加された日時。|  
|restored_by|**nvarchar(128)**|オブジェクトを復元したユーザーの名前。|  
|last_restored_time|**datetimeoffset**|オブジェクトが前回復元された日時。|  
  
## <a name="remarks"></a>Remarks  
 このビューは、カタログの各オブジェクトの行を表示します。  
  
## <a name="permissions"></a>アクセス許可  
 このビュー内の行を表示するには、次のアクセス権限のいずれかが必要です。  
  
-   オブジェクトの READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
> [!NOTE]  
>  行レベルのセキュリティが適用されるため、表示する権限がある行のみが表示されます。  
  
  
