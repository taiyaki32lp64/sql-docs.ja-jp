---
title: MONTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MONTH_TSQL
- MONTH
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], date and time
- dates [SQL Server], functions
- month of year [SQL Server]
- date and time [SQL Server], MONTH
- dateparts [SQL Server], month
- functions [SQL Server], date and time
- dates [SQL Server], MONTH
- MONTH function [SQL Server]
ms.assetid: 9dd8aff7-b0fc-45df-b316-ead14ee9b8b7
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d9fc2c8718fd643e5838172831858c51aea6fd47
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130228"
---
# <a name="month-transact-sql"></a>MONTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定された*日付*の月を表す整数を返します。  
  
 すべての [!INCLUDE[tsql](../../includes/tsql-md.md)] 日付および時刻のデータ型と関数の概要については、「[日付と時刻のデータ型および関数 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
MONTH ( date )  
```  
  
## <a name="arguments"></a>引数  
 *date*  
 **time**、**date**、**smalldatetime**、**datetime**、**datetime2**、または **datetimeoffset** 値に解決できる式です。 *日付* 引数は、式、列式、ユーザー定義変数、または文字列リテラルを指定できます。  
  
## <a name="return-type"></a>戻り値の型  
 **int**  
  
## <a name="return-value"></a>戻り値  
 MONTH は [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**month**、*date*) と同じ値を返します。  
  
 *日付*に時刻部分のみが含まれている場合、戻り値は 1、基本の月です。  
  
## <a name="examples"></a>使用例  
 次のステートメントでは、`4` が返されます。 これは月の数値です。  
  
```  
SELECT MONTH('2007-04-30T01:01:01.1234567 -07:00');  
```  
  
 次のステートメントでは、`1900, 1, 1` が返されます。 引数 *日付* 番号 0です`0`。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、`0` を 1900 年 1 月 1 日と解釈します。  
  
```  
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 次の例では、`4` が返されます。 これは月の数値です。  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP 1 MONTH('2007-04-30T01:01:01.1234')   
FROM dbo.DimCustomer;  
```  
  
 次の例では、`1900, 1, 1` が返されます。 引数 *日付* 番号 0です`0`。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、`0` を 1900 年 1 月 1 日と解釈します。  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP 1 YEAR(0), MONTH(0), DAY(0) FROM dbo.DimCustomer;  
```  
  
## <a name="see-also"></a>参照  
 [CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

