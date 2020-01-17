---
title: Append メソッド (ADOX Groups) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups::raw_Append
- Groups::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 56b94fc6-7ef0-4e4a-82a3-033b94c46036
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8281b8b480289dca2b4976cea61a6d6838fa2779
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967318"
---
# <a name="append-method-adox-groups"></a>Append メソッド (ADOX Groups)
新しく追加[グループ](../../../ado/reference/adox-api/group-object-adox.md)オブジェクトを[グループ](../../../ado/reference/adox-api/groups-collection-adox.md)コレクション。  
  
## <a name="syntax"></a>構文  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>パラメーター  
 *[グループ]*  
 **グループ**オブジェクトを追加するか、グループを作成し、追加の名前。  
  
## <a name="remarks"></a>コメント  
 **グループ**のコレクションを[カタログ](../../../ado/reference/adox-api/catalog-object-adox.md)すべてのカタログのグループ アカウントを表します。 **グループ**のコレクションを[ユーザー](../../../ado/reference/adox-api/user-object-adox.md)ユーザーが所属するグループのみを表します。  
  
 プロバイダーがグループの作成をサポートしていない場合、エラーが発生します。  
  
> [!NOTE]
>  追加の前に、**グループ**オブジェクトを**グループ**のコレクションを**ユーザー**オブジェクト、**グループ**オブジェクトと同じ[名前](../../../ado/reference/adox-api/name-property-adox.md)ように追加する 1 つに既に存在する必要があります、**グループ**のコレクション、**カタログ**します。  
  
## <a name="applies-to"></a>適用対象  
 [Groups コレクション (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>関連項目  
 [Groups および Users Append、ChangePassword メソッドの例 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append メソッド (ADOX Columns)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append メソッド (ADOX Indexes)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append メソッド (ADOX Keys)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append メソッド (ADOX Procedures)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append メソッド (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append メソッド (ADOX Users)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append メソッド (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
