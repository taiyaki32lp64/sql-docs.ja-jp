---
title: サポートされているデータの種類 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de5f805a9d722974adf7975f713436bc7b1ca4d0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63155150"
---
# <a name="supported-data-types"></a>サポートされるデータ型
  次のデータ型は**サポート**でメモリ最適化テーブルおよびネイティブ コンパイル ストアド プロシージャ。  
  
 **数値データ型**  
  
|データ型|詳細情報|  
|---------------|--------------------------|  
|ssNoversion|[int、bigint、smallint 型、および tinyint と #40 です。TRANSACT-SQL と #41 です。](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|BIGINT|[int、bigint、smallint 型、および tinyint と #40 です。TRANSACT-SQL と #41 です。](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|SMALLINT|[int、bigint、smallint 型、および tinyint と #40 です。TRANSACT-SQL と #41 です。](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|TINYINT|[int、bigint、smallint 型、および tinyint と #40 です。TRANSACT-SQL と #41 です。](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|Decimal|[10 進数の数値と #40 です。TRANSACT-SQL と #41 です。](/sql/t-sql/data-types/decimal-and-numeric-transact-sql)|  
|NUMERIC|[10 進数の数値と #40 です。TRANSACT-SQL と #41 です。](/sql/t-sql/data-types/decimal-and-numeric-transact-sql)|  
|FLOAT|[float、real および #40 です。TRANSACT-SQL と #41 です。](/sql/t-sql/data-types/float-and-real-transact-sql)|  
|REAL|[float、real および #40 です。TRANSACT-SQL と #41 です。](/sql/t-sql/data-types/float-and-real-transact-sql)|  
|money|[money および smallmoney & #40 です。TRANSACT-SQL と #41 です。](/sql/t-sql/data-types/money-and-smallmoney-transact-sql)|  
|SMALLMONEY|[money および smallmoney & #40 です。TRANSACT-SQL と #41 です。](/sql/t-sql/data-types/money-and-smallmoney-transact-sql)|  
  
 **文字列データ型**  
  
|データ型|詳細情報|  
|---------------|--------------------------|  
|char(n)|[char および varchar &#40;Transact-SQL&#41;](/sql/t-sql/data-types/char-and-varchar-transact-sql)|  
|varchar(n) <sup>1</sup>|[char および varchar &#40;Transact-SQL&#41;](/sql/t-sql/data-types/char-and-varchar-transact-sql)|  
|nchar(n)|[nchar および nvarchar &#40;Transact-SQL&#41;](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)|  
|nvarchar(n) <sup>1</sup>|[nchar および nvarchar &#40;Transact-SQL&#41;](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)|  
|sysname|[nchar および nvarchar &#40;Transact-SQL&#41;](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)|  
  
 <sup>1</sup>制限では、1 行の合計、8,060 バイトの可変長型の (n) をカウントします。  
  
 サポートされる照合順序については、次を参照してください。 [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)します。  
  
 **日付および時刻のデータ型**  
  
|データ型|詳細情報|  
|---------------|--------------------------|  
|日付|[date &#40;Transact-SQL&#41;](/sql/t-sql/data-types/date-transact-sql)|  
|time|[time &#40;Transact-SQL&#41;](/sql/t-sql/data-types/time-transact-sql)|  
|DATETIME|[datetime (&) #40 です。TRANSACT-SQL と #41 です。](/sql/t-sql/data-types/datetime-transact-sql)|  
|datetime2|[datetime2 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetime2-transact-sql)|  
|smalldatetime|[smalldatetime &#40;Transact-SQL&#41;](/sql/t-sql/data-types/smalldatetime-transact-sql)|  
  
 **バイナリ データ型**  
  
|データ型|詳細情報|  
|---------------|--------------------------|  
|bit|[bit &#40;Transact-SQL&#41;](/sql/t-sql/data-types/bit-transact-sql)|  
|binary(n)|[binary と varbinary &#40;Transact-SQL&#41;](/sql/t-sql/data-types/binary-and-varbinary-transact-sql)|  
|varbinary(n) <sup>1</sup>|[binary と varbinary &#40;Transact-SQL&#41;](/sql/t-sql/data-types/binary-and-varbinary-transact-sql)|  
  
 <sup>1</sup>制限では、1 行の合計、8,060 バイトの可変長型の (n) をカウントします。  
  
 **他のデータ型**  
  
|データ型|詳細情報|  
|---------------|--------------------------|  
|UNIQUEIDENTIFIER|[uniqueidentifier &#40;Transact-SQL&#41;](/sql/t-sql/data-types/uniqueidentifier-transact-sql)|  
  
 **サポートされていないデータ型**  
  
 次のデータ型はサポートされません。  
  
||||  
|-|-|-|  
|DATETIMEOFFSET|GEOGRAPHY|GEOMETRY|  
|HIERARCHYID|ラージ オブジェクト (LOB)。 例: varchar(max)、nvarchar(max)、varbinary(max)、image、xml、text、ntext。|ROWVERSION|  
|sql_variant|CLR 関数|UDT (ユーザー定義型)|  
  
## <a name="see-also"></a>参照  
 [Transact-SQL によるインメモリ OLTP のサポート](transact-sql-support-for-in-memory-oltp.md)   
 [メモリ最適化テーブルへの LOB 列の実装](../../database-engine/implementing-lob-columns-in-a-memory-optimized-table.md)   
 [メモリ最適化テーブルへの SQL_VARIANT の実装](implementing-sql-variant-in-a-memory-optimized-table.md)  
  
  
