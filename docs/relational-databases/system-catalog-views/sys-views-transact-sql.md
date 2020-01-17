---
title: sys.views (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- views_TSQL
- views
- sys.views_TSQL
- sys.views
dev_langs:
- TSQL
helpviewer_keywords:
- sys.views catalog view
ms.assetid: f8a8ea39-5a09-4662-801e-b43519467def
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f5f7d4c9c6bb44d978007170abfff5a7730b028a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095529"
---
# <a name="sysviews-transact-sql"></a>sys.views (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  各ビュー オブジェクトの行を含む**sys.objects.type** V を = です。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<列を継承 >**||このビューが継承する列の一覧は、次を参照してください[sys.objects &#40;TRANSACT-SQL。&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)|  
|**is_replicated**|**bit**|1 = ビューはレプリケートされます。|  
|**has_replication_filter**|**bit**|1 = ビューにレプリケーション フィルターがあります。|  
|**has_opaque_metadata**|**bit**|1 = ビューに VIEW_METADATA オプションが指定されています。 詳細については、「[CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)」を参照してください。|  
|**has_unchecked_assembly_data**|**bit**|1 = ビューには、前回の ALTER ASSEMBLY 中にその定義が変更されたアセンブリに依存する持続データが含まれています。 このデータは、DBCC CHECKDB または DBCC CHECKTABLE が次回正常に終了した後、0 にリセットされます。|  
|**with_check_option**|**bit**|1 = WITH CHECK OPTION がビュー定義に指定されています。|  
|**is_date_correlation_view**|**bit**|1 = システムによって、datetime 列間の相関関係情報を格納するビューが自動的に作成されました。 DATE_CORRELATION_OPTIMIZATION が ON に設定され、このビューの作成が有効になっています。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよくあるご質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
