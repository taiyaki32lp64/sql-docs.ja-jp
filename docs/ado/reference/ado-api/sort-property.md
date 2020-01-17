---
title: プロパティを並べ替える |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::get_Sort
- Recordset15::put_Sort
- Recordset15::PutSort
- Recordset15::GetSort
- Recordset15::Sort
helpviewer_keywords:
- DESC [ADO]
- ASC [ADO]
- Sort property [ADO]
ms.assetid: 3683ffa0-6f93-4906-9533-ef6942f24f39
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 946314f7be9f6c39d47a3f26b577e10834064dab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930946"
---
# <a name="sort-property"></a>Sort プロパティ
1 つまたは複数のフィールド名を示します、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)が並べ替えられると、各フィールドが昇順または降順で並べ替えられたかどうか。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 取得または設定、**文字列**で名前をフィールドを示す値、 **Recordset**並べ替えに使用します。 それぞれの名前は、コンマで区切られます、空白をして、キーワードに続けて**ASC**、昇順でフィールドの並べ替えまたは**DESC**、降順でフィールドの並べ替え。 既定では、キーワードが指定されていない場合、フィールドが昇順に並べ替えられます。  
  
## <a name="remarks"></a>コメント  
 このプロパティには、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティを設定する**adUseClient**します。 各フィールドで指定された一時インデックスが作成されます、**並べ替え**プロパティ、インデックスが存在しない場合。  
  
 データは物理的に並べ替えられるされませんが、インデックスで指定した順序でアクセスされるだけであるために、並べ替え操作が効率的です。  
  
 ときの値、**並べ替え**プロパティが空の文字列以外、**並べ替え**プロパティの順序で指定された順序よりも優先、 **ORDER BY**句開くために使用する SQL ステートメントに含まれる、 **Recordset**します。  
  
 **レコード セット**アクセスする前に開く必要はありません、**並べ替え**プロパティ; 後いつでも設定できます、**レコード セット**オブジェクトがインスタンス化します。  
  
 設定、**並べ替え**プロパティを空の文字列には行は元の順序にリセットされ、一時インデックスを削除します。 既存のインデックスは削除されません。  
  
 **レコード セット**という 3 つのフィールドが含まれています*firstName*、 *middleInitial*、および*lastName*します。 設定、**並べ替え**プロパティを文字列"`lastName DESC, firstName ASC`"、順序は、**レコード セット**で降順に並べ替え、姓、名で昇順に並べ替えます。 ミドル ネームのイニシャルは無視されます。  
  
 フィールド名前を指定できない"ASC"または"DESC"キーワードとそれらの名前が競合するため**ASC**と**DESC**します。 使用して競合するフィールドの別名を作成することができます、 **AS**を返すクエリ内のキーワード、 **Recordset**します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Sort プロパティの例 (VB)](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [Sort プロパティの例 (vc++)](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [Optimize プロパティ-動的 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [SortColumn プロパティ (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection プロパティ (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)
