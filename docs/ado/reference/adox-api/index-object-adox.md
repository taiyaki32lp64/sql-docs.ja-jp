---
title: インデックスのオブジェクト (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index
helpviewer_keywords:
- Index object [ADOX]
ms.assetid: 6b9578c0-bc94-46b9-b801-c18e14b04b31
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7bff462b7c9ffe115cdfd52d1ec1f0a810a50531
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966083"
---
# <a name="index-object-adox"></a>Index オブジェクト (ADOX)
データベース テーブルからインデックスを表します。  
  
## <a name="remarks"></a>コメント  
 次のコード作成、新しい**インデックス**:  
  
```  
Dim obj As New Index  
```  
  
 プロパティのコレクションと、**インデックス**オブジェクトのことができます。  
  
-   使用してインデックスを識別、[名前](../../../ado/reference/adox-api/name-property-adox.md)プロパティ。  
  
-   データベースを使用してインデックスの列へのアクセス、[列](../../../ado/reference/adox-api/columns-collection-adox.md)コレクション。  
  
-   インデックス キーが内で一意である必要があるかどうかを指定、 [Unique](../../../ado/reference/adox-api/unique-property-adox.md)プロパティ。  
  
-   インデックスがテーブルの主キーかどうかを指定する、 [PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md)プロパティ。  
  
-   インデックス フィールドに null 値を持つレコードにインデックス エントリがあるかどうかを指定、 [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md)プロパティ。  
  
-   インデックスがクラスター化されているかどうかを指定、 [Clustered](../../../ado/reference/adox-api/clustered-property-adox.md)プロパティ。  
  
-   プロバイダー固有のインデックスのプロパティにアクセス、[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクション。  
  
> [!NOTE]
>  追加するときにエラーが発生する[列](../../../ado/reference/adox-api/column-object-adox.md)を**列**のコレクション、**インデックス**場合、**列**に存在しません[テーブル](../../../ado/reference/adox-api/table-object-adox.md)オブジェクトに既に追加されて、[テーブル](../../../ado/reference/adox-api/tables-collection-adox.md)コレクション。  
  
> [!NOTE]
>  データ プロバイダーはのすべてのプロパティをサポートしていない**インデックス**オブジェクト。 プロバイダーによってサポートされていないプロパティの値を設定している場合、エラーが発生します。 新しい**インデックス**オブジェクト、オブジェクトは、コレクションに追加されると、エラーが発生します。 既存のオブジェクトは、プロパティの設定時に、エラーが発生します。  
  
> [!NOTE]
>  作成するときに**インデックス**オブジェクトの場合、オプションのプロパティに適切な既定値が存在しないわけでは、プロバイダーが、プロパティをサポートします。 詳細については、プロバイダーでサポートされるプロパティについて、プロバイダーのマニュアルを参照してください。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [Index オブジェクトのプロパティ、メソッド、およびイベント](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [Indexes Append メソッドの例 (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [IndexNulls プロパティの例 (VB)](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [PrimaryKey および Unique プロパティの例 (VB)](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [SortOrder プロパティの例 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [列のコレクション (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Indexes コレクション (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
