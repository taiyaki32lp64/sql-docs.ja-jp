---
title: Bookmark プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Bookmark
helpviewer_keywords:
- Bookmark property [ADO]
ms.assetid: 481dcc93-487b-490e-ac58-a1e9b2ebfd43
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 48b1c90b59b220841aa45f618fdfda5ff2db82da
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920346"
---
# <a name="bookmark-property-ado"></a>Bookmark プロパティ (ADO)
ブックマークの現在のレコードを一意に識別することを示します、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトまたは現在のレコードを設定、**レコード セット**オブジェクトを有効なブックマークで識別されるレコード。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**バリアント**有効なブックマークに評価される式。  
  
## <a name="remarks"></a>コメント  
 使用して、**ブックマーク**プロパティを現在のレコードの位置を保存し、いつでも、そのレコードに戻ります。 のみ使用できます、ブックマークは**Recordset**ブックマーク機能をサポートするオブジェクト。  
  
 開くと、 **Recordset**オブジェクトの一意のブックマークが各レコード。 現在のレコードのブックマークを保存するには、値を割り当てる、**ブックマーク**変数するプロパティ。 別のレコードに移動した後、いつでもそのレコードにすばやく戻る、設定、**レコード セット**オブジェクトの**ブックマーク**プロパティをその変数の値にします。  
  
 ユーザーはできない、ブックマークの値を表示することがあります。 また、ユーザーは、同じレコードを参照する 2 つのブックマークの値が異なる可能性があるために、直接比較するブックマークは期待できません。  
  
 使用する場合、[複製](../../../ado/reference/ado-api/clone-method-ado.md)のコピーを作成する方法、**レコード セット**オブジェクト、**ブックマーク**プロパティの設定元と、重複**レコード セット**オブジェクトが同一で、これらを置き換えて使用することができます。 ただし、さまざまなブックマークを使用することはできません**Recordset**は同じソースまたはコマンドから作成された場合でも、同じ意味では、オブジェクトします。  
  
> [!NOTE]
>  **リモート データ サービスの使用状況**クライアント側で使用すると**レコード セット**オブジェクト、**ブックマーク**プロパティは、常に使用します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [BOF、EOF、および Bookmark プロパティの例 (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF、EOF、および Bookmark プロパティの例 (vc++)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Supports メソッド](../../../ado/reference/ado-api/supports-method.md)
