---
title: EOMONTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EOMONTH
- EOMONTH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EOMONTH function
ms.assetid: 1d060d8e-3297-4244-afef-57df2f8f92e2
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 481faddf2a0a12bcc44a8b4e677101afa68c37a4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904386"
---
# <a name="eomonth-transact-sql"></a>EOMONTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

この関数は、オプションのオフセットを使用して、指定された日付を含んでいる月の最後の日付を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
EOMONTH ( start_date [, month_to_add ] )  
```  
  
## <a name="arguments"></a>引数  
*start_date*  
月の最終日を返す日付を指定する日付の式。  
  
*month_to_add*  
*start_date* に追加する月数を指定する省略可能な整数式。  
  
*month_to_add* 引数に値が指定されると、`EOMONTH` は指定された月数を *start_date* に追加し、結果として生成された月の最終日を返します。 この整数式を追加したことによって有効な日付範囲をオーバーフローすると、`EOMONTH` はエラーを生成します。  
  
## <a name="return-type"></a>戻り値の型  
 **date**  
  
## <a name="remarks"></a>Remarks  
`EOMONTH` 関数は、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降のサーバーに対してリモート処理が可能です。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] よりも前のバージョンのサーバーに対してリモート処理を実行することはできません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-eomonth-with-explicit-datetime-type"></a>A. 明示的な datetime 型を使用する EOMONTH  
  
```  
DECLARE @date DATETIME = '12/1/2011';  
SELECT EOMONTH ( @date ) AS Result;  
GO  
```  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
2011-12-31  
  
(1 row(s) affected)  
```  

### <a name="b-eomonth-with-string-parameter-and-implicit-conversion"></a>B. 文字列パラメーターと暗黙的な変換を使用する EOMONTH  
  
```  
DECLARE @date VARCHAR(255) = '12/1/2011';  
SELECT EOMONTH ( @date ) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
2011-12-31  
  
(1 row(s) affected)  
```  
  
### <a name="c-eomonth-with-and-without-the-monthtoadd-parameter"></a>C. month_to_add パラメーターを使用する EOMONTH と使用しない EOMONTH  
  
注: これらの結果セットに示されている値は、実行日を含む期間を反映します。
        
        12/01/2011
        
        and
        
        12/31/2011

```sql  
DECLARE @date DATETIME = GETDATE();  
SELECT EOMONTH ( @date ) AS 'This Month';  
SELECT EOMONTH ( @date, 1 ) AS 'Next Month';  
SELECT EOMONTH ( @date, -1 ) AS 'Last Month';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
This Month  
-----------------------  
2011-12-31  
  
(1 row(s) affected)  
  
Next Month  
-----------------------  
2012-01-31  
  
(1 row(s) affected)  
  
Last Month  
-----------------------  
2011-11-30  
  
(1 row(s) affected)  
```  
  
  

