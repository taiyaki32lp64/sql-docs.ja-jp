---
title: キーのオブジェクト (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Key
helpviewer_keywords:
- Key object [ADOX]
ms.assetid: 55f116fe-4d56-4892-bffe-0cdd6fc727c9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f7e405cfdde86a4f19590a87035ff574e1d255c9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965908"
---
# <a name="key-object-adox"></a>Key オブジェクト (ADOX)
データベース テーブルから、外部キー、または一意のキー フィールドを表します。  
  
## <a name="remarks"></a>コメント  
 次のコード作成、新しい**キー**:  
  
```  
Dim obj As New Key  
```  
  
 プロパティのコレクションと、**キー**オブジェクトのことができます。  
  
-   キーを識別、[名前](../../../ado/reference/adox-api/name-property-adox.md)プロパティ。  
  
-   キーは、プライマリ、外部キー、または内で一意かどうかを判断、[型](../../../ado/reference/adox-api/type-property-key-adox.md)プロパティ。  
  
-   データベースでキーの列へのアクセス、[列](../../../ado/reference/adox-api/columns-collection-adox.md)コレクション。  
  
-   関連テーブルの名前を指定、 [RelatedTable](../../../ado/reference/adox-api/relatedtable-property-adox.md)プロパティ。  
  
-   削除またはとの主キーの更新プログラムで実行されるアクションを決定、 [DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md)と[UpdateRule](../../../ado/reference/adox-api/updaterule-property-adox.md)プロパティ。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [Key オブジェクトのプロパティ、メソッド、およびイベント](../../../ado/reference/adox-api/key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [Keys Append メソッド、キーの種類、RelatedColumn、RelatedTable、UpdateRule プロパティの例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [列のコレクション (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Keys コレクション (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)
