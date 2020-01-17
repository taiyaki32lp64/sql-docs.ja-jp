---
title: CompareBookmarks メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CompareBookmarks
- Recordset20::CompareBookmarks
- Recordset20::raw_CompareBookmarks
helpviewer_keywords:
- CompareBookmarks method [ADO]
ms.assetid: d0b64286-2cc4-4a22-8f1d-9aefeebbcbc6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0d737c2f031fa3ba630eabb7e52dff0e056c3390
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919598"
---
# <a name="comparebookmarks-method-ado"></a>CompareBookmarks メソッド (ADO)
2 つのブックマークを比較し、これらの相対値を示す値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>戻り値  
 返します、 [CompareEnum](../../../ado/reference/ado-api/compareenum.md)ブックマークによって表される 2 つのレコードの相対行位置を示す値。  
  
#### <a name="parameters"></a>パラメーター  
 *Bookmark1*  
 最初の行のブックマークです。  
  
 *Bookmark2*  
 2 番目の行のブックマークです。  
  
## <a name="remarks"></a>コメント  
 同じブックマークを適用する必要があります[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト、または**レコード セット**オブジェクトとその[複製](../../../ado/reference/ado-api/clone-method-ado.md)します。 さまざまなブックマークを確実に比較することはできません**Recordset**オブジェクトの場合、同じソースまたはコマンドから作成された場合でもです。 ブックマークを比較することも、 **Recordset**オブジェクトの基になるプロバイダーは、比較をサポートしていません。  
  
 ブックマーク内の行を一意に識別する、 **Recordset**オブジェクト。 使用して、[ブックマーク](../../../ado/reference/ado-api/bookmark-property-ado.md)ブックマークを取得する現在の行のプロパティ。  
  
 ADO としてそれを公開して、ブックマークのデータ型は、各プロバイダーに固有であるため、**バリアント**します。 たとえば、SQL Server のブックマークは型 DBTYPE_R8 (**二重**)。 ADO では、次の種類として、**バリアント**のサブタイプで**二重**します。  
  
 ブックマークを比較するときに、ADO は任意の型の強制型変換を行いません。 単に値は、比較が発生したプロバイダーに渡されます。 ブックマークが渡された場合、 **CompareBookmarks**メソッドが異なる型の変数に格納されている、次の型の不一致エラーを生成できます。"引数型が正しくありません、許容の範囲から外れているや、他と競合しています。"  
  
 無効か、形式が正しくないブックマークには、エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [CompareBookmarks メソッドの例 (VB)](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [CompareBookmarks メソッドの例 (vc++)](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [Bookmark プロパティ (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)
