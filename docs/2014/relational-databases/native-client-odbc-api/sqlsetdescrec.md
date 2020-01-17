---
title: SQLSetDescRec |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetDescRec function
ms.assetid: 203d02a2-aa09-462b-a489-a2cdd6f6023b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d323b1b92ba02e55064d2f86c62ee36a4a38d904
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188783"
---
# <a name="sqlsetdescrec"></a>SQLSetDescRec
  このトピックで説明する固有の sqlsetdescrec による機能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client。  
  
## <a name="sqlsetdescrec-and-table-valued-parameters"></a>SQLSetDescRec とテーブル値パラメーター  
 SQLSetDescRec とテーブル値パラメーターおよびテーブル値パラメーター列の記述子フィールドを設定するのに使用できます。 テーブル値パラメーター列は、記述子のヘッダー フィールド SQL_SOPT_SS_PARAM_FOCUS に、SQL_DESC_TYPE が SQL_SS_TABLE に設定されているレコードの序数が設定される場合のみ使用できます。 SQL_SOPT_SS_PARAM_FOCUS の詳細については、次を参照してください。 [SQLSetStmtAttr](sqlsetstmtattr.md)します。  
  
 次の表では、パラメーターと記述子フィールド間のマッピングについて説明します。  
  
|パラメーター|非テーブル値パラメーターの型を使用して、テーブル値パラメーターの列を含む関連する属性|テーブル値パラメーターに関連する属性|  
|---------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------|  
|*型*|SQL_DESC_TYPE|SQL_SS_TABLE|  
|*SubType*|無視|SQL_DATETIME 型または SQL_INTERVAL 型のレコードの場合は、これに SQL_DESC_DATETIME_INTERVAL_CODE を設定します。|  
|*Length*|SQL_DESC_OCTET_LENGTH|テーブル値パラメーターの型名の長さ。 終了すると、型名が null または 0 場合、テーブル値パラメーターの名前を入力する必要はない場合は、SQL_NTS にできます。|  
|*Precision*|SQL_DESC_PRECISION|SQL_DESC_ARRAY_SIZE|  
|*Scale*|SQL_DESC_SCALE|未使用。 このパラメーターは 0 にする必要があります。|  
|*DataPtr*|APD の SQL_DESC_DATA_PTR|SQL_CA_SS_TYPE_NAME<br /><br /> このパラメーターは、ストアド プロシージャの呼び出しでは省略可能で、不要の場合は NULL を指定できます。 このパラメーターは、プロシージャの呼び出し以外の SQL ステートメント用に指定する必要があります。<br /><br /> *DataPtr*アプリケーションは、可変の行バインドを使用する場合は、このテーブル値パラメーターを識別するために使用できる一意の値としても機能します。|  
|*StringLengthPtr*|SQL_DESC_OCTET_LENGTH_PTR|SQL_DESC_OCTET_LENGTH_PTR<br /><br /> テーブル値パラメーターの場合、これは転送する行数または SQL_DATA_AT_EXEC です。 これは、SQLExecDirect で転送する行数を保持する値へのポインターです。|  
|*IndicatorPtr*|SQL_DESC_INDICATOR_PTR|SQL_DESC_INDICATOR_PTR|  
  
 テーブル値パラメーターの詳細については、次を参照してください。[テーブル値パラメーター &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)します。  
  
## <a name="sqlsetdescrec-support-for-enhanced-date-and-time-features"></a>SQLSetDescRec による機能強化された日付と時刻のサポート  
 日付型または時刻型に対して許可される値を次に示します。  
  
||*型*|*SubType*|*Length*|*Precision*|*Scale*|  
|-|------------|---------------|--------------|-----------------|-------------|  
|DATETIME|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|日付|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 詳細については、次を参照してください。[日付と時刻の強化&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)します。  
  
## <a name="sqlsetdescrec-support-for-large-clr-udts"></a>SQLSetDescRec による大きな CLR UDT のサポート  
 `SQLSetDescRec` は、大きな CLR ユーザー定義型 (UDT) をサポートしています。 詳細については、次を参照してください。 [Large CLR User-Defined 型&#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md)します。  
  
## <a name="see-also"></a>参照  
 [SQLSetDescRec](https://go.microsoft.com/fwlink/?LinkId=80704)   
 [ODBC API 実装の詳細](odbc-api-implementation-details.md)  
  
  
