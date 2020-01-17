---
title: STR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STR
- STR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- converting numbers to characters
- characters [SQL Server], converting
- character data [SQL Server]
- STR function
ms.assetid: de03531b-d9e7-4c3c-9604-14e582ac20c6
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 381eb06e646f98b3ec092cbaa4b6431677be559c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906881"
---
# <a name="str-transact-sql"></a>STR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  数値データから変換された文字データを返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
STR ( float_expression [ , length [ , decimal ] ] )  
```  
  
## <a name="arguments"></a>引数  
 *float_expression*  
 小数点付きの概数型 (**float**) の式を指定します。  
  
 *length*  
 全体の長さを指定します。 これには小数点、負号、数字、空白文字も含まれます。 既定値は 10 です。  
  
 *decimal*  
 小数点以下の桁数を指定します。 *decimal* は 16 以下である必要があります。 *decimal* に 16 を超える値を指定した場合、結果は小数点以下 16 桁に切り捨てられます。  
  
## <a name="return-types"></a>戻り値の型  
 **varchar**  
  
## <a name="remarks"></a>Remarks  
 STR で *length* パラメーターと *decimal* パラメーターを指定する場合は、正の値を指定する必要があります。 数値は、既定では整数に丸められます。小数点以下桁数に 0 が指定された場合も同様です。 指定する長さは、その数字の小数点より前の桁数に、符号があればその符号部分を加えた数以上にする必要があります。 短い *float_expression* は、指定された長さで右揃えされ、長い *float_expression* は、指定された小数点以下桁数に切り捨てられます。 たとえば、STR(12 **,** 10) の結果は 12 になります。 これは結果セットの中で右揃えされます。 一方、STR(1223 **,** 2) と指定すると、結果は切り捨てられて ** になります。 文字列関数は入れ子にすることができます。  
  
> [!NOTE]  
>  Unicode データに変換するには、CONVERT または [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) 変換関数の中で STR を使用します。  
  
## <a name="examples"></a>使用例  
 次の例では、5 つの数字と小数点で構成される式を、6 桁の文字列に変換します。 値の小数部は、小数点以下 1 桁になるように丸められます。  
  
```  
SELECT STR(123.45, 6, 1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------  
 123.5  
  
(1 row(s) affected)  
```  
  
 式が指定した長さを超えた場合、STR では `**` が指定の長さだけ返されます。  
  
```  
SELECT STR(123.45, 2, 2);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--  
**  
  
(1 row(s) affected)  
```  
  
 `STR` の中で数値データが入れ子にされていても、結果は指定した形式の文字データになります。  
  
```  
SELECT STR (FLOOR (123.45), 8, 3);
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
 123.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>参照  
 [CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [FORMAT &#40;Transact-SQL&#41;](../../t-sql/functions/format-transact-sql.md)  
 [文字列関数 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

