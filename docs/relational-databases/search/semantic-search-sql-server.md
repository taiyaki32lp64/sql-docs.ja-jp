---
title: セマンティック検索 (SQL Server) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server]
- semantic search [SQL Server], overview
- statistical semantic search [SQL Server]
- statistical semantic search [SQL Server], overview
ms.assetid: cd8faa9d-07db-420d-93f4-a2ea7c974b97
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 70798b0e967d62b51879cc694c8eb43363d364c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912956"
---
# <a name="semantic-search-sql-server"></a>セマンティック検索 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
統計的セマンティック検索では、統計的に関連性がある [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] キー フレーズ *を抽出してインデックスを作成することにより、* データベースに格納されている非構造化ドキュメントを深く解釈することができます。 次に、これらのキー フレーズを使用して、*類似または関連ドキュメント*を特定してインデックスを作成することができます。  
  
##  <a name="whatcanido"></a> セマンティック検索で実行できる操作  
 セマンティック検索は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の既存のフルテキスト検索機能を基にして構築されていますが、キーワード検索を超える新しいシナリオにも対応できます。 フルテキスト検索ではドキュメントの *単語* に対してクエリを実行しますが、セマンティック検索ではドキュメントの *意味* に対してクエリを実行します。 これによって、自動タグ抽出、関連性のあるコンテンツの検出、類似コンテンツにまたがる階層的なナビゲーションなどのソリューションが可能になりました。 たとえば、キー フレーズのインデックスに対してクエリを実行して、ドキュメントの編成またはコーパスに関する分類を作成することができます。 また、ドキュメントの類似性のインデックスに対してクエリを実行して、ジョブの説明に一致するレジュメを特定できます。  
  
 以降の例に、セマンティック検索の機能を示します。 同時に、これらの例では、セマンティック インデックスに対してクエリを実行し、その結果を構造化データとして取得するために使用する 3 つの Transact-SQL 行セット関数を示します。  
  
###  <a name="find1"></a> ドキュメント内のキー フレーズを検索します。  
 次のクエリは、サンプル ドキュメントで識別されたキー フレーズを取得します。 結果は、各キー フレーズの統計的有意性を順位付けするスコアの降順で表されます。
 
 このクエリは、[semantickeyphrasetable](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md) 関数を呼び出します。  
  
```sql  
SET @Title = 'Sample Document.docx'  
  
SELECT @DocID = DocumentID  
    FROM Documents  
    WHERE DocumentTitle = @Title  
  
SELECT @Title AS Title, keyphrase, score  
    FROM SEMANTICKEYPHRASETABLE(Documents, *, @DocID)  
    ORDER BY score DESC  
  
```  
  
###  <a name="find2"></a> Find similar or related documents  
 次のクエリは、サンプル ドキュメントに類似または関連すると識別されたドキュメントを取得します。 結果は、2 つのドキュメントの類似性を順位付けするスコアの降順で表されます。
 
 このクエリは、[semanticsimilaritytable](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md) 関数を呼び出します。  
  
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
 次のクエリは、2 つのサンプル ドキュメント間の類似性または関連性を示すキー フレーズを取得します。 結果は、各キー フレーズの重みを順位付けするスコアの降順で表されます。
 
 このクエリは、[semanticsimilaritydetailstable](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md) 関数を呼び出します。  
  
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
  
##  <a name="store"></a> SQL Server へのドキュメントの保存  
 セマンティック検索でドキュメントのインデックスを作成する前に、ドキュメントを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに保存する必要があります。  
  
 SQL Server の FileTable の機能との組み合わせにより、構造化されていないファイルやドキュメントを、リレーショナル データベースの最上位レベルのオブジェクトにすることができます。 その結果、データベース開発者は、Transact-SQL セットベースの操作で構造化データと共にドキュメントを操作できます。  
  
 FileTable 機能の詳細については、「[FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)」を参照してください。 データベースへのドキュメントの保存の別のオプションである FILESTREAM 機能については、「[FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)」を参照してください。  
  
##  <a name="reltasks"></a> 関連タスク  
 [セマンティック検索のインストールと構成](../../relational-databases/search/install-and-configure-semantic-search.md)  
 統計的セマンティック検索の前提条件と、これらをインストールまたは確認する方法について説明します。  
  
 [テーブルおよび列に対するセマンティック検索の有効化](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)  
 ドキュメントまたはテキストが格納されている選択した列に対して統計的セマンティック インデックス作成を有効または無効にする方法について説明します。  
  
 [セマンティック検索を使用したドキュメント内のキー フレーズの検索](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md)  
 統計的セマンティック インデックス作成用に構成されたドキュメントまたはテキスト列内のキー フレーズのクエリを実行する方法について説明します。  
  
 [セマンティック検索による類似および関連したドキュメントの取得](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)  
 統計的セマンティック インデックス作成用に構成されている列での、類似性または関連性のあるドキュメントやテキスト値の検索方法と、どのように類似または関連しているかという情報の検索方法について説明します。  
  
 [セマンティクス検索の管理および監視](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
 セマンティック インデックス作成プロセスと、インデックスの監視および管理に関連するタスクについて説明します。  
  
##  <a name="relcontent"></a> Related content  
 [セマンティック検索の DDL、関数、ストアド プロシージャ、およびビュー](../../relational-databases/search/semantic-search-ddl-functions-stored-procedures-and-views.md)  
 統計的セマンティック検索をサポートするために追加または変更された Transact-SQL ステートメントおよび SQL Server データベース オブジェクトの一覧を示します。  
  
  
