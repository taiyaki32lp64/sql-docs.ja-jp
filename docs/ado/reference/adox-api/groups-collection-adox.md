---
title: グループのコレクション (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups
- User::Groups
- Catalog::Groups
helpviewer_keywords:
- Groups collection [ADOX]
ms.assetid: 09aa7b0a-69d5-4564-80a7-20ad8189670f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e39be3cf32f04a60e554928f66cdc6123322f19c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966182"
---
# <a name="groups-collection-adox"></a>Groups コレクション (ADOX)
すべてを含む保存[グループ](../../../ado/reference/adox-api/group-object-adox.md)カタログまたはユーザーのオブジェクト。  
  
## <a name="remarks"></a>コメント  
 **グループ**のコレクションを[カタログ](../../../ado/reference/adox-api/catalog-object-adox.md)すべてのカタログのグループ アカウントを表します。 **グループ**のコレクションを[ユーザー](../../../ado/reference/adox-api/user-object-adox.md)ユーザーが所属するグループのみを表します。  
  
 [Append](../../../ado/reference/adox-api/append-method-adox-groups.md)のメソッド、**グループ**コレクションは ADOX に一意です。 可能な代替手段としては以下の方法があります。  
  
-   新しいセキュリティ グループを使用して、コレクションに追加、 **Append**メソッド。  
  
 残りのプロパティとメソッドは、ADO のコレクションに標準的です。 可能な代替手段としては以下の方法があります。  
  
-   使用して、コレクション内のグループへのアクセス、[項目](../../../ado/reference/ado-api/item-property-ado.md)プロパティ。  
  
-   使用して、コレクションに含まれるグループの数を返す、[カウント](../../../ado/reference/ado-api/count-property-ado.md)プロパティ。  
  
-   グループを使用して、コレクションから削除、[削除](../../../ado/reference/adox-api/delete-method-adox-collections.md)メソッド。  
  
-   現在のデータベース スキーマを反映するようにコレクション内のオブジェクトを更新、[更新](../../../ado/reference/ado-api/refresh-method-ado.md)メソッド。  
  
> [!NOTE]
>  追加の前に、**グループ**オブジェクトを**グループ**のコレクションを**ユーザー**オブジェクト、**グループ**オブジェクトと同じ[名前](../../../ado/reference/adox-api/name-property-adox.md)ように追加する 1 つに既に存在する必要があります、**グループ**のコレクション、**カタログ**します。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [Groups コレクションのプロパティ、メソッド、およびイベント](../../../ado/reference/adox-api/groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [Catalog オブジェクト (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Group オブジェクト (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)
