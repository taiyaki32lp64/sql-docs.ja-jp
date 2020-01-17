---
title: フルテキスト検索の概要 | Microsoft Docs
ms.date: 08/22/2016
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text indexes [SQL Server], creating
- full-text search [SQL Server], about
- full-text search [SQL Server], setting up
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 349e00b7734ed8e8176585c55018b7565649cc1f
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72903824"
---
# <a name="get-started-with-full-text-search"></a>フルテキスト検索の概要
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
SQL Server データベースでは、フルテキストが既定で有効になっています。 ただし、フルテキスト クエリを実行するには、事前にフルテキスト カタログを作成し、検索するテーブルまたはインデックス付きビューにフルテキスト インデックスを作成しておく必要があります。

## <a name="set-up-full-text-search-in-two-steps"></a>フルテキスト検索をセットアップする 2 つの手順
フルテキスト検索をセットアップする基本的な手順は 2 つあります。  
1.  フルテキスト カタログを作成します。  
2.  検索するテーブルまたはインデックス付きビューにフルテキスト インデックスを作成します。 

各フルテキスト インデックスは、フルテキスト カタログに属している必要があります。 フルテキスト インデックスごとにテキスト カタログを作成するか、複数のフルテキスト インデックスを特定のカタログに関連付けることができます。 フルテキスト カタログは仮想オブジェクトであり、ファイル グループには属しません。 カタログは、フルテキスト インデックスのグループを指す論理的概念です。

> [!NOTE]
> これらの手順では、SQL Server のインストール時にオプションのフルテキスト検索コンポーネントをインストールしていると想定しています。 インストールしていない場合は、SQL Server セットアップを再実行して追加する必要があります。  

## <a name="set-up-full-text-search-with-a-wizard"></a>ウィザードでフルテキスト検索をセットアップする 
 
ウィザードを使用してフルテキスト検索をセットアップする方法については、「[Use the Full-Text Indexing Wizard](../../relational-databases/search/use-the-full-text-indexing-wizard.md)」 (フルテキスト インデックス作成ウィザードの使用) を参照してください。

## <a name="set-up-full-text-search-with-transact-sql"></a>Transact-SQL でフルテキスト検索をセットアップする 
 次の 2 部構成の例では、AdventureWorks サンプル データベースに `AdvWksDocFTCat` という名前のフルテキスト カタログを作成し、次に、サンプル データベースの `Document` テーブルにフルテキスト インデックスを作成します。 このステートメントによって、SQL Server のセットアップ時に指定した既定のディレクトリ内にフルテキスト カタログが作成されます。 `AdvWksDocFTCat` というフォルダーが既定のディレクトリ内にあります。  
  
1.  `AdvWksDocFTCat`という名前のフルテキスト カタログを作成するために、この例では、 [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md) ステートメントを使用します。  
  
    ```sql
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
    詳細については、「[Create and Manage Full-Text Catalogs](../../relational-databases/search/create-and-manage-full-text-catalogs.md)」 (フルテキスト インデックスの作成と管理) を参照してください。
 
2.  Document テーブルにフルテキスト インデックスを作成する前に、テーブルに一意の単一列で NULL 値にならないインデックスが含まれていることを確認します。 次の [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) ステートメントでは、Document テーブルの DocumentID 列に、一意のインデックス `ui_ukDoc`を作成します。  
  
    ```sql 
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
    ```  

3.  一意のキーを作成したら、次の `Document` CREATE FULLTEXT INDEX [ステートメントを使用して、](../../t-sql/statements/create-fulltext-index-transact-sql.md) テーブルにフルテキスト インデックスを作成できます。  
  
    ```sql  
    CREATE FULLTEXT INDEX ON Production.Document  
    (  
        Document                         --Full-text index column name   
            TYPE COLUMN FileExtension    --Name of column that contains file type information  
            Language 2057                 --2057 is the LCID for British English  
    )  
    KEY INDEX ui_ukDoc ON AdvWksDocFTCat --Unique index  
    WITH CHANGE_TRACKING AUTO            --Population type;  
    GO  
  
    ```  
  
     この例で定義する TYPE COLUMN では、"Document" 列 (バイナリ型) の各行のドキュメント型が含まれる、テーブルの型列を指定します。 この型列には、特定の行のドキュメントのユーザー指定ファイル拡張子 (".doc"、".xls" など) が格納されます。 Full-Text Engine では、特定の行のファイル拡張子を使用して、その行のデータを解析するために使用する正しいフィルターを呼び出します。 フィルターで行のバイナリ データが解析された後は、指定したワード ブレーカーで内容が解析されます (この例では、英語 (英国) のワード ブレーカーが使用されます)。詳細については、「 [検索用フィルターの構成と管理](../../relational-databases/search/configure-and-manage-filters-for-search.md)」を参照してください。  

    詳細については、「[Create and Manage Full-Text Indexes](../../relational-databases/search/create-and-manage-full-text-indexes.md)」 (フルテキスト インデックスの作成と管理) を参照してください。

##  <a name="options"></a> フルテキスト インデックスのオプションの選択 
  
### <a name="choose-a-language"></a>言語の選択  
 列の言語の選択については、「 [フルテキスト インデックス作成時の言語の選択](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)」をご覧ください。  
  
### <a name="choose-a-filegroup"></a>ファイルグループの選択  
 フルテキスト インデックスを構築するプロセスでは、大量の I/O が発生します。 要約すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータの読み取りと、フィルター処理されたデータのフルテキスト インデックスへの反映で構成されます。 I/O パフォーマンスの最大化に最適なデータベース ファイル グループにフルテキスト インデックスを配置するか、他のボリュームの別のファイル グループにフルテキスト インデックスを配置することをお勧めします。
  
### <a name="choose-a-full-text-catalog"></a>フルテキスト カタログの選択   
 
 変更が少ないテーブル、変更が多いテーブル、または特定の時間帯に頻繁に変更されるテーブルなど、同じ更新特性を持つテーブルは、同じフルテキスト カタログの下にまとめて関連付けることをお勧めします。 フルテキスト カタログの作成スケジュールをセットアップすると、データベースの利用率が高いときでもデータベース サーバーのリソース使用に大きな影響を及ぼすことなく、フルテキスト インデックスとテーブルの同期が維持されるようになります。  
  
 次のガイドラインを考慮してください。  
  
-   数百万の行を持つテーブルにインデックスを作成する場合は、そのテーブル専用のフルテキスト カタログを割り当ててください。  
  
-   フルテキスト インデックスを作成するテーブル内の変更量だけではなく、そのテーブル内の行の総数についても考慮してください。 変更される行と、最後にフルテキスト インデックスを作成したときにテーブル内に存在した行の総数が数百万行に及ぶ場合は、そのテーブルを専用のフルテキスト カタログに割り当ててください。  

### <a name="associate-a-unique-index"></a>一意のインデックスを関連付ける
常に、一意なフルテキスト キーに利用可能な最小の一意なインデックスを選択してください。 4 バイトで、整数ベースのインデックスが最適です。これにより、ファイル システム内の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search サービスで必要となるリソースが大幅に減少します。 主キーが大きい場合 (100 バイト以上)、テーブル内の他の一意なインデックスを選択するか、または他の一意なインデックスを作成して、フルテキスト インデックス用のキーにすることを検討してください。 そうしないと、一意なフルテキスト キーのサイズが最大サイズ (900 バイト) を超えた場合、フルテキストの作成を続行できなくなります。  
 
### <a name="associate-a-stoplist"></a>ストップリストを関連付ける   
  *ストップリスト* は、ストップワード (ノイズ ワードとも呼ばれます) の一覧です。 ストップリストは各フルテキスト インデックスに関連付けられ、そのストップリスト内の単語がそのインデックスのフルテキスト クエリに適用されます。 既定では、システム ストップリストは、新しいフルテキスト インデックスに関連付けられます。 独自のストップリストを作成して使用することもできます。   
  
 たとえば、次の [CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでは、システム ストップリストからコピーして、myStoplist という名前の新しいフルテキスト ストップリストを作成します。  
  
```sql  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 次の [ALTER FULLTEXT STOPLIST](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでは、myStoplist という名前のストップリストを変更して、単語 'en' をまずスペイン語用に、次にフランス語用に追加します。  
  
```sql  
ALTER FULLTEXT STOPLIST myStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST myStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
詳細については、「 [フルテキスト検索に使用するストップワードとストップリストの構成と管理](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)」を参照してください。

## <a name="update-a-full-text-index"></a>フルテキスト インデックスを更新する  
 標準の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インデックスと同様に、フルテキスト インデックスは、関連付けられたテーブルの中でデータが変更されると、自動的に更新されます。 これは既定の動作です。 指定したスケジュール間隔または手動でフルテキスト インデックスを最新の状態に保つこともできます。 フルテキスト インデックスの作成には時間がかかり、リソースが大量に消費される可能性があります。 そのため、インデックスの更新は、通常、非同期プロセスで実行します。この非同期プロセスは、バックグラウンドで実行され、ベース テーブルの変更後にフルテキスト インデックスを最新の状態に維持します。 
 
ベース テーブルのそれぞれの変更後すぐにフルテキスト インデックスを更新した場合にも、リソースが大量に消費されます。 そのため、更新、挿入、または削除の率が高い場合は、クエリのパフォーマンスが低下する可能性があります。 この問題が発生した場合、リソースについてクエリと競合しないよう、手動による変更追跡の更新をスケジュール設定して、適宜、大量の変更に対応することを検討してください。  
  
詳細については、「[Populate Full-Text Indexes](../../relational-databases/search/populate-full-text-indexes.md)」 (フルテキスト インデックスの作成) を参照してください。 

## <a name="next-steps"></a>次の手順
SQL Server フルテキスト検索をセットアップすると、フルテキスト クエリを実行できます。 詳細については、「[Query with Full-Text Search](../../relational-databases/search/query-with-full-text-search.md)」 (フルテキスト検索でのクエリ) を参照してください。
