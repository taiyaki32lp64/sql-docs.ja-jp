---
title: State プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command25::State
helpviewer_keywords:
- State property [ADO]
ms.assetid: 0b993bac-2653-40b1-bcbb-5b57b6aae2bf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c45b9331ddd538cdf23a57eaf39b6efb71bccc4a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930854"
---
# <a name="state-property-ado"></a>State プロパティ (ADO)
すべての該当するオブジェクトのオブジェクトの状態がオープンかクローズかどうかを示します。 オブジェクトが非同期メソッドを実行している場合は、オブジェクトの現在の状態が接続になっていること、実行、または取得するかどうかを示します。  
  
## <a name="return-value"></a>戻り値  
 返します、**長い**ことができる値、 [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)値。 既定値は**取得のみ**します。  
  
## <a name="remarks"></a>コメント  
 使用することができます、**状態**プロパティをいつでも、特定のオブジェクトの現在の状態を判断します。  
  
 オブジェクトの**状態**プロパティの値の組み合わせを持つことができます。 たとえば、ステートメントを実行している場合は、このプロパティがの合計値**可能**と**adStateExecuting**します。  
  
 **状態**プロパティは読み取り専用です。  
  
## <a name="applies-to"></a>適用対象  
  
||||  
|-|-|-|  
|[Command オブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>関連項目  
 [ConnectionString、ConnectionTimeout、および状態のプロパティの例 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、ConnectionTimeout、および状態のプロパティの例 (vc++)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
