---
title: Append メソッド (ADOX Procedures) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedures::Append
- Procedures::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 38e3492c-c1e1-42e3-a71a-befdc90204db
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dd64ba8119db1ecf2d2b621cd202c9f700b53475
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967285"
---
# <a name="append-method-adox-procedures"></a>Append メソッド (ADOX Procedures)
新しく追加[プロシージャ](../../../ado/reference/adox-api/procedure-object-adox.md)オブジェクトを[プロシージャ](../../../ado/reference/adox-api/procedures-collection-adox.md)コレクション。  
  
## <a name="syntax"></a>構文  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>パラメーター  
 *名前*  
 A**文字列**を作成し、追加する手順の名前を指定する値。  
  
 *Command*  
 ADO[コマンド](../../../ado/reference/ado-api/command-object-ado.md)を作成し、追加する手順を表すオブジェクト。  
  
## <a name="remarks"></a>コメント  
 指定された属性と名前を持つデータ ソースに新しいプロシージャを作成、**コマンド**オブジェクト。  
  
 ユーザーが指定するコマンド テキストは、プロシージャではなく、ビューを表す場合の動作は使用中のプロバイダーに依存します。 **追加**プロバイダーは永続的なコマンドをサポートしていない場合は失敗します。  
  
> [!NOTE]
>  Microsoft Jet OLE DB Provider を使用する場合、**プロシージャ**コレクション**Append**メソッドには、指定することが、**ビュー**なく**プロシージャ**で、*コマンド*パラメーター。 **ビュー**がデータ ソースに追加されに追加されます、**プロシージャ**コレクション。 後に、 **Append**場合、**プロシージャ**と**ビュー**コレクションが更新されると、**ビュー** でしなくなる**プロシージャ**コレクションに表示されますが、**ビュー**コレクション。  
  
## <a name="applies-to"></a>適用対象  
 [Procedures コレクション (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>関連項目  
 [Procedures Append メソッドの例 (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Append メソッド (ADOX Columns)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append メソッド (ADOX Groups)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append メソッド (ADOX Indexes)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append メソッド (ADOX Keys)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append メソッド (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append メソッド (ADOX Users)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append メソッド (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
