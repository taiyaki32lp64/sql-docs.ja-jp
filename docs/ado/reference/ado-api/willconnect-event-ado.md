---
title: WillConnect イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillConnect
- Connection::WillConnect
helpviewer_keywords:
- WillConnect event [ADO]
ms.assetid: da561d58-eb58-446c-a4fd-1838c76073c0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9fc1ac74e7e3d521bae587957f5f95771e5a5268
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945857"
---
# <a name="willconnect-event-ado"></a>WillConnect イベント (ADO)
**WillConnect**の接続を開始する前に、イベントが呼び出されます。  
  
 **適用対象します。** [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ConnectionString*  
 A**文字列**保留中の接続の接続情報を格納します。  
  
 *UserID*  
 A**文字列**保留中の接続のユーザー名を格納しています。  
  
 *Password*  
 A**文字列**保留中の接続のパスワードを格納しています。  
  
 *[オプション]*  
 A**長い**プロバイダーを評価する方法を示す値、 *ConnectionString*します。 唯一の選択肢は**adAsyncOpen**します。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状態値。  
  
 このパラメーターに設定されているこのイベントが呼び出されると、 **adStatusOK**既定。 設定されている**adStatusCantDeny**場合は、イベントが保留中の操作のキャンセルを要求できません。  
  
 このイベントから制御が戻る前に、このパラメーターを設定**adStatusUnwantedEvent**後続通知しないように設定します。 このパラメーターに設定**adStatusCancel**この通知の取り消しの原因となった接続操作を要求します。  
  
 *pConnection*  
 [接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトをこのイベント通知が適用されます。 パラメーターへの変更、**接続**によって、 **WillConnect**イベント ハンドラーは効果がありません、**接続**します。  
  
## <a name="remarks"></a>コメント  
 ときに**WillConnect**が呼び出される、 *ConnectionString*、 *UserID*、*パスワード*、および*オプション*パラメーターは、(保留中の接続)、このイベントの原因し、イベントを返します。 前に変更することができる操作によって確立されている値に設定されます。 **WillConnect**保留中の接続をキャンセルする要求を返す可能性があります。  
  
 このイベントが取り消されると、 **ConnectComplete**呼び出しに使用されるその*adStatus*パラメーターに設定**adStatusErrorsOccurred**します。  
  
## <a name="see-also"></a>関連項目  
 [ADO イベント モデルの例 (vc++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)
