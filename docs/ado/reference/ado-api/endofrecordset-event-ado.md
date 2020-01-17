---
title: EndOfRecordset イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EndOfRecordset
- Recordset::EndOfRecordset
helpviewer_keywords:
- EndOfRecordset event [ADO]
ms.assetid: 475de5e2-f634-4954-9edf-0027a6ba38d6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a83f101d46a94a4ea43a85424677fc1c8da08be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918939"
---
# <a name="endofrecordset-event-ado"></a>EndOfRecordset イベント (ADO)
**EndOfRecordset**イベントが呼び出されるは、行の末尾に移動する試みがあるときに、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>パラメーター  
 *fMoreData*  
 A **VARIANT_BOOL**値を VARIANT_TRUE に設定、複数の行に追加されたことを示します、 **Recordset**します。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状態値。  
  
 ときに**EndOfRecordset**が呼び出されると、このパラメーターを設定**adStatusOK**イベントの原因となった操作が成功した場合。 設定されている**adStatusCantDeny**場合、このイベントは、このイベントの原因となった操作のキャンセルを要求できません。  
  
 前に**EndOfRecordset**戻り値は、このパラメーターに設定する**adStatusUnwantedEvent**後続通知しないように設定します。  
  
 *pRecordset*  
 A **Recordset**オブジェクト。 **Recordset**のこのイベントが発生しました。  
  
## <a name="remarks"></a>コメント  
 **EndOfRecordset**場合に、イベントが発生する可能性があります、 [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)操作は失敗します。  
  
 末尾を越えた移動を試行したときに、このイベント ハンドラーが呼び出されます、 **Recordset**呼び出しの結果などのオブジェクト**MoveNext**します。 ただし、このイベント中にデータベースから複数のレコードを取得してそれらの末尾に追加、 **Recordset**します。 この場合は、 *fMoreData* 、VARIANT_TRUE とからの戻り値に**EndOfRecordset**します。 呼び出して**MoveNext**新しく取得したレコードにアクセスするには、もう一度です。  
  
## <a name="see-also"></a>関連項目  
 [ADO イベント モデルの例 (vc++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)
