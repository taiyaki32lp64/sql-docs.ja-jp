---
title: Cancel メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::Cancel
- _Record::Cancel
- _Connection::Cancel
- Command25::Cancel
- _Stream::Cancel
helpviewer_keywords:
- Cancel method [ADO]
ms.assetid: e0db4e15-6787-41e2-8f13-9e9b524d620a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db369b32737c0e2dae4603a4a5a6c26cdd3a7142
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920239"
---
# <a name="cancel-method-ado"></a>Cancel メソッド (ADO)
保留中の非同期メソッド呼び出しの実行をキャンセルします。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.Cancel  
```  
  
## <a name="remarks"></a>コメント  
 使用して、**キャンセル**非同期メソッド呼び出しの実行を終了するメソッド: には、メソッドが呼び出された、 **adAsyncConnect**、 **adAsyncExecute**、または**adAsyncFetch**オプション。  
  
 次の表を使用する場合は、どのようなタスクが終了した、**キャンセル**メソッドはオブジェクトの特定の種類。  
  
|場合*オブジェクト*が、|このメソッドの最後の非同期呼び出しが終了しました|  
|----------------------|-------------------------------------------------------------|  
|[Command](../../../ado/reference/ado-api/command-object-ado.md)|[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[Connection](../../../ado/reference/ado-api/connection-object-ado.md)|[実行](../../../ado/reference/ado-api/execute-method-ado-connection.md)または[開く](../../../ado/reference/ado-api/open-method-ado-connection.md)|  
|[レコード](../../../ado/reference/ado-api/record-object-ado.md)|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)、 [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)、 [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)、または[開く](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)|[[ファイル]](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[ストリーム](../../../ado/reference/ado-api/stream-object-ado.md)|[[ファイル]](../../../ado/reference/ado-api/open-method-ado-stream.md)|  
  
## <a name="applies-to"></a>適用対象  
  
||||  
|-|-|-|  
|[Command オブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>関連項目  
 [Cancel メソッドの例 (VB)](../../../ado/reference/ado-api/cancel-method-example-vb.md)   
 [Cancel メソッドの例 (VBScript)](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [Cancel メソッドの例 (vc++)](../../../ado/reference/ado-api/cancel-method-example-vc.md)   
 [Cancel メソッド (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch メソッド (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate メソッド (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate メソッド (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Execute メソッド (ADO Command)](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Execute メソッド (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Open メソッド (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)
