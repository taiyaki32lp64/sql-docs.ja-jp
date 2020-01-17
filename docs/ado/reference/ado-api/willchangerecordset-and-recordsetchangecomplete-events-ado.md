---
title: WillChangeRecordset および RecordsetChangeComplete イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::RecordsetChangeComplete
- RecordsetChangeComplete
- Recordset::WillChangeRecordset
- WillChangeRecordset
helpviewer_keywords:
- RecordsetChangeComplete event [ADO]
- WillChangeRecordset event [ADO]
ms.assetid: d5d44659-e0d9-46d9-a297-99c43555082f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dd4e2f1485c18ce1fecc76d4eb23aa4132d85329
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938682"
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>WillChangeRecordset および RecordsetChangeComplete イベント (ADO)
**WillChangeRecordset**保留中の操作を変更する前に、イベントが呼び出される、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。 **RecordsetChangeComplete**イベントが呼び出された後、 **Recordset**が変更されました。  
  
## <a name="syntax"></a>構文  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>パラメーター  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)このイベントの理由を指定する値。 その値を指定できます**adRsnRequery**、 **adRsnResynch**、 **adRsnClose**、 **adRsnOpen**します。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状態値。  
  
 ときに**WillChangeRecordset**が呼び出されると、このパラメーターを設定**adStatusOK**イベントの原因となった操作が成功した場合。 設定されている**adStatusCantDeny**場合、このイベントは、保留中の操作のキャンセルを要求できません。  
  
 ときに**RecordsetChangeComplete**が呼び出されると、このパラメーターを設定**adStatusOK**場合は、イベントの原因となった操作が成功すると、 **adStatusErrorsOccurred**場合操作に失敗しました、または**adStatusCancel**場合は、操作は、以前に受け入れられたに関連付けられている**WillChangeRecordset**イベントが取り消されました。  
  
 前に**WillChangeRecordset**戻り値は、このパラメーターに設定する**adStatusCancel**保留中の操作のキャンセルを要求または後続を防ぐために adStatusUnwantedEvent にこのパラメーターを設定通知します。  
  
 前に**WillChangeRecordset**または**RecordsetChangeComplete**戻り値は、このパラメーターに設定する**adStatusUnwantedEvent**後続通知しないように設定します。  
  
 *pError*  
 [エラー](../../../ado/reference/ado-api/error-object.md)オブジェクト。 場合に発生したエラーを説明の値*adStatus*は**adStatusErrorsOccurred**; 未設定がそれ以外の場合。  
  
 *pRecordset*  
 A **Recordset**オブジェクト。 **Recordset**のこのイベントが発生しました。  
  
## <a name="remarks"></a>コメント  
 A **WillChangeRecordset**または**RecordsetChangeComplete**ためのイベントが発生する、 **Recordset** [Requery](../../../ado/reference/ado-api/requery-method.md)または[オープン](../../../ado/reference/ado-api/open-method-ado-recordset.md)メソッド。  
  
 プロバイダーは、ブックマークをサポートしていない場合、 **RecordsetChange**イベント通知が新しい行は、プロバイダーから取得されるたびに発生します。 このイベントの頻度によって異なります、 **RecordsetCacheSize**プロパティ。  
  
 設定する必要があります、 **adStatus**パラメーターを**adStatusUnwantedEvent**の可能性のある各**adReason**値が含まれるすべてのイベントのイベント通知を完全に停止するには**adReason**パラメーター。  
  
## <a name="see-also"></a>関連項目  
 [ADO イベント モデルの例 (vc++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)
