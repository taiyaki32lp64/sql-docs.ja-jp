---
title: Ordinal プロパティ (ADO MD セル) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: a6001168-b954-47f0-ba0d-c05c4cc40c58
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 194b72ce66eb2efdc3a246f24948b01c790f7b8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949376"
---
# <a name="ordinal-property-ado-md-cell"></a>Ordinal プロパティ (ADO MD セル)
一意に識別する、[セル](../../../ado/reference/ado-md-api/cell-object-ado-md.md)でセル セット内の位置。  
  
## <a name="return-values"></a>戻り値  
 返します、**長い**整数は読み取り専用とします。  
  
## <a name="remarks"></a>コメント  
 セルの序数値は、セル セット内のセルを一意に識別します。 概念的には、セルの番号付けはセル セットではセル セットが、 *p*の次元の配列、 *p*の数は、[軸](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)。 セルは、行優先順での 0 から始まる番号が付けられます。 セルの序数を計算する数式を次に示します。  
  
 セルの序数値で使用できる、[項目](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)のプロパティ、[セルセット](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)を迅速に取得するオブジェクト、[セル](../../../ado/reference/ado-md-api/cell-object-ado-md.md)します。  
  
## <a name="applies-to"></a>適用対象  
 [Cell オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>関連項目  
 [軸の例 (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Cellset オブジェクト (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Item プロパティ (ADO MD セルセット)](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Ordinal プロパティ (ADO MD 位置)](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)
