---
title: GetSchemaObject メソッド (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- GetSchemaObject
- Cellset::GetSchemaObject
helpviewer_keywords:
- GetSchemaObject method [ADO MD]
ms.assetid: 36b754b4-6b17-4dd1-a925-bca46938b7c4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 690c81a46c62c8844780e82b5c82a0ff7301105d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949760"
---
# <a name="getschemaobject-method-ado-md"></a>GetSchemaObject メソッド (ADO MD)
ADO MD のスキーマ オブジェクトを取得します ([ディメンション](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)、[階層](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)、[レベル](../../../ado/reference/ado-md-api/level-object-ado-md.md)、または[メンバー](../../../ado/reference/ado-md-api/member-object-ado-md.md)) によってその[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md).  
  
## <a name="syntax"></a>構文  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ObjType*  
 A [SchemaObjectTypeEnum](../../../ado/reference/ado-md-api/schemaobjecttypeenum.md) (ディメンション、階層、レベル、またはメンバー) を取得するスキーマ オブジェクトの種類を指定する値。  
  
 *UniqueName*  
 A**文字列**を指定する、 **UniqueName**を取得するオブジェクトのプロパティ値。  
  
## <a name="remarks"></a>コメント  
 **GetSchemaObject**で指定したとおり、一意の名前を使用してオブジェクトを取得、 **UniqueName**プロパティ。 親オブジェクトの名前は、既知である必要はありませんし、親のコレクションは、スキーマ オブジェクトを取得する事前設定する必要はありません。  
  
## <a name="applies-to"></a>適用対象  
 [CubeDef オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>関連項目  
 [CubeDef オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)
