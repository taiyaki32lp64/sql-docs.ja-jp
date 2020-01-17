---
title: sys.registered_search_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.registered_search_properties
- registered_search_properties
- sys.registered_search_properties_TSQL
- registered_search_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search properties [SQL Server]
- property searching [SQL Server], viewing registered properties
- search property lists [SQL Server], viewing registered properties
- sys.registered_search_properties catalog view
ms.assetid: 1b9a7a5c-8c05-4819-83c3-7487dd08fcf7
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 055e64c743c453fb6362d45587b395bf6f3d77bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067894"
---
# <a name="sysregisteredsearchproperties-transact-sql"></a>sys.registered_search_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  検索プロパティが現在のデータベースで、検索プロパティ リストに含まれるごとに行が含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**property_list_id**|**int**|このプロパティが属する検索プロパティ リストの ID です。|  
|**property_set_guid**|**uniqueidentifier**|検索プロパティが属するプロパティ セットを識別するグローバル一意識別子 GUID。|  
|**property_int_id**|**int**|プロパティ内には、この検索プロパティを識別する整数を設定します。 **property_int_id 句**プロパティ セット内で一意です。|  
|**property_name**|**nvarchar(64)**|検索プロパティ ボックスの一覧では、この検索プロパティを一意に識別する名前です。<br /><br /> 注:プロパティを検索するでは、このプロパティ名を指定します、 [CONTAINS](../../t-sql/queries/contains-transact-sql.md)述語。|  
|**property_description**|**nvarchar(512)**|プロパティの説明です。|  
|**property_id**|**int**|によって識別される検索プロパティ リスト内の検索プロパティの内部プロパティ ID、 **property_list_id**値。<br /><br /> 特定のプロパティが特定の検索プロパティ リストに追加されると、Full-Text Engine は、プロパティを登録し、このプロパティ リストに固有の内部プロパティ ID を、そのプロパティに割り当てます。 内部プロパティ ID は、特定の検索プロパティ リストに固有の整数です。 特定のプロパティを複数の検索プロパティ リストに登録した場合、検索プロパティ リストごとに異なる内部プロパティ ID が割り当てられる可能性があります。<br /><br /> 注:内部プロパティ ID は、プロパティを検索プロパティ リストに追加するときに指定されているプロパティ整数識別子とは異なります。 詳細については、「 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)」を参照してください。<br /><br /> フルテキスト インデックスのプロパティに関連するコンテンツを参照してください。 <br />                  [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)|  
  
## <a name="remarks"></a>コメント  
 検索プロパティ リストについて詳しくは、「[検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)」をご覧ください。  
  
## <a name="permissions"></a>アクセス許可  
 検索プロパティのメタデータの可視性では、所有するか、またはいくつかの参照のアクセス許可を付与されて、検索プロパティ リストに含まれるものに限定されます。  
  
> [!NOTE]  
>  検索プロパティ リストの所有者は、リストの参照、またはコントロールのアクセス許可を与えることができます。 CONTROL 権限を持つユーザーは、他のユーザーに REFERENCE 権限を与えることができます。  
  
## <a name="examples"></a>使用例  
 次の例は、登録されている検索プロパティのすべてのメタデータを表示します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.registered_search_properties;   
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
