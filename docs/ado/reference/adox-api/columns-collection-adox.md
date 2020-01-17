---
title: 列のコレクション (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index::Columns
- Table::Columns
- Key::Columns
- Columns
helpviewer_keywords:
- Columns collection [ADOX]
ms.assetid: 23b9fea8-4f76-4a51-95ce-1a6ce4560b34
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc3686ac69d7afeeebec14939a42e073f796b1ec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966845"
---
# <a name="columns-collection-adox"></a>Columns コレクション (ADOX)
すべてを含む[列](../../../ado/reference/adox-api/column-object-adox.md)テーブル、インデックス、またはキーのオブジェクト。  
  
## <a name="remarks"></a>コメント  
 [Append](../../../ado/reference/adox-api/append-method-adox-columns.md)のメソッド、**列**コレクションは ADOX に一意です。 可能な代替手段としては以下の方法があります。  
  
-   使用して、コレクションに新しい列を追加、 **Append**メソッド。  
  
 残りのプロパティとメソッドは、ADO のコレクションに標準的です。 可能な代替手段としては以下の方法があります。  
  
-   使用して、コレクション内の列へのアクセス、[項目](../../../ado/reference/ado-api/item-property-ado.md)プロパティ。  
  
-   使用して、コレクションに含まれる列の数を返す、[カウント](../../../ado/reference/ado-api/count-property-ado.md)プロパティ。  
  
-   使用して、コレクションから列を削除、[削除](../../../ado/reference/adox-api/delete-method-adox-collections.md)メソッド。  
  
-   現在のデータベースのスキーマを反映するようにコレクション内のオブジェクトを更新、[更新](../../../ado/reference/ado-api/refresh-method-ado.md)メソッド。  
  
> [!NOTE]
>  追加するときにエラーが発生する**列**を**列**のコレクション、[インデックス](../../../ado/reference/adox-api/index-object-adox.md)場合、**列**に存在しません[テーブル](../../../ado/reference/adox-api/table-object-adox.md)に既に追加されて、[テーブル](../../../ado/reference/adox-api/tables-collection-adox.md)コレクション。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [Columns コレクションのプロパティ、メソッド、およびイベント](../../../ado/reference/adox-api/columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [Columns および Tables Append メソッド、Name プロパティの例 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close メソッド、Table Type プロパティの例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Keys Append メソッド、キーの種類、RelatedColumn、RelatedTable、UpdateRule プロパティの例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog プロパティの例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder プロパティの例 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Column オブジェクト (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
