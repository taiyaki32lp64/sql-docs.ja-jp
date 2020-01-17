---
title: フルテキストおよびセマンティック検索の動的管理ビュー - Functions |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- dynamic management objects [SQL Server], full-text search
- full-text search [SQL Server], dynamic management views
ms.assetid: 199dbd5a-29f6-4ef0-8e65-86e32c0aaa3a
author: pmasl
ms.author: pelopes
ms.openlocfilehash: ff24122c1a551d6da1ce4ad1ddbb7771e2183c70
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130769"
---
# <a name="full-text-and-semantic-search-dynamic-management-views---functions"></a>フルテキストおよびセマンティック検索の動的管理ビュー - 関数
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  このセクションには、次の動的管理ビューおよび関数、フルテキスト検索およびセマンティック検索に関連付けられているが含まれています。  
  
## <a name="full-text-search-dynamic-management-views-and-functions"></a>フルテキスト検索の動的管理ビューおよび関数  
 [sys.dm_fts_active_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md)  
 サーバー上で進行中の作成操作である、フルテキスト カタログ情報を返します。  
  
 [sys.dm_fts_fdhosts](../../relational-databases/system-dynamic-management-views/sys-dm-fts-fdhosts-transact-sql.md)  
 サーバー インスタンス上のフィルター デーモン ホストの現在のアクティビティに関する情報を返します。  
  
 [sys.dm_fts_index_keywords](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
 指定されたテーブルのフルテキスト インデックスのコンテンツに関する情報を返します。  
  
 [sys.dm_fts_index_keywords_by_document](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
 指定されたテーブルについて、フルテキスト インデックスのドキュメント レベルのコンテンツに関連する情報を返します。 個々のキーワードは、複数のドキュメントに出現する場合があります。  
  
 [sys.dm_fts_index_keywords_by_property](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)  
 特定のテーブルのフルテキスト インデックスのプロパティに関連するコンテンツを返します。 これには、フルテキスト インデックスに関連付けられた検索プロパティ リストによって登録されたすべてのプロパティに属するすべてのデータが含まれます。  
  
 sys.dm_fts_index_keywords_position_by_document  
 ドキュメント内のキーワードの位置を返します。  
  
 [sys.dm_fts_index_population](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
 現在実行中の、フルテキスト インデックス設定に関する情報を返します。  
  
 [sys.dm_fts_memory_buffers](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)  
 フルテキスト クロールまたはフルテキスト クロール範囲の一部として使用される、特定のメモリ プールのメモリ バッファーに関する情報を返します。  
  
 [sys.dm_fts_memory_pools](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)  
 フルテキスト クロールまたはフルテキスト クロール範囲でフルテキスト Gatherer コンポーネントには、使用できる共有メモリ プールに関する情報を返します。  
  
 [sys.dm_fts_outstanding_batches](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md)  
 各フルテキスト インデックス バッチに関する情報を返します。  
  
 [sys.dm_fts_parser](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)  
 特定のワード ブレーカー、類義語辞典、およびストップ リストの組み合わせをクエリ文字列入力に適用すると、最終的なトークン化の結果を返します。 出力は、指定したクエリ文字列が Full-Text Engine に対して発行された場合の出力と同じです。  
  
 [sys.dm_fts_population_ranges](../../relational-databases/system-dynamic-management-views/sys-dm-fts-population-ranges-transact-sql.md)  
 現在進行中のフルテキスト インデックス作成に関連する特定の範囲についての情報を返します。  
  
## <a name="semantic-search-dynamic-management-views-and-functions"></a>セマンティック検索の動的管理ビューおよび関数  
 [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
 関連付けられたセマンティック インデックスを持つ各テーブルの類似性インデックスごとに、ドキュメント類似性インデックスの作成に関する 1 行の状態情報を返します。  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [システム ビュー &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
