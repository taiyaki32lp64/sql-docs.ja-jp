---
title: セマンティクス検索の管理および監視 | Microsoft Docs
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], managing
- semantic search [SQL Server], monitoring
ms.assetid: eb5c3b29-da70-42aa-aa97-7d35a3f1eb98
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: c5e5c8256c117ebd3fbb57b5a7c291b539c5a428
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132251"
---
# <a name="manage-and-monitor-semantic-search"></a>セマンティクス検索の管理および監視
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  セマンティック インデックス作成プロセスと、インデックスの管理および監視に関連するタスクについて説明します。  
  
##  <a name="HowToMonitorStatus"></a> セマンティック インデックス作成の状態の確認  
### <a name="is-the-first-phase-of-semantic-indexing-complete"></a>セマンティック インデックス作成の最初のフェーズは完了していますか?
 動的管理ビュー [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md) に対してクエリを実行し、**status** 列と **status_description** 列を確認します。  
  
 インデックス作成の最初のフェーズでは、フルテキスト キーワード インデックスおよびセマンティック キー フレーズ インデックスの作成のほか、ドキュメンの類似性データの抽出が行われます。  
  
```sql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_index_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
### <a name="is-the-second-phase-of-semantic-indexing-complete"></a>セマンティック インデックス作成の 2 番目のフェーズは完了していますか?
 動的管理ビュー [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md) に対してクエリを実行し、**status** 列と **status_description** 列を確認します。  
  
 インデックス作成の 2 番目のフェーズには、ドキュメントの類似性に関するセマンティック インデックスの作成が含まれます。  
  
```wql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_semantic_similarity_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
##  <a name="HowToCheckSize"></a> セマンティック インデックスのサイズの確認  
### <a name="what-is-the-logical-size-of-a-semantic-key-phrase-index-or-a-semantic-document-similarity-index"></a>セマンティック キー フレーズ インデックスまたはドキュメントの類似性に関するセマンティック インデックスの論理サイズは?
 動的管理ビュー [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md) に対してクエリを実行します。  
  
 論理サイズは、インデックス ページの数で表示されます。  
  
```sql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_db_fts_index_physical_stats WHERE object_id = OBJECT_ID('table_name')  
GO  
```  
  
### <a name="what-is-the-total-size-of-the-full-text-and-semantic-indexes-for-a-full-text-catalog"></a>フルテキスト カタログのフルテキスト インデックスとセマンティック インデックスの合計サイズは?  
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md) メタデータ関数の **IndexSize** プロパティに対してクエリを実行します。  
  
```sql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'IndexSize')  
GO  
```  
  
### <a name="how-many-items-are-indexed-in-the-full-text-and-semantic-indexes-for-a-full-text-catalog"></a>フルテキスト カタログのフルテキスト インデックスおよびセマンティック インデックスでインデックス化されているアイテム数は?  
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md) メタデータ関数の **ItemCount** プロパティに対してクエリを実行します。  
  
```sql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'ItemCount')  
GO  
```  
  
##  <a name="HowToForcePopulation"></a> セマンティック インデックスの強制的な作成  
 START/STOP/PAUSE 句または RESUME POPULATION 句を使用して、フルテキスト インデックスおよびセマンティック インデックスを強制的に作成できます (これらの句の構文と動作については、フルテキスト インデックスに関する説明に示されています)。 詳細については、「[ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)」および「[フルテキスト インデックスの作成](../../relational-databases/search/populate-full-text-indexes.md)」を参照してください。  
  
 セマンティック インデックス作成はフルテキスト インデックス作成に依存しているため、セマンティック インデックスは関連するフルテキスト インデックスが作成されたときにのみ作成されます。  
  
 **例:フルテキスト インデックスとセマンティック インデックスの完全作成を開始する**  
  
 次の例では、AdventureWorks2012 サンプル データベースの **Production.Document** テーブルの既存のフルテキスト インデックスを変更することにより、フルテキスト インデックスとセマンティック インデックスの両方の完全作成を開始します。  
  
```vb  
USE AdventureWorks2012  
GO  
  
ALTER FULLTEXT INDEX ON Production.Document  
    START FULL POPULATION  
GO  
```  
  
##  <a name="HowToDisableIndexing"></a> セマンティック インデックスの作成の無効化または再有効化  
 ENABLE/DISABLE 句を使用して、フルテキスト インデックスまたはセマンティック インデックスの作成を有効または無効にすることができます (これらの句の構文と動作については、フルテキスト インデックスに関する説明に示されています)。 詳細については、「[ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)」を参照してください。  
  
 セマンティック インデックスの作成が無効化または中断された後でもセマンティック データに対するクエリは正常に動作し、以前にインデックスが作成されたデータを返します。 この動作は、フルテキスト検索の動作と一致しません。  
  
```sql  
-- To disable semantic indexing on a table  
USE database_name  
GO  
  
ALTER FULLTEXT INDEX ON table_name DISABLE  
GO  
  
-- To re-enable semantic indexing on a table  
USE database_name  
GO  
  
ALTER FULLTEXT INDEX ON table_name ENABLE  
GO  
```  
  
##  <a name="SemanticIndexing"></a> セマンティック インデックス作成のフェーズについて  
 セマンティック検索では、セマンティック検索が有効なそれぞれの列に対して、次の 2 種類のデータに関するインデックスが作成されます。  
  
1.  **キー フレーズ**  
  
2.  **ドキュメントの類似性**  
  
 セマンティック インデックス作成は、フルテキスト インデックス作成との関連において 2 つのフェーズで行われます。  
  
1.  **フェーズ 1:** フルテキスト キーワード インデックスとセマンティック キー フレーズ インデックスが同時に作成されます。 ドキュメントの類似性に関するインデックスを作成するのに必要なデータもこのとき抽出されます。  
  
2.  **フェーズ 2:** ドキュメントの類似性に関するセマンティック インデックスが作成されます。 このインデックスは、前のフェーズで作成された 2 つのインデックスに依存します。  
  
##  <a name="BestPracticeUnderstand"></a>   
##  <a name="ProblemNotPopulated"></a>問題点: セマンティック インデックスが作成されない  
### <a name="are-the-associated-full-text-indexes-populated"></a>関連するフルテキスト インデックスが作成されていますか?  
 セマンティック インデックス作成はフルテキスト インデックス作成に依存しているため、セマンティック インデックスは関連するフルテキスト インデックスが作成されたときにのみ作成されます。  
  
### <a name="are-full-text-search-and-semantic-search-properly-installed-and-configured"></a>フルテキスト検索およびセマンティック検索が適切にインストールおよび構成されていますか?  
 詳細については、「 [セマンティック検索のインストールと構成](../../relational-databases/search/install-and-configure-semantic-search.md)」を参照してください。  
  
### <a name="is-the-fdhost-service-not-available-or-is-there-another-condition-that-would-cause-full-text-indexing-to-fail"></a>FDHOST サービスが使用できない状態ではありませんか? または、フルテキスト インデックス作成が失敗するそれ以外の原因はありませんか?  
 詳細については、「 [フルテキスト インデックスの作成のトラブルシューティング](../../relational-databases/search/troubleshoot-full-text-indexing.md)」を参照してください。  
  
  
