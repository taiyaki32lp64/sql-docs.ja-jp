---
title: 検索用のワード ブレーカーとステミング機能の構成と管理
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
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
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: 393b6e248962fa496dcdac9fe5def556b766a2bd
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056261"
---
# <a name="configure--manage-word-breakers--stemmers-for-search-sql-server"></a>検索用のワード ブレーカーとステミング機能の構成と管理 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
ワード ブレーカーとステミング機能は、すべてのフルテキスト インデックス データに対して言語分析を実行します。 言語分析では、次の 2 つを行います。

-   **単語の境界 (単語区切り) の検出**。 *ワード ブレーカー* が、言語の語彙の規則に基づいて単語の境界を検出し、個々の単語を識別します。 各単語 ( *トークン*ともいいます) は、サイズを縮小するために圧縮された表現でフルテキスト インデックスに挿入されます。

-   **動詞の活用 (ステミング)** 。 *ステミング機能* はその言語の規則に基づいて特定の語の変化形を生成します (たとえば、"running"、"ran"、"runner" は、"run" という語の変化形です)。

## <a name="word-breakers-and-stemmers-are-language-specific"></a>言語固有のワード ブレーカーとステマー

ワード ブレーカーとステミング機能は言語に固有のものであり、言語分析の規則は言語によって異なります。 言語固有のワード ブレーカーを使用すると、その言語に対する検索結果の精度が高くなります。

ワード ブレーカーとステマーは、SQL Server でサポートされるすべての言語に提供されており、通常は、特に操作をしなくても使用できます。

-   言語ファミリにはワード ブレーカーが存在していても、特定のサブ言語は対象とされない場合は、主言語が使用されます。 たとえば、カナダ系フランス語テキストの処理には、フランス語のワード ブレーカーが使用されます。
-   特定の言語用のワード ブレーカーが使用できない場合は、ニュートラル ワード ブレーカーが使用されます。 ニュートラル ワード ブレーカーを使用すると、単語は空白や句読点などのニュートラル文字で分割されます。

## <a name="get-the-list-of-supported-languages"></a>サポートされる言語の一覧の取得

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フルテキスト検索でサポートされている言語の一覧を見るには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します。 この一覧に含まれる言語については、その言語のワード ブレーカーが登録されています。 
  
```sql
SELECT * FROM sys.fulltext_languages
```

##  <a name="register"></a>登録されているワード ブレーカーの一覧の取得

フルテキスト検索で、ある言語のワード ブレーカーを使用するには、それらが登録されている必要があります。 ワード ブレーカーを登録すると、関連する言語リソース (ステマー、ノイズ ワード (ストップワード)、類義語辞典ファイル) もフルテキスト インデックス操作やフルテキスト クエリ操作で使用できるようになります。

登録されているワード ブレーカー コンポーネントの一覧を表示するには、次のステートメントを使用します。

```sql
EXEC sp_help_fulltext_system_components 'wordbreaker';  
GO  
```

追加のオプションと詳細については、「[sp_help_fulltext_system_components &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)」を参照してください。
 
## <a name="if-you-add-or-remove-a-word-breaker"></a>ワード ブレーカーを追加または削除する場合  
ワード ブレーカーを追加、削除、または変更すると、フルテキスト インデックスおよびフルテキスト クエリでサポートされている Microsoft Windows のロケール識別子 (LCID) の一覧を更新する必要があります。 詳細については、「 [登録済みのフィルターおよびワード ブレーカーの表示または変更](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)」を参照してください。  
  
##  <a name="default"></a> 既定のフルテキスト言語オプションの設定  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のローカライズされたバージョンでは、適切な言語が存在する場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップによって **default full-text language** オプションはサーバーの言語に設定されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のローカライズされていないバージョンでは、 **[既定のフルテキスト言語]** オプションは英語になります。  
  
 フルテキスト インデックスを作成または変更する場合は、フルテキスト インデックス列ごとに言語を指定できます。 列に言語が指定されていない場合、既定では構成オプション **default full-text language**の値になります。  
  
> [!NOTE]  
>  1 つのフルテキスト クエリ関数句に指定されるすべての列は、クエリで LANGUAGE オプションが指定されていない限り、同じ言語を使用する必要があります。 クエリ対象のフルテキスト インデックスが付けられた列に使用する言語によって、フルテキスト クエリの述語 ([CONTAINS](../../t-sql/queries/contains-transact-sql.md) および [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)) および関数 ([CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) および [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md)) の引数に対して実行される言語分析が決まります。  
  
##  <a name="lang"></a> インデックス列の言語の選択  
 フルテキスト インデックスを作成する際には、各インデックス列に対して言語を指定することをお勧めします。 列に言語が指定されていない場合、システムの既定の言語が使用されます。 列のインデックス作成に使用されるワード ブレーカーとステミング機能は、列の言語によって決まります。 また、指定した言語の類義語辞典ファイルが、列のフルテキスト クエリで使用されます。  
  
 フルテキスト インデックスの作成時に列の言語を選択する際には、注意点が 2 つあります。 これらの注意点は、テキストをトークン化する方法と、Full-Text Engine によるインデックス作成の方法にかかわるものです。 詳細については、「 [フルテキスト インデックス作成時の言語の選択](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)」を参照してください。  
  
特定の列のワード ブレーカーの言語を表示するには、次のステートメントを実行します。
   
```sql 
SELECT language_id AS 'LCID' FROM sys.fulltext_index_columns;
```  

追加のオプションと詳細については、「[sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)」をご覧ください。

##  <a name="tshoot"></a> 単語区切りのタイムアウト エラーのトラブルシューティング  
 単語区切りのタイムアウト エラーは、さまざまな状況で発生する可能性があります。 エラーが発生する状況とその対処方法については、「[MSSQLSERVER_30053](../errors-events/mssqlserver-30053-database-engine-error.md)」をご覧ください。

### <a name="info-about-the-mssqlserver_30053-error"></a>MSSQLSERVER_30053 エラーに関する情報
  
|プロパティ|[値]|
|-|-|
|製品名|SQL Server|  
|イベント ID|30053|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|FTXT_QUERY_E_WORDBREAKINGTIMEOUT|  
|メッセージ テキスト|フルテキスト クエリ文字列の単語区切り処理がタイムアウトしました。 このタイムアウトは、ワード ブレーカーによるフルテキスト クエリ文字列の処理が長時間かかったか、サーバー上で実行されているクエリ数が多い場合に発生する可能性があります。 負荷を少なくしてクエリの再実行を試みてください。|  
  
#### <a name="explanation"></a>説明  
 単語区切りのタイムアウト エラーは、次の状況で発生する可能性があります。  
  
-   クエリ言語のワード ブレーカーが正しく構成されていない場合。たとえば、レジストリ設定が正しくない場合です。  
  
-   ワード ブレーカーが特定のクエリ文字列に対して誤動作する。  
  
-   ワード ブレーカーが特定のクエリ文字列に対して過剰なデータを返す。 過剰なデータは、バッファー オーバーラン攻撃を引き起こす可能性のあるものとして処理されます。これにより、単語区切りサービスをホストする、フィルター デーモン プロセス (fdhost.exe) がシャットダウンされます。  
  
-   フィルター デーモン プロセスの構成が正しくない。  
  
     パスワードの期限が切れている場合、またはドメイン ポリシーが原因でフィルター デーモン アカウントがログオンできない場合。この 2 つは、最も一般的な構成上の問題です。  
  
-   クエリが集中的に行われるワークロードをサーバー インスタンスで実行している場合。たとえば、ワード ブレーカーによるフルテキスト クエリ文字列の処理が長時間かかったり、多数のクエリがサーバー上で実行されている場合です。 この状況がエラーの原因になることはまれです。  
  
#### <a name="user-action"></a>ユーザーの操作  
 次に示すように、タイムアウトについて考えられる原因に適した、ユーザーのアクションを選択してください。  
  
|考えられる原因|ユーザーのアクション|  
|--------------------|-----------------|  
|クエリ言語のワード ブレーカーが正しく構成されていない。|サード パーティ製のワード ブレーカーを使用しているとき、ワード ブレーカーがオペレーティング システムに正しく登録されていない場合があります。 この場合は、ワード ブレーカーを再登録してください。 詳細については、「[Revert the Word Breakers Used by Search to the Previous Version](revert-the-word-breakers-used-by-search-to-the-previous-version.md)」(検索で使用するワード ブレーカーを以前のバージョンに戻す) を参照してください。|  
|ワード ブレーカーが特定のクエリ文字列に対して誤動作する。|ワード ブレーカーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされている場合は、マイクロソフト カスタマー サポート サービスに問い合わせてください。|  
|ワード ブレーカーが特定のクエリ文字列に対して過剰なデータを返す。|ワード ブレーカーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされている場合は、マイクロソフト カスタマー サポート サービスに問い合わせてください。|  
|フィルター デーモン プロセスの構成が正しくない。|正しいパスワードを使用していることと、フィルター デーモン アカウントのログオンがドメイン ポリシーによって拒否されていないことを確認してください。|  
|クエリが集中的に行われるワークロードをサーバー インスタンスで実行している。|負荷を少なくしてクエリの再実行を試みてください。|  

##  <a name="impact"></a> 更新されたワード ブレーカーの影響について  
 各バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、通常、新しいワード ブレーカーが含まれています。これらのワード ブレーカーでは、言語の規則が改良されているため、以前のワード ブレーカーよりも精度が向上しています。 新しいワード ブレーカーは、前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]からインポートされたフルテキスト インデックスのワード ブレーカーとは少し動作が異なる場合もあります。
 
データベースが現在のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にアップグレードされたときにフルテキスト カタログをインポートした場合は、この動作の違いが重要になります。 フルテキスト カタログのフルテキスト インデックスで使用される 1 つまたは複数の言語が、新しいワード ブレーカーに関連付けられる可能性があります。 詳細については、「 [フルテキスト検索のアップグレード](../../relational-databases/search/upgrade-full-text-search.md)」を参照してください。  
 
## <a name="see-also"></a>参照  
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)    
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [フルテキスト検索に使用するストップワードとストップリストの構成と管理](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   

