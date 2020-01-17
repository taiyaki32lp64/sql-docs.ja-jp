---
title: CREATE SEARCH PROPERTY LIST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_SEARCH_PROPERTY_LIST_TSQL
- CREATE SEARCH
- CREATE_SEARCH_TSQL
- CREATE_SEARCH_PROPERTY_TSQL
- CREATE SEARCH PROPERTY
- CREATE SEARCH PROPERTY LIST
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], creating
- CREATE SEARCH PROPERTY LIST statement
ms.assetid: 5440cbb8-3403-4d27-a2f9-8e1f5a1bc12b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e838729d064a6101d4efb8fc57c7cd7b9910ad8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117282"
---
# <a name="create-search-property-list-transact-sql"></a>CREATE SEARCH PROPERTY LIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  新しい検索プロパティ リストを作成します。 検索プロパティ リストは、フルテキスト インデックスに含める 1 つまたは複数の検索プロパティを指定するために使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
CREATE SEARCH PROPERTY LIST new_list_name  
   [ FROM [ database_name. ] source_list_name ]  
   [ AUTHORIZATION owner_name ]  
;  
```  
  
## <a name="arguments"></a>引数  
 *new_list_name*  
 新しい検索プロパティ リストの名前を指定します。 *new_list_name* は最大 128 文字の識別子です。 *new_list_name* は、現在のデータベース内のすべてのプロパティ リストの中で一意であり、識別子の規則に準拠している必要があります。 *new_list_name* は、フルテキスト インデックスが作成されるときに使用されます。  
  
 *database_name*  
 *source_list_name* で指定したプロパティ リストが置かれているデータベースの名前です。 指定しない場合、*database_name* は現在のデータベースに設定されます。  
  
 *database_name* には、既存のデータベース名を指定する必要があります。 現在の接続のログインは、*database_name* で指定したデータベースの既存のユーザー ID に関連付ける必要があります。 また、データベースで要求される[権限](#Permissions)を持っている必要があります。  
  
 *source_list_name*  
 新しいプロパティ リストが、*database_name* の既存のプロパティ リストをコピーして作成されることを指定します。 *source_list_name* が存在しない場合、CREATE SEARCH PROPERTY LIST はエラーが発生して失敗します。 *source_list_name* の検索プロパティが、*new_list_name* によって継承されます。  
  
 AUTHORIZATION *owner_name*  
 プロパティ リストを所有するユーザーまたはロールの名前を指定します。 *owner_name* に現在のユーザーがメンバーとなっているロールの名前を指定するか、現在のユーザーが *owner_name* に対する IMPERSONATE 権限を持っている必要があります。 このオプションを指定しない場合は、所有権は現在のユーザーに与えられます。  
  
> [!NOTE]  
>  所有者は、[ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使って変更できます。  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]  
>  プロパティ リストについての一般的な情報については、「[検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)」をご覧ください。  
  
 既定では、新しい検索プロパティ リストは空であるため、1 つまたは複数の検索プロパティを手動で追加する必要があります。 また、既存の検索プロパティ リストをコピーすることもできます。 その場合、コピー元の検索プロパティが新しいリストに継承されます。検索プロパティを追加または削除することによって、新しいリストに変更を加えることができます。 フルテキスト インデックスには、すべてのカタログを次回作成するときの検索プロパティ リスト内にあるプロパティが含まれます。  
  
 CREATE SEARCH PROPERTY LIST ステートメントは、次のような状況で失敗します。  
  
-   *database_name* で指定されたデータベースが存在しない場合。  
  
-   *source_list_name* で指定されたリストが存在しない場合。  
  
-   正しい権限がない場合。  
  
 **リストのプロパティを追加または削除するには**  
  
-   [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)  
  
-   **プロパティ リストを削除するには**  
  
-   [DROP SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)  
  
##  <a name="Permissions"></a> Permissions  
 現在のデータベースには CREATE FULLTEXT CATALOG 権限が必要であり、ソース プロパティ リストのコピー元のデータベースには REFERENCES 権限が必要です。  
  
> [!NOTE]  
>  リストとフルテキスト インデックスを関連付けるには、REFERENCES 権限が必要です。 プロパティを追加または削除するか、リストを削除するには、CONTROL 権限が必要です。 プロパティ リストの REFERENCES 権限または CONTROL 権限は、そのプロパティ リストの所有者が許可できます。 CONTROL 権限を持つユーザーは、他のユーザーに REFERENCES 権限を与えることができます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-an-empty-property-list-and-associating-it-with-an-index"></a>A. 空のプロパティ リストを作成し、インデックスに関連付ける  
 次の例では、`DocumentPropertyList` という名前の新しい検索プロパティ リストを作成します。 次に、[ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) ステートメントを使って、新しいプロパティ リストを `AdventureWorks` データベースにある `Production.Document` テーブルのフルテキスト インデックスに関連付けます。このとき、カタログの作成は開始されません。  
  
> [!NOTE]  
>  定義済みで既知の検索プロパティをこの検索プロパティ リストに追加する例については、「[ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)」をご覧ください。 検索プロパティをリストに追加した後、データベース管理者は、START FULL POPULATION 句を指定して別の ALTER FULLTEXT INDEX ステートメントを使用する必要があります。  
  
```  
CREATE SEARCH PROPERTY LIST DocumentPropertyList;  
GO  
USE AdventureWorks2012;  
ALTER FULLTEXT INDEX ON Production.Document   
   SET SEARCH PROPERTY LIST DocumentPropertyList  
   WITH NO POPULATION;   
GO   
```  
  
### <a name="b-creating-a-property-list-from-an-existing-one"></a>B. 既存のプロパティ リストからプロパティ リストを作成する  
 次の例では、`JobCandidateProperties` データベースのフルテキスト インデックスに関連付けられた、例 A で作成したリスト `DocumentPropertyList` から、新しい検索プロパティ リスト `AdventureWorks2012` を作成します。 次に、ALTER FULLTEXT INDEX ステートメントを使用して、新しいプロパティ リストを、`HumanResources.JobCandidate` データベースにある `AdventureWorks2012` テーブルのフルテキスト インデックスに関連付けます。 この ALTER FULLTEXT INDEX ステートメントにより、完全作成が開始されます。これは、SET SEARCH PROPERTY LIST 句の既定の動作です。  
  
```  
CREATE SEARCH PROPERTY LIST JobCandidateProperties 
FROM AdventureWorks2012.DocumentPropertyList;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate   
   SET SEARCH PROPERTY LIST JobCandidateProperties;  
GO  
  
```  
  
## <a name="see-also"></a>参照  
 [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)   
 [DROP SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)   
 [sys.registered_search_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [検索プロパティのプロパティ セット GUID およびプロパティ整数 ID の取得](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
  
