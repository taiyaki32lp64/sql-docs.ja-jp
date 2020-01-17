---
title: sys.system_components_surface_area_configuration (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.system_components_surface_area_configuration_TSQL
- system_components_surface_area_configuration
- system_components_surface_area_configuration_TSQL
- sys.system_components_surface_area_configuration
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_components_surface_area_configuration catalog view
ms.assetid: d9920008-3387-4f9e-8f21-47473f2ba04f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 665e73b3cd072bfffc214c518d75d96af3591f94
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108871"
---
# <a name="syssystemcomponentssurfaceareaconfiguration-transact-sql"></a>sys.system_components_surface_area_configuration (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  または、有効なセキュリティの構成コンポーネントによって無効になっている実行可能なシステム オブジェクトごとに 1 つの行を返します。 詳細については、「 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**component_name**|**sysname**|コンポーネントの名前。 これにより、キーワード照合順序 Latin1_General_CI_AS_KS_WS があります。 NULL 値は許容されません。|  
|**database_name**|**sysname**|オブジェクトを含むデータベース。 これにより、キーワード照合順序 Latin1_General_CI_AS_KS_WS があります。 次のいずれかを指定する必要があります。<br /><br /> **master**<br /><br /> **msdb**<br /><br /> **mssqlsystemresource**|  
|**schema_name**|**sysname**|オブジェクトを含むスキーマです。 これにより、キーワード照合順序 Latin1_General_CI_AS_KS_WS があります。 NULL 値は許容されません。|  
|**object_name**|**sysname**|オブジェクト名。 これにより、キーワード照合順序 Latin1_General_CI_AS_KS_WS があります。 NULL 値は許容されません。|  
|**state**|**tinyint**|0 = 無効<br /><br /> 1 = 有効|  
|**type**|**char(2)**|オブジェクトの種類です。 次のいずれかになります。<br /><br /> P = SQL_STORED_PROCEDURE<br /><br /> PC = CLR_STORED_PROCEDURE<br /><br /> FN = SQL_SCALAR_FUNCTION<br /><br /> FS CLR_SCALAR_FUNCTION を =<br /><br /> FT = CLR_TABLE_VALUED_FUNCTION<br /><br /> IF SQL_INLINE_TABLE_VALUED_FUNCTION を =<br /><br /> TF SQL_TABLE_VALUED_FUNCTION を =<br /><br /> X EXTENDED_STORED_PROCEDURE を =|  
|**type_desc**|**nvarchar(60)**|オブジェクトの種類の説明をフレンドリ名です。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
