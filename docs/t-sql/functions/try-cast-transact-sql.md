---
title: TRY_CAST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TRY_CAST_TSQL
- TRY_CAST
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_CAST function
ms.assetid: ea3a16de-995b-415c-b5f0-9355cf7bb401
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = azuresqldb-current||>= sql-server-2016 ||>= sql-server-linux-2017||= sqlallproducts-allversions||>= aps-pdw-2016||= azure-sqldw-latest
ms.openlocfilehash: 915ea023442ab9d787a481cab44259b1fc4a3857
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70151952"
---
# <a name="try_cast-transact-sql"></a>TRY_CAST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  指定されたデータ型へのキャストが成功した場合は、キャストされる値が返されます。それ以外の場合は、null が返されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
TRY_CAST ( expression AS data_type [ ( length ) ] )  
```  
  
## <a name="arguments"></a>引数  
 *式 (expression)*  
 キャストされる値。 任意の有効な式。  
  
 *data_type*  
 *expression* をキャストするデータ型。  
  
 *length*  
 対象のデータ型の長さを指定する整数 (省略可能)。  
  
 許容される値の範囲は、*data_type* の値によって決まります。  
  
## <a name="return-types"></a>戻り値の型  
 指定されたデータ型へのキャストが成功した場合は、キャストされる値が返されます。それ以外の場合は、null が返されます。  
  
## <a name="remarks"></a>Remarks  
 **TRY_CAST** は渡された値を使用して、指定された *data_type* への変換を試みます。 キャストが成功した場合、**TRY_CAST** は指定された *data_type* と同じ値を返します。エラーが発生した場合は null が返されます。 ただし、明示的に許可されない変換を要求すると、**TRY_CAST** はエラーが発生して失敗します。  
  
 **TRY_CAST** は予約された新しいキーワードではなく、すべての互換性レベルで使用可能です。 **TRY_CAST** がリモート サーバーに接続するときのセマンティクスは、**TRY_CONVERT** と同じです。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-try_cast-returns-null"></a>A. TRY_CAST が null を返す  
 次の例は、キャストが失敗した場合に TRY_CAST から null が返されることを示しています。  
  
```sql  
SELECT   
    CASE WHEN TRY_CAST('test' AS float) IS NULL   
    THEN 'Cast failed'  
    ELSE 'Cast succeeded'  
END AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
Cast failed  
  
(1 row(s) affected)  
```  
  
 次の例は、式を求められている形式にする必要があることを示しています。  
  
```sql  
SET DATEFORMAT dmy;  
SELECT TRY_CAST('12/31/2010' AS datetime2) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-try_cast-fails-with-an-error"></a>B. TRY_CAST でエラーが発生して失敗する  
 次の例では、キャストが明示的に許可されていない場合に TRY_CAST がエラーを返すことを示します。  
  
```sql  
SELECT TRY_CAST(4 AS xml) AS Result;  
GO  
```  
  
 このステートメントの結果はエラーです。整数を xml データ型にキャストすることはできないからです。  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-try_cast-succeeds"></a>C. TRY_CAST が成功する  
 この例は、式を求められている形式にする必要があることを示しています。  
  
```  
SET DATEFORMAT mdy;  
SELECT TRY_CAST('12/31/2010' AS datetime2) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------------------  
2010-12-31 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>参照  
 [TRY_CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/try-convert-transact-sql.md)   
 [CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
