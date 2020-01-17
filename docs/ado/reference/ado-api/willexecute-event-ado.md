---
title: WillExecute イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillExecute
- Connection::WillExecute
helpviewer_keywords:
- WillExecute event [ADO]
ms.assetid: dd755e46-f589-48a3-93a9-51ff998d44b5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0e7c29be102e9c5c7709816895a6647c95337c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936614"
---
# <a name="willexecute-event-ado"></a>WillExecute イベント (ADO)
**WillExecute**接続で保留中のコマンドを実行する前に、イベントが呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ソース*  
 A**文字列**SQL コマンドまたはストアド プロシージャ名を格納しています。  
  
 *CursorType*  
 A [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)のカーソルの種類を格納している、 **Recordset**は開かれます。 このパラメーターを使用中に任意の型にカーソルを変更することができます、 **Recordset**[Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)操作。 *CursorType*の他の操作は無視されます。  
  
 *LockType*  
 A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)のロックの種類を格納している、 **Recordset**は開かれます。 このパラメーターを使用中に任意の型をロックを変更することができます、 **RecordsetOpen**操作。 *LockType*の他の操作は無視されます。  
  
 *[オプション]*  
 A**長い**コマンドを実行したり、開いたりに使用できるオプションを示す値、 **Recordset**します。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)可能性のある状態値**adStatusCantDeny**または**adStatusOK**このイベントが呼び出された場合。 場合は**adStatusCantDeny**、このイベントは、保留中の操作のキャンセルを要求しない場合があります。  
  
 *pCommand*  
 [コマンド オブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)オブジェクトをこのイベント通知が適用されます。  
  
 *pRecordset*  
 [レコード セット オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトをこのイベント通知が適用されます。  
  
 *pConnection*  
 [接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトをこのイベント通知が適用されます。  
  
## <a name="remarks"></a>コメント  
 A **WillExecute**接続によるイベントが発生します。  [Execute メソッド (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)、 [Execute メソッド (ADO Command)](../../../ado/reference/ado-api/execute-method-ado-command.md)、または[Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)メソッド、 *pConnection*パラメーターにする必要があります常に有効な参照を含める、**接続**オブジェクト。 イベントが原因である場合**Connection.Execute**、 *pRecordset*と*pCommand*パラメーターに設定されて**Nothing**します。 イベントが原因である場合**Recordset.Open**、 *pRecordset*パラメーターで参照、 **Recordset**オブジェクトと*pCommand*パラメーターを設定する**Nothing**します。 イベントが原因である場合**Command.Execute**、 *pCommand*パラメーターで参照、**コマンド**オブジェクトと*pRecordset*パラメーターを設定する**Nothing**します。  
  
 **WillExecute**確認し、保留中の実行のパラメーターを変更することができます。 このイベントは、保留中のコマンドをキャンセルする要求を返す可能性があります。  
  
> [!NOTE]
>  元のソースの場合、**コマンド**によって指定されたストリームは、 [CommandStream プロパティ (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)プロパティを新しい文字列を割り当てる、 **WillExecute** _ソース_パラメーターのソースの変更、**コマンド**します。 **CommandStream**プロパティがクリアして、 [CommandText プロパティ (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)プロパティは、新しいソースで更新されます。 指定された元のストリーム**CommandStream**がリリースされ、アクセスできません。  
  
 新しいソース文字列の言語が、元の設定と異なるかどうか、 [Dialect プロパティ](../../../ado/reference/ado-api/dialect-property.md)プロパティ (これに対応する、 **CommandStream**)、適切な言語を設定して指定する必要があります**言語**プロパティによって参照されるコマンド オブジェクトの*pCommand*します。  
  
## <a name="see-also"></a>関連項目  
 [ADO イベント モデルの例 (vc++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
