---
title: sys.identity_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- identity_columns
- sys.identity_columns
- sys.identity_columns_TSQL
- identity_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.identity_columns catalog view
ms.assetid: 97ee01e6-9c9e-4fd9-884b-68b4084669d5
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 49684671c25ea83fa7554bec7f80d0b16c30d4eb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122715"
---
# <a name="sysidentitycolumns-transact-sql"></a>sys.identity_columns (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Id 列である各列の行が含まれています。  
  
 **Sys.identity_columns**ビューから行を継承する、 **sys.columns**ビュー。 **Sys.identity_columns**ビュー内の列を返します、 **sys.columns**ビューだけでなく、 **seed_value**、 **increment_value**、 **last_value**、および**is_not_for_replication**列。 詳細については、「[カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<sys.columns から継承された列 >**||**Sys.identity_columns**ビューは、すべての列を返します、 **sys.columns**ビュー。 以下に示す追加の列も返します。 列の説明を**sys.identity_columns**ビューが継承**sys.columns**を参照してください[sys.columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)します。|  
|**seed_value**|**sql_variant**|この id 列のシード値。 シード値のデータ型は、列自体のデータ型の場合と同じです。|  
|**increment_value**|**sql_variant**|この ID 列に対する増分値です。 シード値のデータ型は、列自体のデータ型の場合と同じです。|  
|**last_value**|**sql_variant**|この id 列に対して生成された最後の値。 シード値のデータ型は、列自体のデータ型の場合と同じです。|  
|**is_not_for_replication**|**bit**|Id 列は NOT FOR REPLICATION で宣言されています。|  
  
> [!NOTE]  
>  複数のテーブルで使用できる自動的に増分する番号、またはテーブルを参照せずにアプリケーションから呼び出すことができる自動的に増分する番号を作成するには、「[シーケンス番号](../../relational-databases/sequence-numbers/sequence-numbers.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよくあるご質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
