---
title: AND (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AND_TSQL
- AND
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], TRUE
- "TRUE"
- AND, about AND operators
- AND
- combining expressions
ms.assetid: b61d7f8d-5a51-49b7-91dd-f6190a5a0fb9
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fb5211a2d45ef1a5495d1df57143190f1d5f6419
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927378"
---
# <a name="and-transact-sql"></a>AND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  2 つのブール式を結合し、両方の式が **TRUE** の場合、**TRUE** を返します。 1 つのステートメントの中で複数の論理演算子が使われている場合は、**AND** 演算子が最初に評価されます。 かっこを使うと、演算の順序を変更することができます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
boolean_expression AND boolean_expression  
```  
  
## <a name="arguments"></a>引数  
 *boolean_expression*  
 次のブール値を返す有効な[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。**TRUE**、**FALSE**、**UNKNOWN** のいずれかの値をとります。  
  
## <a name="result-types"></a>戻り値の型  
 **Boolean**  
  
## <a name="result-value"></a>結果の値  
 両方の式が TRUE の場合、TRUE を返します。  
  
## <a name="remarks"></a>Remarks  
 次の表は、TRUE 値と FALSE 値を AND 演算子を使用して比較する場合の結果です。  
  
||TRUE|FALSE|UNKNOWN|  
|------|----------|-----------|-------------|  
|**TRUE**|TRUE|FALSE|UNKNOWN|  
|**FALSE**|FALSE|FALSE|FALSE|  
|**UNKNOWN**|UNKNOWN|FALSE|UNKNOWN|  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-the-and-operator"></a>A. AND 演算子の使用  
 次の例では、役職が `Marketing Assistant` で、なおかつ、利用可能な休暇時間数が `41` 時間を超える従業員の情報を選択します。  
  
```  
-- Uses AdventureWorks  
  
SELECT  BusinessEntityID, LoginID, JobTitle, VacationHours   
FROM HumanResources.Employee  
WHERE JobTitle = 'Marketing Assistant'  
AND VacationHours > 41 ;  
```  
  
### <a name="b-using-the-and-operator-in-an-if-statement"></a>B. IF ステートメントでの AND 演算子の使用  
 次の例は、IF ステートメントでの AND の使用方法を示しています。 1 つ目のステートメントでは、`1 = 1` と `2 = 2` の両方が true であるため、結果は true です。 2 つ目の例では、引数 `2 = 17` が false であるため、結果は false です。  
  
```  
IF 1 = 1 AND 2 = 2  
BEGIN  
   PRINT 'First Example is TRUE'  
END  
ELSE PRINT 'First Example is FALSE';  
GO  
  
IF 1 = 1 AND 2 = 17  
BEGIN  
   PRINT 'Second Example is TRUE'  
END  
ELSE PRINT 'Second Example is FALSE' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [組み込み関数 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
