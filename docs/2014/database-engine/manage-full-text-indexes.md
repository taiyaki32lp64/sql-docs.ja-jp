---
title: フルテキスト インデックスの管理 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
ms.assetid: 28ff17dc-172b-4ac4-853f-990b5dc02fd1
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 459bdc20c9698a8b6271092c57ed0de936c4d7f2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775044"
---
# <a name="manage-full-text-indexes"></a>フルテキスト インデックスの管理
     
##  <a name="view"></a> 表示して、フルテキスト インデックスのプロパティを変更します。  
  
#### <a name="to-view-or-change-the-properties-of-a-full-text-index-in-management-studio"></a>Management Studio でフルテキスト インデックスのプロパティを表示または変更するには  
  
1.  オブジェクト エクスプローラーで、サーバーを展開します。  
  
2.  **[データベース]** を展開し、フルテキスト インデックスを含むデータベースを展開します。  
  
3.  **[テーブル]** を展開します。  
  
4.  フルテキスト インデックスが定義されているテーブルを右クリックし、 **[フルテキスト インデックス]** コンテキスト メニューの **[フルテキスト インデックス]** をクリックして、 **[プロパティ]** をクリックします。 **[フルテキスト インデックスのプロパティ]** ダイアログ ボックスが表示されます。  
  
5.  **[ページの選択]** ペインでは、次のいずれかのページを選択できます。  
  
    |ページ|説明|  
    |----------|-----------------|  
    |**全般**|フルテキスト インデックスの基本的なプロパティが表示されます。 これには、いくつかの変更可能なプロパティと、データベース名、テーブル名、フルテキスト キー列の名前など多数の変更不可能なプロパティが含まれます。 変更可能なプロパティは次のとおりです。<br /><br /> **フルテキスト インデックス ストップリスト**<br /><br /> **フルテキスト インデックス有効**<br /><br /> **変更の追跡**<br /><br /> **検索プロパティ リスト**<br /><br /> <br /><br /> 詳細については、「 [フルテキスト インデックス プロパティ &#40;[全般] ページ&#41;](full-text-index-properties-general-page.md)」を参照してください。|  
    |**[列]**|フルテキスト インデックスを作成できるテーブル列が表示されます。 選択した列にフルテキスト インデックスが作成されます。 フルテキスト インデックスに含める列はいくつでも選択できます。 詳細については、「 [フルテキスト インデックス プロパティ &#40;[列] ページ&#41;](../../2014/database-engine/full-text-index-properties-columns-page.md)」を参照してください。|  
    |**スケジュール**|このページでは、フルテキスト インデックスを作成するためのテーブルの増分作成を開始する SQL Server エージェント ジョブのスケジュールを作成または管理できます。 詳細については、「 [フルテキスト インデックスの作成](../relational-databases/indexes/indexes.md)」をご覧ください。<br /><br /> <strong>\*\* 重要な\* \*</strong> を終了した後、 **、フルテキスト インデックスのプロパティ**ダイアログ ボックスで、新規作成したスケジュールは、SQL Server エージェント ジョブ (開始テーブルで増分作成をに関連付けられています*database_name*.*table_name*)。|  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)] をクリックして変更を保存し、 **[フルテキスト インデックスのプロパティ]** ダイアログ ボックスを終了します。  
  
##  <a name="props"></a> インデックス付きのテーブルと列のプロパティを表示します。  
 OBJECTPROPERTYEX など、[!INCLUDE[tsql](../includes/tsql-md.md)] 関数の中には、さまざまなフルテキスト インデックス プロパティの値を取得できるものがあります。 この情報は、フルテキスト検索の管理およびトラブルシューティングに役立ちます。  
  
 次の表に、インデックスが作成されたテーブルおよび列に関連したフルテキスト プロパティと、それに関連する [!INCLUDE[tsql](../includes/tsql-md.md)] 関数の一覧を示します。  
  
|プロパティ|説明|関数|  
|--------------|-----------------|--------------|  
|`FullTextTypeColumn`|列のドキュメント型情報を保持する、テーブル内の TYPE COLUMN。|[COLUMNPROPERTY](/sql/t-sql/functions/columnproperty-transact-sql)|  
|`IsFulltextIndexed`|列に対してフルテキスト インデックスを作成できるかどうかを示します。|COLUMNPROPERTY|  
|`IsFulltextKey`|インデックスがテーブルのフルテキスト キーであるかどうかを示します。|[INDEXPROPERTY](/sql/t-sql/functions/indexproperty-transact-sql)|  
|**TableFulltextBackgroundUpdateIndexOn**|テーブルがフルテキスト インデックスをバックグラウンドで更新できるかどうかを示します。|[OBJECTPROPERTYEX](/sql/t-sql/functions/objectproperty-transact-sql)|  
|`TableFulltextCatalogId`|テーブルのフルテキスト インデックス データが存在する、フルテキスト カタログ ID。|OBJECTPROPERTYEX|  
|`TableFulltextChangeTrackingOn`|テーブルでフルテキストの変更の追跡が有効になっているかどうかを示します。|OBJECTPROPERTYEX|  
|`TableFulltextDocsProcessed`|フルテキスト インデックス作成の開始以降に処理された行の数。|OBJECTPROPERTYEX|  
|**TableFulltextFailCount**|フルテキスト検索によるインデックスが設定されなかった行数。|OBJECTPROPERTYEX|  
|**TableFulltextItemCount**|フルテキスト インデックスが正常に設定された行数。|OBJECTPROPERTYEX|  
|`TableFulltextKeyColumn`|一意なフルテキスト キー列の列 ID。|OBJECTPROPERTYEX|  
|`TableFullTextMergeStatus`|現在マージ中のフルテキスト インデックスがテーブルにあるかどうかを示します。|OBJECTPROPERTYEX|  
|**TableFulltextPendingChanges**|変更の追跡が処理されていないエントリ数。|OBJECTPROPERTYEX|  
|`TableFulltextPopulateStatus`|フルテキスト テーブルの作成状態。|OBJECTPROPERTYEX|  
|`TableHasActiveFulltextIndex`|テーブルが有効なフルテキスト インデックスを持っているかどうかを示します。|OBJECTPROPERTYEX|  
  
##  <a name="key"></a> フルテキスト キー列に関する情報の取得  
 通常、行セット値関数 CONTAINSTABLE または FREETEXTTABLE の結果をベース テーブルと結合します。 その場合、一意なキー列の名前を把握している必要があります。 一意のインデックスがフルテキスト キーとして使用されているかどうかを調査したり、フルテキスト キー列の識別子を取得したりできます。  
  
#### <a name="to-inquire-whether-a-given-unique-index-is-used-as-the-full-text-key-column"></a>一意のインデックスがフルテキスト キー列として使用されているかどうかを調査するには  
  
1.  [SELECT](/sql/t-sql/queries/select-transact-sql) ステートメントを使用して、 [INDEXPROPERTY](/sql/t-sql/functions/indexproperty-transact-sql) 関数を呼び出します。 関数の呼び出しは、テーブルの名前を変換する OBJECT_ID 関数を使用 (*table_name*) をテーブル ID に、テーブルの一意のインデックスの名前を指定し、指定、`IsFulltextKey`インデックス プロパティを次のようにします。  
  
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
  
#### <a name="to-find-the-identifier-of-the-full-text-key-column"></a>フルテキスト キー列の識別子を検索するには  
  
1.  フルテキスト処理に対応する各テーブルには、テーブルの行を一意にするための列があります ("*一意なキー列*")。 OBJECTPROPERTYEX 関数で取得できる `TableFulltextKeyColumn` プロパティには、この一意なキー列の列 ID が格納されます。  
  
     この識別子を取得するには、SELECT ステートメントで OBJECTPROPERTYEX 関数を呼び出します。 テーブルの名前を変換する OBJECT_ID 関数を使用して (*table_name*) をテーブル ID を指定し、`TableFulltextKeyColumn`次のように、プロパティ。  
  
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
  
##  <a name="disable"></a> 無効にするか、フルテキスト インデックス作成のテーブルを再度有効にします。  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]では、既定によりユーザーが作成したすべてのデータベースでフルテキストが有効になります。 さらに、個々のテーブルに対してフルテキスト インデックスを作成し、これに列を追加すると、その時点で、このテーブルでは自動的にフルテキスト インデックスが有効になります。 フルテキスト インデックスから最後の列を削除すると、このテーブルでは自動的にフルテキスト インデックスが無効になります。  
  
 フルテキスト インデックスのあるテーブルでは、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を使用して手動でフルテキスト インデックスを無効にしたり、再度有効にしたりすることができます。  
  
#### <a name="to-enable-a-table-for-full-text-indexing"></a>テーブルでフルテキスト インデックスを有効にするには  
  
1.  サーバー グループを展開し、 **[データベース]** を展開して、フルテキスト インデックスを有効にするテーブルを含むデータベースを展開します。  
  
2.  **[テーブル]** を展開し、フルテキスト インデックスを無効または再度有効にするテーブルを右クリックします。  
  
3.  **[フルテキスト インデックス]** を選択し、 **[フルテキスト インデックスを無効化]** または **[フルテキスト インデックスを有効化]** をクリックします。  
  
##  <a name="remove"></a> テーブルからフルテキスト インデックスの削除  
  
#### <a name="to-remove-a-full-text-index-from-a-table"></a>テーブルからフルテキスト インデックスを削除するには  
  
1.  オブジェクト エクスプローラーで、削除するフルテキスト インデックスが含まれているテーブルを右クリックします。  
  
2.  **[フルテキスト インデックスの削除]** を選択します。  
  
3.  フルテキスト インデックスの削除を確認するメッセージが表示されたら、 **[OK]** をクリックします。  
  
  
