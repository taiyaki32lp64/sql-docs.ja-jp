---
title: DAY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DAY_TSQL
- DAY
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], DAY
- dates [SQL Server], functions
- DAY function [SQL Server]
- dates [SQL Server], days
- functions [SQL Server], date and time
- dateparts [SQL Server], day
ms.assetid: 2f4410ea-fd3e-4d69-ac4b-3b0091a084bc
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0f1d58e89e6fd7cdc4d8af85d3d8745e1bc15fa7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119057"
---
# <a name="day-transact-sql"></a>DAY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

この関数は、指定された *date* の日 (月の日にち) を表す整数を返します。
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] の日付と時刻のあらゆるデータ型と関数に関する概要については、「[日付と時刻のデータ型および関数 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)」を参照してください。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DAY ( date )  
```  
  
## <a name="arguments"></a>引数  
*date*  
次のいずれかのデータ型に解決される式。

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**

*date* の場合、`DAY` では、列式、式、文字列リテラル、ユーザー定義の変数が受け入れられます。
  
## <a name="return-type"></a>戻り値の型  
**int**
  
## <a name="return-value"></a>戻り値  
DAY は [DATEPART](../../t-sql/functions/datepart-transact-sql.md)(**day**, *date*) と同じ値を返します。
  
*date* に時刻部分のみが含まれる場合、`DAY` は基本の日である 1 を返します。
  
## <a name="examples"></a>使用例  
このステートメントは、日にち自体の数である `30` を返します。
  
```sql
SELECT DAY('2015-04-30 01:01:01.1234567');  
```  
  
このステートメントは `1900, 1, 1` を返します。 *date* 引数の数値は `0` になります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、`0` を 1900 年 1 月 1 日と解釈します。
  
```sql
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>参照
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


