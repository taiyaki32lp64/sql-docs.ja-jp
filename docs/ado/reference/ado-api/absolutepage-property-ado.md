---
title: AbsolutePage プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePage
helpviewer_keywords:
- AbsolutePage property [ADO]
ms.assetid: ddb58a35-ec3a-423c-a504-3c65e62c23d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 12b2e6c6f12fc06cb223551b55cb7f9a38df9ac3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921832"
---
# <a name="absolutepage-property-ado"></a>AbsolutePage プロパティ (ADO)
現在のレコードがどのページが存在することを示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 32 ビット コードでは、設定または取得を**長い**1 からのページ数の値、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト ([PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)) のいずれかを返しますまたは、 [PositionEnum](../../../ado/reference/ado-api/positionenum.md)値。  
  
 64 ビット コードでは、64 ビット値のストレージを提供するデータ型を使用します。 いずれかを使用するなど、**長い**または別の値は 64 ビット長 DBORDINAL などを使用できます。 使用しない**PositionEnum**値は 32 ビットの長さに制限されるためです。  
  
## <a name="remarks"></a>コメント  
 このプロパティは、現在のレコードが配置されているページ番号を識別するために使用できます。 使用して、 [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)の行セットの合計数を論理的に分割するプロパティ、**レコード セット**オブジェクトを一連のページで、それぞれに等しいレコードの数を持つ**PageSize**(を除く、最後のページ、レコードを減らすことがある)。 プロバイダーは、このプロパティを使用するための適切な機能をサポートする必要があります。  
  
-   取得または設定するときに、 **AbsolutePage**プロパティ、ADO は、 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)プロパティおよび[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)として次のようにグループ化のプロパティ。  
  
-   取得する、 **AbsolutePage**、ADO をまず取得、 **AbsolutePosition**、を除算し、 **PageSize**します。  
  
-   設定する、 **AbsolutePage**、ADO の移動、 **AbsolutePosition**次のように:、乗算、 **PageSize**新しい**AbsolutePage**値し、値に 1 を加算します。 その結果、内の現在位置、**レコード セット**正常に設定した後**AbsolutePage**はそのページの最初のレコード。  
  
 ように、 **AbsolutePosition**プロパティ、 **AbsolutePage**は 1 に基づいており、現在のレコードが最初のレコードは 1 に等しい、 **Recordset**します。 特定のページの最初のレコードに移動するには、このプロパティを設定します。 ページの合計数を取得、 **PageCount**プロパティ。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [AbsolutePage、PageCount、PageSize プロパティの例 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、PageCount、PageSize プロパティの例 (vc++)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePosition プロパティ (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [PageCount プロパティ (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [PageSize プロパティ (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)
