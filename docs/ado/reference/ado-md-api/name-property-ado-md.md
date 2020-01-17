---
title: Name プロパティ (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Name
- CubeDef::Name
- Member::Name
- Catalog::Name
- Dimension::Name
- Name
- Axis::Name
- Hierarchy::Name
helpviewer_keywords:
- Name property [ADO MD]
ms.assetid: 4a04380b-51dc-4aaf-8d25-123cdd589641
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c248139abfd136d5c79658592e0e49d5e10444aa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949395"
---
# <a name="name-property-ado-md"></a>Name プロパティ (ADO MD)
オブジェクトの名前を示します。  
  
## <a name="return-values"></a>戻り値  
 返します、**文字列**は読み取り専用であるとします。  
  
## <a name="remarks"></a>コメント  
 取得することができます、**名前**名前で直接その後、オブジェクトを参照できます、序数参照によってオブジェクトのプロパティ。 たとえば場合、 `cdf.CubeDefs(0).Name` "振りビデオ Store"が生成されますこれを参照することができます[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)として`cdf.CubeDefs("Bobs Video Store")`します。  
  
## <a name="applies-to"></a>適用対象  
  
||||  
|-|-|-|  
|[Axis オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|[Catalog オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[CubeDef オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|  
|[Dimension オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[Hierarchy オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|[Level オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|  
|[Member オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)|||  
  
## <a name="see-also"></a>関連項目  
 [カタログの例 (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Caption プロパティ (ADO MD)](../../../ado/reference/ado-md-api/caption-property-ado-md.md)   
 [Description プロパティ (ADO MD)](../../../ado/reference/ado-md-api/description-property-ado-md.md)   
 [UniqueName プロパティ (ADO MD)](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)
