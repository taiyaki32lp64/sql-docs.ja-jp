---
title: WillMove および MoveComplete イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::MoveComplete
- WillMove
- MoveComplete
- Recordset::WillMove
helpviewer_keywords:
- MoveComplete event [ADO]
- WillMove event [ADO]
ms.assetid: 1a3d1042-4f30-4526-a0c7-853c242496db
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c91f3166b493ac1e2fada3e759cb107e34c7ca81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945913"
---
# <a name="willmove-and-movecomplete-events-ado"></a>WillMove および MoveComplete イベント (ADO)
**WillMove**保留中の操作の現在の位置を変更する前に、イベントが呼び出される、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。 **MoveComplete**内の現在位置の後にイベントが呼び出される、 **Recordset**変更します。  
  
## <a name="syntax"></a>構文  
  
```  
  
WillMove adReason, adStatus, pRecordset  
MoveComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>パラメーター  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)このイベントの理由を指定する値。 その値を指定できます**adRsnMoveFirst**、 **adRsnMoveLast**、 **adRsnMoveNext**、 **adRsnMovePrevious**、 **adRsnMove**、または**adRsnRequery**します。  
  
 *pError*  
 [エラー](../../../ado/reference/ado-api/error-object.md)オブジェクト。 場合に発生したエラーを説明の値*adStatus*は**adStatusErrorsOccurred**; それ以外の場合、パラメーターは設定されていません。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状態値。  
  
 ときに**WillMove**が呼び出されると、このパラメーターを設定**adStatusOK**イベントの原因となった操作が成功した場合。 設定されている**adStatusCantDeny**場合、このイベントは、保留中の操作のキャンセルを要求できません。  
  
 ときに**MoveComplete**が呼び出されると、このパラメーターを設定**adStatusOK**イベントの原因となった操作が成功した場合または**adStatusErrorsOccurred**場合、操作に失敗しました。  
  
 前に**WillMove**戻り値は、このパラメーターに設定する**adStatusCancel**保留中の操作のキャンセルを要求またはこのパラメーターに設定する**adStatusUnwantedEvent**後続の通知をしないように設定します。  
  
 前に**MoveComplete**戻り値は、このパラメーターに設定する**adStatusUnwantedEvent**後続通知しないように設定します。  
  
 *pRecordset*  
 A [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。 **Recordset**のこのイベントが発生しました。  
  
## <a name="remarks"></a>コメント  
 A **WillMove**または**MoveComplete**イベントは、以下の理由により発生する可能性があります**Recordset**操作。[開いている](../../../ado/reference/ado-api/open-method-ado-recordset.md)、[移動](../../../ado/reference/ado-api/move-method-ado.md)、 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)、および[Requery](../../../ado/reference/ado-api/requery-method.md)します。 これらのイベントは、次のプロパティのため発生します。[フィルター](../../../ado/reference/ado-api/filter-property.md)、[インデックス](../../../ado/reference/ado-api/index-property.md)、[ブックマーク](../../../ado/reference/ado-api/bookmark-property-ado.md)、 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)、および[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)します。 これらのイベントは、子の場合にも発生**レコード セット**が**レコード セット**接続されているイベントとその親**レコード セット**が移動します。  
  
 設定する必要があります、 *adStatus*パラメーターを**adStatusUnwantedEvent**の可能性のある各*adReason*任意のイベントのイベント通知を完全に停止するには値を含まれています、 *adReason*パラメーター。  
  
## <a name="see-also"></a>関連項目  
 [ADO イベント モデルの例 (vc++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
