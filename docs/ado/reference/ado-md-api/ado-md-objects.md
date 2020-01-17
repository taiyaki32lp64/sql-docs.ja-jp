---
title: ADO MD オブジェクト |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, objects
- objects [ADO MD]
ms.assetid: 2a32e873-3282-4520-a7ed-89493f1da80e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d568ca20cca6c12a04c0f3d54a2c134d59a0d7fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930575"
---
# <a name="ado-md-objects"></a>ADO MD オブジェクト

|||  
|-|-|  
|[Axis](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|1 つまたは複数のディメンションの選択したメンバーを含むセル セットのフィルター軸または位置指定を表します。|  
|[Catalog](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|多次元データ プロバイダー (MDP) に固有の多次元スキーマ情報 (つまり、キューブと基になるディメンション、階層、レベル、およびメンバー) が含まれています。|  
|[セル](../../../ado/reference/ado-md-api/cell-object-ado-md.md)|セル セットに含まれる軸座標の交差部分にデータを表します。|  
|[Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|多次元クエリの結果を表します。 これは、キューブまたはその他のセルセットから選択したセルのコレクションです。|  
|[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|関連するディメンションのセットを含む多次元スキーマからキューブを表します。|  
|[Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|1 つまたは複数のメンバーの階層を含む多次元キューブのディメンションの 1 つを表します。|  
|[Hierarchy](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|ディメンションのメンバーを集計または「ロール アップ」の 1 つの方法を示します ディメンションは、1 つまたは複数の階層に従って集計できます。|  
|[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)|それぞれが階層内で同じランクを持つメンバーのセットが含まれています。|  
|[Member](../../../ado/reference/ado-md-api/member-object-ado-md.md)|キューブでは、レベルのメンバー、レベルのメンバーまたはセル セットの軸に沿った位置のメンバーの子を表します。|  
|[[Position]](../../../ado/reference/ado-md-api/position-object-ado-md.md)|軸に沿ったポイントを定義するさまざまなディメンションの 1 つまたは複数のメンバーのセットを表します。|  
  
 また、**Catalog** オブジェクトは ADO **Connection** オブジェクトに接続されており、これは標準の ADO ライブラリに含まれています。  
  
|オブジェクト|説明|  
|------------|-----------------|  
|[Connection](../../../ado/reference/ado-api/connection-object-ado.md)|データ ソースへの接続を開くを表します。|  
  
 これらのオブジェクト間のリレーションシップは、「、 [ADO MD オブジェクト モデル](../../../ado/reference/ado-md-api/ado-md-object-model.md)します。  
  
 ADO MD オブジェクトの多くは、対応するコレクションに格納することができます。 たとえば、 [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) オブジェクトは **Catalog** の [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) コレクションに格納できます。 詳細については、次を参照してください。 [ADO MD のコレクション](../../../ado/reference/ado-md-api/ado-md-collections.md)します。  
  
## <a name="see-also"></a>参照  
 [ADO MD の API リファレンス](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [ADO MD のコード例](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [ADO MD のコレクション](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [ADO MD の列挙定数](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [ADO MD のメソッド](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [ADO MD オブジェクト モデル](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO MD のプロパティ](../../../ado/reference/ado-md-api/ado-md-properties.md)
