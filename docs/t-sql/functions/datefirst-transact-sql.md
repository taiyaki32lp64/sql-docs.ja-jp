---
title: '@@DATEFIRST (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATE_FORMAT_TSQL
- DATE FORMAT
- '@@DATEFIRST_TSQL'
- '@@DATEFIRST'
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], SET DATEFIRST
- first day of week [SQL Server]
- dates [SQL Server], first day of week
- day of week [SQL Server]
- SET DATEFIRST option [SQL Server]
- date and time [SQL Server], DATEFIRST
- DATEFIRST option [SQL Server]
- date and time [SQL Server], @@DATEFIRST
- weekdays [SQL Server]
- '@@DATEFIRST function [SQL Server]'
- functions [SQL Server], date and time
- options [SQL Server], date
ms.assetid: a178868e-49d5-4bd5-a5e2-1283409c8ce6
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2fc2ca71731fa632db2a857e1b727574722058c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119175"
---
# <a name="x40x40datefirst-transact-sql"></a>&#x40;&#x40;DATEFIRST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

この関数は、特定のセッションにおける、[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md) の現在の値を返します。
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] の日付と時刻のあらゆるデータ型と関数に関する概要については、「[日付と時刻のデータ型および関数 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)」を参照してください。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```
@@DATEFIRST  
```  
  
## <a name="return-type"></a>戻り値の型  
**tinyint**
  
## <a name="remarks"></a>Remarks  
SET DATEFIRST *n* では、週の最初の日 (日曜日、月曜日、火曜日など) を指定します。 *n* の値は、1 から 7 までの範囲となります。

```sql
SET DATEFIRST 3;
GO  
SELECT @@DATEFIRST; -- 3 (Wednesday)
GO
```  

米国の英語環境の場合、@DATEFIRST の既定値は 7 (日曜日) です。
  
この言語設定は、SQL Server で文字列がデータベース ストレージ用の日付値に変換されるときに、文字列の解釈に影響を与えます。 この設定はまた、データベースに格納されている日付値の表示にも影響を与えます。 この設定は日付データのストレージ形式には影響しません。

この例ではまず、言語を `Italian` に設定します。 `SELECT @@DATEFIRST;` ステートメントからは `1` が返されます。 次のステートメントで、言語を `us_english` に設定します。 最後のステートメント `SELECT @@DATEFIRST;` からは、`7` が返されます。
  
```sql
SET LANGUAGE Italian;  
GO  
SELECT @@DATEFIRST;  
GO  
SET LANGUAGE us_english;  
GO  
SELECT @@DATEFIRST;  
```  
  
## <a name="examples"></a>使用例  
この例では、週の最初の曜日を `5` (金曜日) に設定します。現在の曜日 `Today` は土曜日であると仮定します。 `SELECT` ステートメントでは、`DATEFIRST` の値と現在の曜日を示す数値が返されます。
  
```sql
SET DATEFIRST 5;  
SELECT @@DATEFIRST AS 'First Day'  
    ,DATEPART(dw, SYSDATETIME()) AS 'Today';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
First Day         Today  
----------------  --------------  
5                 2  
```  
  
## <a name="example"></a>例
 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT @@DATEFIRST;  
```  
  
## <a name="see-also"></a>参照
[構成関数 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)
  
  

