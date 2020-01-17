---
title: BeginTrans、CommitTrans、RollbackTrans イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CommitTransComplete
- Connection::BeginTransComplete
- Connection::RollbackTransComplete
- Connection::CommitTransComplete
- RollbackTransComplete
- BeginTransComplete
helpviewer_keywords:
- CommitTransComplete event [ADO]
- RollbackTransComplete event [ADO]
- BeginTransComplete event [ADO]
ms.assetid: ec4e4b38-e9c6-4757-b2ef-4e468ae5f1d8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 750e89e97eb916c7db23e71475b753a57a4d90e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920444"
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>BeginTransComplete、CommitTransComplete、および RollbackTransComplete イベント (ADO)
これらのイベントが関連付けられている操作の後に呼び出される、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトの実行が終了します。  
  
-   **BeginTransComplete**が呼び出された後、 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)操作。  
  
-   **CommitTransComplete**が呼び出された後、 [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)操作。  
  
-   **RollbackTransComplete**が呼び出された後、 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)操作。  
  
## <a name="syntax"></a>構文  
  
```  
  
BeginTransComplete TransactionLevel, pError, adStatus, pConnection  
CommitTransComplete pError, adStatus, pConnection  
RollbackTransComplete pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>パラメーター  
 *TransactionLevel*  
 A**長い**新しいトランザクションのレベルを含む値、 **BeginTrans**このイベントの原因となった。  
  
 *pError*  
 [エラー](../../../ado/reference/ado-api/error-object.md)オブジェクト。 EventStatusEnum の値がある場合に発生したエラーについて説明します**adStatusErrorsOccurred**。 それ以外の場合に設定されていません。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状態値。 このパラメーターに設定されているこれらのイベントのいずれかが呼び出されると**adStatusOK**イベントの原因となった操作が成功した場合または**adStatusErrorsOccurred**操作に失敗した場合。  
  
 これらのイベントは、後続の通知を防ぐためこのパラメーターを設定して**adStatusUnwantedEvent**前に、イベントを返します。  
  
 *pConnection*  
 **接続**オブジェクトをこのイベントが発生しました。  
  
## <a name="remarks"></a>コメント  
 Visual C で複数**接続**同じイベント処理メソッドを共有することができます。 メソッドを使用して、返された**接続**オブジェクト イベントの原因を判断するオブジェクト。  
  
 場合、[属性](../../../ado/reference/ado-api/attributes-property-ado.md)プロパティに設定されて**adXactCommitRetaining**または**adXactAbortRetaining**、コミットやトランザクションをロールバックした後、新しいトランザクションを開始します。 使用して、 **BeginTransComplete**すべて無視するイベントが最初のトランザクションの開始イベント。  
  
## <a name="see-also"></a>関連項目  
 [ADO イベント モデルの例 (vc++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [BeginTrans、CommitTrans、および RollbackTrans メソッドの例 (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [BeginTrans、CommitTrans、および RollbackTrans メソッド (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)
