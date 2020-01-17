---
title: フルテキスト インデックスの作成と管理 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], about
ms.assetid: f8a98486-5438-44a8-b454-9e6ecbc74f83
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c5e7595b421627266c7f08ca76588f481a19554f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257666"
---
# <a name="create-and-manage-full-text-indexes"></a>フルテキスト インデックスの作成と管理
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
このトピックでは、SQL Server でフルテキスト インデックスを作成、入力、および管理する方法について説明します。
  
## <a name="prerequisite---create-a-full-text-catalog"></a>前提条件 - フルテキスト カタログを作成する
フルテキスト インデックスを作成する前に、フルテキスト カタログを作成する必要があります。 カタログは、1 つまたは複数のフルテキスト インデックス用の仮想コンテナーです。 詳細については、「[Create and Manage Full-Text Catalogs](../../relational-databases/search/create-and-manage-full-text-catalogs.md)」 (フルテキスト インデックスの作成と管理) を参照してください。
  
##  <a name="tasks"></a>フルテキスト インデックスを作成、変更、または削除する  
### <a name="create-a-full-text-index"></a>フルテキスト インデックスを作成する  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)  
  
### <a name="alter-a-full-text-index"></a>フルテキスト インデックスを変更する
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
### <a name="drop-a-full-text-index"></a>フルテキスト インデックスを削除する 
  
-   [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)

## <a name="populate-a-full-text-index"></a>フルテキスト インデックスに入力する
フルテキスト インデックスを作成および保守するプロセスを *作成* ( *クロール*とも呼ばれます) といいます。 3 種類のフルテキスト インデックスの入力方法があります。
-   すべてのカタログの作成
-   変更の追跡に基づく作成
-   タイムスタンプに基づく増分作成

詳細については、「[Populate Full-Text Indexes](../../relational-databases/search/populate-full-text-indexes.md)」 (フルテキスト インデックスの作成) を参照してください。

##  <a name="view"></a> フルテキスト インデックスのプロパティを表示する
### <a name="view-the-properties-of-a-full-text-index-with-transact-sql"></a>Transact-SQL で、フルテキスト インデックスのプロパティを表示する

|カタログ ビューまたは動的管理ビュー|[説明]|  
|----------------------------------------|-----------------|  
|[sys.fulltext_index_catalog_usages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)|フルテキスト カタログからフルテキスト インデックスへの参照ごとに 1 行のデータを返します。|  
|[sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)|フルテキスト インデックスの一部となっている列ごとに 1 行のデータを格納します。|  
|[sys.fulltext_index_fragments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)|フルテキスト インデックスでは、フルテキスト インデックス フラグメントと呼ばれる内部テーブルを使用して逆インデックスのデータを保存します。 このビューを使用すると、これらのフラグメントに関するメタデータをクエリできます。 このビューは、フルテキスト インデックスが含まれているすべてのテーブルのフルテキスト インデックス フラグメントごとに 1 行のデータを格納しています。|  
|[sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)|表形式オブジェクトのフルテキスト インデックスごとに 1 行のデータを保持します。|  
|[sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)|指定されたテーブルのフルテキスト インデックスのコンテンツに関する情報を返します。|  
|[sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)|指定されたテーブルについて、フルテキスト インデックスのドキュメント レベルのコンテンツに関連する情報を返します。 個々のキーワードは、複数のドキュメントに出現する場合があります。|  
|[sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)|現在実行中の、フルテキスト インデックス設定に関する情報を返します。|  
 
### <a name="view-the-properties-of-a-full-text-index-with-management-studio"></a>Management Studio で、フルテキスト インデックスのプロパティを表示する 
1.  Management Studio で、オブジェクト エクスプローラーでサーバーを展開します。  
  
2.  **[データベース]** を展開し、フルテキスト インデックスを含むデータベースを展開します。  
  
3.  **[テーブル]** を展開します。  
  
4.  フルテキスト インデックスが定義されているテーブルを右クリックし、 **[フルテキスト インデックス]** コンテキスト メニューの **[フルテキスト インデックス]** をクリックして、 **[プロパティ]** をクリックします。 **[フルテキスト インデックスのプロパティ]** ダイアログ ボックスが表示されます。  
  
5.  **[ページの選択]** ペインでは、次のいずれかのページを選択できます。  
  
    |ページ|[説明]|  
    |----------|-----------------|  
    |**全般**|フルテキスト インデックスの基本的なプロパティが表示されます。 これには、いくつかの変更可能なプロパティと、データベース名、テーブル名、フルテキスト キー列の名前など多数の変更不可能なプロパティが含まれます。 変更可能なプロパティは次のとおりです。<br /><br /> **フルテキスト インデックス ストップリスト**<br /><br /> **フルテキスト インデックス有効**<br /><br /> **変更の追跡**<br /><br /> **検索プロパティ リスト**|  
    |**[列]**|フルテキスト インデックスを作成できるテーブル列が表示されます。 選択した列にフルテキスト インデックスが作成されます。 フルテキスト インデックスに含める列はいくつでも選択できます。 詳細については、「[Populate Full-Text Indexes](populate-full-text-indexes.md)」 (フルテキスト インデックスの作成) を参照してください。|
    |**スケジュール**|このページでは、フルテキスト インデックスを作成するためのテーブルの増分作成を開始する SQL Server エージェント ジョブのスケジュールを作成または管理できます。 詳細については、「[Populate Full-Text Indexes](../../relational-databases/search/populate-full-text-indexes.md)」 (フルテキスト インデックスの作成) を参照してください。<br /><br /> 注: **[フルテキスト インデックスのプロパティ]** ダイアログ ボックスを閉じると、新規作成したスケジュールが SQL Server エージェント ジョブ (*database_name*.*table_name* でテーブルの増分作成を開始) に関連付けられます。|  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] をクリックして変更を保存し、 **[フルテキスト インデックスのプロパティ]** ダイアログ ボックスを終了します。  
  
##  <a name="props"></a>インデックスが作成されたテーブルと列のプロパティの表示  
 OBJECTPROPERTYEX など、[!INCLUDE[tsql](../../includes/tsql-md.md)] 関数の中には、さまざまなフルテキスト インデックス プロパティの値を取得できるものがあります。 この情報は、フルテキスト検索の管理およびトラブルシューティングに役立ちます。  
  
 次の表に、インデックスが作成されたテーブルおよび列に関連したフルテキスト プロパティと、それに関連する [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数の一覧を示します。  
  
|プロパティ|[説明]|Function|  
|--------------|-----------------|--------------|  
|**FullTextTypeColumn**|列のドキュメント型情報を保持する、テーブル内の TYPE COLUMN。|[COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md)|  
|**IsFulltextIndexed**|列に対してフルテキスト インデックスを作成できるかどうかを示します。|COLUMNPROPERTY|  
|**IsFulltextKey**|インデックスがテーブルのフルテキスト キーであるかどうかを示します。|[INDEXPROPERTY](../../t-sql/functions/indexproperty-transact-sql.md)|  
|**TableFulltextBackgroundUpdateIndexOn**|テーブルがフルテキスト インデックスをバックグラウンドで更新できるかどうかを示します。|[OBJECTPROPERTYEX](../../t-sql/functions/objectpropertyex-transact-sql.md)|  
|**TableFulltextCatalogId**|テーブルのフルテキスト インデックス データが存在する、フルテキスト カタログ ID。|OBJECTPROPERTYEX|  
|**TableFulltextChangeTrackingOn**|テーブルでフルテキストの変更の追跡が有効になっているかどうかを示します。|OBJECTPROPERTYEX|  
|**TableFulltextDocsProcessed**|フルテキスト インデックス作成の開始以降に処理された行の数。|OBJECTPROPERTYEX|  
|**TableFulltextFailCount**|フルテキスト検索によるインデックスが設定されなかった行数。|OBJECTPROPERTYEX|  
|**TableFulltextItemCount**|フルテキスト インデックスが正常に設定された行数。|OBJECTPROPERTYEX|  
|**TableFulltextKeyColumn**|一意なフルテキスト キー列の列 ID。|OBJECTPROPERTYEX|  
|**TableFullTextMergeStatus**|現在マージ中のフルテキスト インデックスがテーブルにあるかどうかを示します。|OBJECTPROPERTYEX|  
|**TableFulltextPendingChanges**|変更の追跡が処理されていないエントリ数。|OBJECTPROPERTYEX|  
|**TableFulltextPopulateStatus**|フルテキスト テーブルの作成状態。|OBJECTPROPERTYEX|  
|**TableHasActiveFulltextIndex**|テーブルが有効なフルテキスト インデックスを持っているかどうかを示します。|OBJECTPROPERTYEX|  
  
##  <a name="key"></a>フルテキスト キー列の情報の取得  
 通常、行セット値関数 CONTAINSTABLE または FREETEXTTABLE の結果をベース テーブルと結合します。 その場合、一意なキー列の名前を把握している必要があります。 一意のインデックスがフルテキスト キーとして使用されているかどうかを調査したり、フルテキスト キー列の識別子を取得したりできます。  
  
### <a name="determine-whether-a-given-unique-index-is-used-as-the-full-text-key-column"></a>一意のインデックスがフルテキスト キー列として使用されているかどうかを調査する  
  
[SELECT](../../t-sql/queries/select-transact-sql.md) ステートメントを使用して、 [INDEXPROPERTY](../../t-sql/functions/indexproperty-transact-sql.md) 関数を呼び出します。 この関数呼び出しでは、次のように、OBJECT_ID 関数を使用してテーブル名 (*table_name*) をテーブル ID に変換します。その際、対象テーブルの一意のインデックスの名前と **IsFulltextKey** インデックス プロパティを指定します。  
  
```  
SELECT INDEXPROPERTY( OBJECT_ID('table_name'), 'index_name',  'IsFulltextKey' );  
```  
  
 このステートメントでは、このインデックスを使用してフルテキスト キー列の一意性を確保している場合には 1 が返され、そうでない場合には 0 が返されます。  
  
 **例**  
  
 次の例では、フルテキスト キー列の一意性を確保するために `PK_Document_DocumentID` インデックスが使用されているかどうかを確認します。  
  
```  
USE AdventureWorks  
GO  
SELECT INDEXPROPERTY ( OBJECT_ID('Production.Document'), 'PK_Document_DocumentID',  'IsFulltextKey' )  
```  
  
 `PK_Document_DocumentID` インデックスを使用してフルテキスト キー列の一意性が確保されている場合には 1 が返されます。 それ以外のときは 0 または NULL が返されます。 NULL は、無効なインデックス名が使用されている、インデックス名がテーブルに対応していない、テーブルが存在しないなどを意味します。  
  
### <a name="find-the-identifier-of-the-full-text-key-column"></a>フルテキスト キー列の識別子を検索する  
  
フルテキスト処理に対応する各テーブルには、テーブルの行を一意にするための列があります ("*一意なキー列*")。 OBJECTPROPERTYEX 関数で取得できる **TableFulltextKeyColumn** プロパティには、この一意なキー列の列 ID が格納されます。  
 
この識別子を取得するには、SELECT ステートメントで OBJECTPROPERTYEX 関数を呼び出します。 次のようにテーブル名 (*table_name*) をテーブル ID に変換する OBJECT_ID 関数を使用し、 **TableFulltextKeyColumn** プロパティを指定します。  
  
```  
SELECT OBJECTPROPERTYEX(OBJECT_ID( 'table_name'), 'TableFulltextKeyColumn' ) AS 'Column Identifier';  
```  
  
 **使用例**  
  
 次の例では、フルテキスト キー列の識別子または NULL が返されます。 NULL は、無効なインデックス名が使用されている、インデックス名がテーブルに対応していない、テーブルが存在しないなどを意味します。  
  
```  
USE AdventureWorks;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('Production.Document'), 'TableFulltextKeyColumn');  
GO  
```  
  
 次の例は、一意のキー列の識別子からその列の名前を取得する方法を示しています。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @key_column sysname  
SET @key_column = Col_Name(Object_Id('Production.Document'),  
ObjectProperty(Object_id('Production.Document'),  
'TableFulltextKeyColumn')   
)  
SELECT @key_column AS 'Unique Key Column';  
GO  
```  
  
 この例では、 `Unique Key Column`という名前の結果セット列が返され、Document テーブルの一意のキー列の名前 DocumentID を含む単一行が表示されます。 このクエリに無効なインデックス名が使用されている、インデックス名がテーブルに対応していない、テーブルが存在しないなどの場合には、NULL が返されます。  

## <a name="index-varbinarymax-and-xml-columns"></a>varbinary(max) 列および xml 列のインデックス  
 **varbinary(max)** 列、 **varbinary**列、または **xml** 列にフルテキスト インデックスが設定されている場合は、他のフルテキスト インデックス列と同様に、フルテキスト述語 (CONTAINS および FREETEXT) とフルテキスト関数 (CONTAINSTABLE および FREETEXTTABLE) を使用して、これらの列に対するクエリを実行できます。
   
### <a name="index-varbinarymax-or-varbinary-data"></a>varbinary(max) データまたは varbinary データのインデックス  
 単一の **varbinary(max)** 列、または **varbinary** 列は、さまざまな種類のドキュメントを格納できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、専用のフィルターがオペレーティング システムにインストールされ、使用できるようになっている任意のドキュメント型がサポートされます。 各ドキュメントのドキュメント型は、ドキュメントのファイル拡張子によって識別されます。 たとえば、ファイル拡張子が .doc である場合、フルテキスト検索では、Microsoft Word ドキュメントをサポートするフィルターが使用されます。 使用可能なドキュメント型の一覧を確認するには、 [sys.fulltext_document_types](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md) カタログ ビューに対してクエリを実行してください。  
  
Full-Text Engine では、オペレーティング システムにインストールされている既存のフィルターを利用できます。 オペレーティング システムのフィルター、ワード ブレーカー、およびステミング機能を使用する前に、次のコードを実行してこれらのリソースをサーバー インスタンスに読み込む必要があります。  
  
```sql  
EXEC sp_fulltext_service @action='load_os_resources', @value=1  
```  
  
**varbinary(max)** 列にフルテキスト インデックスを作成するには、Full-Text Engine が **varbinary(max)** 列にあるドキュメントのファイル拡張子にアクセスする必要があります。 この情報は、型列と呼ばれるテーブル列に格納されている必要があります。型列は、フルテキスト インデックスの **varbinary(max)** 列に関連付けられている必要があります。 Full-Text Engine は、ドキュメントにインデックスを作成する際に、型列のファイル拡張子を参照して、使用するフィルターを特定します。  
   
### <a name="index-xml-data"></a>xml データのインデックス  
 **xml** データ型の列には、XML ドキュメントと XML フラグメントのみが格納されます。XML ドキュメントには XML フィルターのみが使用されるため、 型列は必要ありません。 **xml** 列では、フルテキスト インデックスによって XML 要素のコンテンツにインデックスが設定されますが、XML マークアップは無視されます。 属性値には、数値でない限り、フルテキスト インデックスが設定されます。 要素タグはトークンの境界として使用されます。 複数言語を含む整形式の XML または HTML ドキュメントやフラグメントはサポートされます。  
  
 **xml** 列に対するインデックス作成とクエリの実行の詳細については、「[XML 列でのフルテキスト検索の使用](../../relational-databases/xml/use-full-text-search-with-xml-columns.md)」を参照してください。  
  
##  <a name="disable"></a> テーブルのフルテキスト インデックスを無効または再度有効にする   
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、既定によりユーザーが作成したすべてのデータベースでフルテキストが有効になります。 さらに、個々のテーブルに対してフルテキスト インデックスを作成し、これに列を追加すると、その時点で、このテーブルでは自動的にフルテキスト インデックスが有効になります。 フルテキスト インデックスから最後の列を削除すると、このテーブルでは自動的にフルテキスト インデックスが無効になります。  
  
 フルテキスト インデックスのあるテーブルでは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して手動でフルテキスト インデックスを無効にしたり、再度有効にしたりすることができます。  

1.  サーバー グループを展開し、 **[データベース]** を展開して、フルテキスト インデックスを有効にするテーブルを含むデータベースを展開します。  
  
2.  **[テーブル]** を展開し、フルテキスト インデックスを無効または再度有効にするテーブルを右クリックします。  
  
3.  **[フルテキスト インデックス]** を選択し、 **[フルテキスト インデックスを無効化]** または **[フルテキスト インデックスを有効化]** をクリックします。  
  
##  <a name="remove"></a>テーブルからフルテキスト インデックスを削除する  
  
1.  オブジェクト エクスプローラーで、削除するフルテキスト インデックスが含まれているテーブルを右クリックします。  
  
2.  **[フルテキスト インデックスの削除]** を選択します。  
  
3.  フルテキスト インデックスの削除を確認するメッセージが表示されたら、 **[OK]** をクリックします。  
  
  
