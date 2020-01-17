---
title: フルテキスト検索に使用するストップワードとストップリストの構成と管理
ms.date: 02/02/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], noise words
- noise words [full-text search]
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 43b5ce7b-9f09-4443-8a5b-c3da6eb28bcc
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: 872f5207f673c5047475220b1da01a41678c1c6d
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056139"
---
# <a name="configure-and-manage-stopwords-and-stoplists-for-full-text-search"></a>フルテキスト検索に使用するストップワードとストップリストの構成と管理
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  フルテキスト インデックスが肥大化するのを防ぐため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、頻繁に出現する、検索に役立たない文字列を破棄するメカニズムがあります。 破棄されるこのような文字列を *ストップワード*と呼びます。 インデックスの作成中、Full-Text Engine により、フルテキスト インデックスからストップワードが除外されます。 つまり、フルテキスト クエリでは、ストップワードが検索されません。  
   
**ストップワード**」を参照してください。 ストップワードには、特定の言語で意味を持つ単語を指定できます。 たとえば、英語では、"a"、"and"、"is"、"the" などの単語は、検索に役立たないことが知られているため、フルテキスト インデックスから除外されます。 また、ストップワードは言語的な意味を持たない*トークン*でも構いません。  

**ストップリスト**。 ストップワードは、ストップリストと呼ばれるオブジェクトを使用してデータベースで管理されます。 *ストップリスト* は、フルテキスト インデックスに関連付けられている場合、そのインデックスのフルテキスト クエリに適用されるストップワードの一覧です。
   
## <a name="use-an-existing-stoplist"></a>既存のストップリストを使用する  
 次の方法で既存のストップリストを使用できます。  
  
-   データベースにシステムによって用意されたストップリストを使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、よく使用されるストップワードを含むシステム ストップリストが、サポート対象の言語ごとに用意されています。つまり、既定で、特定のワード ブレーカーに関連付けられている言語ごとにストップリストが用意されています。 システム ストップリストをコピーし、ストップワードを追加したり削除したりして、そのコピーをカスタマイズできます。  
  
     システム ストップリストは [Resource](../../relational-databases/databases/resource-database.md) データベースにインストールされます。  
  
-   現在のサーバー インスタンスで他のデータベースの既存のカスタム ストップリストを使用して、適宜、ストップワードを追加および削除します。  
  
## <a name="create-a-new-stoplist"></a>新しいストップリストを作成する 
### <a name="create-a-new-stoplist-with-transact-sql"></a>Transact SQL で新しいストップリストを作成する
[CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md) を使用します。

### <a name="create-a-new-stoplist-with-management-studio"></a>Management Studio で新しいストップリストを作成する
  
1.  オブジェクト エクスプローラーで、サーバーを展開します。  
  
2.  **[データベース]** を展開し、フルテキスト ストップリストを作成する対象のデータベースを展開します。  
  
3.  **[ストレージ]** を展開し、 **[フルテキスト ストップリスト]** を右クリックします。  
  
4.  **[新しいフルテキスト ストップリスト]** をクリックします。  
  
5.  新しいストップリストの名前を入力します。  
  
6.  必要に応じて、他のユーザーをストップリストの所有者として指定します。  
  
7.  次に示すストップリスト作成オプションのいずれかを選択します。  
  
    -   **[空のストップリストを作成する]**  
  
    -   **[システム ストップリストから作成する]**  
  
    -   **[既存のフルテキスト ストップリストから作成する]**  
  
     詳細については、「[新しいフルテキスト ストップリスト &#40;[全般] ページ&#41;](https://msdn.microsoft.com/library/97f8e82d-82ab-4525-91c9-1ee3ae217309)」を参照してください。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="use-a-stoplist-in-full-text-queries"></a>フルテキスト クエリでのストップリストの使用  
 クエリでストップリストを使用するには、ストップリストをフルテキスト インデックスに関連付ける必要があります。 インデックスの作成時にストップリストをフルテキスト インデックスにアタッチしたり、後でインデックスを変更してストップリストを追加したりできます。  
  
### <a name="create-a-full-text-index-and-associate-a-stoplist-with-it"></a>フルテキスト インデックスを作成してストップリストを関連付ける
[CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md) を使用します。
  
### <a name="associate-or-disassociate-a-stoplist-with-an-existing-full-text-index"></a>既存のフルテキスト インデックスに対してストップリストの関連付けまたは関連付け解除を行う
[ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md) を使用します。 
  
## <a name="change-the-stopwords-in-a-stoplist"></a>ストップリストのストップワードの変更  
### <a name="add-or-drop-stopwords-from-a-stoplist-with-transact-sql"></a>Transact-SQL でストップリストからストップワードを追加または削除する
[ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md) を使用します。
  
### <a name="add-or-drop-stopwords-from-a-stoplist-with-management-studio"></a>Management Studio でストップリストからストップワードを追加または削除する  
  
1.  オブジェクト エクスプローラーで、サーバーを展開します。  
  
2.  **[データベース]** を展開し、データベースを展開します。  
  
3.  **[ストレージ]** を展開し、 **[フルテキスト ストップリスト]** をクリックします。  
  
4.  プロパティを変更するストップリストを右クリックし、 **[プロパティ]** をクリックします。  
  
5.  [[フルテキスト ストップリストのプロパティ]](https://msdn.microsoft.com/library/2e907f5b-0cf9-484a-afcf-a4e7f1e2f87f) ダイアログ ボックスで:  
  
    1.  **[アクション]** リスト ボックスで、次のいずれかのアクションを選択します。 **[ストップワードの追加]** 、 **[ストップワードの削除]** 、 **[Delete all stopwords]\(すべてのストップワードの削除\)** 、または **[ストップリストのクリア]** 。  
  
    2.  選択したアクションに対して **[ストップワード]** ボックスが有効になっている場合は、単一のストップワードを入力します。 このストップワードは一意である必要があります。つまり、選択した言語で、このストップリストにまだ含まれていないものである必要があります。  
  
    3.  選択したアクションに対して **[フルテキスト言語]** ボックスの一覧が有効になっている場合は、言語を選択します。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="manage-stoplists-and-their-usage"></a>ストップ リストとその使用の管理
  
### <a name="view-all-the-stopwords-in-a-stoplist"></a>ストップリスト内のすべてのストップワードの表示
[sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md) を使用します。 
  
### <a name="get-info-about-all-the-stoplists-in-the-current-database"></a>現在のデータベース内にあるすべてのストップリストに関する情報を取得する
[sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md) と [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md) を使用します。
  
### <a name="view-the-tokenization-result-of-a-word-breaker-thesaurus-and-stoplist-combination"></a>ワード ブレーカー、類語辞典、ストップリストの組み合わせによるトークン化の結果を表示する
[sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md) を使用します。

### <a name="suppress-an-error-message-if-stopwords-cause-a-boolean-operation-on-a-full-text-query-to-fail"></a>ストップワードが原因でフルテキスト クエリのブール演算が失敗する場合に、エラー メッセージを非表示にする
[transform noise words サーバー構成オプション](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md) を使用します。 
   
## <a name="more-info-about-stopword-position"></a>ストップ ワードの位置に関する詳細情報
 含まれるストップワードは無視されますが、フルテキスト インデックスではその位置が考慮されます。 たとえば、"Instructions are applicable to these Adventure Works Cycles models" という句があるとします。 以下のテーブルは、句の中の語の位置を表しています。  
  
|Word|[位置]|  
|----------|--------------|  
|Instructions|1|  
|are|2|  
|applicable|3|  
|から|4|  
|these|5|  
|Adventure|6|  
|Works|7|  
|Cycles|8|  
|モデル|9|  
  
 位置 2、4、および 5 にあるストップワード "are"、"to"、"these" は、フルテキスト インデックスから除外されます。 ただし、その位置情報は保持されるため、語句内の他の語の位置は変わりません。   
  
## <a name="upgrade-noise-words-from-sql-server-2005"></a>SQL Server 2005 からのノイズ ワードのアップグレード  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] のノイズ ワードは、ストップワードになりました。 データベースが [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]からアップグレードされると、ノイズ ワード ファイルは使用されなくなります。 ただし、ノイズ ワード ファイルは FTDATA\ FTNoiseThesaurusBak フォルダーに保存され、後で更新する際、または対応するストップリストを作成する際に使用できます。 ノイズ ワード ファイルをストップリストにアップグレードする方法の詳細については、「 [フルテキスト検索のアップグレード](../../relational-databases/search/upgrade-full-text-search.md)」を参照してください。  
  
  
  
