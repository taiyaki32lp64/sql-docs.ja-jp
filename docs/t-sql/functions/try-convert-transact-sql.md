---
title: TRY_CONVERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TRY_CONVERT_TSQL
- TRY_CONVERT
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_CONVERT function
ms.assetid: 3e6e7825-6482-4cb2-a8c2-9abc99e265a6
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = azuresqldb-current||>= sql-server-2016 ||>= sql-server-linux-2017||= sqlallproducts-allversions||>= aps-pdw-2016||= azure-sqldw-latest
ms.openlocfilehash: ace985045db2bf10b1ef0e80a2b05ea3e0cb85ca
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70151963"
---
# <a name="try_convert-transact-sql"></a>TRY_CONVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  指定されたデータ型へのキャストが成功した場合は、キャストされる値が返されます。それ以外の場合は、null が返されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
TRY_CONVERT ( data_type [ ( length ) ], expression [, style ] )  
```  
  
## <a name="arguments"></a>引数  
 *data_type [ ( length ) ]*  
 *expression* をキャストするデータ型。  
  
 *式 (expression)*  
 キャストされる値。  
  
 *style*  
 **TRY_CONVERT** 関数が *expression* を変換する方法を指定する省略可能な整数式。  
  
 *style* は、**CONVERT** 関数の *style* パラメーターと同じ値を使用します。 詳細については、「[CAST and CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)」を参照してください。  
  
 許容される値の範囲は、*data_type* の値によって決まります。 *style* が null の場合、**TRY_CONVERT** は null を返します。  
  
## <a name="return-types"></a>戻り値の型  
 指定されたデータ型へのキャストが成功した場合は、キャストされる値が返されます。それ以外の場合は、null が返されます。  
  
## <a name="remarks"></a>Remarks  
 **TRY_CONVERT** は渡された値を使用して、指定された *data_type* への変換を試みます。 キャストが成功した場合、**TRY_CONVERT** は指定された *data_type* と同じ値を返します。エラーが発生した場合は null が返されます。 ただし、明示的に許可されない変換を要求すると、**TRY_CONVERT** はエラーが発生して失敗します。  
  
 互換性レベル 110 以上では、**TRY_CONVERT** は予約されたキーワードです。  
  
 この関数は、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以上のバージョンがインストールされているサーバーに対してリモート処理が可能です。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] より前のバージョンをインストールしているサーバーには、リモート処理が行われません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-try_convert-returns-null"></a>A. TRY_CONVERT は null を返します。  
 次の例は、キャストが失敗した場合に TRY_CONVERT から null が返されることを示しています。  
  
```sql  
SELECT   
    CASE WHEN TRY_CONVERT(float, 'test') IS NULL   
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
SELECT TRY_CONVERT(datetime2, '12/31/2010') AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-try_convert-fails-with-an-error"></a>B. TRY_CONVERT でエラーが発生して失敗する  
 次の例では、キャストが明示的に許可されていない場合に TRY_CONVERT がエラーを返すことを示します。  
  
```sql  
SELECT TRY_CONVERT(xml, 4) AS Result;  
GO  
```  
  
 このステートメントの結果はエラーです。整数を xml データ型にキャストすることはできないからです。  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-try_convert-succeeds"></a>C. TRY_CONVERT が成功する  
 この例は、式を求められている形式にする必要があることを示しています。  
  
```  
SET DATEFORMAT mdy;  
SELECT TRY_CONVERT(datetime2, '12/31/2010') AS Result;  
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
 [CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
