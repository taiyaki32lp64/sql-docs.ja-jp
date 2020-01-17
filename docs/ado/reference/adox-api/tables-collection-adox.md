---
title: テーブルのコレクション (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog::Tables
- Tables
helpviewer_keywords:
- Tables collection [ADOX]
ms.assetid: 38d750e7-f3fb-426e-b4b4-55eea4f1a654
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0bf28af10084a30a5c81c76fe7e44781178979ad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965130"
---
# <a name="tables-collection-adox"></a>Tables コレクション (ADOX)
すべてを含む[テーブル](../../../ado/reference/adox-api/table-object-adox.md)カタログのオブジェクト。  
  
## <a name="remarks"></a>コメント  
 [Append](../../../ado/reference/adox-api/append-method-adox-tables.md)のメソッド、**テーブル**コレクションは ADOX に一意です。 可能な代替手段としては以下の方法があります。  
  
-   新しいテーブルを使用して、コレクションに追加、 **Append**メソッド。  
  
 残りのプロパティとメソッドは、ADO のコレクションに標準的です。 可能な代替手段としては以下の方法があります。  
  
-   使用して、コレクション内のテーブルへのアクセス、[項目](../../../ado/reference/ado-api/item-property-ado.md)プロパティ。  
  
-   コレクションに含まれているテーブルの数を返す、[カウント](../../../ado/reference/ado-api/count-property-ado.md)プロパティ。  
  
-   テーブルを使用して、コレクションから削除、[削除](../../../ado/reference/adox-api/delete-method-adox-collections.md)メソッド。  
  
-   現在のデータベース スキーマを反映するようにコレクション内のオブジェクトを更新、[更新](../../../ado/reference/ado-api/refresh-method-ado.md)メソッド。  
  
 一部のプロバイダーで、ビューなどの他のスキーマ オブジェクトを返す可能性があります、**テーブル**コレクション。 そのため、一部の ADOX のコレクションでは、同じオブジェクトに複数の参照を含めることができます。 1 つのコレクションからオブジェクトを削除する必要があります、変更は表示されませんまで、削除されたオブジェクトを参照する別のコレクションで、**更新**メソッドが、コレクションで呼び出されます。 たとえばで、OLE DB Provider for Microsoft Jet、ビューが返されますと、**テーブル**コレクション。 更新する必要があります、ビューを削除する場合、**テーブル**コレクション、コレクション変更が反映される前にします。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [Tables コレクションのプロパティ、メソッド、およびイベント](../../../ado/reference/adox-api/tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [カタログ ActiveConnection プロパティの例 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Columns および Tables Append メソッド、Name プロパティの例 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close メソッド、Table Type プロパティの例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Keys Append メソッド、キーの種類、RelatedColumn、RelatedTable、UpdateRule プロパティの例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Catalog オブジェクト (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Table オブジェクト (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
