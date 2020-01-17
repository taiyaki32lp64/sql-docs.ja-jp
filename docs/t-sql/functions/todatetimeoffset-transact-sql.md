---
title: TODATETIMEOFFSET (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TO_DATETIMEOFFSET_TSQL
- SWITCH_TZ_TSQL
- SWITCH_TZ
- TO_DATETIMEOFFSET
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], TODATETIMEOFFSET
- TODATETIMEOFFSET function
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: b5fafc08-efd4-4a3b-a0b3-068981a0a685
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7f6978a8344b7a1c9100a701d582193295f34c12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098974"
---
# <a name="todatetimeoffset-transact-sql"></a>TODATETIMEOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返します、 **datetimeoffset** 値から変換されたです、 **datetime2** 式です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
TODATETIMEOFFSET ( expression , time_zone )  
```  
  
## <a name="arguments"></a>引数  
 *式 (expression)*  
 [datetime2](../../t-sql/data-types/datetime2-transact-sql.md) 値に解決される[式](../../t-sql/language-elements/expressions-transact-sql.md)です。  
  
> [!NOTE]  
>  型の式をすることはできません **テキスト**, 、**ntext**, 、または **イメージ** に、これらの型を暗黙的に変換できないため **varchar** または **nvarchar**です。  
  
 *time_zone*  
 タイム ゾーン オフセットを表す式です。たとえば、分単位で表す式 (整数の場合) は -120、時間と分単位で表す式 (文字列の場合) は '+13:00' です。 範囲は +14 ～ -14 (時間) です。 式は、指定された time_zone のローカル時刻で解釈されます。  
  
> [!NOTE]  
>  式が文字列の場合、{+|-}TZH:THM の形式にする必要があります。  
  
## <a name="return-type"></a>戻り値の型  
 **datetimeoffset**. 小数部の有効桁数が同じ、 *datetime* 引数。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-changing-the-time-zone-offset-of-the-current-date-and-time"></a>A. 現在の日付と時刻のタイム ゾーン オフセットを変更する  
 次の例では、現在の日付と時刻のゾーン オフセットを、タイム ゾーン `-07:00` に変更します。  
  
```sql  
DECLARE @todaysDateTime datetime2;  
SET @todaysDateTime = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDateTime, '-07:00');  
-- RETURNS 2019-04-22 16:23:51.7666667 -07:00  
```  
  
### <a name="b-changing-the-time-zone-offset-in-minutes"></a>B. タイム ゾーン オフセットを分単位で変更する  
 次の例では、現在のタイム ゾーンを `-120` 分に変更します。  
  
```sql  
SELECT TODATETIMEOFFSET(SYSDATETIME(), -120)
-- RETURNS: 2019-04-22 11:39:21.6986813 -02:00  
```  
  
### <a name="c-adding-a-13-hour-time-zone-offset"></a>C. 13 時間のタイム ゾーン オフセットを追加する  
 次の例では、日付と時刻に 13 時間のタイム ゾーン オフセットを追加します。  
  
```sql  
SELECT TODATETIMEOFFSET(SYSDATETIME(), '+13:00')
-- RETURNS: 2019-04-22 11:39:29.0339301 +13:00
```  
  
## <a name="see-also"></a>参照  
 [CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [日付と時刻のデータ型および関数 (Transact-SQL)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  

