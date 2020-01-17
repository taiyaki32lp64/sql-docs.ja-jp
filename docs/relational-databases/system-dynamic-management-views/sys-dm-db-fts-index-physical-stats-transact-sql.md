---
title: sys.dm_db_fts_index_physical_stats (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_fts_index_physical_stats_TSQL
- dm_db_fts_index_physical_stats
- dm_db_fts_index_physical_stats_TSQL
- sys.dm_db_fts_index_physical_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_fts_index_physical_stats dynamic management view
ms.assetid: 997c3278-3630-47f6-ada3-190b6c16ce0e
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4394483cd17510c998126a70c12f4d669c9282aa
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264494"
---
# <a name="sysdm_db_fts_index_physical_stats-transact-sql"></a>sys.dm_db_fts_index_physical_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  フルテキスト インデックスまたはセマンティック インデックスを関連付けられている各テーブル内のフルテキスト インデックスまたはセマンティック インデックスごとに 1 行のデータを返します。  
  
||||  
|-|-|-|  
|**列名**|**型**|**[説明]**|  
|**object_id**|int|インデックスを含むテーブルのオブジェクト ID。|  
|**fulltext_index_page_count**|**bigint**|インデックス ページの数で表された、抽出の論理サイズ。|  
|**keyphrase_index_page_count**|**bigint**|インデックス ページの数で表された、抽出の論理サイズ。|  
|**similarity_index_page_count**|**bigint**|インデックス ページの数で表された、抽出の論理サイズ。|  
  
## <a name="general-remarks"></a>全般的な解説  
 詳細については、次を参照してください。[モニター セマンティック検索の管理と](../../relational-databases/search/manage-and-monitor-semantic-search.md)します。  
  
## <a name="metadata"></a>メタデータ  
 セマンティック インデックス作成の状態の詳細については、次の動的管理ビューに対してクエリを実行してください。  
  
-   [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   

## <a name="examples"></a>使用例  
 次の例では、フルテキスト インデックスまたはセマンティック インデックスを関連付けられているすべてのテーブル内の各フルテキスト インデックスまたはセマンティック インデックスの論理サイズについてクエリを実行する方法を示しています。  
  
```  
SELECT * FROM sys.dm_db_fts_index_physical_stats;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [セマンティック検索の管理および監視](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
  
  
