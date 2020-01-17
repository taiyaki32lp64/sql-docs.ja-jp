---
title: ユーザー オブジェクト (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- User
helpviewer_keywords:
- User object [ADOX]
ms.assetid: f68e32ce-ef7c-407d-bdb5-d280947ae0e2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf454e28e7a823eb643b5bbd92b0396fac15a028
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964974"
---
# <a name="user-object-adox"></a>User オブジェクト (ADOX)
セキュリティで保護されたデータベース内のアクセス許可を持つユーザー アカウントを表します。  
  
## <a name="remarks"></a>コメント  
 [ユーザー](../../../ado/reference/adox-api/users-collection-adox.md)のコレクションを[カタログ](../../../ado/reference/adox-api/catalog-object-adox.md)カタログのすべてのユーザーを表します。 **ユーザー**のコレクションを[グループ](../../../ado/reference/adox-api/group-object-adox.md)特定のグループのユーザーのみを表します。  
  
 プロパティ、コレクション、およびメソッドの使用、**ユーザー**オブジェクトのことができます。  
  
-   持つユーザーを識別、[名前](../../../ado/reference/adox-api/name-property-adox.md)プロパティ。  
  
-   持つユーザーのパスワードを変更、 [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md)メソッド。  
  
-   ユーザーが読み取りになっているかどうかを判断する書き込み、または削除のアクセス許可、 [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md)と[SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)メソッド。  
  
-   アクセスをユーザーが所属するグループ、[グループ](../../../ado/reference/adox-api/groups-collection-adox.md)コレクション。  
  
-   プロバイダー固有のプロパティにアクセス、[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクション。  
  
-   確認、 [ParentCatalog](../../../ado/reference/adox-api/parentcatalog-property-adox.md)ユーザー。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [User オブジェクトのプロパティ、メソッド、およびイベント](../../../ado/reference/adox-api/user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [GetPermissions および SetPermissions メソッドの例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Groups コレクション (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Users コレクション (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
