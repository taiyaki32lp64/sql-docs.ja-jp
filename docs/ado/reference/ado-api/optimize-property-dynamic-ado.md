---
title: Optimize プロパティ-動的 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Optimize property [ADO]
ms.assetid: a491c4ce-2b04-4c84-be83-3846bde8d16b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e8bb3c3787effe8418db735a72425a793b73e35
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931851"
---
# <a name="optimize-property-dynamic-ado"></a>Optimize プロパティ - 動的 (ADO)
インデックスを作成する必要があるかどうかを指定します、[フィールド](../../../ado/reference/ado-api/field-object.md)します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**ブール**インデックスを作成するかどうかを示す値です。  
  
## <a name="remarks"></a>コメント  
 インデックスは、検索や内の値を並べ替え操作のパフォーマンスを向上させることができます、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。 インデックスが ADO; 内部明示的にアクセスできない、またはアプリケーションで使用します。  
  
 フィールドのインデックスを作成するには設定、**最適化**プロパティを**True**します。 インデックスを削除するには、このプロパティを設定**False**します。  
  
 **最適化**に動的なプロパティが追加、[フィールド](../../../ado/reference/ado-api/field-object.md)オブジェクト[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクション時に、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) に設定されて**adUseClient**します。  
  
## <a name="usage"></a>使用方法  
  
```  
Dim rs As New Recordset  
Dim fld As Field  
rs.CursorLocation = adUseClient      'Enable index creation  
rs.Fields.Append "Field1", adChar, 35, adFldIsNullable  
rs.Open  
Set fld = rs.Fields(0)  
fld.Properties("Optimize") = True    'Create an index  
fld.Properties("Optimize") = False   'Delete an index  
```  
  
## <a name="applies-to"></a>適用対象  
 [Field オブジェクト](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>関連項目  
 [Optimize プロパティの例 (VB)](../../../ado/reference/ado-api/optimize-property-example-vb.md)   
 [Optimize プロパティの例 (vc++)](../../../ado/reference/ado-api/optimize-property-example-vc.md)   
 [プロパティをフィルター処理します。](../../../ado/reference/ado-api/filter-property.md)   
 [Find メソッド (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Sort プロパティ](../../../ado/reference/ado-api/sort-property.md)
