---
title: Item プロパティ (ADO MD セルセット) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Item
- Cellset::Item
helpviewer_keywords:
- Item property [ADO MD]
ms.assetid: 0e93d79b-b12e-4e98-889e-c2dfcca20fd0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c7fbce544cac188db7ed3b3d40478aa63809405
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949622"
---
# <a name="item-property-ado-md-cellset"></a>Item プロパティ (ADO MD セルセット)
セルを取得します、[セルセット](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)の座標を使用します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set  
Cell = Cellset.Item ( Positions)  
```  
  
## <a name="parameters"></a>パラメーター  
 *位置*  
 A **VariantArray**のセルを一意に指定する値。 *位置*次のいずれかを指定できます。  
  
-   位置の数値の配列  
  
-   メンバー名の配列  
  
-   序数の位置  
  
## <a name="remarks"></a>コメント  
 使用して、**項目**プロパティを返す、[セル](../../../ado/reference/ado-md-api/cell-object-ado-md.md)オブジェクト内を[セルセット](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)オブジェクト。 場合、**項目**に対応するセル プロパティを見つけられない、*位置*引数、エラーが発生します。  
  
 **項目**プロパティの既定のプロパティは、**セルセット**オブジェクト。 次の構文形式は交換できます。  
  
```  
  
Cellset.Item ( Positions )Cellset ( Positions )  
```  
  
## <a name="remarks"></a>コメント  
 *位置*引数が返されるセルを指定します。 セルの序数位置または各軸に沿った位置を指定できます。 各軸に沿った位置を指定してセルを指定する場合は、位置の数値の値または各位置のメンバーの名前を指定できます。  
  
 序数の位置は内で 1 つのセルを一意に識別する番号、**セルセット**します。 内のセルの番号付け概念的には、**セルセット**場合と、**セルセット**された、 *p*-次元の配列場所*p*軸の数です。 セルは、行優先順で指定されます。 セルの序数を計算する数式を次に示します。  
  
 として文字列をメンバー名が渡された場合**項目**軸の数値識別子の増加順に、メンバーを一覧表示する必要があります。 軸内で、メンバーは、ディメンションの入れ子の増加順に一覧表示する必要があります - は、最も外側にあるディメンションのメンバーは、最初に、内部のディメンションのメンバーが従います。 別個の文字列によって表される各ディメンションおよびメンバーの文字列のリストをコンマで区切る必要があります。  
  
> [!NOTE]
>  データ プロバイダーによってセル メンバー名の取得をサポートされていない可能性があります。 詳細については、プロバイダーのマニュアルを参照してください。  
  
## <a name="applies-to"></a>適用対象  
 [CellSet オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>関連項目  
 [Cell オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [CellSet オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)
