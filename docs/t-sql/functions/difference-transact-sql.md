---
title: DIFFERENCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DIFFERENCE
- DIFFERENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DIFFERENCE function
- comparing SOUNDEX values
- SOUNDEX values
ms.assetid: c58ca25d-d6ea-48fa-93bb-c9374b0b2a2b
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fe01e0d9465495cbf4943ba7867ebf262a1f3dd1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135929"
---
# <a name="difference-transact-sql"></a>DIFFERENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

この関数は、2 つの異なる文字式を対象に [SOUNDEX()](./soundex-transact-sql.md) 値の差を測定し、整数値を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
DIFFERENCE ( character_expression , character_expression )  
```  
  
## <a name="arguments"></a>引数  
*character_expression*  
文字データの英数字[式](../../t-sql/language-elements/expressions-transact-sql.md)。 *character_expression* には定数、変数、または列を指定できます。  
  
## <a name="return-types"></a>戻り値の型  
**int**  
 
## <a name="remarks"></a>Remarks  
`DIFFERENCE` は 2 つの異なる `SOUNDEX` 値を比較し、整数値を返します。 この値は、0 から 4 のスケールで、`SOUNDEX` 値が一致する度合いを測定します。 値が 0 の場合、SOUNDEX 値の類似性が弱いか、類似性がまったくなく、4 の場合、類似性が強いか、まったく同じになります。  
  
`DIFFERENCE` と `SOUNDEX` には、照合順序の区別があります。  
  
## <a name="examples"></a>使用例  
この例の最初の部分で、2 つの非常に似た文字列の `SOUNDEX` 値が比較されます。 照合順序 Latin1_General に対して、`DIFFERENCE` は値 `4` を返します。 この例の 2 番目の部分では、2 つの大きく異なる文字列の `SOUNDEX` 値が比較されます。照合順序 Latin1_General に対して、`DIFFERENCE` は値 `0` を返します。  
  
```  
-- Returns a DIFFERENCE value of 4, the least possible difference.  
SELECT SOUNDEX('Green'), SOUNDEX('Greene'), DIFFERENCE('Green','Greene');  
GO  
-- Returns a DIFFERENCE value of 0, the highest possible difference.  
SELECT SOUNDEX('Blotchet-Halls'), SOUNDEX('Greene'), DIFFERENCE('Blotchet-Halls', 'Greene');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----- ----- -----------   
G650  G650  4             
  
(1 row(s) affected)  
  
----- ----- -----------   
B432  G650  0             
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>参照  
 [SOUNDEX &#40;Transact-SQL&#41;](../../t-sql/functions/soundex-transact-sql.md)   
 [文字列関数 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

