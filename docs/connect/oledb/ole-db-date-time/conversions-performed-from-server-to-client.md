---
title: サーバーからクライアントへの変換 |Microsoft Docs
description: サーバーからクライアントへの変換
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB], server to client
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 22f3b681f9c4256087c17bd1e74011c2ba0916fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015809"
---
# <a name="conversions-performed-from-server-to-client"></a>サーバーからクライアントへの変換
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  この記事では、[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (以降) と OLE DB Driver for SQL Server を使用して作成されたクライアント アプリケーションとの間で実行される日付または時刻の変換について説明します。  
  
## <a name="conversions"></a>コンバージョン  
 次の表では、クライアントに返される型とバインドの型との間の変換について説明しています。 出力パラメーターの場合、ICommandWithParameters:: SetParameterInfo が呼び出され、 *pwszDataSourceType*で指定された型がサーバー上の実際の型と一致しない場合、サーバーによって暗黙的な変換が実行され、返された型が返されます。クライアントは、ICommandWithParameters:: SetParameterInfo によって指定された型と一致します。 これにより、サーバーの変換規則がこの記事の内容と異なると、予期しない変換結果が発生する場合があります。 たとえば、既定の日付を指定する必要がある場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では 1899-12-30 ではなく 1900-1-1 が使用されます。  
  
|To -><br /><br /> From|DATE|DBDATE|DBTIME|DBTIME2|DBTIMESTAMP|DBTIMESTAMPOFFSET|FILETIME|BYTES|VARIANT|SSVARIANT|BSTR|STR|WSTR|  
|----------------------|----------|------------|------------|-------------|-----------------|-----------------------|--------------|-----------|-------------|---------------|----------|---------|----------|  
|date|1、7|[OK]|-|-|1|1、3|1、7|-|[OK] \(VT_BSTR)|[OK]|[OK]|4|4|  
|Time|5、6、7|-|9|[OK]|6|3、6|5、6|-|[OK] \(VT_BSTR)|[OK]|[OK]|4|4|  
|Smalldatetime|7|8|9、10|10|[OK]|3|7|-|7 (VT_DATE)|[OK]|[OK]|4|4|  
|DATETIME|5、7|8|9、10|10|[OK]|3|7|-|7 (VT_DATE)|[OK]|[OK]|4|4|  
|Datetime2|5、7|8|9、10|10|7|3|5、7|-|[OK]\ (VT_BSTR)|[OK]|[OK]|4|4|  
|Datetimeoffset|5、7、11|8、11|9、10、11|10、11|7、11|[OK]|5、7、11|-|[OK]\ (VT_BSTR)|[OK]|[OK]|4|4|  
|Char、Varchar、<br /><br /> Nchar、Nvarchar|7、13|12|12、9|12|12|12|7、13|なし|なし|なし|なし|なし|なし|  
|Sql_variant<br /><br /> (datetime)|7|8|9、10|10|[OK]|3|7|-|7 (VT_DATE)|[OK]|[OK]|4|4|  
|Sql_variant<br /><br /> (smalldatetime)|7|8|9、10|10|[OK]|3|7|-|7 (VT_DATE)|[OK]|[OK]|4|4|  
|Sql_variant<br /><br /> (date)|1、7|[OK]|2|2|1|1、3|1、7|-|OK (VT_BSTR)|[OK]|[OK]|4|4|  
|Sql_variant<br /><br /> (time)|5、6、7|2|6|[OK]|6|3、6|5、6|-|OK (VT_BSTR)|[OK]|[OK]|4|4|  
|Sql_variant<br /><br /> (datetime2)|5、7|8|9、10|10|[OK]|3|5、7|-|OK (VT_BSTR)|[OK]|[OK]|4|4|  
|Sql_variant<br /><br /> (datetimeoffset)|5、7、11|8、11|9、10、11|10、11|7、11|[OK]|5、7、11|-|OK (VT_BSTR)|[OK]|[OK]|4|4|  
  
## <a name="key-to-symbols"></a>記号の説明  
  
|Symbol|意味|  
|------------|-------------|  
|[OK]|変換は必要ありません。|  
|-|変換はサポートされていません。 IAccessor:: CreateAccessor が呼び出されたときにバインディングが検証されると、DBBINDSTATUS_UPSUPPORTEDCONVERSION が*rgStatus*に返されます。 アクセサー検証が遅延する場合は、DBSTATUS_E_BADACCESSOR が設定されます。|  
|1|時刻フィールドに 0 が設定されます。|  
|2|DBSTATUS_E_CANTCONVERTVALUE が設定されます。|  
|3|タイムゾーンは 0 に設定されます。|  
|4|クライアント バッファーのサイズが十分でない場合、DBSTATUS_S_TRUNCATED が設定されます。 サーバーの型に秒の小数部が含まれている場合、結果文字列の桁数はサーバーの型の小数点以下桁数と完全に一致します。|  
|5|秒または秒の小数部の切り捨ては無視されます。|  
|6|日付は現在の日付に設定されます。ただし、変換元が時間の文字列リテラルで、変換先が DBTYPE_DATE の場合は別です。 この場合、1899-12-30 が使用されます。|  
|7|値がオーバーフローする場合は、DBSTATUS_E_DATAOVERFLOW が設定されます。|  
|8|時刻フィールドは無視されます。|  
|9|秒の小数部のフィールドは無視されます。|  
|10|日付部分は無視されます。|  
|11|時刻はクライアントのタイム ゾーンに変換されます。 この変換中にエラーが発生した場合、DBSTATUS_E_DATAOVERFLOW が設定されます。|  
|12|文字列は ISO リテラルとして解析され、対象の型に変換されます。 これが失敗すると、文字列は OLE 日付リテラル (時刻要素も含む) として解析され、OLE Date (DBTYPE_DATE) から対象の型に変換されます。 文字列は、ISO 形式の解析を成功させるために許可された対象の型のリテラルの構文に準拠している必要があります。 OLE での解析を成功させるには、文字列は OLE で認識される構文に準拠している必要があります。 文字列を解析できない場合は、DBSTATUS_E_CANTCONVERTVALUE が設定されます。 任意の部分の値が範囲外の場合は、DBSTATUS_E_DATAOVERFLOW が設定されます。|  
|13|文字列は ISO リテラルとして解析され、対象の型に変換されます。 これが失敗すると、文字列は OLE 日付リテラル (時刻要素も含む) として解析され、OLE Date (DBTYPE_DATE) から対象の型に変換されます。 文字列は datetime リテラルの構文に準拠している必要があります。ただし、変換先が DBTYPE_DATE または DBTYPE_DBTIMESTAMP の場合は別です。 この場合、ISO 形式の解析を成功させるために、datetime リテラルまたは時刻リテラルが許容されています。 OLE での解析を成功させるには、文字列は OLE で認識される構文に準拠している必要があります。 文字列を解析できない場合は、DBSTATUS_E_CANTCONVERTVALUE が設定されます。 任意の部分の値が範囲外の場合は、DBSTATUS_E_DATAOVERFLOW が設定されます。|  
  
## <a name="see-also"></a>参照  
 [バインドと変換 &#40;OLE DB&#41;](../../oledb/ole-db-date-time/conversions-ole-db.md)  
  
  
