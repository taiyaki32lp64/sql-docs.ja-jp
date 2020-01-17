---
title: resource_governor_configuration (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_configuration_TSQL
- sys.resource_governor_configuration
- resource_governor_configuration_TSQL
- resource_governor_configuration
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor_configuration catalog view
ms.assetid: 89099668-1dc6-4b07-9d8b-49bc95c7bfc0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8e4068d9763460995335fe5adbd6684ecb70d8b7
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982615"
---
# <a name="sysresource_governor_configuration-transact-sql"></a>sys.resource_governor_configuration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  格納されている Resource Governor 状態を返します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|classifier_function_id|**int**|メタデータに格納されている分類子関数の ID。 NULL 値は許可されません。<br /><br /> **メモ**この関数は、新しいセッションを分類し、ルールを使用してワークロードを適切なワークロードグループにルーティングするために使用されます。 詳細については、「[リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)」を参照してください。|  
|is_enabled|**bit**|リソース ガバナーの現在の状態を示します。<br /><br /> 0 = Resource Governor が有効になっていません。<br /><br /> 1 = Resource Governor が有効になっています。<br /><br /> NULL 値は許可されません。|  
|max_outstanding_io_per_volume|**int**|**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。<br /><br /> ボリュームごとの未処理の I/O の最大数。|  
  
## <a name="remarks"></a>Remarks  
 カタログ ビューには、メタデータに格納されているリソース ガバナー構成が表示されます。 メモリ内の構成を表示するには、対応する動的管理ビューを使用します。  
  
## <a name="permissions"></a>アクセス許可  
 内容を表示するには VIEW ANY DEFINITION 権限が必要です。内容を変更するには CONTROL SERVER 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、格納されているメタデータ値と Resource Governor 構成のメモリ内の値を取得して比較する方法を示します。  
  
```  
USE master;  
GO  
-- Get the stored metadata.  
SELECT   
object_schema_name(classifier_function_id) AS 'Classifier UDF schema in metadata',   
object_name(classifier_function_id) AS 'Classifier UDF name in metadata'  
FROM   
sys.resource_governor_configuration;  
GO  
-- Get the in-memory configuration.  
SELECT   
object_schema_name(classifier_function_id) AS 'Active classifier UDF schema',   
object_name(classifier_function_id) AS 'Active classifier UDF name'  
FROM   
sys.dm_resource_governor_configuration;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Resource Governor カタログビュー &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [dm_resource_governor_configuration &#40;transact-sql&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql.md)   
 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)  
  
  
