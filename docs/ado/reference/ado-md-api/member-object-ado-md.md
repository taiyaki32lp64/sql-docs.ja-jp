---
title: メンバー オブジェクト (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member
helpviewer_keywords:
- Member object [ADO MD], members
ms.assetid: 3dedf755-0741-4c3f-8b4e-bff8ff8809c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44d6b5f06bffb1cea786ba34d3d2aa8a3efb45ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949494"
---
# <a name="member-object-ado-md"></a>Member オブジェクト (ADO MD)
キューブでは、レベルのメンバー、レベルのメンバーまたはセル セットの軸に沿った位置のメンバーの子を表します。  
  
## <a name="remarks"></a>コメント  
 プロパティを**メンバー**が使用されているコンテキストによって異なります。 A**メンバー**の[レベル](../../../ado/reference/ado-md-api/level-object-ado-md.md)で、 [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)が、[子](../../../ado/reference/ado-md-api/children-property-ado-md.md)プロパティを返す、**メンバー**で現在の階層内の次の下位レベル**メンバー**します。 **メンバー**の[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)、**子**コレクションが空では常にします。 また、[型](../../../ado/reference/ado-md-api/type-property-ado-md.md)プロパティにのみ適用されます**メンバー**の**レベル**します。  
  
 A**メンバー**の**位置**が 2 つのプロパティを表示するときに利用できる、[セルセット](../../../ado/reference/ado-md-api/cellset-object-ado-md.md):[DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md)と[ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)します。 これらのプロパティにアクセスする場合、エラーが発生する**メンバー**の**レベル**します。  
  
 コレクションのプロパティと、**メンバー**のオブジェクトを**レベル**次を行うことができます。  
  
-   識別、**メンバー**で、[名前](../../../ado/reference/ado-md-api/name-property-ado-md.md)と[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)プロパティ。  
  
-   表示するときに使用する文字列を返す、**メンバー**で、[キャプション](../../../ado/reference/ado-md-api/caption-property-ado-md.md)プロパティ。  
  
-   メジャーまたは式を記述する意味のある文字列を返す**メンバー**で、[説明](../../../ado/reference/ado-md-api/description-property-ado-md.md)プロパティ。  
  
-   性質を特定、**メンバー**で、[型](../../../ado/reference/ado-md-api/type-property-ado-md.md)プロパティ。  
  
-   に関する情報を取得、**レベル**の**メンバー**で、 [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md)と[LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md)プロパティ。  
  
-   取得関連**メンバー**で、[階層](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)で、[親](../../../ado/reference/ado-md-api/parent-property-ado-md.md)と[子](../../../ado/reference/ado-md-api/children-property-ado-md.md)プロパティ。  
  
-   子の数、**メンバー**で、 [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)プロパティ。  
  
-   標準の ADO を使用して[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクションに関する追加情報を取得、**レベル**オブジェクト。  
  
 コレクションのプロパティと、**メンバー**の**位置**に沿って、[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)次を行うことができます。  
  
-   識別、**メンバー**で、[名前](../../../ado/reference/ado-md-api/name-property-ado-md.md)と[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)プロパティ。  
  
-   表示するときに使用する文字列を返す、**メンバー**で、[キャプション](../../../ado/reference/ado-md-api/caption-property-ado-md.md)プロパティ。  
  
-   メジャーまたは式を記述する意味のある文字列を返す**メンバー**で、[説明](../../../ado/reference/ado-md-api/description-property-ado-md.md)プロパティ。  
  
-   に関する情報を取得、**レベル**の**メンバー**で、 [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md)と[LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md)プロパティ。  
  
-   子の数、**メンバー**で、 [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)プロパティ。  
  
-   使用して、 [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md)に少なくとも 1 つの子があるかどうかを決定するプロパティ、**軸**直後に続くこの**メンバー**。  
  
-   使用、 [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)プロパティを確認するかどうかこの親**メンバー**その直前の親と同じです**メンバー**します。  
  
-   標準の ADO を使用して[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクションに関する追加情報を取得、**レベル**オブジェクト。  
  
 **プロパティ**コレクションには、プロバイダーが指定したプロパティが含まれています。 次の表は、使用可能な可能性があるプロパティを一覧表示します。 実際のプロパティの一覧は、プロバイダーの実装によって異なる場合があります。 使用可能なプロパティの詳細な一覧については、プロバイダーのドキュメントを参照してください。  
  
|名前|説明|  
|----------|-----------------|  
|CatalogName|このキューブが所属するカタログの名前。|  
|ChildrenCardinality|メンバーが持つ子の数。|  
|CubeName|キューブの名前。|  
|説明|メンバーのわかりやすい説明。|  
|DimensionUniqueName|明確な名前、[ディメンション](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)します。|  
|HierarchyUniqueName|階層の明確な名前。|  
|LevelNumber|レベルと階層のルート間の距離。|  
|LevelUniqueName|明確なレベルの名前。|  
|MemberCaption|メンバーに関連付けられたラベルまたはキャプション。|  
|MemberGUID|メンバーの GUID。|  
|メンバー名|メンバーの名前。|  
|MemberOrdinal|メンバーの序数。|  
|MemberType|メンバーの種類。|  
|MemberUniqueName|メンバーの明確な名前。|  
|ParentCount|このメンバーが持つ親の数の数。|  
|ParentLevel|メンバーの親のレベル数。|  
|ParentUniqueName|メンバーの親の明確な名前。|  
|SchemaName|このキューブが所属するスキーマの名前。|  
  
 このセクションには、次のトピックが含まれています。  
  
-   [プロパティ、メソッド、およびイベント](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [カタログの例 (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Members コレクション (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
