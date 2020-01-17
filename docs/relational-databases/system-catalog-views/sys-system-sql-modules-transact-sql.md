---
title: sys.system_sql_modules (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- system_sql_modules_TSQL
- sys.system_sql_modules
- sys.system_sql_modules_TSQL
- system_sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_sql_modules catalog view
ms.assetid: ad3548bc-4780-4821-b962-b421d52daed9
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fe249cd389e71fa5565e2877fba46b47cf0a4f38
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108782"
---
# <a name="syssystemsqlmodules-transact-sql"></a>sys.system_sql_modules (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  SQL 言語定義モジュールを含むシステム オブジェクトごとに 1 行のデータを返します。 システム オブジェクト、P、PC、TF、V、関連する SQL モジュールがある場合に、FN を入力します。 親オブジェクトを識別するにはこのビューに参加できる[sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|親オブジェクト、データベース内で一意のオブジェクト id 番号。|  
|**definition**|**nvarchar(max)**|このモジュールを定義する SQL テキスト。|  
|**uses_ansi_nulls**|**bit**|1 = モジュールは、SET ANSI_NULLS データベース オプションを ON に作成されました。<br /><br /> 常に 1 を返します。|  
|**uses_quoted_identifier**|**bit**|1 = モジュールは、SET QUOTED_IDENTIFIER ON の状態で作成されました。<br /><br /> 常に 1 を返します。|  
|**is_schema_bound**|**bit**|0 = モジュールは、SCHEMABINDING オプションでは作成されませんでした。<br /><br /> 常に 0 を返します。|  
|**uses_database_collation**|**bit**|0 = モジュールは、データベースの既定の照合順序に依存していません。<br /><br /> 常に 0 を返します。|  
|**is_recompiled**|**bit**|0 = プロシージャは、WITH RECOMPILE オプションを使って作成されませんでした。<br /><br /> 常に 0 を返します。|  
|**null_on_null_input**|**bit**|0 = モジュールは、任意の NULL 入力に対して NULL 出力を生成するために作成されませんでした。<br /><br /> 常に 0 を返します。|  
|**execute_as_principal_id**|**int**|常に NULL を返します|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.all_sql_modules &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-sql-modules-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [オブジェクト カタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
