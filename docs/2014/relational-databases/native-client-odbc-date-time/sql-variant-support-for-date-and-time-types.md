---
title: sql_variant による日付と時刻型向けのサポート |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sql_variant data type
ms.assetid: 12ff1ea6-e2cc-40e6-910c-3126974a90b3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0cbde879e2b7f215c5044936dfbdacab9196f02d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63215964"
---
# <a name="sql_variant-support-for-date-and-time-types"></a>sql_variant による日付型と時刻型のサポート
  このトピックでは、日付と時刻に関する `sql_variant` データ型の機能強化について説明します。  
  
 SQL_CA_SS_VARIANT_TYPE 列属性は、バリアント型結果列の C 型を返すために使用されます。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SQL_CA_SS_VARIANT_SQL_TYPE は、実装行記述子 (IRD) 内のバリアント型結果列の SQL 型を設定する、追加の属性について説明します。 SQL_SS_VARIANT 型で SQL_C_BINARY C 型を持つ SQL_SS_TIMESTAMPOFFSET パラメーターがバインドされているまたは SQL_SS_TIME2 の SQL 型を指定する実装パラメーター記述子 (IPD) で SQL_CA_SS_VARIANT_SQL_TYPE が使用こともできます。  
  
 SQLColAttribute によって SQL_SS_TIME2 および SQL_SS_TIMESTAMPOFFSET、新しい型を設定できます。 SQL_CA_SS_VARIANT_SQL_TYPE は、SQLGetDescField によって返されることができます。  
  
 結果列については、ドライバーによってバリアント型から日付型または時刻型に変換されます。 詳細については、次を参照してください。 [SQL から C への変換](datetime-data-type-conversions-from-sql-to-c.md)します。SQL_C_BINARY へのバインドでは、バッファー長は、SQL 型に対応する構造体を受け取るのに十分な大きさである必要があります。  
  
 SQL_SS_TIME2 パラメーターおよび SQL_SS_TIMESTAMPOFFSET パラメーターについては、次の表に示すように、ドライバーによって C 値が `sql_variant` 値に変換されます。 パラメーターが SQL_C_BINARY としてバインドされ、かつ、サーバー型が SQL_SS_VARIANT である場合、アプリケーションで SQL_CA_SS_VARIANT_SQL_TYPE が別の SQL 型に設定されていない限り、バイナリ値として扱われます。 この場合は、SQL_CA_SS_VARIANT_SQL_TYPE が優先されます。つまり、SQL_CA_SS_VARIANT_SQL_TYPE が設定されている場合、C 型からバリアントの SQL 型を推定するという既定の動作がオーバーライドされます。  
  
|C 型|サーバーの種類|コメント|  
|------------|-----------------|--------------|  
|SQL_C_CHAR|varchar|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_WCHAR|nvarcar|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_TINYINT|SMALLINT|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_STINYINT|SMALLINT|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_SHORT|SMALLINT|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_SSHORT|SMALLINT|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_USHORT|int|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_LONG|int|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_SLONG|int|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_ULONG|BIGINT|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_SBIGINT|BIGINT|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_FLOAT|REAL|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_DOUBLE|FLOAT|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_BIT|bit|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_UTINYINT|TINYINT|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_BINARY|varbinary|SQL_CA_SS_VARIANT_SQL_TYPE は設定されません。|  
|SQL_C_BINARY|time|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIME2<br /><br /> スケール セットは SQL_DESC_PRECISION (、 *DecimalDigits*パラメーターの`SQLBindParameter`)。|  
|SQL_C_BINARY|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIMESTAMPOFFSET<br /><br /> スケール セットは SQL_DESC_PRECISION (、 *DecimalDigits*パラメーターの`SQLBindParameter`)。|  
|SQL_C_TYPE_DATE|日付|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_TYPE_TIME|time(0)|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_TYPE_TIMESTAMP|datetime2|スケール セットは SQL_DESC_PRECISION (、 *DecimalDigits*パラメーターの`SQLBindParameter`)。|  
|SQL_C_NUMERIC|Decimal|有効桁数は SQL_DESC_PRECISION に設定されます (、 *ColumnSize*パラメーターの`SQLBindParameter`)。<br /><br /> スケール セットの SQL_DESC_SCALE (、 *DecimalDigits* SQLBindParameter のパラメーター)。|  
|SQL_C_SS_TIME2|time|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_SS_TIMESTAMPOFFSET|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
  
## <a name="see-also"></a>参照  
 [日付と時刻の強化&#40;ODBC&#41;](date-and-time-improvements-odbc.md)  
  
  
