---
title: UnderlyingValue プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::GetUnderlyingValue
- Field20::get_UnderlyingValue
- Field20::UnderlyingValue
helpviewer_keywords:
- UnderlyingValue property
ms.assetid: 00a0c8b8-8b63-433f-95b8-020ab05874a0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 582d0b87edd4729ce54cc2a7323b0a63443cab82
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938853"
---
# <a name="underlyingvalue-property"></a>UnderlyingValue プロパティ
現在の値を示す、[フィールド](../../../ado/reference/ado-api/field-object.md)データベース内のオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 返します、**バリアント**の値を示す値、**フィールド**します。  
  
## <a name="remarks"></a>コメント  
 使用して、 **UnderlyingValue**プロパティをデータベースの現在のフィールドの値を返します。 フィールドの値で、 **UnderlyingValue**プロパティは、値は、トランザクションを表示し、別のトランザクションによって新しい更新プログラムの結果である可能性があります。 これが異なる場合があります、 [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)プロパティで、最初に返された値が反映されて、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。  
  
 使用してに似ています、[再同期](../../../ado/reference/ado-api/resync-method.md)メソッドが、 **UnderlyingValue**プロパティは、現在のレコードから特定のフィールドの値のみを返します。 これは、同じ値を[再同期](../../../ado/reference/ado-api/resync-method.md)メソッドを使用して、置換、[値](../../../ado/reference/ado-api/value-property-ado.md)プロパティ。  
  
 このプロパティを使用すると、 **OriginalValue**プロパティ、バッチ更新プログラムに起因する競合を解決することができます。  
  
## <a name="record"></a>レコード  
 [レコード](../../../ado/reference/ado-api/record-object-ado.md)オブジェクトの場合、このプロパティは空にする前に追加されたフィールドについてなります[Update](../../../ado/reference/ado-api/update-method.md)が呼び出されます。  
  
## <a name="applies-to"></a>適用対象  
 [Field オブジェクト](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>関連項目  
 [OriginalValue および UnderlyingValue プロパティの例 (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue および UnderlyingValue プロパティの例 (vc++)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [OriginalValue プロパティ (ADO)](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [Resync メソッド](../../../ado/reference/ado-api/resync-method.md)
