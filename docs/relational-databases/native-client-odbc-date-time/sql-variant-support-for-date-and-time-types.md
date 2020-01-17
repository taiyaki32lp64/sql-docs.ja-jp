---
title: 日付型と時刻型のサポートの sql_variantMicrosoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sql_variant data type
ms.assetid: 12ff1ea6-e2cc-40e6-910c-3126974a90b3
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f795f1848f3e4c9fe1239df79677c35c38ba3b58
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73783510"
---
# <a name="sql_variant-support-for-date-and-time-types"></a>sql_variant による日付型と時刻型のサポート
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  このトピックでは、 **sql_variant**データ型が、強化された日付と時刻の機能をサポートする方法について説明します。  
  
 SQL_CA_SS_VARIANT_TYPE 列属性は、バリアント型結果列の C 型を返すために使用されます。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] には、追加の属性 SQL_CA_SS_VARIANT_SQL_TYPE が導入されています。この属性は、実装行記述子 (IRD) のバリアント結果列の SQL 型を設定します。 SQL_CA_SS_VARIANT_SQL_TYPE を実装パラメーター記述子 (IPD) で使用して、型 SQL_SS_VARIANT で SQL_C_BINARY C 型にバインドされている SQL_SS_TIME2 または SQL_SS_TIMESTAMPOFFSET パラメーターの SQL 型を指定することもできます。  
  
 新しい型 SQL_SS_TIME2 と SQL_SS_TIMESTAMPOFFSET は、SQLColAttribute によって設定できます。 SQL_CA_SS_VARIANT_SQL_TYPE は、SQLGetDescField で返すことができます。  
  
 結果列については、ドライバーによってバリアント型から日付型または時刻型に変換されます。 詳細については、「 [SQL から C への変換](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)」を参照してください。SQL_C_BINARY にバインドする場合、バッファーの長さは、SQL 型に対応する構造体を受け取るのに十分な大きさである必要があります。  
  
 次の表で説明するように、ドライバーは、SQL_SS_TIME2 パラメーターと SQL_SS_TIMESTAMPOFFSET パラメーターに対して C 値を**sql_variant**値に変換します。 パラメーターが SQL_C_BINARY としてバインドされ、かつ、サーバー型が SQL_SS_VARIANT である場合、アプリケーションで SQL_CA_SS_VARIANT_SQL_TYPE が別の SQL 型に設定されていない限り、バイナリ値として扱われます。 この場合は、SQL_CA_SS_VARIANT_SQL_TYPE が優先されます。つまり、SQL_CA_SS_VARIANT_SQL_TYPE が設定されている場合、C 型からバリアントの SQL 型を推定するという既定の動作がオーバーライドされます。  
  
|C 型|サーバーの種類|コメント|  
|------------|-----------------|--------------|  
|SQL_C_CHAR|varchar|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_WCHAR|nvarcar|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_TINYINT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_STINYINT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_SHORT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_SSHORT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_USHORT|int|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_LONG|int|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_SLONG|int|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_ULONG|bigint|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_SBIGINT|bigint|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_FLOAT|real|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_DOUBLE|float|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_BIT|bit|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_UTINYINT|tinyint|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_BINARY|varbinary|SQL_CA_SS_VARIANT_SQL_TYPE は設定されません。|  
|SQL_C_BINARY|time|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIME2<br /><br /> Scale は SQL_DESC_PRECISION ( **SQLBindParameter**の*DecimalDigits*パラメーター) に設定されます。|  
|SQL_C_BINARY|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIMESTAMPOFFSET<br /><br /> Scale は SQL_DESC_PRECISION ( **SQLBindParameter**の*DecimalDigits*パラメーター) に設定されます。|  
|SQL_C_TYPE_DATE|date|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_TYPE_TIME|time(0)|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_TYPE_TIMESTAMP|datetime2|Scale は SQL_DESC_PRECISION ( **SQLBindParameter**の*DecimalDigits*パラメーター) に設定されます。|  
|SQL_C_NUMERIC|DECIMAL|有効桁数が SQL_DESC_PRECISION ( **SQLBindParameter**の*columnsize*パラメーター) に設定されています。<br /><br /> スケールセットを SQL_DESC_SCALE (SQLBindParameter の*DecimalDigits*パラメーター) に設定します。|  
|SQL_C_SS_TIME2|time|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
|SQL_C_SS_TIMESTAMPOFFSET|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE は無視されます。|  
  
## <a name="see-also"></a>参照  
 [日付と時刻の&#40;機能強化 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
