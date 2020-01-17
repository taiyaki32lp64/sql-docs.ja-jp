---
title: 列オブジェクト (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Column
helpviewer_keywords:
- Column object [ADOX]
ms.assetid: 6e772783-1bc8-4ea7-94b2-7d7a52ea5c47
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db2c2dbe6af2a50fc2507a9ade92d83e0502f2ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966914"
---
# <a name="column-object-adox"></a>Column オブジェクト (ADOX)
テーブル、インデックス、またはキーから列を表します。  
  
## <a name="remarks"></a>コメント  
 次のコード作成、新しい**列**:  
  
 `Dim obj As New Column`  
  
 プロパティのコレクションと、**列**オブジェクトのことができます。  
  
-   列を識別、[名プロパティ (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)プロパティ。  
  
-   列のデータ型を指定、 [Type プロパティ (キー) (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md)プロパティ。  
  
-   決定列が固定長の場合、または null 値を含めることができる場合、[属性プロパティ (ADOX)](../../../ado/reference/adox-api/attributes-property-adox.md)プロパティ。  
  
-   列の最大サイズを指定、 [DefinedSize プロパティ (ADOX)](../../../ado/reference/adox-api/definedsize-property-adox.md)プロパティ。  
  
-   数値データの値の指定とスケール、 [NumericScale プロパティ (ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md)プロパティ。  
  
-   数値データの値と最大有効桁数を指定、[精度プロパティ (ADOX)](../../../ado/reference/adox-api/precision-property-adox.md)プロパティ。  
  
-   指定、[カタログ オブジェクト (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)で列を所有している、 [ParentCatalog プロパティ (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md)プロパティ。  
  
-   関連テーブルに関連する列の名前を指定、キー列の[RelatedColumn プロパティ (ADOX)](../../../ado/reference/adox-api/relatedcolumn-property-adox.md)プロパティ。  
  
-   インデックス列で並べ替え順序が昇順または降順でかどうかを指定、 [SortOrder プロパティ (ADOX)](../../../ado/reference/adox-api/sortorder-property-adox.md)プロパティ。  
  
-   プロバイダー固有のプロパティにアクセス、[プロパティ コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)コレクション。  
  
> [!NOTE]
>  すべてのプロパティの**列**オブジェクトは、データ プロバイダーによってサポート可能性があります。 プロバイダーがサポートされていないプロパティの値を設定している場合、エラーが発生します。 新しい**列**オブジェクト、オブジェクトは、コレクションに追加されると、エラーが発生します。 既存のオブジェクトは、プロパティの設定時に、エラーが発生します。  
>   
>  作成するときに**列**オブジェクトの場合、オプションのプロパティに適切な既定値が存在しないわけでは、プロバイダーが、プロパティをサポートします。 詳細については、プロバイダーでサポートされるプロパティについて、プロバイダーのマニュアルを参照してください。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [Column オブジェクトのプロパティ、メソッド、およびイベント](../../../ado/reference/adox-api/column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [Columns および Tables Append メソッド、Name プロパティの例 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close メソッド、Table Type プロパティの例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Keys Append メソッド、キーの種類、RelatedColumn、RelatedTable、UpdateRule プロパティの例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ADOX のコード例:NumericScale および Precision プロパティの例 (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [ParentCatalog プロパティの例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder プロパティの例 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [列のコレクション (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
