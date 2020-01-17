---
title: Status プロパティ (ADO Recordset) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetStatus
- Recordset15::Status
helpviewer_keywords:
- Status property [ADO Recordset]
ms.assetid: 41d70d89-880f-4850-9d17-19d9790cc8eb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1d91c3e92be7679ad6fbbb4a4ee7bd1bb6a48422
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916839"
---
# <a name="status-property-ado-recordset"></a>Status プロパティ (ADO Recordset)
バッチ更新プログラムに関して現在のレコードやその他の一括操作の状態を示します。  
  
## <a name="return-value"></a>戻り値  
 1 つまたは複数の合計を返します[可能](../../../ado/reference/ado-api/recordstatusenum.md)値。  
  
## <a name="remarks"></a>コメント  
 使用、**状態**プロパティをどのような変更が保留中のバッチを更新中に変更されたレコードの。 使用することも、**状態**などを呼び出すと、一括操作中に失敗したレコードの状態を表示するプロパティ、[再同期](../../../ado/reference/ado-api/resync-method.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)、または[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)メソッド、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト、または設定、[フィルター](../../../ado/reference/ado-api/filter-property.md)プロパティを**レコード セット**ブックマークの配列へのオブジェクト。 このプロパティは、特定のレコードが失敗し、それに応じて解決方法を決定できます。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Status プロパティの例 (Recordset) (VB)](../../../ado/reference/ado-api/status-property-example-recordset-vb.md)   
 [Status プロパティの例 (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
