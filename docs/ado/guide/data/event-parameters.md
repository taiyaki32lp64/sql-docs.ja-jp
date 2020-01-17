---
title: イベント パラメーター |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Error parameter [ADO]
- Object parameter [ADO]
- Status parameter [ADO]
- events [ADO], parameters
- Reason parameter [ADO]
- event parameters [ADO]
ms.assetid: bd5c5afa-d301-4899-acda-40f98a6afa4d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 26caf2b54b4f0affbbe7cdc58fa2bf742f0d4101
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925367"
---
# <a name="event-parameters"></a>イベント パラメーター
すべてのイベント ハンドラーでは、イベント ハンドラーを制御する状態パラメーターがあります。 完全なイベントは、このパラメーターもイベントを生成する操作の成否を示すために使用されます。 最も包括的なイベントは、エラーが発生した場合をし、操作を実行するために使用する ADO オブジェクトを参照する 1 つまたは複数のオブジェクトのパラメーターに関する情報を提供するエラー パラメーターを指定します。 たとえば、 [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)イベントにはオブジェクトのパラメーターが含まれています、**コマンド**、**レコード セット**、および**接続**オブジェクトイベントに関連付けられています。 Microsoft® Visual Basic® の次の例では、pCommand、pRecordset、および表す pConnection オブジェクトを参照できます、**コマンド**、 **Recordset**、および**の接続**オブジェクトによって使用される、 **Execute**メソッド。  
  
```  
Private Sub connEvent_ExecuteComplete(ByVal RecordsAffected As Long, _  
     ByVal pError As ADODB.Error, _  
     adStatus As ADODB.EventStatusEnum, _  
     ByVal pCommand As ADODB.Command, _  
     ByVal pRecordset As ADODB.Recordset, _  
     ByVal pConnection As ADODB.Connection)  
```  
  
 を除き、**エラー**オブジェクトはイベントに同じパラメーターが渡されます。 それぞれの保留中の操作で使用され、操作が完了できるかどうかを決定するオブジェクトを確認するこのことができます。  
  
 いくつかのイベント ハンドラーが、*理由*イベントが発生した理由に関する追加情報を提供するパラメーター。 たとえば、 **WillMove**と**MoveComplete**ナビゲーション方法のいずれかによりイベントを発生させる (**MoveNext**、 **MovePrevious**など) が呼び出されるか、クエリの結果として。  
  
## <a name="status-parameter"></a>状態パラメーター  
 イベント ハンドラー ルーチンが呼び出されたときに、*状態*パラメーターは、次の値のいずれかに設定します。  
  
|値|説明|  
|-----------|-----------------|  
|**adStatusOK**|完了イベントの両方に渡されます。 この値は、正常に完了イベントを原因となった操作を意味します。|  
|**adStatusErrorsOccurred**|完全なイベントのみに渡されます。 この値は、イベントの原因となった操作が成功すると、かはイベントには、操作がキャンセルされたことを意味します。 チェック、*エラー*パラメーターの詳細。|  
|**adStatusCantDeny**|イベントのみに渡されます。 この値はイベントによって、操作をキャンセルすることはできないことを意味します。 実行する必要があります。|  
  
 操作を続行する必要がありますがイベントで判断した場合、以下のままにして、*状態*パラメーター。 受信状態のパラメーターに設定されませんでした限り**adStatusCantDeny**、変更することで保留中の操作をキャンセルできます*状態*に**adStatusCancel**します。 操作に関連付けられている完全なイベントには、これを行うときにその*状態*パラメーターに設定**adStatusErrorsOccurred**します。 **エラー**完了イベントに渡されるオブジェクトの値を含む**adErrOperationCancelled**します。  
  
 不要になったイベントを処理する場合は、設定*状態*に**adStatusUnwantedEvent**アプリケーションでは、そのイベントの通知を受け取る不要になったとします。 ただし、1 つ以上の理由で一部のイベントが発生することに注意してください。 その場合は、指定する必要があります**adStatusUnwantedEvent**の考えられる各理由。 たとえば、保留中の通知の受信を停止する**RecordChange** 、イベントを設定する必要がある、*状態*パラメーターを**adStatusUnwantedEvent**の**adRsnAddNew**、 **adRsnDelete**、 **adRsnUpdate**、 **adRsnUndoUpdate**、 **adRsnUndoAddNew**、**adRsnUndoDelete**、および**adRsnFirstChange**発生するとします。  
  
|値|説明|  
|-----------|-----------------|  
|**adStatusUnwantedEvent**|このイベント ハンドラーがさらに通知を受信しないことを要求します。|  
|**adStatusCancel**|実行される操作のキャンセルを要求します。|  
  
## <a name="error-parameter"></a>エラー パラメーター  
 *エラー*パラメーターは、ADO への参照を[エラー](../../../ado/reference/ado-api/error-object.md)オブジェクト。 ときに、*状態*にパラメーターが設定されている**adStatusErrorsOccurred**、**エラー**オブジェクトには、操作が失敗した理由の詳細が含まれています。 完了イベントに関連付けられているはイベントが設定して、操作をキャンセルされた場合、*状態*パラメーターを**adStatusCancel**、エラー オブジェクトは常に設定**adErrOperationCancelled**します。  
  
## <a name="object-parameter"></a>オブジェクトのパラメーター  
 各イベントは、操作に関連するオブジェクトを表す 1 つまたは複数のオブジェクトを受け取ります。 など、 **ExecuteComplete**イベントを受信、**コマンド**オブジェクト、**レコード セット**オブジェクト、および**接続**オブジェクト。  
  
## <a name="reason-parameter"></a>Reason パラメータ  
 *理由*パラメーター、 *adReason*イベントが発生した理由に関する追加情報を提供します。 イベントを*adReason*パラメーターは、毎回のさまざまな理由のため、同じ操作の場合でもを複数回呼び出すことができます。 たとえば、 **WillChangeRecord**またはしないで、挿入、削除、またはレコードの変更を元に戻すには操作のイベント ハンドラーが呼び出されます。 使用することが何らかの理由で発生したときにのみイベントを処理する場合、 *adReason*パラメーターが必要ない出現回数を除外します。 たとえば、レコードが追加された理由で発生した場合にのみ、レコードの変更イベントを処理したい場合は、次のようを使用できます。  
  
```  
' BeginEventExampleVB01  
Private Sub rsTest_WillChangeRecord(ByVal adReason As ADODB.EventReasonEnum, ByVal cRecords As Long, adStatus As ADODB.EventStatusEnum, ByVal pRecordset As ADODB.Recordset)  
   If adReason = adRsnAddNew Then  
       ' Process event  
       '...  
   Else  
       ' Cancel event notification for all  
       ' other possible adReason values.  
       adStatus = adStatusUnwantedEvent  
   End If  
End Sub  
' EndEventExampleVB01  
```  
  
 この場合、通知可能性のあるその他の理由の各発生します。 ただし、これは 1 回だけ動機ごと。 通知が各理由の 1 回発生した後、新しいレコードを追加するためだけの通知が届きます。  
  
 設定する必要がこれに対し、 *adStatus*に**adStatusUnwantedEvent**を要求に 1 回だけことがなく、イベント ハンドラー、 **adReason**パラメーター停止の受信イベント通知します。  
  
## <a name="see-also"></a>関連項目  
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [言語で ADO イベントのインスタンス化](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [イベント ハンドラーの連携](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [イベントの種類](../../../ado/guide/data/types-of-events.md)
