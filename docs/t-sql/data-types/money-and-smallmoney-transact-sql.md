---
title: money と smallmoney (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- money_TSQL
- money
- smallmoney
- smallmoney_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- money data type, about money data type
- money data type
- smallmoney data type
- values [SQL Server], monetary
- currency [SQL Server]
ms.assetid: 57861137-89ea-4b89-b361-390597d7bccc
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7ad26acc2f1e23b61e9692dcf2720d7ee6dd8639
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077812"
---
# <a name="money-and-smallmoney-transact-sql"></a>money と smallmoney (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

金額値または通貨値を表すデータ型。
  
## <a name="remarks"></a>Remarks  
  
|データ型|範囲|ストレージ|  
|---|---|---|
|**money**|-922,337,203,685,477.5808 ～ 922,337,203,685,477.5807 (Informatica では -922,337,203,685,477.58<br />～ 922,337,203,685,477.58。  Informatica では、小数点以下 4 桁ではなく、小数点以下 2 桁 のみをサポートします。)|8 バイト|  
|**smallmoney**|- 214,748.3648 ～ 214,748.3647|4 バイト|  
  
**Money** と **smallmoney** データ型を表している通貨単位の 10,000 の精度はします。 Informatica では、**money** データ型と **smallmoney** データ型の精度は、それらが表している通貨単位の 1/100 です。
  
全体の通貨単位からセントなどの部分的な通貨単位を分離するには、ピリオドを使用します。 たとえば、2.15 は 2 ドル 15 セントを表します。
  
これらのデータ型では、次の通貨記号のいずれかを使用できます。
  
![通貨記号と 16 進値の表](../../t-sql/data-types/media/money01.gif "通貨記号と 16 進値の表")
  
通貨データまたは金額データは、単一引用符 (') で囲む必要はありません。 通貨記号が前に付いた金額値を指定することはできますが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はその記号に関連付けられた通貨情報を格納せず、数値のみを格納することに注意してください。
  
## <a name="converting-money-data"></a>money 型データの変換
変換すると **money** から整数データ型は、単位は金額であると仮定します。 4 の整数値を変換するなど、 **money** 4 通貨単位に相当します。
  
次の例では、変換 **smallmoney** と **money** 値を **varchar** と **10 進** それぞれのデータ型します。
  
```sql
DECLARE @mymoney_sm smallmoney = 3148.29,  
        @mymoney    money = 3148.29;  
SELECT  CAST(@mymoney_sm AS varchar) AS 'SM_MONEY varchar',  
        CAST(@mymoney AS decimal)    AS 'MONEY DECIMAL';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
SM_MONEY VARCHAR               MONEY DECIMAL  
------------------------------ ----------------------  
3148.29                        3148    
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>参照
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)
[CAST と CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)
[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
[sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
