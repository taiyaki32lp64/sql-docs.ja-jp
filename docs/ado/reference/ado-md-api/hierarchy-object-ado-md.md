---
title: Hierarchy オブジェクト (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Hierarchy
helpviewer_keywords:
- Hierarchy object [ADO MD]
ms.assetid: 034af340-ac79-494e-ba5e-2b57da1cb9de
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 35e02e4823d0a3abf245e1885b95176d6350d712
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949693"
---
# <a name="hierarchy-object-ado-md"></a>Hierarchy オブジェクト (ADO MD)
1 つの方法を表すのメンバー、[ディメンション](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)集計または「ロール アップ」ことができます ディメンションは、1 つまたは複数の階層に従って集計できます。  
  
## <a name="remarks"></a>コメント  
 コレクションのプロパティと、**階層**オブジェクトを次を行うことができます。  
  
-   識別、**階層**で、[名前](../../../ado/reference/ado-md-api/name-property-ado-md.md)と[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)プロパティ。  
  
-   説明するわかりやすい文字列を返す、**階層**で、[説明](../../../ado/reference/ado-md-api/description-property-ado-md.md)プロパティ。  
  
-   返す、[レベル](../../../ado/reference/ado-md-api/level-object-ado-md.md)を構成するオブジェクト、**階層**で、[レベル](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)コレクション。  
  
-   標準の ADO を使用して[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクションに関する追加情報を取得、**階層**オブジェクト。  
  
 **プロパティ**コレクションには、プロバイダーが指定したプロパティが含まれています。 次の表は、使用可能な可能性があるプロパティを一覧表示します。 実際のプロパティの一覧は、プロバイダーの実装によって異なる場合があります。 使用可能なプロパティの詳細な一覧については、プロバイダーのドキュメントを参照してください。  
  
|名前|説明|  
|----------|-----------------|  
|AllMember|階層でプログラムのロールアップの最高レベルのメンバー。|  
|CatalogName|このキューブが所属するカタログの名前。|  
|CubeName|キューブの名前。|  
|DefaultMember|この階層の既定のメンバーの一意の名前。|  
|説明|階層のわかりやすい説明。|  
|DimensionType|この階層が所属するディメンションの種類。|  
|DimensionUniqueName|ディメンションの明確な名前。|  
|HierarchyCaption|階層に関連付けられたラベルまたはキャプション。|  
|HierarchyCardinality|階層内のメンバーの数。|  
|HierarchyGUID|階層の GUID です。|  
|HierarchyName|階層の名前です。|  
|HierarchyUniqueName|階層の明確な名前。|  
|SchemaName|このキューブが所属するスキーマの名前。|  
  
 このセクションには、次のトピックが含まれています。  
  
-   [プロパティ、メソッド、およびイベント](../../../ado/reference/ado-md-api/hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [CubeDef の例 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Dimension オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [Hierarchies コレクション (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Levels コレクション (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
