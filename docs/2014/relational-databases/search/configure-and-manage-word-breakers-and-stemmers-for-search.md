---
title: 検索用のワード ブレーカーとステマーの構成と管理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- languages [full-text search]
- full-text search [SQL Server], stemmers
- linguistic analysis [full-text search]
- full-text indexes [SQL Server], linguistic analysis
- full-text search [SQL Server], word breakers
- default full-text language option
- stemmers [full-text search]
- conjugating verbs [full-text search]
- word breakers [full-text search]
ms.assetid: d4bdd16b-a2db-4101-a946-583d1c674229
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: eaa80c71dcc58cbd780a664d2466a3bf3cec2a4c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011540"
---
# <a name="configure-and-manage-word-breakers-and-stemmers-for-search"></a>検索用のワード ブレーカーとステミング機能の構成と管理
  ワード ブレーカーとステミング機能は、すべてのフルテキスト インデックス データに対して言語分析を実行します。 言語分析には、単語の境界 (単語の区切り) の検索と動詞の活用 (ステミング) が含まれます。 ワード ブレーカーとステミング機能は言語に固有のものであり、言語分析の規則は言語によって異なります。 特定の言語において、 *ワード ブレーカー* によって、言語の語彙の規則に基づいて単語の境界を検出し、個々の単語を識別します。 各単語 ( *トークン*ともいいます) は、サイズを縮小するために圧縮された表現でフルテキスト インデックスに挿入されます。 *ステミング機能* はその言語の規則に基づいて特定の語の変化形を生成します (たとえば、"running"、"ran"、"runner" は、"run" という語の変化形です)。  
  
 言語固有のワード ブレーカーを使用すると、その言語に対する検索結果の精度が高くなります。 言語ファミリにはワード ブレーカーが存在していても、特定のサブ言語は対象とされない場合は、主言語が使用されます。 たとえば、カナダ系フランス語テキストの処理には、フランス語のワード ブレーカーが使用されます。 特定の言語用のワード ブレーカーが使用できない場合は、ニュートラル ワード ブレーカーが使用されます。 ニュートラル ワード ブレーカーを使用すると、単語は空白や句読点などのニュートラル文字で分割されます。  
  
##  <a name="register"></a> ワード ブレーカーを登録します。  
 言語のワード ブレーカーを使用する場合は、そのワード ブレーカーを登録する必要があります。 登録されているワード ブレーカーは、関連する言語リソース ステマー、ノイズ ワード (ストップ ワード)、および類義語辞典ファイルにもフルテキスト インデックス作成とクエリ操作に使用できるようになります。 現在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にワード ブレーカーが登録されている言語の一覧を表示するには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します。  
  
 SELECT * FROM sys.fulltext_languages  
  
 ワード ブレーカーを追加、削除、または変更すると、フルテキスト インデックスおよびフルテキスト クエリでサポートされている Microsoft Windows のロケール識別子 (LCID) の一覧を更新する必要があります。 詳細については、「 [登録済みのフィルターおよびワード ブレーカーの表示または変更](view-or-change-registered-filters-and-word-breakers.md)」を参照してください。  
  
##  <a name="default"></a> 既定のフルテキスト言語オプションの設定  
 ローカライズされたバージョン[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]セットのセットアップ、`default full-text language`適切な一致が存在する場合に、サーバーの言語オプションします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカライズされていないバージョンでは、`default full-text language` オプションは英語になります。  
  
 フルテキスト インデックスを作成または変更する際には、フルテキスト インデックス列ごとに言語を指定できます。 列に言語が指定されていない場合、既定では構成オプション `default full-text language` の値になります。  
  
> [!NOTE]  
>  1 つのフルテキスト クエリ関数句に指定されるすべての列は、クエリで LANGUAGE オプションが指定されていない限り、同じ言語を使用する必要があります。 クエリ対象のフルテキスト インデックスが付けられた列に使用する言語によって、フルテキスト クエリの述語 ([CONTAINS](/sql/t-sql/queries/contains-transact-sql) および [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)) および関数 ([CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) および [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql)) の引数に対して実行される言語分析が決まります。  
  
##  <a name="lang"></a> インデックス付き列の言語を選択します。  
 フルテキスト インデックスを作成する際には、各インデックス列に対して言語を指定することをお勧めします。 列に言語が指定されていない場合、システムの既定の言語が使用されます。 列のインデックス作成に使用されるワード ブレーカーとステミング機能は、列の言語によって決まります。 また、指定した言語の類義語辞典ファイルが、列のフルテキスト クエリで使用されます。  
  
 フルテキスト インデックスの作成時に列の言語を選択する際には、注意点が 2 つあります。 これらの注意点は、テキストをトークン化する方法と、Full-Text Engine によるインデックス作成の方法にかかわるものです。 詳細については、「 [フルテキスト インデックス作成時の言語の選択](choose-a-language-when-creating-a-full-text-index.md)」を参照してください。  
  
 **列のワード ブレーカーの言語を表示するには**  
  
-   [フルテキスト インデックスの管理](../indexes/indexes.md)  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)  
  
    ```  
    SELECT 'language_id' AS "LCID" FROM sys.fulltext_index_columns;  
    ```  
  
##  <a name="info"></a> ワード ブレーカーの情報を取得します。  
 **ワード ブレーカー、類義語辞典、およびストップ リストの組み合わせのトークン化の結果を表示します。**  
  
-   [sys.dm_fts_parser &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql)  
  
 **登録されているワード ブレーカーに関する情報を返す**  
  
-   [sp_help_fulltext_system_components &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql)  
  
##  <a name="tshoot"></a> 単語区切りのタイムアウト エラーのトラブルシューティング  
 単語区切りのタイムアウト エラーは、さまざまな状況で発生する可能性があります。 エラーが発生する状況とその対処方法については、「 [MSSQLSERVER_30053](../errors-events/mssqlserver-30053-database-engine-error.md)」を参照してください。  
  
##  <a name="impact"></a> 新しいワード ブレーカーの影響を理解します。  
 各バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、通常、新しいワード ブレーカーが含まれています。これらのワード ブレーカーでは、言語の規則が改良されているため、以前のワード ブレーカーよりも精度が向上しています。 新しいワード ブレーカーは、前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]からインポートされたフルテキスト インデックスのワード ブレーカーとは少し動作が異なる場合もあります。 データベースが現在のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にアップグレードされたときにフルテキスト カタログをインポートした場合は、この動作の違いが重要になります。 フルテキスト カタログのフルテキスト インデックスで使用される 1 つまたは複数の言語が、新しいワード ブレーカーに関連付けられる可能性があります。 詳細については、「 [フルテキスト検索のアップグレード](upgrade-full-text-search.md)」を参照してください。  
  
 すべてのワード ブレーカーの一覧については、次を参照してください。 [sys.fulltext_languages &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)します。  
  
## <a name="see-also"></a>参照  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)   
 [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)   
 [フルテキスト検索に使用するストップワードとストップリストの構成と管理](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [フルテキスト検索のアップグレード](upgrade-full-text-search.md)  
  
  
