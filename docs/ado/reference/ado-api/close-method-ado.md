---
title: Close メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Close
- _Stream::Close
- _Record::Close
helpviewer_keywords:
- Close method [ADO]
ms.assetid: 3cdf27d1-a180-4cff-8e42-95dec5fb1b55
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8a1d153d1433a377bb488366111b75a986365132
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919932"
---
# <a name="close-method-ado"></a>Close メソッド (ADO)
開いているオブジェクトとすべての依存オブジェクトを閉じます。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>コメント  
 使用して、**閉じます**を終了するメソッド、[接続](../../../ado/reference/ado-api/connection-object-ado.md)、[レコード](../../../ado/reference/ado-api/record-object-ado.md)、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)、または[Stream](../../../ado/reference/ado-api/stream-object-ado.md)オブジェクト関連付けられたシステム リソースを解放します。 オブジェクトを閉じるは削除されません。 メモリからそのプロパティの設定を変更でき、後でもう一度開きます。 メモリからオブジェクトを完全になくすためには、オブジェクトを閉じて、オブジェクト変数を設定し、 *Nothing* (Visual Basic) でします。  
  
## <a name="connection"></a>接続  
 使用して、**閉じます**を終了するメソッド、**接続**オブジェクトでは、アクティブなも閉じられます**レコード セット**接続に関連付けられているオブジェクト。 A[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクトに関連付けられている、**接続**閉じようとしているオブジェクトが保持されますが、そのとは関連付けられなくなった、**接続**オブジェクト、つまりその[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)プロパティに設定する**Nothing**します。 また、**コマンド**オブジェクトの[パラメーター](../../../ado/reference/ado-api/parameters-collection-ado.md)任意のプロバイダー定義パラメーターのコレクションはクリアされます。  
  
 後で呼び出すことができます、[オープン](../../../ado/reference/ado-api/open-method-ado-connection.md)メソッドを同じまたは別のデータ ソースへの接続を再確立します。 中に、**接続**オブジェクトが閉じられた、データ ソースへの開いた接続を必要とするメソッドを呼び出すと、エラーが発生します。  
  
 閉じる、**接続**オブジェクトがある、開いている間**レコード セット**接続上のオブジェクト内のロールバック保留中の変更のすべて、**レコード セット**オブジェクト。 明示的に閉じられて、**接続**オブジェクト (呼び出し、**閉じる**メソッド)、トランザクションの中の進行状況、エラーが発生します。 場合、**接続**トランザクションの進行状況の中に、オブジェクトがスコープ外が、ADO に自動的にトランザクションをロールバックします。  
  
## <a name="recordset-record-stream"></a>レコード セット、レコード、Stream  
 使用して、**閉じます**を終了するメソッド、 **Recordset**、**レコード**、または**Stream**オブジェクトが関連付けられているデータと任意の排他アクセスを解放この特定のオブジェクトを使用してデータを必要があるがある可能性があります。 後で呼び出すことができます、[オープン](../../../ado/reference/ado-api/open-method-ado-recordset.md)同じ、または変更、オブジェクトを再度開くメソッドの属性します。  
  
 中に、 **Recordset**オブジェクトが閉じられて、ライブのカーソルを必要とするメソッドを呼び出すと、エラーが発生します。  
  
 編集が即時更新モードで実行中の場合は、呼び出し、**閉じる**メソッドはエラーを生成しますが、代わりに、[更新](../../../ado/reference/ado-api/update-method.md)または[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)メソッド最初。 閉じた場合、 **Recordset**バッチ更新モード、最後のすべての変更中にオブジェクト[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)呼び出しは失われます。  
  
 使用する場合、[複製](../../../ado/reference/ado-api/clone-method-ado.md)、オープンのコピーを作成するメソッドを**レコード セット**オブジェクト、元のまたは複製を閉じるには影響しません、他のコピーのいずれか。  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>関連項目  
 [Open および Close メソッドの例 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open および Close メソッドの例 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open および Close メソッドの例 (vc++)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open メソッド (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Save メソッド](../../../ado/reference/ado-api/save-method.md)
