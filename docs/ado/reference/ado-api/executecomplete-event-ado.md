---
title: ExecuteComplete イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- ExecuteComplete event [ADO]
ms.assetid: 62470d42-e511-494c-bec4-ad4591734b7b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 62b78b608526ae0d6943a7416a21687fd1e51412
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918782"
---
# <a name="executecomplete-event-ado"></a>ExecuteComplete イベント (ADO)
**ExecuteComplete**イベントは、コマンドの実行が完了した後に呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
ExecuteComplete RecordsAffected, pError, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>パラメーター  
 *RecordsAffected*  
 A**長い**コマンドによって影響を受けたレコード数を示す値。  
  
 *pError*  
 [エラー](../../../ado/reference/ado-api/error-object.md)オブジェクト。 場合に発生したエラーを説明の値**adStatus**は**adStatusErrorsOccurred**; 未設定がそれ以外の場合。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状態値。 このパラメーターに設定されているこのイベントが呼び出されると、 **adStatusOK**イベントの原因となった操作が成功した場合または**adStatusErrorsOccurred**操作に失敗した場合。  
  
 このイベントから制御が戻る前に、このパラメーターを設定**adStatusUnwantedEvent**後続通知しないように設定します。  
  
 *pCommand*  
 [コマンド](../../../ado/reference/ado-api/command-object-ado.md)が実行されたオブジェクト。 含まれています、**コマンド**オブジェクトの呼び出し時にも**Connection.Execute**または**Recordset.Open**明示的に作成せず、**コマンド**、どのような場合、**コマンド**オブジェクトは ADO によって内部的に作成します。  
  
 *pRecordset*  
 A [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)実行されたコマンドの結果を表すオブジェクト。 これは、 **Recordset**空にすることがあります。 このイベント ハンドラー内からこのレコード セット オブジェクトは破棄しないでください。 ADO が、存在しなくなったオブジェクトにアクセスしようとしています。 これがアクセス違反に発生します。  
  
 *pConnection*  
 A[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。 操作の実行を接続します。  
  
## <a name="remarks"></a>コメント  
 **ExecuteComplete**ためにイベントが発生する、**接続**。[実行](../../../ado/reference/ado-api/execute-method-ado-connection.md)、**コマンド**。[実行](../../../ado/reference/ado-api/execute-method-ado-command.md)、**レコード セット**。[オープン](../../../ado/reference/ado-api/open-method-ado-recordset.md)、**レコード セット**。[Requery](../../../ado/reference/ado-api/requery-method.md)、または**レコード セット**。[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)メソッド。  
  
## <a name="see-also"></a>関連項目  
 [ADO イベント モデルの例 (vc++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)
