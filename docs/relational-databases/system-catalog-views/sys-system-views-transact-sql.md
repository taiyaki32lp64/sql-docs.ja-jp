---
title: sys.system_views (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.system_views_TSQL
- system_views
- system_views_TSQL
- sys.system_views
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_views catalog view
ms.assetid: a526c410-e7b5-4075-8103-e1f3c6837c3c
author: stevestein
ms.author: sstein
ms.openlocfilehash: fce2816d8cb169c5761f47dd0f9dd0a6ed1959f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078613"
---
# <a name="syssystemviews-transact-sql"></a>sys.system_views (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  1 行に含まれる各システム ビューのデータを含む[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]します。 という名前のスキーマのすべてのシステム ビューが含まれている**sys**または**INFORMATION_SCHEMA**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|\<列を継承 >||このビューが継承する列の一覧は、次を参照してください。 [sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)します。|  
|**is_replicated**|**bit**|1 = ビューはレプリケートされます。|  
|**has_replication_filter**|**bit**|1 = ビューにレプリケーション フィルターがあります。|  
|**has_opaque_metadata**|**bit**|1 = ビューに VIEW_METADATA オプションが指定されています。 詳細については、「[CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)」を参照してください。|  
|**has_unchecked_assembly_data**|**bit**|1 = テーブルに、前回の ALTER ASSEMBLY で定義が変更されたアセンブリに依存する、持続データが含まれています。 次の成功した DBCC CHECKDB または DBCC CHECKTABLE の後に 0 にリセットされます。|  
|**with_check_option**|**bit**|1 = WITH CHECK OPTION がビュー定義に指定されています。|  
|**is_date_correlation_view**|**bit**|1 = ビューは、間の相関関係情報を格納するシステムによって自動的に作成された**datetime**列。 DATE_CORRELATION_OPTIMIZATION が ON に設定され、このビューの作成が有効になっています。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
  
