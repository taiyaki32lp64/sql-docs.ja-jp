---
title: FetchComplete イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- FetchComplete event [ADO]
ms.assetid: a28d3858-566c-468d-b070-d1de4339fbea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f3e5f5ae1c886f8d08d522fac19cee563efbb86c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932832"
---
# <a name="fetchcomplete-event-ado"></a>FetchComplete イベント (ADO)
**FetchComplete**に時間のかかる非同期操作のすべてのレコードが取得された後、イベントが呼び出される、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
FetchComplete pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>パラメーター  
 *pError*  
 [エラー](../../../ado/reference/ado-api/error-object.md)オブジェクト。 場合に発生したエラーを説明の値**adStatus**は**adStatusErrorsOccurred**; 未設定がそれ以外の場合。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状態値。 このパラメーターに設定されているこのイベントが呼び出されると、 **adStatusOK**イベントの原因となった操作が成功した場合または**adStatusErrorsOccurred**操作に失敗した場合。  
  
 このイベントから制御が戻る前に、このパラメーターを設定**adStatusUnwantedEvent**後続通知しないように設定します。  
  
 *pRecordset*  
 A **Recordset**オブジェクト。 対象のレコードを取得したオブジェクト。  
  
## <a name="remarks"></a>コメント  
 使用する**FetchComplete** Microsoft Visual Basic、Visual Basic 6.0 以降が必要です。  
  
## <a name="see-also"></a>関連項目  
 [ADO イベント モデルの例 (vc++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)
