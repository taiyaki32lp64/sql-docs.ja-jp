---
title: WillChangeRecord および RecordChangeComplete イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- RecordChangeComplete
- Recordset::WillChangeRecord
- WillChangeRecord
- Recordset::RecordChangeComplete
helpviewer_keywords:
- WillChangeRecord event [ADO]
- recordchangecomplete event [ADO]
ms.assetid: cbc369fd-63af-4a7d-96ae-efa91b78ca69
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6e632db34fbbacbee61cd943067052af27a8cfe8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938672"
---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>WillChangeRecord および RecordChangeComplete イベント (ADO)
**WillChangeRecord**イベントが 1 つまたは複数のレコード (行) の前に呼び出されます、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)を変更します。 **RecordChangeComplete**イベントが呼び出された後に 1 つまたは多くのレコードを変更します。  
  
## <a name="syntax"></a>構文  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>パラメーター  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)このイベントの理由を指定する値。 その値を指定できます**adRsnAddNew**、 **adRsnDelete**、 **adRsnUpdate**、 **adRsnUndoUpdate**、 **adRsnUndoAddNew**、 **adRsnUndoDelete**、または**adRsnFirstChange**します。  
  
 *cRecords*  
 A**長い**(影響) を変更するレコードの数を示す値。  
  
 *pError*  
 [エラー](../../../ado/reference/ado-api/error-object.md)オブジェクト。 場合に発生したエラーを説明の値*adStatus*は**adStatusErrorsOccurred**; 未設定がそれ以外の場合。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状態値。  
  
 ときに**WillChangeRecord**が呼び出されると、このパラメーターを設定**adStatusOK**イベントの原因となった操作が成功した場合。 設定されている**adStatusCantDeny**場合、このイベントは、保留中の操作のキャンセルを要求できません。  
  
 ときに**RecordChangeComplete**が呼び出されると、このパラメーターを設定**adStatusOK**イベントの原因となった操作が成功した場合または**adStatusErrorsOccurred**場合操作に失敗しました。  
  
 前に**WillChangeRecord**戻り値は、このパラメーターに設定する**adStatusCancel**このイベントを発生したか、このパラメーターに設定する操作のキャンセルを要求**adStatusUnwantedEvent**後続通知しないように設定します。  
  
 前に**RecordChangeComplete**戻り値は、このパラメーターに設定する**adStatusUnwantedEvent**後続通知しないように設定します。  
  
 *pRecordset*  
 A **Recordset**オブジェクト。 **Recordset**のこのイベントが発生しました。  
  
## <a name="remarks"></a>コメント  
 A **WillChangeRecord**または**RecordChangeComplete** 、以下の理由により行の最初の変更されたフィールドのイベントが発生する**Recordset**操作。[Update](../../../ado/reference/ado-api/update-method.md)、[削除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)、 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)、 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)、および[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md). 値、 **Recordset** [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)イベントが発生する操作を指定します。  
  
 中に、 **WillChangeRecord** 、イベント、**レコード セット**[フィルター](../../../ado/reference/ado-api/filter-property.md)プロパティに設定されて**adFilterAffectedRecords**します。 イベントの処理中に、このプロパティを変更することはできません。  
  
 設定する必要があります、 **adStatus**パラメーターを**adStatusUnwantedEvent**の可能性のある各**adReason**値が含まれるすべてのイベントのイベント通知を完全に停止するには**adReason**パラメーター。  
  
## <a name="see-also"></a>関連項目  
 [ADO イベント モデルの例 (vc++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)
