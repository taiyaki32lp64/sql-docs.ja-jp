---
title: sys.types (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- types
- types_TSQL
- sys.types_TSQL
- sys.types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.types catalog view
- table-valued parameters,sys.types
ms.assetid: a5dbc842-71a0-4f62-b5e0-f560a99b7f8c
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ff4cd58fcd7d11679cf410c9f379b101d42ce4bf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095572"
---
# <a name="systypes-transact-sql"></a>sys.types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  システム型とユーザー定義の型ごとに 1 行のデータを格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|型の名前。 スキーマ内で一意です。|  
|**system_type_id**|**tinyint**|型の内部システム型の ID。|  
|**user_type_id**|**int**|型の ID。 データベース内で一意です。 システム データ型、 **user_type_id** = **system_type_id**します。|  
|**schema_id**|**int**|型が所属するスキーマの ID。|  
|**principal_id**|**int**|スキーマの所有者と異なる場合は、個々 の所有者の ID。 既定では、スキーマに含まれるオブジェクトは、スキーマの所有者によって所有されます。 ただし、所有権を変更する ALTER AUTHORIZATION ステートメントを使用して、別の所有者を指定できます。<br /><br /> 別の所有者がいない場合は NULL になります。|  
|**max_length**|**smallint**|型のバイト単位で最大長。<br /><br /> -1 = 列のデータ型は**varchar (max)** 、 **nvarchar (max)** 、 **varbinary (max)** 、または**xml**します。<br /><br /> **テキスト**、列、 **max_length**値は 16 になります。|  
|**precision**|**tinyint**|型の数値に基づく場合の最大有効桁数それ以外の場合、0 を返します。|  
|**scale**|**tinyint**|型の数値に基づく場合の最大スケールそれ以外の場合、0 を返します。|  
|**collation_name**|**sysname**|文字ベース以外の場合、型の照合順序の名前その他の賢明では、NULL。|  
|**is_nullable**|**bit**|型は、null 値は。|  
|**is_user_defined**|**bit**|1 = ユーザー定義型です。<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム データ型。|  
|**is_assembly_type**|**bit**|1 = 型の実装は CLR アセンブリで定義します。<br /><br /> 0 = 型はに基づいて、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]システム データ型。|  
|**default_object_id**|**int**|使用して、型にバインドされているスタンドアロンの既定の ID [sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)します。<br /><br /> 0 = 既定値が存在します。|  
|**rule_object_id**|**int**|使用して、型にバインドされているスタンドアロン ルールの ID [sp_bindrule](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)します。<br /><br /> 0 = ルールは存在しません。|  
|**is_table_type**|**bit**|型がテーブルであることを示します。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [スカラー型カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよくあるご質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
