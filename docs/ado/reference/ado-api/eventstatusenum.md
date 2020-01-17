---
title: EventStatusEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EventStatusEnum
helpviewer_keywords:
- EventStatusEnum enumeration [ADO]
ms.assetid: ebfd4cda-4017-4873-9d28-38b1c7db12a8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8883679a85d1e134b1759c90cde524bb97995130
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932862"
---
# <a name="eventstatusenum"></a>EventStatusEnum
イベントの実行の現在の状態を指定します。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adStatusCancel**|4|イベントの発生の原因となった操作のキャンセルを要求します。|  
|**adStatusCantDeny**|3|操作が保留中の操作のキャンセルを要求できないことを示します。|  
|**adStatusErrorsOccurred**|2|エラーまたはエラーのために、イベントの原因となった操作が失敗したことを示します。|  
|**adStatusOK**|1|イベントの原因となった操作が成功したことを示します。|  
|**adStatusUnwantedEvent**|5|イベント メソッドの実行が完了する前に、後続の通知をできないようにします。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.EventStatus.CANCEL|  
|AdoEnums.EventStatus.CANTDENY|  
|AdoEnums.EventStatus.ERRORSOCCURRED|  
|AdoEnums.EventStatus.OK|  
|AdoEnums.EventStatus.UNWANTEDEVENT|  
  
## <a name="applies-to"></a>適用対象  
  
||||  
|-|-|-|  
|[BeginTransComplete、CommitTransComplete、および RollbackTransComplete イベント (ADO)](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|[ConnectComplete および Disconnect イベント (ADO)](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|[EndOfRecordset イベント (ADO)](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|  
|[ExecuteComplete イベント (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)|[FetchComplete イベント (ADO)](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|[InfoMessage イベント (ADO)](../../../ado/reference/ado-api/infomessage-event-ado.md)|  
|[WillChangeField および FieldChangeComplete イベント (ADO)](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|[WillChangeRecord および RecordChangeComplete イベント (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|[WillChangeRecordset および RecordsetChangeComplete イベント (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|  
|[WillConnect イベント (ADO)](../../../ado/reference/ado-api/willconnect-event-ado.md)|[WillExecute イベント (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|[WillMove および MoveComplete イベント (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|
