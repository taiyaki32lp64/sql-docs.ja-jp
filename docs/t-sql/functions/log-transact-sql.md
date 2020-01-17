---
title: LOG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- LOG
- LOG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- float expressions
- logarithm of expression
- LOG function
ms.assetid: f7c39511-cd84-4362-93ba-0d93655217ee
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1d3cbf58a3a85d84daf5b0f83006a7cdcb24b589
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982257"
---
# <a name="log-transact-sql"></a>LOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定したの自然対数を返します **float** 内の式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for SQL Server  
  
LOG ( float_expression [, base ] )  
```  
  
```  
-- Syntax for Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
LOG ( float_expression )  
```  
  
## <a name="arguments"></a>引数  
 *float_expression*  
 **float** 型、または暗黙的に **float** 型に変換できる[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。  
  
 *base*  
 対数の底を設定するオプションの整数引数です。  
  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降
  
## <a name="return-types"></a>戻り値の型  
 **float**  
  
## <a name="remarks"></a>Remarks  
 既定では、 を持つ **LOG()** 自然対数を返します。 以降で [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], 、対数の底を別の値に変更するには、(省略可能) を使用して *基本* パラメーター。  
  
 自然対数は **e** を底とする対数です。ここで、**e** は 2.718281828 にほぼ等しい無理定数です。  
  
 数値の指数の自然対数は、その数値自体になります。LOG( EXP( *n* ) ) = *n*。 また、数値の自然対数の指数は、その数値自体になります。EXP( LOG( *n* ) ) = *n*。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-calculating-the-logarithm-for-a-number"></a>A. 数値の自然対数を計算する  
 次の例では、指定された **float** 式の `LOG` を計算します。  
  
```  
DECLARE @var float = 10;  
SELECT 'The LOG of the variable is: ' + CONVERT(varchar, LOG(@var));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------------------------  
The LOG of the variable is: 2.30259  
  
(1 row(s) affected)  
```  
  
### <a name="b-calculating-the-logarithm-of-the-exponent-of-a-number"></a>B. 数値の指数の自然対数を計算する  
 次の例では、数値の指数の `LOG` を計算します。  
  
```  
SELECT LOG (EXP (10));  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------------------------  
10  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-calculating-the-logarithm-for-a-number"></a>C. 数値の自然対数を計算する  
 次の例では、指定された **float** 式の `LOG` を計算します。  
  
```  
SELECT LOG(10);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ----------------`  
  
 2.30
 ```  
  
## <a name="see-also"></a>参照  
 [数学関数 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [EXP &#40;Transact-SQL&#41;](../../t-sql/functions/exp-transact-sql.md)   
 [LOG10 &#40;Transact-SQL&#41;](../../t-sql/functions/log10-transact-sql.md)  
  
  

