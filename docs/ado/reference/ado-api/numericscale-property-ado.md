---
title: NumericScale プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::NumericScale
- Field20::NumericScale
helpviewer_keywords:
- NumericScale property [ADO]
ms.assetid: 29a02992-64be-4fcd-be13-445cba205893
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 38d283e8fedb90ed5a99143090bc6a077efa8512
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932103"
---
# <a name="numericscale-property-ado"></a>NumericScale プロパティ (ADO)
内の数値の小数点以下桁数を示す、[パラメーター](../../../ado/reference/ado-api/parameter-object.md)または[フィールド](../../../ado/reference/ado-api/field-object.md)オブジェクト。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**バイト**どの数値の小数点以下桁数を示す値が解決されます。  
  
## <a name="remarks"></a>コメント  
 使用して、 **NumericScale**プロパティを数値の値を表す小数点の右側に数字の数に使用する特定**パラメーター**または**フィールド**オブジェクト。  
  
 **パラメーター** 、オブジェクト、 **NumericScale**読み取り/書き込みプロパティです。  
  
 **フィールド**オブジェクト、 **NumericScale**は通常読み取り専用です。 ただし、新規の**フィールド**に追加されたオブジェクト、[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)のコレクションを[レコード](../../../ado/reference/ado-api/record-object-ado.md)、 **NumericScale**は読み取り/書き込みした場合のみ、[値](../../../ado/reference/ado-api/value-property-ado.md)プロパティを**フィールド**が指定されているデータ プロバイダーからその新しいが正常に追加し、**フィールド**を呼び出すことによって[Update](../../../ado/reference/ado-api/update-method.md)のメソッド、[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)コレクション。  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[Parameter オブジェクト](../../../ado/reference/ado-api/parameter-object.md)|[Field オブジェクト](../../../ado/reference/ado-api/field-object.md)|  
  
## <a name="see-also"></a>関連項目  
 [NumericScale および Precision プロパティの例 (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale および Precision プロパティの例 (vc++)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [Precision プロパティ (ADO)](../../../ado/reference/ado-api/precision-property-ado.md)
