---
title: Move メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Move
- Recordset15::raw_Move
helpviewer_keywords:
- Move method [ADO]
ms.assetid: 13fe9381-d00b-4f4a-9162-83c3f21b3837
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d76f239094185af7a3e940201b3f99132c0194a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918193"
---
# <a name="move-method-ado"></a>Move メソッド (ADO)
現在のレコードの位置を移動、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>パラメーター  
 *NumRecords*  
 符号付き**長い**レコードの現在の位置を移動するレコードの数を指定する式。  
  
 *[開始]*  
 任意。 A**文字列**値または**バリアント**ブックマークに評価されます。 使用することも、 [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)値。  
  
## <a name="remarks"></a>コメント  
 **移動**メソッドがすべてでサポートされている**Recordset**オブジェクト。  
  
 場合、 *NumRecords*引数に 0 を超えると、現在のレコードの位置を前方に移動 (の終了に向けて、 **Recordset**)。 場合*NumRecords* 0、現在のレコードの位置は後方に移動します未満です (の先頭に向かって、 **Recordset**)。  
  
 場合、**移動**呼び出しは、最初のレコードの前に、のポイントに現在のレコードの位置を移動、ADO レコード セット内の最初のレコードの前に位置する現在のレコードを設定する ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)は**は True。** ). 旧バージョンとのときに移動しよう、 **BOF**プロパティが既に**True**エラーが生成されます。  
  
 場合、**移動**呼び出しは最後のレコードの後のポイントに現在のレコードの位置を移動すると、ADO レコード セットの最後のレコードの後に、現在のレコードを位置に設定する ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)は**は True。** ). 転送時に移動しよう、 **EOF**プロパティが既に**True**エラーが生成されます。  
  
 呼び出す、**移動**メソッド空から**レコード セット**オブジェクト、エラーが発生します。  
  
 渡す場合、*開始*レコード、このブックマークを基準とした引数では、この移動と仮定すると、**レコード セット**オブジェクトは、ブックマークをサポートしています。 指定しない場合、この移動は現在のレコードを基準とは。  
  
 使用する場合、 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)渡す、プロバイダーからのレコードをローカルにキャッシュするプロパティを*NumRecords*引数キャッシュされたレコードの現在のグループの外側、現在のレコードの位置を移動します。強制的に目的のレコードからレコードの新しいグループを取得します。 **CacheSize**プロパティは、新たに取得したグループのサイズを決定し、目的のレコードが最初のレコードを取得します。  
  
 場合、 **Recordset**オブジェクトは順方向専用、ユーザーが受け渡すことができます、 *NumRecords* 0 より小さい引数がキャッシュされているレコードの現在のセット内に、変換先を提供します。 場合、**移動**呼び出しは、現在のレコードの位置に移動、最初のキャッシュされたレコードより前に、のレコード、エラーが発生します。 したがって、前方スクロールのみをサポートするプロバイダーには、完全なスクロールをサポートしているレコードのキャッシュを使用できます。 キャッシュ レコードはメモリに読み込まれる、ため、多くのレコードが必要以上のキャッシュを避ける必要があります。 順方向専用の場合でも**レコード セット**呼び出すオブジェクトでサポートされる旧バージョンとは、この方法で移動、 [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)メソッドいずれかを順方向専用**レコード セット**オブジェクトがあります。エラーを生成します。  
  
> [!NOTE]
>  順方向専用で後方に移動するためのサポート**Recordset**はプロバイダーによっては、予測できません。 現在のレコードは、後の最後のレコードに位置付けられている場合、**レコード セット**、**移動**内を後方に向かってされないことがある現在の正しい位置にします。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Move メソッドの例 (VB)](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [Move メソッドの例 (VBScript)](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [Move メソッドの例 (vc++)](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [MoveFirst、MoveLast、MoveNext、MovePrevious メソッド (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst、MoveLast、MoveNext、MovePrevious メソッド (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord メソッド (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
