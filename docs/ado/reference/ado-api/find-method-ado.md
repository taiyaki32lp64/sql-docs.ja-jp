---
title: Find メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Find
- Recordset15::Find
helpviewer_keywords:
- Find method [ADO]
ms.assetid: 55c9810a-d8ca-46c2-a9dc-80e7ee7aa188
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9f394d5e3b3021ca240675d6979152c63b903190
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918627"
---
# <a name="find-method-ado"></a>Find メソッド (ADO)
検索、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)を指定した条件を満たす行のできます。 必要に応じて、検索、開始行、および開始行からのオフセットの方向を指定することがあります。 現在の行位置が; 検出されたレコードの設定、条件が満たされた場合(先頭または末尾) に、位置を設定する場合は、 **Recordset**します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *条件*  
 A**文字列**検索に使用するには、列名、比較演算子、および値を指定するステートメントを含む値。  
  
 *SkipRows*  
 任意。 A**長い**既定値が 0 で、現在の行から行オフセットを指定する値または*開始*検索を開始するブックマーク。 既定では、現在の行に、検索を開始します。  
  
 *SearchDirection*  
 任意。 A [SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)検索の方向で使用可能な次の行または現在の行に検索を開始するかどうかを指定する値。 最後に停止する検索が失敗した、**レコード セット**値が場合**adSearchForward**します。 検索が失敗したの停止の開始時、**レコード セット**値が場合**adSearchBackward**します。  
  
 *[開始]*  
 任意。 A**バリアント**検索の開始位置として機能するブックマーク。  
  
## <a name="remarks"></a>コメント  
 単一の列名のみを指定することがあります*条件*します。 このメソッドは、複数列の検索をサポートしていません。  
  
 比較演算子*条件*可能性があります" **>** 「(より大きい)、」 **\<** "(より小さい)、「=」(等しい)、"> ="(より大きいまたは等しい)"< ="(以下)、"<>"(等しくない)、または"like"(パターン一致)。  
  
 値*条件*文字列、浮動小数点数、または日付があります。 文字列の値が単一引用符または「#」(シャープ記号) で区切られた (たとえば、"状態 = 'WA'"または"の状態 = WA #")。 日付の値は「#」(シャープ記号) 記号で区切られます (たとえば、"start_date > #7/22/97 #")。 これらの値は、時間、分、および秒を示すタイムスタンプを含めることができますが、ミリ秒を含めることはできませんまたはエラーが発生します。  
  
 比較演算子が"like"の場合は、文字列値は、任意の文字または部分文字列の 1 つ以上の出現位置を検索のアスタリスク (*) を含めることができます。 たとえば、"のような状態は\*'"Maine とマサチューセッツ州に一致します。 値内に含まれる部分文字列を検索するのに先頭および末尾のアスタリスクを使用することもできます。 たとえば、"のような状態 '\*として\*'"アラスカ、アーカンソー、およびマサチューセッツ州に一致します。  
  
 アスタリスクできます使用条件の文字列の末尾または先頭と条件の文字列の末尾の両方に上記のようです。 先頭のワイルドカードとしてアスタリスクを使用することはできません ('* str')、または、埋め込みワイルドカード ('s として\*r')。 これにより、エラーが発生します。  
  
> [!NOTE]
>  現在の行位置を呼び出す前に設定されていない場合、エラーが発生**検索**します。 などの行の位置を設定するメソッド[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、呼び出す前に呼び出す必要がある**検索**します。  
  
> [!NOTE]
>  呼び出す場合、**検索**、レコード セットとレコード セット内の現在位置でメソッドが、最後のレコードまたはファイルの終わり (EOF) で、何も検索されません。 呼び出す必要があります、 **MoveFirst**レコード セットの先頭に現在の位置/カーソルを設定します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Find メソッドの例 (VB)](../../../ado/reference/ado-api/find-method-example-vb.md)   
 [インデックスのプロパティ](../../../ado/reference/ado-api/index-property.md)   
 [Optimize プロパティ-動的 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Seek メソッド](../../../ado/reference/ado-api/seek-method.md)
