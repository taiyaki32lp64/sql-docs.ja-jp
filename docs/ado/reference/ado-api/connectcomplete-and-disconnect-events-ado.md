---
title: ConnectComplete および Disconnect イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Disconnect
- Connection::ConnectComplete
- ConnectComplete
- Connection::Disconnect
helpviewer_keywords:
- Disconnect event [ADO]
- ConnectComplete event [ADO]
ms.assetid: 568f5252-d069-4d99-a01b-2ada87ad1304
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 448270ddf0e8cd7efb5ec39a93d4ff993360730e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919579"
---
# <a name="connectcomplete-and-disconnect-events-ado"></a>ConnectComplete および Disconnect イベント (ADO)
**ConnectComplete**接続が開始した後にイベントが呼び出されます。 **切断**接続が終了した後にイベントが呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
ConnectComplete pError, adStatus, pConnection  
Disconnect adStatus, pConnection  
```  
  
#### <a name="parameters"></a>パラメーター  
 *pError*  
 [エラー](../../../ado/reference/ado-api/error-object.md)オブジェクト。 場合に発生したエラーを説明の値*adStatus*は**adStatusErrorsOccurred**; 未設定がそれ以外の場合。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)値を返しますでは常に**adStatusOK**します。  
  
 ときに**ConnectComplete**が呼び出されると、このパラメーターを設定**adStatusCancel**場合、 **WillConnect**イベントが保留中の接続のキャンセルを要求します。  
  
 どちらのイベントから制御が戻る前に、このパラメーターを設定**adStatusUnwantedEvent**後続通知しないように設定します。 ただし、終了および再開、[接続](../../../ado/reference/ado-api/connection-object-ado.md)これらのイベントを再度発生させます。  
  
 *pConnection*  
 **接続**オブジェクトをこのイベントが適用されます。  
  
## <a name="see-also"></a>関連項目  
 [ADO イベント モデルの例 (vc++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)
