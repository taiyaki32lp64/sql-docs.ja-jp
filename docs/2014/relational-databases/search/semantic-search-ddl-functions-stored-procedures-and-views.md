---
title: セマンティック検索の DDL、関数、ストアド プロシージャ、およびビュー | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], database objects
ms.assetid: 182f395f-3168-48a4-b723-ef4403544f9f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ee5cf7136739b012615121e00d8b8d3ed7c7c6ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011035"
---
# <a name="semantic-search-ddl-functions-stored-procedures-and-views"></a>セマンティック検索の DDL、関数、ストアド プロシージャ、およびビュー
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の統計的セマンティック検索をサポートする Transact-SQL ステートメントおよびデータベース オブジェクトの一覧を示します。  
  
 フルテキスト検索をサポートするステートメントおよびデータベース オブジェクトの一覧については、「 [フルテキスト検索の DDL、関数、ストアド プロシージャ、およびビュー](../views/views.md)」を参照してください。  
  
##  <a name="ddl"></a> Transact-SQL データ定義言語 (DDL) ステートメント  
  
|オブジェクト|詳細情報|  
|------------|----------------------|  
|[ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)|[テーブルおよび列に対するセマンティック検索の有効化](enable-semantic-search-on-tables-and-columns.md)|  
|[CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)|[テーブルおよび列に対するセマンティック検索の有効化](enable-semantic-search-on-tables-and-columns.md)|  
  
##  <a name="func"></a> システム関数  
  
|オブジェクト|詳細情報|  
|------------|----------------------|  
|[semantickeyphrasetable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql)|[セマンティック検索を使用したドキュメント内のキー フレーズの検索](find-key-phrases-in-documents-with-semantic-search.md)|  
|[semanticsimilaritydetailstable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql)|[セマンティック検索による類似および関連したドキュメントの取得](find-similar-and-related-documents-with-semantic-search.md)|  
|[semanticsimilaritytable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql)|[セマンティック検索による類似および関連したドキュメントの取得](find-similar-and-related-documents-with-semantic-search.md)|  
  
##  <a name="meta"></a> システム メタデータ関数  
  
|オブジェクト|詳細情報|  
|------------|----------------------|  
|[COLUMNPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/columnproperty-transact-sql)|[テーブルおよび列に対するセマンティック検索の有効化](enable-semantic-search-on-tables-and-columns.md)|  
|[DATABASEPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/databasepropertyex-transact-sql)|[テーブルおよび列に対するセマンティック検索の有効化](enable-semantic-search-on-tables-and-columns.md)|  
|[FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)|[セマンティクス検索の管理および監視](manage-and-monitor-semantic-search.md)|  
|[INDEXPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/indexproperty-transact-sql)|[セマンティック検索の管理および監視](manage-and-monitor-semantic-search.md)|  
|[OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)|[テーブルおよび列に対するセマンティック検索の有効化](enable-semantic-search-on-tables-and-columns.md)|  
|[SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)|[セマンティック検索のインストールと構成](install-and-configure-semantic-search.md)|  
  
##  <a name="sproc"></a> システム ストアド プロシージャ  
  
|オブジェクト|詳細情報|  
|------------|----------------------|  
|[sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql)|[セマンティック検索のインストールと構成](install-and-configure-semantic-search.md)|  
|[sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql)|[セマンティック検索のインストールと構成](install-and-configure-semantic-search.md)|  
  
##  <a name="cv"></a> システム ビュー - カタログ ビュー  
  
|オブジェクト|詳細情報|  
|------------|----------------------|  
|[sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)|[セマンティック検索の管理および監視](manage-and-monitor-semantic-search.md)|  
|[sys.fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql)|[セマンティック検索のインストールと構成](install-and-configure-semantic-search.md)|  
|[sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql)|[セマンティック検索のインストールと構成](install-and-configure-semantic-search.md)|  
  
##  <a name="dmv"></a> システム ビュー - 動的管理ビュー  
  
|オブジェクト|詳細情報|  
|------------|----------------------|  
|[sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql)|[セマンティック検索の管理および監視](manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_index_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)|[セマンティック検索の管理および監視](manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql)|[セマンティック検索の管理および監視](manage-and-monitor-semantic-search.md)|  
  
## <a name="see-also"></a>関連項目  
 [セマンティック検索の管理および監視](manage-and-monitor-semantic-search.md)  
  
  
