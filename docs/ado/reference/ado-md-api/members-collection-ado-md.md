---
title: Members コレクション (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Members
- Members
- Position::Members
helpviewer_keywords:
- Members collection [ADO MD]
ms.assetid: 3a647cde-efdc-4394-b1b9-8cbb1b9d689f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 79394abee5b12bb10f34a34e882d2ac0562722fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949430"
---
# <a name="members-collection-ado-md"></a>Members コレクション (ADO MD)
含まれています、[メンバー](../../../ado/reference/ado-md-api/member-object-ado-md.md)レベル、または軸に沿った位置からのオブジェクト。  
  
## <a name="remarks"></a>コメント  
 A**メンバー**は次の種類のメンバーを格納するコレクションを使用します。  
  
-   キューブ内のレベルを構成するメンバー。 含まれる、**メンバー**のコレクションを[レベル](../../../ado/reference/ado-md-api/level-object-ado-md.md)オブジェクト。 たとえばからサンプルを使用して[多次元スキーマの概要とデータ](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)、国レベルの 4 つのメンバーには、カナダ、米国、英国、およびドイツ。  
  
-   階層内の特定のメンバーの子であるメンバー。 これらのメンバーがによって返される、[子](../../../ado/reference/ado-md-api/children-property-ado-md.md)、親**メンバー**オブジェクト。 たとえば、もう一度同じサンプルを使用して、Canada メンバーの 2 つの子は、カナダ東部、カナダ西部は。  
  
-   軸に沿った特定の位置を定義するメンバーを[セルセット](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)します。 セル セットを使用して[多次元データを扱う](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)バレンタインとシアトル例として、x 軸の最初の位置の 2 つのメンバーは、します。 これらのメンバーに含まれる、**メンバー**のコレクションを[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)オブジェクト。  
  
 **メンバー**は、標準の ADO のコレクションです。 プロパティとメソッドのコレクションでは、次の操作を実行できます。  
  
-   使用して、コレクション内のオブジェクトの数を取得、[カウント](../../../ado/reference/ado-api/count-property-ado.md)プロパティ。  
  
-   既定値は、コレクションからオブジェクトを返す[項目](../../../ado/reference/ado-api/item-property-ado.md)プロパティ。  
  
-   コレクション内のプロバイダーからオブジェクトを更新、[更新](../../../ado/reference/ado-api/refresh-method-ado.md)メソッド。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [プロパティ、メソッド、およびイベント](../../../ado/reference/ado-md-api/members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>関連項目  
 [メンバーの例 (VBScript)](../../../ado/reference/ado-md-api/members-example-vbscript.md)   
 [Member オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)
