---
title: GetPermissions メソッド (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User25::GetPermissions
- _Group25::raw_GetPermissions
- _Group25::GetPermissions
- _User25::raw_GetPermissions
helpviewer_keywords:
- GetPermissions method [ADOX]
ms.assetid: df201c1f-c76a-465d-98f0-83b7fc36e6e3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5f5b2a5170b499f5e88d4caac4822d2998691eea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966226"
---
# <a name="getpermissions-method-adox"></a>GetPermissions メソッド (ADOX)
に対する権限を返します、[グループ](../../../ado/reference/adox-api/group-object-adox.md)または[ユーザー](../../../ado/reference/adox-api/user-object-adox.md)オブジェクトまたはオブジェクトのコンテナー。  
  
## <a name="syntax"></a>構文  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>戻り値  
 返します、**長い**グループまたはユーザーのオブジェクトのアクセス許可を含むビットマスクを指定する値。 この値は 1 つ以上には、 [RightsEnum](../../../ado/reference/adox-api/rightsenum.md)定数。  
  
#### <a name="parameters"></a>パラメーター  
 *名前*  
 A**バリアント**アクセス許可を設定する対象のオブジェクトの名前を指定する値。 設定*名前*オブジェクト コンテナーのアクセス許可を取得する場合は、null 値にします。  
  
 *ObjectType*  
 A**長い**いずれかの値の[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)定数は、アクセス許可を取得する対象のオブジェクトの型を指定します。  
  
 *ObjectTypeId*  
 任意。 A**バリアント**OLE DB 仕様で定義されていないプロバイダー オブジェクトの種類の GUID を指定する値。 このパラメーターは必要な場合*ObjectType*に設定されている**adPermObjProviderSpecific**。 それ以外は使用されません。  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[Group オブジェクト (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[User オブジェクト (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>関連項目  
 [GetPermissions および SetPermissions メソッドの例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Name プロパティ (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [SetPermissions メソッド (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
