---
title: DATETIMEOFFSETFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATETIMEOFFSETFROMPARTS_TSQL
- DATETIMEOFFSETFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEOFFSETFROMPARTS function
ms.assetid: 463da1f4-b4b6-45a3-9a95-ea1f99575542
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 786729a6bfcae37e3c2fb1aa9a9e85839ca9c127
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119105"
---
# <a name="datetimeoffsetfromparts-transact-sql"></a>DATETIMEOFFSETFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

指定された日付引数と時刻引数に対する **datetimeoffset** 値を返します。 返される値は、精度引数によって指定された有効桁数と、オフセット引数によって指定されたオフセットを持ちます。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DATETIMEOFFSETFROMPARTS ( year, month, day, hour, minute, seconds, fractions, hour_offset, minute_offset, precision )  
```  
  
## <a name="arguments"></a>引数  

*year*  
年を指定する整数式。  
  
*month*  
月を指定する整数式。  
  
*day*  
日を指定する整数式。  
  
*hour*  
時間を指定する整数式。  
  
*minute*  
分を指定する整数式。  
  
*seconds*  
秒を指定する整数式。  
  
*fractions*  
秒の小数部を指定する整数式。  
  
*hour_offset*  
タイム ゾーン オフセットの時間部分を指定する整数式。  
  
*minute_offset*  
タイム ゾーン オフセットの分部分を指定する整数式。  
  
*有効桁数 (precision)*  
`DATETIMEOFFSETFROMPARTS` が返す **datetimeoffset** 値の有効桁数を指定する整数リテラル値です。  
  
## <a name="return-types"></a>戻り値の型
**datetimeoffset(** *precision* **)**  
  
## <a name="remarks"></a>Remarks  

`DATETIMEOFFSETFROMPARTS` は、完全に初期化された **datetimeoffset** データ型を返します。 オフセット引数は、タイム ゾーンのオフセットを表します。 オフセット引数を省略すると、`DATETIMEOFFSETFROMPARTS` はタイム ゾーン オフセットが `00:00` (つまり、タイム ゾーン オフセットなし) であるものと想定します。 オフセット引数が指定される場合、`DATETIMEOFFSETFROMPARTS` は両方の引数の値が指定され、両方とも正の値または両方とも負の値であるものと想定します。 *minute_offset* の値が設定されていて、*hour_offset* の値が設定されていない場合、`DATETIMEOFFSETFROMPARTS` はエラーになります。 他の引数が無効な値の場合、`DATETIMEOFFSETFROMPARTS` はエラーになります。 必須引数の少なくとも 1 つが `NULL` 値である場合、`DATETIMEOFFSETFROMPARTS` は `NULL` を返します。 ただし、*precision* 引数が `NULL` 値の場合は、`DATETIMEOFFSETFROMPARTS` はエラーを生成します。  
  
*fractions* 引数は、precision 引数によって異なります。 たとえば、precision の値が 7 の場合、小数部分はそれぞれ 100 ナノ秒を表します。precision の値が 3 の場合、小数部分はそれぞれ 1 ミリ秒を表します。 precision 値がゼロの場合、fractions の値もゼロでなければなりません。それ以外の場合、`DATETIMEOFFSETFROMPARTS` はエラーを生成します。  
  
この関数は、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] サーバー以降のリモート処理に対応しています。 バージョンが [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] より前の場合、サーバーのリモート処理には対応していません。
  
## <a name="examples"></a>使用例  
  
### <a name="a-an-example-without-fractions-of-a-second"></a>A. 秒の小数部を使用しない場合の例  
  
```sql
SELECT DATETIMEOFFSETFROMPARTS ( 2010, 12, 31, 14, 23, 23, 0, 12, 0, 7 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
----------------------------------
2010-12-31 14:23:23.0000000 +12:00  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. 秒の小数部を使用する場合の例  

この例は、*fractions* パラメーターと *precision* パラメーターの使用方法を示しています。  

1. *fractions* の値が 5 のとき、*precision* の値が 1 であれば、*fractions* の値は 1 秒の 5/10 になります。  

2. *fractions* の値が 50 のとき、*precision* の値が 2 であれば、*fractions* の値は 1 秒の 50/100 になります。  

3. *fractions* の値が 500 で、*precision* の値が 3 の場合、*fractions* の値は 1 秒の 500/1000 を表します。  
  
```sql
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 5, 12, 30, 1 );  
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 50, 12, 30, 2 );  
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 500, 12, 30, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------------------  
2011-08-15 14:30:00.5 +12:30  
  
(1 row(s) affected)  
  
----------------------------------  
2011-08-15 14:30:00.50 +12:30  
  
(1 row(s) affected)  
  
----------------------------------  
2011-08-15 14:30:00.500 +12:30  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>参照
[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
[AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  


