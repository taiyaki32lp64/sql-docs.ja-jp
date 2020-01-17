---
title: テーブルのオブジェクト (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table
helpviewer_keywords:
- Table object [ADOX]
ms.assetid: a6d74000-0828-49ba-850a-63da865f8802
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 10f3add3cb243d54643c3294104ec2546e7737d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965162"
---
# <a name="table-object-adox"></a>Table オブジェクト (ADOX)
列、インデックス、およびキーを含むデータベース テーブルを表します。  
  
## <a name="remarks"></a>コメント  
 次のコード作成、新しい**テーブル**:  
  
```  
Dim obj As New Table  
```  
  
 プロパティのコレクションと、**テーブル**オブジェクトのことができます。  
  
-   テーブルを識別、[名プロパティ (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)プロパティ。  
  
-   テーブルの種類を判断、 [Type プロパティ (テーブル) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md)プロパティ。  
  
-   テーブルのデータベース列へのアクセス、[列コレクション (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)コレクション。  
  
-   テーブルのインデックスへのアクセス、[インデックス コレクション (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)します。  
  
-   テーブルのキーへのアクセス、[キー コレクション (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)します。  
  
-   テーブルを所有するカタログの指定、 [ParentCatalog プロパティ (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md)プロパティ。  
  
-   日付情報を返す、 [DateCreated プロパティ (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)と[DateModified プロパティ (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)プロパティ。  
  
-   プロバイダー固有のテーブルのプロパティにアクセス、[プロパティ コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)コレクション。  
  
> [!NOTE]
>  データ プロバイダーはのすべてのプロパティをサポートしていない**テーブル**オブジェクト。 プロバイダーがサポートされていないプロパティの値を設定している場合、エラーが発生します。 新しい**テーブル**オブジェクト、オブジェクトは、コレクションに追加されると、エラーが発生します。 既存のオブジェクトは、プロパティの設定時に、エラーが発生します。  
>   
>  作成するときに**テーブル**オブジェクトの場合、オプションのプロパティに適切な既定値が存在しないわけでは、プロバイダーが、プロパティをサポートします。 詳細については、プロバイダーでサポートされるプロパティについて、プロバイダーのマニュアルを参照してください。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [Table オブジェクトのプロパティ、メソッド、およびイベント](../../../ado/reference/adox-api/table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [カタログ ActiveConnection プロパティの例 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Columns および Tables Append メソッド、Name プロパティの例 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close メソッド、Table Type プロパティの例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Keys Append メソッド、キーの種類、RelatedColumn、RelatedTable、UpdateRule プロパティの例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog プロパティの例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [列のコレクション (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Indexes コレクション (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Keys コレクション (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Tables コレクション (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
