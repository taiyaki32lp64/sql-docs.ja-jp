---
title: DefinedSize プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::DefinedSize
helpviewer_keywords:
- DefinedSize property [ADO]
ms.assetid: 3ee27314-a305-4fbc-8433-9ee9a909afd6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4bfb0db701801f1853009594b9d6d24aeb41c629
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933212"
---
# <a name="definedsize-property"></a>DefinedSize プロパティ
データ容量を示します、[フィールド](../../../ado/reference/ado-api/field-object.md)オブジェクト。  
  
## <a name="return-value"></a>戻り値  
 返します、**長い**フィールド オブジェクトのデータ型によって異なります。 を参照してください フィールドの定義のサイズを反映した値[型](../../../ado/reference/ado-api/type-property-ado.md)詳細についてはします。 固定長データ型を使用するフィールドの場合は、戻り値は、(バイト単位) のデータ型のサイズです。 可変長データ型を使用するフィールドの場合これは、次のいずれかです。  
  
1.  文字のフィールドの最大長 (の**adVarChar**と**adVarWChar**) または (バイト単位) (の**adVarBinary**、および**adVarNumeric**) フィールドに定義された長さがある場合。 たとえば、 **adVarChar(5)** フィールドが 5 の最大長。  
  
2.  文字データ型の最大長 (の**ファミリ**と**adWChar**) または (バイト単位) (の**adBinary**と**adNumeric**) 場合、フィールドには、定義された期間はありません。  
  
3.  ~ 0 (ビット演算子、値は 0。 すべてのビットが 1 に設定されます) が定義されている最大長のフィールドもデータ型でもない場合。  
  
4.  長さがないデータ型では、この設定は ~ 0 (ビット演算子、値は 0。 すべてのビットが 1 に設定されます)。  
  
## <a name="remarks"></a>コメント  
 使用して、 **DefinedSize**のデータ容量を決定するプロパティを**フィールド**オブジェクト。  
  
 **DefinedSize**と[ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)プロパティは異なります。 たとえば、**フィールド**の宣言された型を持つオブジェクト**adVarChar**と**DefinedSize** 50、1 つの文字を含むプロパティの値。 **ActualSize**返すプロパティの値が 1 つの文字の長さ (バイト単位)。  
  
## <a name="applies-to"></a>適用対象  
 [Field オブジェクト](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>関連項目  
 [ActualSize および DefinedSize プロパティの例 (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize および DefinedSize プロパティの例 (vc++)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [ActualSize プロパティ (ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
