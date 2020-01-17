---
title: sys.partition_parameters (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- partition_parameters_TSQL
- partition_parameters
- sys.partition_parameters_TSQL
- sys.partition_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partition_parameters catalog view
ms.assetid: 2012ed9d-3ea3-4c29-9b78-dfa54a392dce
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 32fe257f14c1e085a43b4150ee933888a83d5d14
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125342"
---
# <a name="syspartitionparameters-transact-sql"></a>sys.partition_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  パーティション関数の各パラメーターの行を保持します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**function_id**|**int**|このパラメーターが属するパーティション関数の ID です。|  
|**parameter_id**|**int**|パラメーターの ID。 1 から始まるパーティション関数内で一意です。|  
|**system_type_id**|**tinyint**|パラメーターのシステム型の ID。 対応する、 **system_type_id**の列、 **sys.types**カタログ ビューです。|  
|**max_length**|**smallint**|(バイト単位) のパラメーターの最大長。|  
|**有効桁数 (precision)**|**tinyint**|数値に基づく場合は、パラメーターの有効桁数それ以外の場合、0 を返します。|  
|**scale**|**tinyint**|数値に基づく場合は、パラメーターの小数点以下桁数それ以外の場合、0 を返します。|  
|**collation_name**|**sysname**|文字ベース以外の場合、パラメーターの照合順序の名前それ以外の場合は NULL です。|  
|**user_type_id**|**int**|型の ID。 データベース内で一意です。 システム データ型、 **user_type_id** = **system_type_id**します。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [関数のカタログ ビューをパーティション分割&#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.partition_functions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_range_values &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)  
  
  
