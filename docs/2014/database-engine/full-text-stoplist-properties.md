---
title: フルテキスト ストップ リストのプロパティ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftstoplistproperties.general.f1
- sql12.swb.fulltextsearch.ftstoplistproperties.schedule.f1
ms.assetid: 2e907f5b-0cf9-484a-afcf-a4e7f1e2f87f
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 4cfdd308ab7488633721ddaac55d3d926a276b0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779409"
---
# <a name="full-text-stoplist-properties"></a>[フルテキスト ストップリストのプロパティ]
  このダイアログ ボックスを使用すると、個々のストップワードの追加や削除、特定の言語のすべてのストップワードの削除、および現在のストップリストのクリアを実行できます。 ストップワードは、ストップリストで一般的に使用される単語です。 ストップリスト内のストップワードは、ストップリストを使用するテーブルのフルテキスト インデックスから省略されます。 詳細については、「 [フルテキスト検索に使用するストップワードとストップリストの構成と管理](../relational-databases/search/full-text-search.md)」を参照してください。  
  
 **SQL Server Management Studio を使用してストップ リストのプロパティを変更するには**  
  
-   [フルテキスト検索に使用するストップワードとストップリストの構成と管理](../relational-databases/search/full-text-search.md)  
  
## <a name="options"></a>および  
 **操作**  
 実行するアクションを指定します。  
  
 **ストップ ワードを追加します。**  
 一般的に使用される単語をストップリストに追加します。  
  
 **ストップ ワードの削除します。**  
 ストップリストからストップワードを削除します。  
  
 **すべてのストップ ワードを削除します。**  
 特定の言語のストップワードをすべて削除します。  
  
 **ストップ リストのクリア**  
 すべての言語のストップワードをすべて削除することによって、ストップリストをクリアします。  
  
 **ストップ ワード**  
 **[ストップワードの追加]** または **[ストップワードの削除]** を選択した場合は、 **[ストップワード]** フィールドにストップワードを入力します。 新しいストップワードは一意である、つまり、選択した言語のこのストップリストにまだ含まれていない必要があります。  
  
 **フルテキスト言語**  
 **[ストップワードの追加]** 、 **[ストップワードの削除]** 、または **[すべてのストップワードの削除]** を選択した場合は、このリスト ボックスから、操作対象のストップワードの言語を選択します。 このリスト ボックスには、サーバー インスタンスでサポートされているすべてのフルテキスト言語が表示されます。  
  
## <a name="see-also"></a>参照  
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)   
 [フルテキスト検索に使用するストップワードとストップリストの構成と管理](../relational-databases/search/full-text-search.md)   
 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)   
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)  
  
  
