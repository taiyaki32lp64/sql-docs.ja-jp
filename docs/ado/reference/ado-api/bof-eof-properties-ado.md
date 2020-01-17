---
title: BOF、EOF プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::BOF
- Recordset15::EOF
helpviewer_keywords:
- EOF property [ADO]
- BOF property [ADO]
ms.assetid: 36c31ab2-f3b6-4281-89b6-db7e04e38fd2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4932d3349c2d4e2948ddd28d9df3a30424064dcb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920388"
---
# <a name="bof-eof-properties-ado"></a>BOF、EOF プロパティ (ADO)
-   **BOF**の最初のレコードの前に、現在のレコードの位置があることを示します、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。  
  
-   **EOF**の最後のレコードの後、現在のレコードの位置にあることを示します、 **Recordset**オブジェクト。  
  
## <a name="return-value"></a>戻り値  
 **BOF**と**EOF**プロパティの戻り値**ブール**値。  
  
## <a name="remarks"></a>コメント  
 使用、 **BOF**と**EOF**プロパティを確認するかどうかを**レコード セット**レコードまたはかどうかが確認済みの制限を超えるオブジェクトが含まれています、**レコード セット**レコード間を移動するときのオブジェクトします。  
  
 **BOF**プロパティが返す**True** (-1) 場合、現在のレコードの位置を先頭レコードの前に、と**False**レコードの現在の位置は 1 つ目以降の場合は (0)レコードです。  
  
 **EOF**プロパティが返す**True**レコードの現在の位置が最後のレコード後がある場合と**False**レコードの現在の位置がまたは最後のレコードの前にある場合。  
  
 どちらの場合、 **BOF**または**EOF**プロパティは**True**、現在のレコードはありません。  
  
 開く場合、**レコード セット**オブジェクト、レコードが含まれていない、 **BOF**と**EOF**プロパティに設定されます**True** (を参照してください、 [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)プロパティのこの状態の詳細については、 **Recordset**)。 開くと、**レコード セット**に少なくとも 1 つのレコード、最初のレコードを格納しているオブジェクトが現在のレコードと**BOF**と**EOF**プロパティは、 **False**.  
  
 最後の残りのレコードを削除する場合、**レコード セット**オブジェクト、 **BOF**と**EOF**プロパティが残る可能性がある**False**まで現在のレコードの位置を変更しようとしてください。  
  
 次の表では**移動**のさまざまな組み合わせで使用できるメソッド、 **BOF**と**EOF**プロパティ。  
  
||MoveFirst、<br /><br /> MoveLast|MovePrevious、<br /><br /> < 0 を移動します。|0 を移動します。|MoveNext、<br /><br /> > 0 を移動します。|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**BOF**=**True**、 **EOF**=**False**|Allowed|Error|Error|Allowed|  
|**BOF**=**False**、 **EOF**=**は True。**|Allowed|Allowed|Error|Error|  
|両方**は True。**|Error|Error|Error|Error|  
|どちらも**False**|Allowed|Allowed|Allowed|Allowed|  
  
 許可、**移動**メソッドでは、メソッドが正常にレコードを見つけるは保証されません。 その呼び出し、指定したに過ぎません**移動**メソッドでは、エラーは生成されません。  
  
 次の表は、事象、 **BOF**と**EOF**さまざまな呼び出すときに、プロパティの設定**移動**メソッド、ことはできませんが正常にレコードを検索します。  
  
||BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**、 **MoveLast**|設定**は True。**|設定**は True。**|  
|**移動**0|変更なし|変更なし|  
|**MovePrevious**、**移動**< 0|設定**は True。**|変更なし|  
|**MoveNext**、**移動**> 0|変更なし|設定**は True。**|  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [BOF、EOF、および Bookmark プロパティの例 (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF、EOF、および Bookmark プロパティの例 (vc++)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
