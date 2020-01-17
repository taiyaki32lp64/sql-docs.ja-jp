---
title: MoveFirst、MoveLast、MoveNext、MovePrevious メソッド (ADO)、|Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MoveLast
- Recordset15::MoveNext
- Recordset15::raw_MoveNext
- Recordset15::raw_MovePrevious
- Recordset15::MoveFirst
- Recordset15::raw_MoveLast
- Recordset15::MovePrevious
- Recordset15::raw_MoveFirst
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- MovePrevious method [ADO]
ms.assetid: a61a01a7-5b33-4150-9126-21dfa63654cb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5f0cdacc6e0d7e5512dbc259815e5b9562c9b68
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918108"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>MoveFirst、MoveLast、MoveNext、MovePrevious メソッド (ADO)
First、last に移動します。 次に、または前のレコードを、指定した[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトと、そのレコードを現在のレコード。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>コメント  
 使用して、 **MoveFirst**メソッドの最初のレコードを現在のレコードの位置を移動する、 **Recordset**します。  
  
 使用して、 **MoveLast**に最後のレコードの現在の位置に移動する方法を記録、 **Recordset**します。 **Recordset**オブジェクトには、ブックマークまたは旧バージョンとカーソルの動きをサポートする必要があります。 それ以外の場合、メソッドの呼び出しでエラーが発生します。  
  
 いずれかへの呼び出し**MoveFirst**または**MoveLast**ときに、 **Recordset**が空 (両方**BOF**と**EOF**True は、)、エラーが発生します。  
  
 使用して、 **MoveNext**メソッドは、現在のレコードを移動する転送の 1 つのレコードの位置 (の下部に、**レコード セット**)。 最後のレコードが現在のレコードを呼び出す場合、 **MoveNext**メソッド、ADO、現在のレコードを位置設定後の最後のレコード、 **Recordset** ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)は**True**)。 転送時に移動しよう、 **EOF**プロパティが既に**True**エラーが生成されます。  
  
 ADO では 2.5 以降の場合に、**レコード セット**フィルター選択された並べ替えられ、現在のレコードのデータを変更すると、呼び出すことや、 **MoveNext**メソッドは、2 つのカーソルのレコードが現在のレコードから転送を移動します. これは、次のレコードが新しい現在のレコードになる、現在のレコードが変更されたときにためにです。 呼び出す**MoveNext**変更は、新しい現在のレコードからカーソル 1 レコード フォワードを移動した後。 これは、異なる ADO 2.1 で動作し、以前です。 これらの以前のバージョンでは、並べ替えまたはフィルター選択された現在のレコードのデータを変更する**レコード セット**、現在のレコードの位置は変更されず**MoveNext**次のレコードにカーソルを移動します。直後に、現在のレコード。  
  
 使用して、 **MovePrevious**メソッドは、現在のレコードを移動する 1 つのレコードを旧バージョンとの位置 (の上部で、**レコード セット**)。 **Recordset**オブジェクトには、ブックマークまたは旧バージョンとカーソルの動きをサポートする必要があります。 それ以外の場合、メソッドの呼び出しでエラーが発生します。 最初のレコードが現在のレコードを呼び出す場合、 **MovePrevious**メソッド、ADO は最初のレコードの前に、現在のレコードを設定、 **Recordset** ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)は**True**)。 旧バージョンとのときに移動しよう、 **BOF**プロパティが既に**True**エラーが生成されます。 場合、 **Recordset**オブジェクトはブックマークまたは旧バージョンとカーソルの動きをサポートしていません、 **MovePrevious**メソッドには、エラーが発生します。  
  
 場合、 **Recordset**前方参照専用、前方と後方スクロールをサポートする、使用することができます、 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)旧バージョンとカーソルの動きをサポートするレコードのキャッシュを作成するプロパティを通じて、[移動](../../../ado/reference/ado-api/move-method-ado.md)メソッド。 キャッシュ レコードはメモリに読み込まれる、ために、必要以上のレコードをキャッシュを避ける必要があります。 呼び出すことができます、 **MoveFirst**順方向専用のメソッド**Recordset**オブジェクトは、プロバイダーを再生成するコマンドを実行する場合がありますが、 **Recordset**オブジェクト.  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [MoveFirst、MoveLast、MoveNext、MovePrevious メソッドの例 (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [MoveFirst、MoveLast、MoveNext、MovePrevious メソッドの例 (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst、MoveLast、MoveNext、MovePrevious メソッドの例 (vc++)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Move メソッド (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst、MoveLast、MoveNext、MovePrevious メソッド (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord メソッド (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
