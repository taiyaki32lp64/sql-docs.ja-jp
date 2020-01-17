---
title: セマンティック検索 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server]
- semantic search [SQL Server], overview
- statistical semantic search [SQL Server]
- statistical semantic search [SQL Server], overview
ms.assetid: cd8faa9d-07db-420d-93f4-a2ea7c974b97
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 651705426b52b822c3eb8c7cf9d341968bbc088f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010991"
---
# <a name="semantic-search-sql-server"></a>セマンティック検索 (SQL Server)
  統計的セマンティック検索では、統計的に関連性がある*キー フレーズ*を抽出してインデックスを作成することにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに格納されている非構造化ドキュメントを深く解釈することができます。 次に、これらのキー フレーズを使用して、 *類似または関連ドキュメント*を特定してインデックスを作成することもできます。  
  
 3 つの Transact-SQL 行セット関数を使用することにより、これらのセマンティック インデックスに対してクエリを実行して、結果を構造化データとして取得することができます。  
  
##  <a name="whatcanido"></a> セマンティック検索では、どうすればでしょうか。  
 セマンティック検索は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の既存のフルテキスト検索機能を基にして構築されていますが、キーワード検索を超える新しいシナリオにも対応できます。 フルテキスト検索ではドキュメントの *単語* に対してクエリを実行しますが、セマンティック検索ではドキュメントの *意味* に対してクエリを実行します。 これによって、自動タグ抽出、関連性のあるコンテンツの検出、類似コンテンツにまたがる階層的なナビゲーションなどのソリューションが可能になりました。 たとえば、キー フレーズのインデックスに対してクエリを実行して、ドキュメントの編成またはコーパスに関する分類を作成することができます。 また、ドキュメントの類似性のインデックスに対してクエリを実行して、ジョブの説明に一致するレジュメを特定できます。  
  
 以降の例に、セマンティック検索の機能を示します。  
  
###  <a name="find1"></a> ドキュメント内のキー フレーズを検索します。  
 次のクエリは、サンプル ドキュメントで識別されたキー フレーズを取得します。 結果は、各キー フレーズの統計的有意性を順位付けするスコアの降順で表されます。 このクエリは、[semantickeyphrasetable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql) 関数を呼び出します。  
  
```sql  
SET @Title = 'Sample Document.docx'  
  
SELECT @DocID = DocumentID  
    FROM Documents  
    WHERE DocumentTitle = @Title  
  
SELECT @Title AS Title, keyphrase, score  
    FROM SEMANTICKEYPHRASETABLE(Documents, *, @DocID)  
    ORDER BY score DESC  
  
```  
  
  
  
###  <a name="find2"></a> 類似または関連ドキュメントを検索します。  
 次のクエリは、サンプル ドキュメントに類似または関連すると識別されたドキュメントを取得します。 結果は、2 つのドキュメントの類似性を順位付けするスコアの降順で表されます。 このクエリは、[semanticsimilaritytable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql) 関数を呼び出します。  
  
```vb  
SET @Title = 'Sample Document.docx'  
  
SELECT @DocID = DocumentID  
    FROM Documents  
    WHERE DocumentTitle = @Title  
  
SELECT @Title AS SourceTitle, DocumentTitle AS MatchedTitle,  
        DocumentID, score  
    FROM SEMANTICSIMILARITYTABLE(Documents, *, @DocID)  
    INNER JOIN Documents ON DocumentID = matched_document_key  
    ORDER BY score DESC  
  
```  
  
  
  
###  <a name="find3"></a> 類似または関連ドキュメントを示すキー フレーズを検索します。  
 次のクエリは、2 つのサンプル ドキュメント間の類似性または関連性を示すキー フレーズを取得します。 結果は、各キー フレーズの重みを順位付けするスコアの降順で表されます。 このクエリは、[semanticsimilaritydetailstable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql) 関数を呼び出します。  
  
```sql  
SET @SourceTitle = 'first.docx'  
SET @MatchedTitle = 'second.docx'  
  
SELECT @SourceDocID = DocumentID FROM Documents WHERE DocumentTitle = @SourceTitle  
SELECT @MatchedDocID = DocumentID FROM Documents WHERE DocumentTitle = @MatchedTitle  
  
SELECT @SourceTitle AS SourceTitle, @MatchedTitle AS MatchedTitle, keyphrase, score  
    FROM semanticsimilaritydetailstable(Documents, DocumentContent,  
        @SourceDocID, DocumentContent, @MatchedDocID)  
    ORDER BY score DESC  
  
```  
  
  
  
##  <a name="store"></a> SQL Server のドキュメントを保存します。  
 セマンティック検索でドキュメントのインデックスを作成する前に、ドキュメントを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに保存する必要があります。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の FileTable の機能との組み合わせにより、構造化されていないファイルやドキュメントを、リレーショナル データベースの最上位レベルのオブジェクトにすることができます。 その結果、データベース開発者は、Transact-SQL セットベースの操作で構造化データと共にドキュメントを操作できます。  
  
 FileTable 機能の詳細については、「[FileTables &#40;SQL Server&#41;](../blob/filetables-sql-server.md)」をご覧ください。 データベースへのドキュメントの保存の別のオプションである FILESTREAM 機能の詳細については、「[FILESTREAM &#40;SQL Server&#41;](../blob/filestream-sql-server.md)」をご覧ください。  
  
  
  
##  <a name="reltasks"></a> 関連タスク  
 [セマンティック検索のインストールと構成](install-and-configure-semantic-search.md)  
 統計的セマンティック検索の前提条件と、これらをインストールまたは確認する方法について説明します。  
  
 [テーブルおよび列に対するセマンティック検索の有効化](enable-semantic-search-on-tables-and-columns.md)  
 ドキュメントまたはテキストが格納されている選択した列に対して統計的セマンティック インデックス作成を有効または無効にする方法について説明します。  
  
 [セマンティック検索を使用したドキュメント内のキー フレーズの検索](find-key-phrases-in-documents-with-semantic-search.md)  
 統計的セマンティック インデックス作成用に構成されたドキュメントまたはテキスト列内のキー フレーズのクエリを実行する方法について説明します。  
  
 [セマンティック検索による類似および関連したドキュメントの取得](find-similar-and-related-documents-with-semantic-search.md)  
 統計的セマンティック インデックス作成用に構成されている列での、類似性または関連性のあるドキュメントやテキスト値の検索方法と、どのように類似または関連しているかという情報の検索方法について説明します。  
  
 [セマンティクス検索の管理および監視](manage-and-monitor-semantic-search.md)  
 セマンティック インデックス作成プロセスと、インデックスの監視および管理に関連するタスクについて説明します。  
  
##  <a name="relcontent"></a> 関連コンテンツ  
 [セマンティック検索の DDL、関数、ストアド プロシージャ、およびビュー](../views/views.md)  
 統計的セマンティック検索をサポートするために追加または変更された Transact-SQL ステートメントおよび SQL Server データベース オブジェクトの一覧を示します。  
  
  
