---
title: GetObjectOwner メソッド (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::raw_GetObjectOwner
- _Catalog::GetObjectOwner
helpviewer_keywords:
- GetObjectOwner method [ADOX]
ms.assetid: 8965adf0-9075-4125-8142-73eb700029c3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ff85491cf7ca30e3f95526aa7043f321a65cccc5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966270"
---
# <a name="getobjectowner-method-adox"></a>GetObjectOwner メソッド (ADOX)
内のオブジェクトの所有者を返します、[カタログ](../../../ado/reference/adox-api/catalog-object-adox.md)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>戻り値  
 返します、**文字列**を指定する値、[名前](../../../ado/reference/adox-api/name-property-adox.md)の[ユーザー](../../../ado/reference/adox-api/user-object-adox.md)または[グループ](../../../ado/reference/adox-api/group-object-adox.md)オブジェクトを所有しています。  
  
#### <a name="parameters"></a>パラメーター  
 *ObjectName*  
 A**文字列**所有者を取得する対象のオブジェクトの名前を指定する値。  
  
 *ObjectType*  
 A**長い**いずれかの値の[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)定数は、所有者を取得する対象のオブジェクトの型を指定します。  
  
 *ObjectTypeId*  
 任意。 A**バリアント**OLE DB 仕様で定義されていないプロバイダー オブジェクトの種類の GUID を指定する値。 このパラメーターは必要な場合*ObjectType*に設定されている**adPermObjProviderSpecific**。 それ以外は使用されません。  
  
## <a name="remarks"></a>コメント  
 プロバイダーが返すオブジェクトの所有者をサポートしていない場合、エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [Catalog オブジェクト (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>関連項目  
 [GetObjectOwner および SetObjectOwner メソッドの例 (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [SetObjectOwner メソッド](../../../ado/reference/adox-api/setobjectowner-method.md)
