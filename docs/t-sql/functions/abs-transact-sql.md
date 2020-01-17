---
title: ABS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ABS_TSQL
- ABS
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], positive
- values [SQL Server], absolute
- ABS function
- absolute positive value
ms.assetid: e2ea7a6d-3e2f-472c-afbc-437d3b835c03
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 23782f796bae3dee795fbafacd2d0d4436337f38
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040423"
---
# <a name="abs-transact-sql"></a>ABS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

指定した数値式の絶対値 (正値) を返す数学関数です。 (`ABS` は、負の値を正の値を変更します `ABS` は、0 または正の値には影響しません)。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
ABS ( numeric_expression )  
```  
  
## <a name="arguments"></a>引数  
*numeric_expression*  
真数のデータ型または概数のデータ型の式を指定します。
  
## <a name="return-types"></a>戻り値の型  
*numeric_expression*と同じ型を返します。
  
## <a name="examples"></a>使用例  
次の例では、3 つの異なる値に対して `ABS` 関数を使用した結果を示します。
  
```sql
SELECT ABS(-1.0), ABS(0.0), ABS(1.0);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---- ---- ----  
1.0  .0   1.0  
```  
  
`ABS` 関数では、数値の絶対値が指定のデータ型で表現できる最大値を超えている場合に、オーバーフロー エラーを生成することができます。 たとえば、`int` データ型の値の範囲が `-2,147,483,648` から `2,147,483,647` だとします。 符号付き整数 `-2,147,483,648` の絶対値を計算すると、`int` データ型の正数範囲の上限を超えるため、オーバーフロー エラーが発生します。
  
```sql
DECLARE @i int;  
SET @i = -2147483648;  
SELECT ABS(@i);  
GO  
```  
  
次のエラー メッセージが返されます。
  
"メッセージ 8115、レベル 16、状態 2、行 3"
  
"式をデータ型 int に変換中に演算のオーバーフロー エラーが発生しました"

  
## <a name="see-also"></a>参照
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[数学関数 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[組み込み関数 &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)
  
  

