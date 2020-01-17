---
title: 有効桁数、小数点以下桁数、および長さ (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], length
- data types [SQL Server], scale
- precision [SQL Server], data types
- lengths [SQL Server], data types
- number of digits
- scale [SQL Server]
- scale [SQL Server], data types
- data types [SQL Server], precision
ms.assetid: fbc9ad2c-0d3b-4e98-8fdd-4d912328e40a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 65154f6e4ffd67a207db9a3b6c5044710249c1eb
ms.sourcegitcommit: 445842da7c7d216b94a9576e382164c67f54e19a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71682058"
---
# <a name="precision-scale-and-length-transact-sql"></a>有効桁数、小数点以下桁数、および長さ (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

precision は、数値全体の桁数です。 scale は、数値の中で小数点より右側の桁数です。 たとえば、123.45 という値の場合、precision は 5 で、scale は 2 になります。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、**numeric** および **decimal** データ型の precision の既定の最大値は 38 です。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、既定の最大値は 28 桁です。
  
数値データ型の長さは、数値の格納に使用されるバイト数です。 varchar および char の場合、文字列の長さはバイト数です。 nvarchar および nchar の場合、文字列の長さはバイトペアの数です。 **binary**、**varbinary**、および **image** データ型の長さはバイト数です。 たとえば、**int** データ型は 10 桁を保持することができ、4 バイトに格納され、小数点は許可されません。 **Int** データ型の precision は 10、長さは 4、scale は 0 です。
  
**char**、**varchar**、**binary**、または **varbinary** 式を 2 つ連結する場合、結果として得られる式の長さは 2 つのソース式の長さの合計 (上限は 8,000 バイト) です。
  
**nchar** または **nvarchar** 式を 2 つ連結する場合、結果として得られる式の長さは 2 つのソース式の長さの合計 (上限は 4,000 バイトペア) です。
  
同じデータ型で長さが異なる 2 つの式が、UNION、EXCEPT、または INTERSECT を使って比較される場合、結果の長さは 2 つの式のうち長い方です。
  
**decimal** を除いた数値データ型の precision と scale は固定です。 同じデータ型の 2 つの式に算術演算子を使用する場合、得られる結果のデータ型は同じになり、そのデータ型に定義されている precision と scale が適用されます。 異なるデータ型の 2 つの式に演算子を使用する場合、結果のデータ型はデータ型の優先順位規則によって決まります。 結果には、そのデータ型に定義されている precision と scale が適用されます。
  
次の表では、演算の結果が **decimal** 型の場合に precision と scale がどのように計算されるかを定義しています。 次のいずれかの場合、結果は **decimal** です。
-   両方の式が **decimal** である。  
-   一方の式が **decimal** で、もう一方が **decimal** よりも優先順位の低いデータ型である。  
  
オペランド式は、precision が p1 で scale が s1 の式 e1 と、precision が p2 で scale が s2 の式 e2 で表されます。 **decimal** でない任意の式の precision と scale は、その式のデータ型に定義された precision と scale です。 関数 max(a,b) は、"a" と "b" のうち、大きいほうの値を取ることを意味します。 同様に、min(a,b) は、"b" と "a"のうち、小さいほうの値を取ることを示しています。
  
|演算|結果の precision|結果の scale *|  
|---|---|---|
|e1 + e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 - e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 * e2|p1 + p2 + 1|s1 + s2|  
|e1 / e2|p1 - s1 + s2 + max(6, s1 + p2 + 1)|max(6, s1 + p2 + 1)|  
|e1 { UNION &#124; EXCEPT &#124; INTERSECT } e2|max(s1, s2) + max(p1-s1, p2-s2)|max(s1, s2)|  
|e1 % e2|min(p1-s1, p2 -s2) + max( s1,s2 )|max(s1, s2)|  
  
\* 結果の precision と scale の絶対最大値は 38 です。 結果の precision が 38 桁を超える場合は 38 桁に減らされます。この際、結果の整数部分が切り捨てられることを防ぐために、scale が減らされます。 乗算や除算などの演算では、decimal の precision を維持するために scale が減らされることはありません。これは、オーバーフロー エラーが発生する可能性がある場合でも同じです。

加算と減算では、decimal の整数部を格納するのに `max(p1 - s1, p2 - s2)` 桁必要です。 それらを格納できる十分な領域がない (つまり `max(p1 - s1, p2 - s2) < min(38, precision) - scale`) の場合は、整数部の領域を提供するために、scale が減らされます。 結果の scale は `MIN(precision, 38) - max(p1 - s1, p2 - s2)` になるため、この桁数に収まるように小数部が丸められます。

乗算と除算では、結果の整数部を格納するのに `precision - scale` 桁必要です。 次のルールを使用して、scale が減らされることがあります。
1.  整数部が 32 桁よりも少ない場合、結果の scale は `38 - (precision-scale)` を超えることはできないため、`min(scale, 38 - (precision-scale))` に減らされます。 これに該当する場合、結果は丸められる可能性があります。
1. scale が 6 桁未満であり、整数部が 32 を超える場合、scale が変更されることはありません。 これに該当する場合、decimal(38, scale) に収まらなければ、オーバーフロー エラーが発生することがあります 
1. scale が 6 桁以上であり、整数部が 32 を超える場合、scale は 6 に設定されます。 これに該当する場合、整数部の桁数と scale の両方が減らされ、結果の型は decimal(38,6) になります。 結果は、小数点以下の桁数が 6 桁に丸められるか、整数部を 32 桁に収めることができない場合はオーバーフロー エラーがスローされます。

## <a name="examples"></a>使用例
次の式は、丸めなしの結果 `0.00000090000000000` を返します。これは、結果が `decimal(38,17)` に収まるためです。
```sql
select cast(0.0000009000 as decimal(30,20)) * cast(1.0000000000 as decimal(30,20)) [decimal 38,17]
```
ここでは、precision は 61 であり、scale は 40 です。
整数部 (precision-scale = 21) が 32 未満であり、乗算ルールの (1) に該当するため、scale は `min(scale, 38 - (precision-scale)) = min(40, 38 - (61-40)) = 17` で計算されます。 結果のデータ型は `decimal(38,17)` です。

次の式は、`decimal(38,6)` に収めた結果 `0.000001` を返します。
```sql
select cast(0.0000009000 as decimal(30,10)) * cast(1.0000000000 as decimal(30,10)) [decimal(38, 6)]
```
ここでは、precision は 61 であり、scale は 20 です。
scale が 6 桁を越えており、整数部 (`precision-scale = 41`) が 32 を超えています。 これは乗算ルールの (3) に該当するため、結果の型は `decimal(38,6)` になります。

## <a name="see-also"></a>参照
[式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
