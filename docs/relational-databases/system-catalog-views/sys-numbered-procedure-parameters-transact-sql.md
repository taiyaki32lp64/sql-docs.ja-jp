---
title: sys.numbered_procedure_parameters (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- numbered_procedure_parameters_TSQL
- sys.numbered_procedure_parameters_TSQL
- numbered_procedure_parameters
- sys.numbered_procedure_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.numbered_procedure_parameters catalog view
ms.assetid: a441d46d-1f30-41c2-8d94-e9442f59786e
author: stevestein
ms.author: sstein
ms.openlocfilehash: d07ca74ffb2b793038f230d2b3a5b265101a7eb8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102345"
---
# <a name="sysnumberedprocedureparameters-transact-sql"></a>sys.numbered_procedure_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  番号付きプロシージャのパラメーターごとに 1 つの行が含まれています。 番号付きストアド プロシージャを作成する場合は、ベース プロシージャの番号が 1 になり、 以降のプロシージャの番号は 2、3 のように続きます。 **sys.numbered_procedure_parameters**番号が 2 のすべての後続プロシージャのパラメーターの定義が含まれています以上。 このビューでは、ベース ストアド プロシージャ (番号 = 1) のパラメーターは示されません。 ベース ストアド プロシージャは、類似のストアド プロシージャに似ています。 そのため、そのパラメーターはで表されます[sys.parameters (TRANSACT-SQL)](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)します。  
  
> [!IMPORTANT]  
>  番号付きプロシージャは非推奨とされます。 番号付きプロシージャの使用はお勧めします。 このカタログ ビューを使用するクエリをコンパイルすると、DEPRECATION_ANNOUNCEMENT イベントが発生します。  
  
> [!NOTE]  
>  XML および CLR パラメーターは、番号付きプロシージャではサポートされていません。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|このパラメーターが所属するオブジェクトの ID。|  
|**procedure_number**|**smallint**|2 以上、オブジェクト内でこの手順の数。|  
|**name**|**sysname**|パラメーターの名前。 内で一意では、 **procedure_number**します。|  
|**parameter_id**|**int**|パラメーターの ID。 内で一意では、 **procedure_number**します。|  
|**system_type_id**|**tinyint**|パラメーターのシステム型の ID|  
|**user_type_id**|**int**|パラメーターのユーザーによって定義されている、型の ID。|  
|**max_length**|**smallint**|(バイト単位) のパラメーターの最大長。<br /><br /> -1 = 列のデータ型が varchar (max)、nvarchar (max)、または varbinary (max)。|  
|**有効桁数 (precision)**|**tinyint**|数値に基づく場合は、パラメーターの有効桁数それ以外の場合、0 を返します。|  
|**scale**|**tinyint**|数値に基づく場合は、パラメーターの小数点以下桁数それ以外の場合、0 を返します。|  
|**is_output**|**bit**|1 = パラメーターは出力または戻り値です。それ以外の場合は 0 です。|  
|**is_cursor_ref**|**bit**|1 = パラメーターはカーソル参照パラメーター。|  
  
> [!NOTE]  
>  XML および CLR パラメーターは、番号付きプロシージャではサポートされていません。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
