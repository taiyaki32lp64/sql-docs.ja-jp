---
title: フルテキスト検索の概要 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text indexes [SQL Server], creating
- full-text search [SQL Server], about
- full-text search [SQL Server], setting up
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fd5ced641ee8fc17f0be7d7b6e19aff17dcb69bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011288"
---
# <a name="get-started-with-full-text-search"></a>フルテキスト検索の概要
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータベースでは、フルテキストが既定で有効になっています。 ただし、テーブルでフルテキスト インデックスを使用するには、Full-Text Engine を使用してアクセスするテーブルの列に対してフルテキスト インデックス作成機能をセットアップする必要があります。  
  
##  <a name="configure"></a> データベースのフルテキスト検索の構成  
 どのシナリオでも、データベース管理者は次の基本的な手順を実行して、データベースでフルテキスト検索用のテーブル列を構成します。  
  
1.  フルテキスト カタログを作成します。  
  
2.  検索する各テーブルに、次の方法でフルテキスト インデックスを作成します。  
  
    1.  フルテキスト インデックスに含めるテキスト列を特定します。  
  
    2.  指定された列にバイナリ データとして格納されているドキュメントが含まれるかどうか (`varbinary(max)`、または`image`データ)、テーブルの列を指定する必要があります (、*型の列*) インデックスが作成される列内の各ドキュメントの種類を識別します。  
  
    3.  列内のドキュメントに対してフルテキスト検索で使用される言語を指定します。  
  
    4.  ベース テーブルとその列での変更を追跡するためにフルテキスト インデックスで使用する変更追跡メカニズムを選択します。  
  
 フルテキスト検索では、ワード ブレーカー、ステマー、ストップワード (ノイズ ワードとも呼ばれます) を含んだストップリスト、類義語辞典ファイルの各*言語コンポーネント*を使用して、複数の言語がサポートされます。 類義語辞典ファイルと (場合によって) ストップリストは、データベース管理者が構成する必要があります。 特定の類義語辞典ファイルは、対応する言語を使用するすべてのフルテキスト インデックスをサポートし、特定のストップリストには任意の数のフルテキスト インデックスを関連付けることができます。  
  
##  <a name="setup"></a> フルテキスト カタログとインデックスを設定します。  
 この作業には、次の基本的な手順が含まれます。  
  
1.  フルテキスト インデックスを格納するフルテキスト カタログを作成する。  
  
     各フルテキスト インデックスは、フルテキスト カタログに属している必要があります。 フルテキスト インデックスごとにテキスト カタログを作成するか、複数のフルテキスト インデックスを特定のカタログに関連付けることができます。 フルテキスト カタログは仮想オブジェクトであり、ファイル グループには属しません。 カタログは、フルテキスト インデックスのグループを指す論理的概念です。  
  
2.  テーブルまたはインデックス付きビューで、フルテキスト インデックスを作成する。  
  
     フルテキスト インデックスは、Full-Text Engine により構築および管理されるトークンベースの特殊な機能インデックスです。 テーブルまたはビューにフルテキスト検索を作成するには、そのテーブルまたはビューに、単一列で非 NULL 値の一意なインデックスが作成されている必要があります。 Full-Text Engine では、テーブルの各行を一意の圧縮可能なキーにマップするために、この一意のインデックスが必要になります。 フルテキスト インデックスには、`char`、`varchar`、`nchar`、`nvarchar`、`text`、`ntext`、`image`、`xml`、`varbinary`、`varbinary(max)` 型の列を含めることができます。 詳細については、「 [フルテキスト インデックスの作成と管理](create-and-manage-full-text-indexes.md)」をご覧ください。  
  
 フルテキスト インデックスの作成について学習する前に、フルテキスト インデックスと標準の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インデックスの違いを見ることが重要です。 次の表に、両方のインデックスの相違点を示します。  
  
|フルテキスト インデックス|標準の SQL Server インデックス|  
|------------------------|--------------------------------|  
|1 つのテーブルに対し、1 つのフルテキスト インデックスしか使用できません。|1 つのテーブルに対し、複数の標準インデックスを使用できます。|  
|フルテキスト インデックスへのデータの追加は*作成*と呼ばれ、スケジュールによる要求または個別の要求のどちらかを通じて要求できます。または、新規データの追加と共に自動的に行うことができます。|関連するデータが挿入、更新、または削除されたときに、自動的に更新されます。|  
|同じデータベース内で 1 つ以上のフルテキスト カタログにグループ化されます。|グループ化されません。|  
  
  
##  <a name="options"></a> フルテキスト インデックスのオプションを選択します。  
 ここでは、次について説明します。  
  
-   列の言語の選択  
  
-   フルテキスト インデックスのファイル グループの選択  
  
-   フルテキスト カタログへのフルテキスト インデックスの割り当て  
  
-   ストップリストとフルテキスト インデックスの関連付け  
  
-   フルテキスト インデックスの更新  
  
### <a name="choosing-the-column-language"></a>列の言語の選択  
 列の言語を選択する際の考慮点については、「[フルテキスト インデックス作成時の言語の選択](choose-a-language-when-creating-a-full-text-index.md)」を参照してください。  
  
### <a name="choosing-a-filegroup-for-a-full-text-index"></a>フルテキスト インデックスのファイル グループの選択  
 フルテキスト インデックスの作成処理では、I/O が非常に集中します (高い頻度で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からデータを読み取り、フィルター選択されたデータをフルテキスト インデックスに反映するため)。 I/O パフォーマンスの最大化に最適なデータベース ファイル グループにフルテキスト インデックスを配置するか、他のボリュームの別のファイル グループにフルテキスト インデックスを配置することをお勧めします。  
  
 管理のしやすさが重要である場合は、テーブル データと関連するフルテキスト カタログは同じファイル グループに格納することをお勧めします。 パフォーマンス上の理由から、別々のボリュームに格納されている別々のファイル グループにテーブル データとフルテキスト インデックスを配置して、I/O 並列処理を最大限に高めることが必要になる場合もあります。  
  
  
### <a name="assigning-the-full-text-index-to-a-full-text-catalog"></a>フルテキスト カタログへのフルテキスト インデックスの割り当て  
 フルテキスト カタログ内のテーブルに対するフルテキスト インデックスの割り当てを立案することは重要です。  
  
 変更が少ないテーブル、変更が多いテーブル、または特定の時間帯に頻繁に変更されるテーブルなど、同じ更新特性を持つテーブルは、同じフルテキスト カタログの下にまとめて関連付けることをお勧めします。 フルテキスト カタログの作成スケジュールをセットアップすると、データベースの利用率が高いときでもデータベース サーバーのリソース使用に大きな影響を及ぼすことなく、フルテキスト インデックスとテーブルの同期が維持されるようになります。  
  
 フルテキスト カタログにテーブルを割り当てる際には、次のガイドラインを考慮してください。  
  
-   常に、一意なフルテキスト キーに利用可能な最小の一意なインデックスを選択してください。 4 バイトで、整数ベースのインデックスが最適です。これにより、ファイル システム内の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search サービスで必要となるリソースが大幅に減少します。 主キーが大きい場合 (100 バイト以上)、テーブル内の他の一意なインデックスを選択するか、または他の一意なインデックスを作成して、フルテキスト インデックス用のキーにすることを検討してください。 そうしないと、一意なフルテキスト キーのサイズが最大サイズ (900 バイト) を超えた場合、フルテキストの作成を続行できなくなります。  
  
-   数百万の行を持つテーブルにインデックスを作成しようとしている場合、そのテーブル専用のフルテキスト カタログを割り当ててください。  
  
-   フルテキスト インデックスを作成するテーブル内の変更量だけではなく、そのテーブル内の行の総数についても考慮してください。 変更される行と、最後にフルテキスト インデックスを作成したときにテーブル内に存在した行の総数が数百万行に及ぶ場合は、そのテーブルを専用のフルテキスト カタログに割り当ててください。  
  
  
### <a name="associating-a-stoplist-with-the-full-text-index"></a>ストップリストとフルテキスト インデックスの関連付け  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] では、ストップリストが導入されています。 *ストップリスト* は、ストップワード (ノイズ ワードとも呼ばれます) の一覧です。 ストップリストは各フルテキスト インデックスに関連付けられ、そのストップリスト内の単語がそのインデックスのフルテキスト クエリに適用されます。 既定では、システム ストップリストは、新しいフルテキスト インデックスに関連付けられます。 ただし、独自のストップリストを作成して使用することもできます。 詳細については、「 [フルテキスト検索に使用するストップワードとストップリストの構成と管理](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)」を参照してください。  
  
 たとえば、次[CREATE FULLTEXT STOPLIST](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)]ステートメント、システム ストップ リストからコピーして、myStoplist3 という名前、新しいフルテキスト ストップ リストを作成します。  
  
```  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 次[ALTER FULLTEXT STOPLIST](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)]ステートメントでは、単語 'en' をまずスペイン語用、フランス語を追加すること、myStoplist という名前のストップ リストを変更します。  
  
```  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
  
  
### <a name="updating-a-full-text-index"></a>フルテキスト インデックスの更新  
 標準の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インデックスと同様に、フルテキスト インデックスは、関連付けられたテーブルの中でデータが変更されると、自動的に更新されます。 これは既定の動作です。 指定したスケジュール間隔または手動でフルテキスト インデックスを最新の状態に保つこともできます。 フルテキスト インデックスの作成は時間とリソースの消費が大きいため、インデックスの更新は、通常、非同期プロセスで実行します。この非同期プロセスは、バックグラウンドで実行され、ベース テーブルの変更後にフルテキスト インデックスを最新の状態に維持します。 ベース テーブルのそれぞれの変更後すぐにフルテキスト インデックスを更新すると、リソースを大量に消費することがあります。 そのため、更新、挿入、または削除の率が非常に高い場合は、クエリのパフォーマンスが低下する可能性があります。 この問題が発生した場合、リソースについてクエリと競合しないよう、手動による変更追跡の更新をスケジュール設定して、適宜、大量の変更に対応することを検討してください。  
  
 作成状態を監視するには、FULLTEXTCATALOGPROPERTY 関数または OBJECTPROPERTYEX 関数を使用します。 カタログ作成状態を取得するには、次のステートメントを実行します。  
  
```  
SELECT FULLTEXTCATALOGPROPERTY('AdvWksDocFTCat', 'Populatestatus');  
```  
  
 通常、カタログ全体の作成を実行している間は、結果として 1 が返されます。  
  
  
##  <a name="example"></a> 例: フルテキスト検索のセットアップ  
 次の 2 部構成の例では、AdventureWorks データベースに `AdvWksDocFTCat` という名前のフルテキスト カタログを作成し、次に、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] の `Document` テーブルにフルテキスト インデックスを作成します。 このステートメントによって、セットアップ時に指定した既定のディレクトリ内にフルテキスト カタログが作成されます。 `AdvWksDocFTCat` というフォルダーが既定のディレクトリ内にあります。  
  
1.  `AdvWksDocFTCat` という名前のフルテキスト カタログを作成するために、この例では、[CREATE FULLTEXT CATALOG](/sql/t-sql/statements/create-fulltext-catalog-transact-sql) ステートメントを使用します。  
  
    ```  
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
  
2.  Document テーブルにフルテキスト インデックスを作成する前に、テーブルに一意の単一列で NULL 値にならないインデックスが含まれていることを確認します。 次の [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql) ステートメントでは、Document テーブルの DocumentID 列に、一意のインデックス `ui_ukDoc`を作成します。  
  
    ```  
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
    ```  
  
3.  一意のキーを作成したら、次の `Document` CREATE FULLTEXT INDEX [ステートメントを使用して、](/sql/t-sql/statements/create-fulltext-index-transact-sql) テーブルにフルテキスト インデックスを作成できます。  
  
    ```  
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
  
     この例で定義する TYPE COLUMN では、"Document" 列 (バイナリ型) の各行のドキュメント型が含まれる、テーブルの型列を指定します。 型の列は、特定の行で、ユーザー指定のファイル拡張機能-".doc"、".xls"などとなどのドキュメントを格納します。 Full-Text Engine では、特定の行のファイル拡張子を使用して、その行のデータを解析するために使用する正しいフィルターを呼び出します。 その行のバイナリ データをフィルターが解析した後、指定されたワード ブレーカーがコンテンツを解析します (この例では、英語 (U.K.) のワード ブレーカーを使用します)。 フィルター処理が行われるのは、インデックス作成時か、フルテキスト インデックスへの自動変更追跡が有効になっている場合にユーザーがベース テーブルで列を挿入または列を更新したときだけである点に注意してください。 詳細については、「 [検索用フィルターの構成と管理](configure-and-manage-filters-for-search.md)」を参照してください。  
  
  
##  <a name="tasks"></a> 一般的なタスク  
  
### <a name="to-create-a-full-text-catalog"></a>フルテキスト カタログを作成するには  
  
-   [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)  
  
-   [フルテキスト カタログの作成と管理](create-and-manage-full-text-catalogs.md)  
  
### <a name="to-view-the-indexes-of-a-table-or-view"></a>テーブル (またはビュー) のインデックスを表示するには  
  
-   [sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)  
  
### <a name="to-create-a-unique-index"></a>一意のインデックスを作成するには  
  
-   [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
-   [テーブル デザイナーを開く &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)  
  
### <a name="to-create-a-full-text-index"></a>フルテキスト インデックスを作成するには  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
-   [フルテキスト インデックスの作成と管理](create-and-manage-full-text-indexes.md)  
  
### <a name="to-view-information-about-a-full-text-index"></a>フルテキスト インデックスに関する情報を表示するには  
  
|カタログ ビューまたは動的管理ビュー|説明|  
|----------------------------------------|-----------------|  
|[sys.fulltext_index_catalog_usages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql)|フルテキスト カタログからフルテキスト インデックスへの参照ごとに 1 行のデータを返します。|  
|[sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)|フルテキスト インデックスの一部となっている列ごとに 1 行のデータを格納します。|  
|[sys.fulltext_index_fragments &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql)|フルテキスト インデックスでは、フルテキスト インデックス フラグメントと呼ばれる内部テーブルを使用して逆インデックスのデータを保存します。 このビューを使用すると、これらのフラグメントに関するメタデータをクエリできます。 このビューは、フルテキスト インデックスが含まれているすべてのテーブルのフルテキスト インデックス フラグメントごとに 1 行のデータを格納しています。|  
|[sys.fulltext_indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql)|表形式オブジェクトのフルテキスト インデックスごとに 1 行のデータを保持します。|  
|[sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql)|指定されたテーブルのフルテキスト インデックスのコンテンツに関する情報を返します。|  
|[sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql)|指定されたテーブルについて、フルテキスト インデックスのドキュメント レベルのコンテンツに関連する情報を返します。 個々のキーワードは、複数のドキュメントに出現する場合があります。|  
|[sys.dm_fts_index_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)|現在実行中の、フルテキスト インデックス設定に関する情報を返します。|  
  
  
## <a name="see-also"></a>参照  
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)   
 [フルテキスト インデックスの作成](populate-full-text-indexes.md)   
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)  
  
  
