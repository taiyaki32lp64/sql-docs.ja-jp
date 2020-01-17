---
title: EventReasonEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EventReasonEnum
helpviewer_keywords:
- EventReasonEnum enumeration [ADO]
ms.assetid: 7d4a5496-ec2d-4936-b36a-7049a82be4b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c37a7385cc3aabb725f86261203d22b5b10c3be6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918872"
---
# <a name="eventreasonenum"></a>EventReasonEnum
イベントの発生の原因となった理由を指定します。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|操作は、新しいレコードを追加します。|  
|**adRsnClose**|9|操作の終了、 **Recordset**します。|  
|**adRsnDelete**|2|操作は、レコードを削除します。|  
|**adRsnFirstChange**|11|操作は、レコードに、最初の変更を加えた。|  
|**adRsnMove**|10|操作内のレコード ポインターを移動する、 **Recordset**します。|  
|**adRsnMoveFirst**|12|操作の最初のレコードをレコード ポインターを移動する、 **Recordset**します。|  
|**adRsnMoveLast**|15|操作は、最後のレコードをレコード ポインターを移動、 **Recordset**します。|  
|**adRsnMoveNext**|13|操作は次のレコードをレコード ポインターを移動、 **Recordset**します。|  
|**adRsnMovePrevious**|14|操作の前のレコードをレコード ポインターを移動する、 **Recordset**します。|  
|**adRsnRequery**|7|クエリを再実行する操作、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。|  
|**adRsnResynch**|8|操作が再同期、 **Recordset**データベースとします。|  
|**adRsnUndoAddNew**|5|新しいレコードの追加が取り消されました。|  
|**adRsnUndoDelete**|6|レコードの削除が取り消されました。|  
|**adRsnUndoUpdate**|4|レコードの更新が取り消されました。|  
|**adRsnUpdate**|3|操作は、既存のレコードを更新します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.EventReason.ADDNEW|  
|AdoEnums.EventReason.CLOSE|  
|AdoEnums.EventReason.DELETE|  
|AdoEnums.EventReason.FIRSTCHANGE|  
|AdoEnums.EventReason.MOVE|  
|AdoEnums.EventReason.MOVEFIRST|  
|AdoEnums.EventReason.MOVELAST|  
|AdoEnums.EventReason.MOVENEXT|  
|AdoEnums.EventReason.MOVEPREVIOUS|  
|AdoEnums.EventReason.REQUERY|  
|AdoEnums.EventReason.RESYNCH|  
|AdoEnums.EventReason.UNDOADDNEW|  
|AdoEnums.EventReason.UNDODELETE|  
|AdoEnums.EventReason.UNDOUPDATE|  
|AdoEnums.EventReason.UPDATE|  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[WillChangeRecord および RecordChangeComplete イベント (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|[WillChangeRecordset および RecordsetChangeComplete イベント (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|  
|[WillMove および MoveComplete イベント (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)||
