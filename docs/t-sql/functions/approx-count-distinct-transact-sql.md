---
title: APPROX_COUNT_DISTINCT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- APPROX_COUNT_DISTINCT
dev_langs:
- TSQL
author: joesackmsft
ms.author: josack
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9f5a9846ddc19320b3299893929c7ebf11ca0269
ms.sourcegitcommit: eae9efe2a2d3758685e85039ffb8fa698aa47f9b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73962340"
---
# <a name="approx_count_distinct-transact-sql"></a>APPROX_COUNT_DISTINCT (Transact-SQL)
[!INCLUDE[appliesto-xx-asdb-asdw-pdw-md](../../includes/appliesto-xx-asdb-asdw-pdw-md.md)]

この関数は、グループ内の一意の非 null 値の概数を返します。 
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
-- Syntax for Azure SQL Database, Azure SQL Data Warehouse and Parallel Data Warehouse  

APPROX_COUNT_DISTINCT ( expression )   
```  
  
## <a name="arguments"></a>引数  
*式 (expression)*  
**image**、**sql_variant**、**ntext**、**text** を除く、任意の型の[式](../../t-sql/language-elements/expressions-transact-sql.md)です。 

## <a name="return-types"></a>戻り値の型
 **bigint**  
  
## <a name="remarks"></a>Remarks  
`APPROX_COUNT_DISTINCT( expression )` はグループ内の各行に対して式を評価し、グループ内の一意の非 null 値の概数を返します。 この関数は、絶対的な精度よりも応答性が重要となる場合に、大規模なデータ セット全体の集計を提供するために設計されています。  

`APPROX_COUNT_DISTINCT` はビッグ データのシナリオで使用するために設計されており、次の条件に向けて最適化されています。
- 数百万行以上のデータ セットへのアクセス、"*および*"
- 異なる値を多数持つ 1 つまたは複数の列の集計

97% の確率でエラー率が最大 2% 以内に収まることが、関数の実装によって保証されます。 

`APPROX_COUNT_DISTINCT` に必要なメモリは、完全な COUNT DISTINCT 操作よりも少なくて済みます。  メモリの使用量が少ないため、`APPROX_COUNT_DISTINCT` がメモリをディスクに書き込む可能性は、正確な COUNT DISTINCT 操作に比べて小さくなります。 これを実現するために使用されるアルゴリズムの詳細については、「[HyperLogLog](https://en.wikipedia.org/wiki/HyperLogLog)」をご覧ください。

> [!NOTE]
> 照合順序に依存する文字列では、APPROX_COUNT_DISTINCT ではバイナリ一致が使用され、BIN 照合順序がある場合 (BIN2 はなし) に生成されるのと同じ結果が提供されます。 
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-approx_count_distinct"></a>A. APPROX_COUNT_DISTINCT を使用する 
この例では、orders テーブルのさまざまな順序キーの概数が返されます。
  
```sql
SELECT APPROX_COUNT_DISTINCT(O_OrderKey) AS Approx_Distinct_OrderKey
FROM dbo.Orders;
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Approx_Distinct_OrderKey
------------------------
15164704
```
  
### <a name="b-using-approx_count_distinct-with-group-by"></a>B. GROUP BY と共に APPROX_COUNT_DISTINCT を使用する 
この例では、orders テーブルのさまざまな順序キーの概数が、順序のステータスによって返されます。 
  
```sql
SELECT O_OrderStatus, APPROX_COUNT_DISTINCT(O_OrderKey) AS Approx_Distinct_OrderKey
FROM dbo.Orders
GROUP BY O_OrderStatus
ORDER BY O_OrderStatus; 
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
O_OrderStatus                                                    Approx_Distinct_OrderKey
---------------------------------------------------------------- ------------------------
F                                                                7397838
O                                                                7387803
P                                                                388036
```
    
## <a name="see-also"></a>参照
[集計関数 &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT &#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md) 
