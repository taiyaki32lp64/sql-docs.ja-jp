---
title: GetChunk メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::raw_GetChunk
- Field20::GetChunk
helpviewer_keywords:
- GetChunk method [ADO]
ms.assetid: fc268e22-205b-44a3-9038-ffed51e23e10
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43c5fef08d22364b9842c58fc82d46ba4bfa00bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918560"
---
# <a name="getchunk-method-ado"></a>GetChunk メソッド (ADO)
大きなテキストまたはバイナリ データの内容の一部、または返します[フィールド](../../../ado/reference/ado-api/field-object.md)オブジェクト。  
  
## <a name="syntax"></a>構文  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>戻り値  
 返します、**バリアント**します。  
  
#### <a name="parameters"></a>パラメーター  
 *Size*  
 A**長い**バイト数または取得する文字数と同じである式。  
  
## <a name="remarks"></a>コメント  
 使用して、 **GetChunk**メソッドを**フィールド**その時間の長いバイナリまたは文字データの一部またはすべてを取得するオブジェクト。 システム メモリが限られている状況で使用することができます、 **GetChunk**全体ではなく、特定の部分で長い値を操作するメソッド。  
  
 データを**GetChunk**に割り当てられている呼び出しが戻る*変数*します。 場合*サイズ*が残りのデータよりも大きい、 **GetChunk**パディングなしの残りのデータのみを返します*変数*空のスペース。 フィールドが空の場合、 **GetChunk**メソッドは、null 値を返します。  
  
 後に続く各**GetChunk**呼び出し場所からデータを取得する前**GetChunk**呼び出しが中断します。 ただしから 1 つのフィールドと設定または現在のレコードの別のフィールドの値を読み取り、データを取得する ADO は最初のフィールドからのデータの取得が完了したらを想定します。 呼び出す場合、 **GetChunk**最初のフィールド、ADO メソッドは、新しい呼び出しを解釈**GetChunk**操作し、データの先頭から読み取りを開始します。 他のフィールドへのアクセス[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)最初のクローンではないオブジェクトを**Recordset**オブジェクトを妨害しない**GetChunk**操作。  
  
 場合、 **adFldLong**ビット、[属性](../../../ado/reference/ado-api/attributes-property-ado.md)のプロパティを**フィールド**にオブジェクトが設定されている**True**、使用することができます、 **GetChunk**そのフィールドのメソッド。  
  
 使用すると、現在のレコードがない場合、 **GetChunk**メソッドを**フィールド**オブジェクト、3021 (現在のレコードがありません) エラーが発生します。  
  
> [!NOTE]
>  **GetChunk**についてメソッドは動作しません**フィールド**のオブジェクトを[レコード](../../../ado/reference/ado-api/record-object-ado.md)オブジェクト。 操作は実行しないと、実行時エラーが生成されます。  
  
## <a name="applies-to"></a>適用対象  
 [Field オブジェクト](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>関連項目  
 [AppendChunk および GetChunk メソッドの例 (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk および GetChunk メソッドの例 (vc++)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [AppendChunk メソッド (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Attributes プロパティ (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
