---
title: ユーザー コレクション (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group::Users
- Users
- Catalog::Users
helpviewer_keywords:
- Users collection [ADOX]
ms.assetid: 0a30fa74-6f10-4410-bd70-882e7c43cd46
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a6146a942e572e28692ceaafd77d6958cdab9dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964950"
---
# <a name="users-collection-adox"></a>Users コレクション (ADOX)
すべてが含まれます格納[ユーザー](../../../ado/reference/adox-api/user-object-adox.md)のオブジェクトを[カタログ](../../../ado/reference/adox-api/catalog-object-adox.md)または[グループ](../../../ado/reference/adox-api/group-object-adox.md)します。  
  
## <a name="remarks"></a>コメント  
 **ユーザー**のコレクションを[カタログ](../../../ado/reference/adox-api/catalog-object-adox.md)カタログのすべてのユーザーを表します。 **ユーザー**のコレクションを[グループ](../../../ado/reference/adox-api/group-object-adox.md)を特定のグループのメンバーシップを持つユーザーのみを表します。  
  
 [Append](../../../ado/reference/adox-api/append-method-adox-users.md)のメソッド、**ユーザー**コレクションは ADOX に一意です。 可能な代替手段としては以下の方法があります。  
  
-   使用してコレクションに新しいユーザーを追加、 **Append**メソッド。  
  
 残りのプロパティとメソッドは、ADO のコレクションに標準的です。 可能な代替手段としては以下の方法があります。  
  
-   使用して、コレクション内のユーザーのアクセス、[項目](../../../ado/reference/ado-api/item-property-ado.md)プロパティ。  
  
-   使用して、コレクションに含まれるユーザーの数を返す、[カウント](../../../ado/reference/ado-api/count-property-ado.md)プロパティ。  
  
-   使用して、コレクションからユーザーを削除、[削除](../../../ado/reference/adox-api/delete-method-adox-collections.md)メソッド。  
  
-   現在のデータベースのスキーマを反映するようにコレクション内のオブジェクトを更新、[更新](../../../ado/reference/ado-api/refresh-method-ado.md)メソッド。  
  
> [!NOTE]
>  追加の前に、**ユーザー**オブジェクトを**ユーザー**のコレクションを**グループ**オブジェクト、**ユーザー**オブジェクトと同じ[名](../../../ado/reference/adox-api/name-property-adox.md)ように追加する 1 つに既に存在する必要があります、**ユーザー**のコレクション、**カタログ**します。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [User コレクションのプロパティ、メソッド、およびイベント](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [GetPermissions および SetPermissions メソッドの例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Catalog オブジェクト (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [User オブジェクト (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
