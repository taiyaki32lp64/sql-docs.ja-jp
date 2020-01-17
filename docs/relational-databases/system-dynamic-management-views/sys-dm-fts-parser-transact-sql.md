---
title: sys.dm_fts_parser (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_parser_TSQL
- dm_fts_parser
- dm_fts_parser_TSQL
- sys.dm_fts_parser
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_parser dynamic management function
- troubleshooting [SQL Server], full-text search
ms.assetid: 2736d376-fb9d-4b28-93ef-472b7a27623a
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: fa60c1785e0740dde4bc6b3755dea36db8a5a21a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900916"
---
# <a name="sysdmftsparser-transact-sql"></a>sys.dm_fts_parser (TRANSACT-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  適用した後、最終的なトークン化の結果を返します、指定された[ワード ブレーカー](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)、[類義語辞典](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)、および[ストップ リスト](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)の組み合わせをクエリ文字列入力をします。 トークン化の結果は、指定したクエリ文字列の Full-text Engine の出力と同じです。  
  
 sys.dm_fts_parser は動的管理関数です。  
  
## <a name="syntax"></a>構文  
  
```  
sys.dm_fts_parser('query_string', lcid, stoplist_id, accent_sensitivity)  
```  
  
## <a name="arguments"></a>引数  
 *query_string*  
 このクエリを解析します。 *query_string*される文字列チェーンを指定できます[CONTAINS](../../t-sql/queries/contains-transact-sql.md)構文のサポート。 たとえば、変化形、類義語辞典、および論理演算子を含めることができます。  
  
 *lcid*  
 解析するために使用されるワード ブレーカーのロケール識別子 (LCID) *query_string*します。  
  
 *stoplist_id*  
 いずれかで識別されるワード ブレーカーが使用する場合は、ストップ リストの ID *lcid*します。 *stoplist_id*は**int**します。'NULL' を指定する場合は、ストップ リストは使用されません。 0 を指定する場合は、システム ストップ リストが使用されます。  
  
 ストップ リスト ID は、データベース内で一意です。 特定のテーブルの使用上のフルテキスト インデックスのストップ リスト ID を取得する、 [sys.fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)カタログ ビューです。  
  
 *accent_sensitivity*  
 フルテキスト検索で分音文字を区別するかしないかを制御するブール値です。 *accent_sensitivity*は**ビット**、次の値のいずれかの。  
  
|値|アクセントを区別します。|  
|-----------|----------------------------|  
|0|小文字を区別しません。<br /><br /> 「カフェ」と「カフェ」などの単語は同一に扱われます。|  
|1|区別する<br /><br /> 「カフェ」と「カフェ」などの単語は異なる方法で扱われます。|  
  
> [!NOTE]  
>  フルテキスト カタログのこの値の現在の設定を表示するには、次を実行[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメント: `SELECT fulltextcatalogproperty('` *catalog_name*`', 'AccentSensitivity');`します。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|キーワード (keyword)|**varbinary (128)**|ワード ブレーカーによって返される特定のキーワードの 16 進数表現。 この表記は、フルテキスト インデックスにキーワードを格納するために使用します。 この値は人間が判読できるなど、フルテキスト インデックスのコンテンツを返す他の動的管理ビューによって返される関連する特定のキーワードを出力するため便利ですが、 [sys.dm_fts_index_keywords](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)と[sys.dm_fts_index_keywords_by_document](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)します。<br /><br /> **注:** 0 Xff は、ファイルまたはデータセットの終了位置を示す特殊文字を表します。|  
|group_id|**int**|特定の用語の生成元となる論理グループを区別するのに役立つ整数値が含まれます。 たとえば、英語の場合、'`Server AND DB OR FORMSOF(THESAURUS, DB)"`' で次の group_id 値が生成されます。<br /><br /> 1:Server<br />2:DB (DB)<br />3:DB (DB)|  
|phrase_id|**int**|これで、フルテキストなどの複合語の代替形式がワード ブレーカーによって発行されたケースを差別化に役立つ整数値が含まれています。 複合語 ('multi-million' など) が存在する場合、ワード ブレーカーによって代替形式が発行されることがあります。 このような代替形式 (語句) は区別が必要になる場合があります。<br /><br /> たとえば、英語の場合、'`multi-million`' で次の phrase_id 値が生成されます。<br /><br /> 場合は 1 `multi`<br />場合は 1 `million`<br />2 `multimillion`|  
|occurrence|**int**|解析結果の各用語の順序を示します。 たとえば、英語の "`SQL Server query processor`" という語句の場合、occurrence には語句内の用語に対する次のオカレンス値が格納されます。<br /><br /> 場合は 1 `SQL`<br />2 `Server`<br />3 `query`<br />4 `processor`|  
|special_term|**nvarchar (4000)**|ワード ブレーカーによって発行されている用語の特性に関する情報を格納します。次のいずれかになります。<br /><br /> 完全一致<br /><br /> ノイズ ワード<br /><br /> 文の終了<br /><br /> 段落の末尾<br /><br /> 章の末尾|  
|display_term|**nvarchar (4000)**|人間が判読できる形式キーワードにはが含まれています。 フルテキスト インデックスのコンテンツにアクセスするように設計されている関数と同様に、ここに表示される用語は、非正規化の制限のため元の用語と同一とは限りません。 ただし、元の入力を識別するのに十分な精度が必要です。|  
|expansion_type|**int**|特定の用語の拡張の特性に関する情報を格納します。次のいずれかになります。<br /><br /> 0 = 1 つの単語の場合<br /><br /> 2 = 変化形の拡張<br /><br /> 4 = 類義語辞典の拡張と置換<br /><br /> たとえば、類義語辞典で run が `jog` の拡張として定義されている場合を考えてみます。<br /><br /> `<expansion>`<br /><br /> `<sub>run</sub>`<br /><br /> `<sub>jog</sub>`<br /><br /> `</expansion>`<br /><br /> 用語`FORMSOF (FREETEXT, run)`次の出力が生成されます。<br /><br /> `run` : expansion_type=0<br /><br /> `runs` : expansion_type=2<br /><br /> `running` : expansion_type=2<br /><br /> `ran` : expansion_type=2<br /><br /> `jog` : expansion_type=4|  
|source_term|**nvarchar (4000)**|特定の用語の生成元または解析元になった用語または語句です。 たとえば、英語の場合、`word breakers" AND stemmers'` に対するクエリで次の source_term 値が生成されます。<br /><br /> `word breakers` display_term の`word`<br />`word breakers` display_term の`breakers`<br />`stemmers` display_term の`stemmers`|  
  
## <a name="remarks"></a>コメント  
 **sys.dm_fts_parser**など、構文と、フルテキスト述語では、機能をサポートしている[CONTAINS](../../t-sql/queries/contains-transact-sql.md)と[FREETEXT](../../t-sql/queries/freetext-transact-sql.md)、関数、およびなど[CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)と[FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md)します。  
  
## <a name="using-unicode-for-parsing-special-characters"></a>特殊文字の解析での Unicode の使用  
 クエリ文字列を解析するときに**sys.dm_fts_parser** Unicode として、クエリ文字列を指定しない限り、接続先データベースの照合順序を使用します。 そのため、ü、ザ行などの特殊文字を含む非 Unicode 文字列に出力できない可能性があります、データベースの照合順序によって、予期されます。 データベースの照合順序とは別にクエリ文字列を処理するには、プレフィックス文字列を`N`、つまり`N'` *query_string*`'`します。  
  
 詳細については、「c. を参照してください。 特殊文字を含む文字列の出力を表示する」を参照してください。  
  
## <a name="when-to-use-sysdmftsparser"></a>Sys.dm_fts_parser を使用するときに  
 **sys.dm_fts_parser**デバッグのための非常に強力なことができます。 いくつかの主要な使用シナリオは次のとおりです。  
  
-   特定のワード ブレーカーが特定の入力を処理する方法を理解するには  
  
     クエリには、予期しない結果が返される、ときに考えられる原因、ワード ブレーカーが解析と、データを分割する方法です。 sys.dm_fts_parser を使用すると、ワード ブレーカーからフルテキスト インデックスに渡される結果を検出できます。 さらに、用語がフルテキスト インデックスで検索されないストップ ワードを表示できます。 用語が特定の言語によって異なりますで指定されたストップ リスト内にあるかどうかにストップ ワードをどのようにがかどうか、 *stoplist_id*関数で宣言されている値。  
  
     ユーザーがワード ブレーカーによる入力の解析方法を確認できるようにするアクセントの区別フラグには、アクセントの区別に関する情報が格納されているので、これも確認してください。  
  
-   指定された入力の語幹検索のしくみを理解するには  
  
     ワード ブレーカーとステミング機能の解析方法によるクエリ用語とそのステミング形式は次の FORMSOF 句を含む CONTAINS または CONTAINSTABLE クエリを指定することで確認できます。  
  
    ```  
    FORMSOF( INFLECTIONAL, query_term )  
    ```  
  
     この結果から、フルテキスト インデックスに渡されている用語がわかります。  
  
-   類義語辞典で拡張する方法や、入力の一部またはすべてを置換する方法を理解するには  
  
     指定できます。  
  
    ```  
    FORMSOF( THESAURUS, query_term )  
    ```  
  
     このクエリの結果は、クエリ用語に対するワード ブレーカーと類義語辞典の対話方法を説明します。 類義語辞典から拡張または置換を確認し、フルテキスト インデックスに対して実際に発行されているクエリを特定することができます。  
  
     場合にユーザーの問題に注意してください。  
  
    ```  
    FORMSOF( FREETEXT, query_term )  
    ```  
  
     変化形および類義語辞典の機能が自動的に実行します。  
  
 上記の使用シナリオに加え、sys.dm_fts_parser は、フルテキスト クエリに関する他の多くの問題の理解やトラブルシューティングに大きく役立ちます。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **sysadmin**サーバー ロールとアクセス権を指定したストップ リストを修正しました。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-displaying-the-output-of-a-given-word-breaker-for-a-keyword-or-phrase"></a>A. キーワードまたは語句に関する特定のワード ブレーカーの出力を表示する  
 次の例には、次のクエリ文字列での LCID が 1033 の英語のワード ブレーカーを使用してからの出力となしのストップ リストが返されます。  
  
 `The Microsoft business analysis`  
  
 アクセントの区別は無効になっています。  
  
```sql
SELECT * FROM sys.dm_fts_parser (' "The Microsoft business analysis" ', 1033, 0, 0);  
```  
  
### <a name="b-displaying-the-output-of-a-given-word-breaker-in-the-context-of-stoplist-filtering"></a>B. ストップ リスト フィルターのコンテキストで特定のワード ブレーカーの出力を表示します。  
 次の例では、次のクエリ文字列に対して LCID が 1033 の英語のワード ブレーカーと ID が 77、英語のストップ リストを使用してから、出力が返されます。  
  
 `"The Microsoft business analysis" OR "MS revenue"`  
  
 アクセントの区別は無効になっています。  
  
```sql
SELECT * FROM sys.dm_fts_parser (' "The Microsoft business analysis"  OR " MS revenue" ', 1033, 77, 0);  
```  
  
### <a name="c-displaying-the-output-of-a-string-that-contains-special-characters"></a>C. 特殊文字を含む文字列の出力を表示します。  
 次の例では、Unicode を使用して次のフランス語の文字列を解析します。  
  
 `français`  
  
 この例では、フランス語の LCID として `1036` と、ユーザー定義のストップリストの ID として `5` を指定します。 アクセントの区別が有効になっているとします。  
  
```sql
SELECT * FROM sys.dm_fts_parser(N'français', 1036, 5, 1);  
```  
  
## <a name="see-also"></a>関連項目  
 [フルテキスト検索とセマンティック検索の動的管理ビューおよび関数&#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [フルテキスト検索](../../relational-databases/search/full-text-search.md)   
 [検索用のワード ブレーカーとステミング機能の構成と管理](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [構成して、フルテキスト検索の類義語辞典ファイルを管理](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [フルテキスト検索に使用するストップワードとストップリストの構成と管理](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)   
 [フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)   
 [セキュリティ保護可能](../../relational-databases/security/securables.md)  
  
  
