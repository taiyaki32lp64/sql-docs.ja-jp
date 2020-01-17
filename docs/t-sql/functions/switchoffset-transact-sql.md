---
title: SWITCHOFFSET (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/02/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SWITCHTZ
- SWITCHTZ_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- functions [SQL Server], time
- functions [SQL Server], date and time
- SWITCHOFFSET function [SQL Server]
- time [SQL Server], functions
- date and time [SQL Server], SWITCHOFFSET
- time zones [SQL Server]
ms.assetid: 32a48e36-0aa4-4260-9fe9-cae9197d16c5
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2ce69487c1550314dc7cfe3641333728fd07155e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117559"
---
# <a name="switchoffset-transact-sql"></a>SWITCHOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返します、 **datetimeoffset** 、保存されているタイム ゾーン オフセットから、指定された新しいタイム ゾーン オフセットへ変更された値。  
  
 すべての [!INCLUDE[tsql](../../includes/tsql-md.md)] 日付および時刻のデータ型と関数の概要については、「[日付と時刻のデータ型および関数 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
SWITCHOFFSET ( DATETIMEOFFSET, time_zone )   
```  
  
## <a name="arguments"></a>引数  
 *DATETIMEOFFSET*  
 **datetimeoffset(n)** 値に解決可能な式を指定する。  
  
 *time_zone*  
 [+|-]TZH:TZM 形式の文字列か、またはタイムゾーンのオフセットを表す符号付き整数 (分) です。夏時間対応であり調整済みと見なされます。  
  
## <a name="return-type"></a>戻り値の型  
 **datetimeoffset** の小数部の有効桁数を持つ、 *DATETIMEOFFSET* 引数。  
  
## <a name="remarks"></a>Remarks  
 SWITCHOFFSET を使用して、選択、 **datetimeoffset** に最初に格納されているタイム ゾーン オフセットとは異なるタイム ゾーン オフセットの値です。 SWITCHOFFSET は、保存されているは更新されません *time_zone* 値。  
  
 SWITCHOFFSET を使用して、更新、 **datetimeoffset** 列です。  
  
 GETDATE() 関数と一緒に SWITCHOFFSET を使用すると、クエリの実行速度が遅くなる場合があります。 これは、クエリ オプティマイザーが datetime 値のカーディナリティを正確に推定できないためです。 この問題を解決するには、OPTION (RECOMPILE) クエリ ヒントを使用し、次に同じクエリが実行されるときにクエリ オプティマイザーによってクエリ プランが強制的に再コンパイルされるようにします。 そうすると、オプティマイザーによって、正確なカーディナリティの推定値が取得され、より効率的なクエリ プランが生成されます。 詳細については、RECOMPILE クエリ ヒント、を参照してください。 [クエリ ヒント &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
```  
DECLARE @dt datetimeoffset = switchoffset (CONVERT(datetimeoffset, GETDATE()), '-04:00');   
SELECT * FROM t    
WHERE c1 > @dt OPTION (RECOMPILE);  
  
```  
  
## <a name="examples"></a>使用例  
 次の例では、`SWITCHOFFSET` を使用して、データベースに保存されている値とは異なるタイム ゾーン オフセットを表示します。  
  
```  
CREATE TABLE dbo.test   
    (  
    ColDatetimeoffset datetimeoffset  
    );  
GO  
INSERT INTO dbo.test   
VALUES ('1998-09-20 7:45:50.71345 -5:00');  
GO  
SELECT SWITCHOFFSET (ColDatetimeoffset, '-08:00')   
FROM dbo.test;  
GO  
--Returns: 1998-09-20 04:45:50.7134500 -08:00  
SELECT ColDatetimeoffset  
FROM dbo.test;  
--Returns: 1998-09-20 07:45:50.7134500 -05:00  
```  
  
## <a name="see-also"></a>参照  
 [CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  


