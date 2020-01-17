---
title: WillChangeField および FieldChangeComplete イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldChangeComplete
- Recordset::WillChangeField
- Recordset::FieldChangeComplete
- WillChangeField
helpviewer_keywords:
- WillChangeField event [ADO]
- fieldchangecomplete event [ADO]
ms.assetid: 3e49fb89-c45b-4d39-823e-3cc887c59b37
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7484e2a57925cc22c83456c244dc67aded5cefd2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945880"
---
# <a name="willchangefield-and-fieldchangecomplete-events-ado"></a>WillChangeField および FieldChangeComplete イベント (ADO)
**WillChangeField**保留中の操作が 1 つまたは複数の値を変更する前に、イベントが呼び出される[フィールド](../../../ado/reference/ado-api/field-object.md)内のオブジェクト、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)します。 **FieldChangeComplete**イベントが 1 つ以上の値の後に呼び出される**フィールド**オブジェクトが変更されました。  
  
## <a name="syntax"></a>構文  
  
```  
  
WillChangeField cFields, Fields, adStatus, pRecordset  
FieldChangeComplete cFields, Fields, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>パラメーター  
 *cFields*  
 A**長い**の数を示す**フィールド**オブジェクト*フィールド*します。  
  
 *Fields*  
 **WillChangeField**、*フィールド*パラメーターが配列の**バリアント**を格納している**フィールド**元の値を持つオブジェクト。 **FieldChangeComplete**、*フィールド*パラメーターが配列の**バリアント**を格納している**フィールド**値が変更されたオブジェクト.  
  
 *pError*  
 [エラー](../../../ado/reference/ado-api/error-object.md)オブジェクト。 場合に発生したエラーを説明の値*adStatus*は**adStatusErrorsOccurred**; 未設定がそれ以外の場合。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状態値。  
  
 ときに**WillChangeField**が呼び出されると、このパラメーターを設定**adStatusOK**イベントの原因となった操作が成功した場合。 設定されている**adStatusCantDeny**場合、このイベントは、保留中の操作のキャンセルを要求できません。  
  
 ときに**FieldChangeComplete**が呼び出されると、このパラメーターを設定**adStatusOK**イベントの原因となった操作が成功した場合または**adStatusErrorsOccurred**場合操作に失敗しました。  
  
 前に**WillChangeField**戻り値は、このパラメーターに設定する**adStatusCancel**保留中の操作のキャンセルを要求します。  
  
 前に**FieldChangeComplete**戻り値は、このパラメーターに設定する**adStatusUnwantedEvent**後続通知しないように設定します。  
  
 *pRecordset*  
 A **Recordset**オブジェクト。 **Recordset**のこのイベントが発生しました。  
  
## <a name="remarks"></a>コメント  
 A **WillChangeField**または**FieldChangeComplete**を設定するときに、イベントが発生する可能性があります、[値](../../../ado/reference/ado-api/value-property-ado.md)プロパティと呼び出し、 [Update](../../../ado/reference/ado-api/update-method.md)メソッドフィールドと値の配列パラメーター。  
  
## <a name="see-also"></a>関連項目  
 [ADO イベント モデルの例 (vc++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)
