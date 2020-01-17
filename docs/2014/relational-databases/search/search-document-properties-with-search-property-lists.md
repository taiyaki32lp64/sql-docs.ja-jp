---
title: 検索プロパティ リストを使用したドキュメント プロパティの検索 | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- full-text search [SQL Server], properties
- search property lists [SQL Server]
- property searching [SQL Server], about
- full-text indexes [SQL Server], search property lists
- search property lists [SQL Server], about
- property searching [SQL Server]
ms.assetid: ffae5914-b1b2-4267-b927-37e8382e0a9e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7a4dbc20442181ce97b060118094dfa0667803db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011077"
---
# <a name="search-document-properties-with-search-property-lists"></a>検索プロパティ リストを使用したドキュメント プロパティの検索
  以前のバージョンでは、ドキュメント プロパティの内容はドキュメントの本文の内容と区別できませんでした。 この制限により、フルテキスト クエリは、ドキュメント全体に対する汎用検索に制限されていました。 しかし、現在のバージョンでは、`varbinary`、`varbinary(max)` (`FILESTREAM` を含む)、または `image` バイナリ データ列がサポートされているドキュメントの種類については、フルテキスト インデックスを構成することで、Author や Title などの特定のプロパティに対するプロパティ スコープの検索をサポートすることができます。 この形式の検索を、 *プロパティ検索*と呼びます。  
  
 特定の種類のドキュメントでプロパティ検索が可能かどうかは、対応する [フィルター](configure-and-manage-filters-for-search.md) (IFilter) によって異なります。 ドキュメントの種類によっては、ドキュメント本文の内容に加えて、そのドキュメントの種類に対して定義されている検索プロパティの一部またはすべてが、対応する IFilter によって抽出されます。 フルテキスト インデックスの作成時に IFilter によって抽出されたプロパティに対してのみプロパティ検索をサポートするように、フルテキスト インデックスを構成することができます。 さまざまなドキュメント プロパティを抽出する IFilter の一例として、Microsoft Office のドキュメントの種類 (.docx、.xlsx、.pptx など) に対応した IFilter があります。 一方、XML IFilter では、プロパティは生成されません。  
  
##  <a name="How_FTS_Works_with_search_properties"></a> 検索プロパティのフルテキスト検索  
  
### <a name="internal-property-ids"></a>内部プロパティ ID  
 Full-Text Engine は、登録されている各プロパティに対して内部プロパティ ID を適宜割り当てます。この内部プロパティ ID は、特定の検索リスト内のプロパティを一意に識別するためのもので、検索プロパティ リストで固有の ID になります。 また、1 つのプロパティを複数の検索プロパティ リストに追加した場合、その内部 ID がリスト間で異なる可能性があります。  
  
 プロパティを検索リストに追加したときに、Full-Text Engine によって *内部プロパティ ID* がプロパティに適宜割り当てられます。 この内部プロパティ ID は、該当する検索プロパティ リスト内のプロパティを一意に識別する整数です。  
  
 次の図は、Title と Keywords の 2 つのプロパティを指定する検索プロパティ リストの論理的なビューを示しています。 Keywords のプロパティ リスト名は "Tags" です。 これらのプロパティは、F29F85E0-4FF9-1068-AB91-08002B27B3D9 という GUID を持つ同じプロパティ セットに属します。 Title のプロパティ整数識別子は 2、Tags (Keywords) のプロパティ整数識別子は 5 です。 Full-Text Engine は、各プロパティを、検索プロパティ リストで一意となる内部プロパティ ID に適宜関連付けます。 Title プロパティの内部プロパティ ID は 1、Tags プロパティの内部プロパティ ID は 2 になります。  
  
 ![内部テーブルへの検索プロパティ リストのマッピング](../../database-engine/media/ifts-spl-w-title-and-keywords.gif "内部テーブルへの検索プロパティ リストのマッピング")  
  
 内部プロパティ ID は、プロパティのプロパティ整数識別子とは異なる場合があります。 特定のプロパティを複数の検索プロパティ リストに登録した場合、検索プロパティ リストごとに異なる内部プロパティ ID が割り当てられる可能性があります。 たとえば、ある検索プロパティ リストでは内部プロパティ ID が 4 である一方で、別の検索プロパティ リストでは内部プロパティ ID が 1 であったり 3 であったりする場合があります。 これに対し、プロパティ整数識別子はプロパティに固有な識別子であるため、プロパティがどこで使用されるかに関係なく同じ値になります。  
  
  
  
### <a name="indexing-of-registered-properties"></a>登録済みのプロパティのインデックスの作成  
 フルテキスト インデックスが検索プロパティ リストに関連付けらた後で、プロパティに固有の検索語句のインデックスを作成するために、インデックスを再作成する必要があります。 フルテキスト インデックスの作成中、すべてのプロパティの内容が他の内容と共にフルテキスト インデックスに格納されます。 登録されたプロパティに含まれている検索語句のインデックスを作成しているときには、フルテキスト インデクサーによって、対応する内部プロパティ ID も語句と共に格納されます。 一方、プロパティが登録されていない場合、プロパティはドキュメントの本文の一部であるかのようにフルテキスト インデックスに格納され、内部プロパティ ID として値 0 が割り当てられます。  
  
 次の図に、フルテキスト インデックスに示された検索語句の論理ビューを示します。このフルテキスト インデックスは、前の図に示した検索プロパティ リストに関連付けられています。 サンプル ドキュメント Document 1 には、ドキュメントの本文に加えて、Title、Author、および Keywords の 3 つのプロパティが含まれています。 検索プロパティ リストに指定されている Title と Keywords のプロパティの場合、検索語句がフルテキスト インデックスの対応する内部プロパティ ID に関連付けられています。 これに対し、Author プロパティの内容については、ドキュメントの本文の一部であるかのようにインデックスが作成されます。 これは、プロパティを登録することにより、プロパティに格納されている内容の量に応じてフルテキスト インデックスのサイズが増加することを示しています。  
  
 ![検索プロパティ リストを使用するフルテキスト インデックス](../../database-engine/media/ifts-spl-and-fti.gif "検索プロパティ リストを使用するフルテキスト インデックス")  
  
 Title プロパティの検索語句 ("Favorite"、"Biking"、および "Trails") は、このインデックスの Title に割り当てられた内部プロパティ ID 値 1 に関連付けられます。 Keywords プロパティの検索語句 ("biking" および "mountain") は、このインデックスの Tags に割り当てられた内部プロパティ ID 値 2 に関連付けられます。 Author プロパティの検索語句 ("Jane" および "Doe") およびドキュメントの本文の検索語句の内部プロパティ ID は 0 です。 ここで、"biking" という語句は、Title プロパティ、Keywords (Tags) プロパティ、およびドキュメントの本文に出現します。 Title プロパティまたは Keywords (Tags) プロパティに対して "biking" をプロパティ検索すると、このドキュメントが結果として返されます。 "biking" の汎用フルテキスト クエリを実行した場合も、プロパティ検索用にインデックスが構成されていないかのように、このドキュメントが返されます。 Author プロパティに対して "biking" のプロパティ検索を実行した場合、このドキュメントは返されません。  
  
 プロパティスコープのフルテキスト クエリでは、フルテキスト インデックスの現在の検索プロパティ リストに登録されている内部プロパティ ID が使用されます。  
  
  
  
##  <a name="impact"></a> プロパティ検索を有効にした場合の影響  
 1 つまたは複数のプロパティを対象とした検索をサポートするようにフルテキスト インデックスを構成すると、検索プロパティ リストに指定したプロパティの数および各プロパティの内容に応じて、インデックスのサイズが増加します。  
  
 Microsoft Word の一般的なコーパスのテストで<sup>??</sup>、Excel<sup>??</sup>、および PowerPoint<sup>??</sup> ドキュメント、フルテキスト インデックスにインデックスの一般的な検索プロパティを構成しました。 これらのプロパティのインデックスを作成した結果、フルテキスト インデックスのサイズは約 5% 増加しました。 サイズの増加に関するこの概算値は、ほとんどのドキュメント コーパスに当てはまると考えられます。 ただし、最終的には、サイズの増加量は、全体的なデータ量に関連する特定のドキュメント コーパス内のプロパティ データの量に依存します。  
  
  
  
##  <a name="creating"></a> 検索プロパティ リストの作成とプロパティ検索の有効化  
  
###  <a name="creating_sub"></a> 検索プロパティ リストの作成  
 **Transact-SQL を使用して検索プロパティ リストを作成するには**  
  
 少なくともリストの名前を指定して、[CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-search-property-list-transact-sql) ステートメントを使用します。  
  
##### <a name="to-create-a-search-property-list-in-management-studio"></a>Management Studio で検索プロパティ リストを作成するには  
  
1.  オブジェクト エクスプローラーで、サーバーを展開します。  
  
2.  **[データベース]** を展開し、検索プロパティ リストを作成する対象のデータベースを展開します。  
  
3.  **[ストレージ]** を展開し、 **[検索プロパティ リスト]** を右クリックします。  
  
4.  **[新しい検索プロパティ リスト]** をクリックします。  
  
5.  プロパティ リストの名前を指定します。  
  
6.  必要に応じて、他のユーザーをプロパティ リストの所有者として指定します。  
  
7.  以下のオプションの 1 つを選択します。  
  
    -   **[空の検索プロパティ リストを作成する]**  
  
    -   **[既存の検索プロパティ リストから作成する]**  
  
     詳細については、「 [New Search Property List](../../database-engine/new-search-property-list.md)」を参照してください。  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 
  
###  <a name="adding"></a> 検索プロパティ リストへのプロパティの追加  
 プロパティを検索するには、 *検索プロパティ リスト* を作成し、検索可能にする 1 つまたは複数のプロパティを指定する必要があります。 プロパティを検索プロパティ リストに追加すると、プロパティはその特定のリスト用に登録されます。 プロパティを検索プロパティ リストに追加するには、次の値が必要です。  
  
-   プロパティ セット GUID  
  
     それぞれの検索プロパティは、関連するプロパティのグループを含む単一のプロパティ セットに属します。 それぞれのプロパティ セットは、グローバル一意識別子 (GUID) によって識別されます。  
  
-   プロパティ整数識別子  
  
     それぞれの検索プロパティは、プロパティ セット内で一意な識別子を持っています。 特定のプロパティでは、識別子が整数または文字列である場合があります。ただし、フルテキスト検索では、整数識別子のみがサポートされます。  
  
-   プロパティ名  
  
     これは、プロパティを検索するフルテキスト クエリでユーザーが指定する名前です。 プロパティ名の内部にはスペースを含めることができます。 最大長は 256 文字です。  
  
     プロパティ名として、次のいずれかを指定できます。  
  
    -   Windows の正規のプロパティ名 (`System.Author`、`System.Contact.HomeAddress` など)。  
  
    -   ユーザーにとって覚えやすくわかりやすい名前。 いくつかのプロパティは "Author" や "Home Address" などの一般的なわかりやすい名前に関連付けられていますが、ユーザーにとって最も適した任意の名前を指定できます。  
  
    > [!NOTE]  
    >  プロパティ セット GUID とプロパティ識別子の特定の組み合わせは、特定の検索プロパティ リスト内で一意である必要があります。 これは、同じプロパティを別の名前または説明を使用して複数回追加できないことを意味します。  
  
-   プロパティの説明 (省略可能)  
  
     検索プロパティを検索プロパティ リストに追加するとき、オプションで説明を記述できます。 たとえば、名前からはその内容がわかりにくいプロパティに関する情報を記述したり、プロパティのプロパティ セットに関する説明を記述したりできます。  
  
 **検索プロパティ リストの値を取得するには**  
  
 「 [検索プロパティのプロパティ セット GUID およびプロパティ整数 ID の取得](find-property-set-guids-and-property-integer-ids-for-search-properties.md)」を参照してください。  
  
 **Transact-SQL を使用してプロパティを検索プロパティ リストに追加するには**  
  
 [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-search-property-list-transact-sql) ステートメントを、「[検索プロパティのプロパティ セット GUID およびプロパティ整数 ID の取得](find-property-set-guids-and-property-integer-ids-for-search-properties.md)」に説明されているいずれかの方法を使用して取得した値と共に使用します。  
  
 次の例では、これらの値を使用してプロパティを検索プロパティ リストに追加する方法を示しています。  
  
```  
ALTER SEARCH PROPERTY LIST DocumentTablePropertyList  
   ADD 'Title'  
   WITH ( PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9', PROPERTY_INT_ID = 2,   
      PROPERTY_DESCRIPTION = 'System.Title - Title of the item.' );  
```  
  
 **Management Studio でプロパティを検索プロパティ リストに追加するには**  
  
 **[検索プロパティ リストのプロパティ]** ダイアログ ボックスを使用して、検索プロパティを追加および削除します。 オブジェクト エクスプローラーでは、関連するデータベースの **[ストレージ]** ノードの下に **[検索プロパティ リスト]** があります。  
  
  
  
###  <a name="associating"></a> 検索プロパティ リストとフルテキスト インデックスの関連付け  
 検索プロパティ リストに登録されているプロパティを対象としたプロパティ検索をフルテキスト インデックスでサポートするためには、検索プロパティ リストとインデックスを関連付けた後、インデックスを再作成する必要があります。 フルテキスト インデックスを再作成すると、登録された各プロパティに含まれている検索語句に対して、プロパティ固有のインデックス エントリが作成されます。  
  
 フルテキスト インデックスがこの検索プロパティ リストに関連付けられている限り、フルテキスト クエリで CONTAINS 述語の PROPERTY オプションを使用して、検索プロパティ リストに登録されているプロパティを対象に検索を実行できます。  
  
 フルテキスト インデックスに関連付けられている検索プロパティ リストを変更した場合は、インデックスを一貫性のある状態に保つために、インデックスの再構築が必要になります。 インデックスは即座に切り捨てられ、完全作成が実行されるまで空になります。 検索プロパティ リストの変更によってインデックスが再構築される場合の詳細については、「[ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)」の「解説」を参照してください。  
  
 **Transact-SQL を使用して検索プロパティ リストをフルテキスト インデックスに関連付けるには**  
  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql) ステートメントを `SET SEARCH PROPERTY LIST = <property_list_name>` 句と共に使用します。  
  
 **Management Studio を使用して検索プロパティ リストをフルテキスト インデックスに関連付けるには**  
  
 **[フルテキスト インデックスのプロパティ]** ダイアログ ボックスの **[全般]** ページで、 **[検索プロパティ リスト]** の値を指定します。  
  
  
  
##  <a name="Ov_CONTAINS_using_PROPERTY"></a> CONTAINS を使用した検索プロパティのクエリ  
 プロパティ スコープのフルテキスト クエリのための [CONTAINS](/sql/t-sql/queries/contains-transact-sql) の基本的な構文を次に示します。  
  
```sql  
SELECT column_name FROM table_name  
  WHERE CONTAINS ( PROPERTY ( column_name, 'property_name' ), '<contains_search_condition>' )  
```  
  
 たとえば、次のクエリは、 `Title`データベースの `Document` テーブルの `Production.Document` 列内で、インデックス化されたプロパティ `AdventureWorks` に対する検索を実行します。 このクエリは、 `Title` という文字列が `Maintenance` プロパティに含まれているドキュメントのみを返します。 `Repair`  
  
```  
USE AdventureWorks  
GO  
SELECT Document FROM Production.Document  
  WHERE CONTAINS ( PROPERTY ( Document, 'Title' ), 'Maintenance OR Repair')  
GO  
```  
  
 この例では、ドキュメントの IFilter で Title プロパティが抽出されること、Title プロパティが検索プロパティ リストに追加されること、および検索プロパティ リストがフルテキスト インデックスに関連付けられていることを前提としています。  
  
  
  
##  <a name="managing"></a> 検索プロパティ リストの管理  
  
###  <a name="viewing"></a> 検索プロパティ リストの表示および変更  
 **Transact-SQL を使用して検索プロパティ リストを変更するには**  
  
 [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-search-property-list-transact-sql) ステートメントを使用して、検索プロパティを追加または削除します。  
  
##### <a name="to-view-and-change-a-search-property-list-in-management-studio"></a>Management Studio で検索プロパティ リストを表示および変更するには  
  
1.  オブジェクト エクスプローラーで、サーバーを展開します。  
  
2.  **[データベース]** を展開し、データベースを展開します。  
  
3.  **[ストレージ]** を展開します。  
  
4.  **[検索プロパティ リスト]** を展開して、検索プロパティ リストを表示します。  
  
5.  プロパティ リストを右クリックし、 **[プロパティ]** をクリックします。  
  
6.  **[検索プロパティ リスト エディター]** ダイアログ ボックスで、プロパティ グリッドを使用して、検索プロパティを追加または削除します。  
  
    1.  ドキュメント プロパティを削除するには、プロパティの左側にある行ヘッダーをクリックして、Del キーを押します。  
  
    2.  ドキュメント プロパティを追加するには、リストの末尾で **\*** の右側の空白行をクリックして、新しいプロパティの値を入力します。  
  
         これらの値の詳細については、「 [検索プロパティ リスト エディター](../../database-engine/search-property-list-editor.md)」を参照してください。 Microsoft によって定義されているプロパティのこれらの値を取得する方法については、「 [検索プロパティのプロパティ セット GUID およびプロパティ整数 ID の取得](find-property-set-guids-and-property-integer-ids-for-search-properties.md)」を参照してください。 独立系ソフトウェア ベンダー (ISV) によって定義されたプロパティの詳細については、そのベンダーのマニュアルを参照してください。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
###  <a name="deleting"></a> 検索プロパティ リストの削除  
 リストがいずれかのフルテキスト インデックスに関連付けられている場合は、データベースからプロパティ リストを削除できません。  
  
 **Transact-SQL を使用して検索プロパティ リストを削除するには**  
  
 [DROP SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-search-property-list-transact-sql) ステートメントを使用します。  
  
##### <a name="to-delete-a-search-property-list-in-management-studio"></a>Management Studio で検索プロパティ リストを削除するには  
  
1.  オブジェクト エクスプローラーで、サーバーを展開します。  
  
2.  **[データベース]** を展開し、データベースを展開します。  
  
3.  **[ストレージ]** を展開し、 **[検索プロパティ リスト]** ノードを展開します。  
  
4.  削除するプロパティ リストを右クリックして、 **[削除]** をクリックします。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

  
## <a name="see-also"></a>参照  
 [検索プロパティのプロパティ セット GUID およびプロパティ整数 ID の取得](find-property-set-guids-and-property-integer-ids-for-search-properties.md)   
 [検索用フィルターの構成と管理](configure-and-manage-filters-for-search.md)  
  
  
