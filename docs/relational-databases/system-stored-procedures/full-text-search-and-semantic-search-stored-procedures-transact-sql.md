---
title: フルテキスト検索およびセマンティック検索ストアド プロシージャ (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], stored procedures
- full-text search [SQL Server], stored procedures
- full-text catalogs [SQL Server], stored procedures
- system stored procedures [SQL Server], full-text search
ms.assetid: 0d185a16-2b16-4958-884f-efe675e2e551
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c0bf121cdb6007783cca682125dad04c01ab59ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942208"
---
# <a name="full-text-search-and-semantic-search-stored-procedures-transact-sql"></a>フルテキスト検索およびセマンティック検索ストアド プロシージャ (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 実装し、フルテキスト インデックスおよびセマンティック インデックスをクエリに使用される次のシステム ストアド プロシージャをサポートしています。  
  
## <a name="full-text-search-stored-procedures"></a>フルテキスト検索ストアド プロシージャ  
 [sp_fulltext_catalog](../../relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql.md)  
 フルテキスト カタログの作成と削除、およびカタログのインデックス作成の開始と中止を行います。 データベースごとに複数のフルテキスト カタログを作成できます。  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 使用[CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)、 [ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)、および[DROP FULLTEXT CATALOG](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)代わりにします。  
  
 [sp_fulltext_column](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)  
 テーブルの特定の列がフルテキスト インデックスに参加するかどうかを指定します。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md)代わりにします。  
  
 [sp_fulltext_database](../../relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql.md)  
 フルテキスト カタログにも何も起こりません[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]以降のバージョンとの下位互換性のみがサポートされます。  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 [sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)  
 ドキュメント識別子の間のマッピングを返します (**DocId**s) とフルテキスト キー値。  
  
 [sp_fulltext_load_thesaurus_file](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)  
 解析し、LCID に対応し、類義語辞典を使用して、フルテキスト クエリの再コンパイルする更新された類義語辞典ファイルからデータを読み込みます。  
  
 [sp_fulltext_pendingchanges](../../relational-databases/system-stored-procedures/sp-fulltext-pendingchanges-transact-sql.md)  
 保留中の挿入、更新、および削除の場合は、指定したテーブルを使用している変更の追跡など返しますが、変更にまだ処理されていません。  
  
 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)  
 SQL Server のフルテキスト検索のサーバーのプロパティを変更します。  
  
 [sp_fulltext_table](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)  
 フルテキスト インデックスに対してテーブルをマークしたりマークします。  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 使用[CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md)、 [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md)、および[DROP FULLTEXT INDEX](../../t-sql/statements/drop-fulltext-index-transact-sql.md)代わりにします。  
  
 [sp_help_fulltext_catalog_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalog-components-transact-sql.md)  
 現在のデータベースにあるすべてのフルテキスト カタログに使用されている、すべてのコンポーネント (フィルター、ワード ブレーカー、プロトコル ハンドラー) の一覧を返します。  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 [sp_help_fulltext_catalogs](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)  
 ID、名、ルート ディレクトリ、ステータス、および指定したフルテキスト カタログのフルテキスト インデックス付きテーブルの数を返します。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用して、 [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)カタログ ビューを代わりにします。  
  
 [sp_help_fulltext_catalogs_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)  
 カーソルを使用して、ID、名、ルート ディレクトリ、ステータス、および指定したフルテキスト カタログのフルテキスト インデックス付きテーブルの数を返します。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用して、 [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)カタログ ビューを代わりにします。  
  
 [sp_help_fulltext_columns](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)  
 フルテキスト インデックス作成用として指定された列を返します。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用して、 [sys.fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)カタログ ビューを代わりにします。  
  
 [sp_help_fulltext_columns_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)  
 カーソルを使用して、フルテキスト インデックス作成用に指定された列を返します。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用して、 [sys.fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)カタログ ビューを代わりにします。  
  
 [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
 データベースと、指定されたコンポーネントを使用しているフルテキスト カタログの識別子の一覧に加え、登録済みのワード ブレーカー、フィルター、およびプロトコル ハンドラーの情報を返します。  
  
 [sp_help_fulltext_tables](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)  
 フルテキスト インデックス作成のために登録されているテーブルの一覧を返します。  
  
 [sp_help_fulltext_tables_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)  
 フルテキスト インデックス作成のために登録されているテーブルの一覧を返します。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用して、 [sys.fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)カタログ ビューを代わりにします。  
  
## <a name="semantic-search-stored-procedures"></a>セマンティック検索ストアド プロシージャ  
 [sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の現在のインスタンスで、事前にデータが設定されているセマンティック言語統計データベースを登録します。  
  
 [sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql.md)  
 既存のセマンティック言語統計データベースの現在のインスタンスからの登録を解除します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]し、関連付けられているメタデータを削除します。  
  
## <a name="see-also"></a>関連項目  
 [フルテキスト検索およびセマンティック検索カタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/full-text-search-and-semantic-search-catalog-views-transact-sql.md)   
 [フルテキスト検索とセマンティック検索の動的管理ビューおよび関数&#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [フルテキスト検索](../../relational-databases/search/full-text-search.md)  
  
  
