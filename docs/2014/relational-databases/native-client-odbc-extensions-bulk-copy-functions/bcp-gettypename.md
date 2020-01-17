---
title: bcp_gettypename による |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_gettypename
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_gettypename function
ms.assetid: 65f036d1-f60e-4b8a-97b3-76fccf0dfed4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5bc7caa063d14967e576fd009a23110b9647836b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62689027"
---
# <a name="bcpgettypename"></a>bcp_gettypename
  指定された BCP 型トークンの SQL 型名を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
RETCODE bcp_gettypename (  
INT   
token  
,  
DBBOOL   
fIsMaxType  
);  
  
```  
  
## <a name="arguments"></a>引数  
 *token*  
 BCP 型トークンを示す値です。  
  
 *field*  
 要求されたトークンが max 型かどうかを示します。  
  
## <a name="returns"></a>戻り値  
 BCP 型に対応する SQL 型名を含む文字列を返します。 無効な BCP 型が指定されると、空文字列を返します。  
  
## <a name="remarks"></a>コメント  
 BCP 型トークンは、sqlncli.h ヘッダー ファイルと sqlncli11.lib ライブラリで定義されています。  
  
 次の表では、指定できる BCP 型、それらの BCP 型が max 型かどうか、および予想される出力を示しています。  
  
|BCP 型名|MaxType|[出力]|  
|-------------------|-------------|------------|  
|`SQLDECIMAL`|接続前/接続後|**decimal**|  
|`SQLNUMERIC`|接続前/接続後|**numeric**|  
|`SQLINT1`|接続前/接続後|**tinyint**|  
|`SQLINT2`|接続前/接続後|**smallint**|  
|`SQLINT4`|接続前/接続後|**int**|  
|`SQLMONEY`|接続前/接続後|**money**|  
|`SQLFLT8`|接続前/接続後|**float**|  
|`SQLDATETIME`|接続前/接続後|**datetime**|  
|`SQLBITN`|接続前/接続後|**bit-null**|  
|`SQLBIT`|接続前/接続後|**bit**|  
|`SQLBIGCHAR`|いいえ|**char**|  
|`SQLCHARACTER`|いいえ|**char**|  
|`SQLBIGVARCHAR`|いいえ|**varchar**|  
|`SQLVARCHAR`|いいえ|**varchar**|  
|`SQLTEXT`|接続前/接続後|**text**|  
|`SQLBIGBINARY`|いいえ|**[バイナリ]**|  
|`SQLBINARY`|いいえ|**Binary**|  
|`SQLBIGVARBINARY`|いいえ|**varbinary**|  
|`SQLVARBINARY`|いいえ|**varbinary**|  
|`SQLIMAGE`|接続前/接続後|**[イメージ]**|  
|`SQLINTN`|接続前/接続後|**int-null**|  
|`SQLDATETIMN`|接続前/接続後|**datetime-null**|  
|`SQLMONEYN`|接続前/接続後|**money-null**|  
|`SQLFLTN`|接続前/接続後|**float-null**|  
|`SQLAOPSUM`|接続前/接続後|**Sum**|  
|`SQLAOPAVG`|接続前/接続後|**Avg**|  
|`SQLAOPCNT`|接続前/接続後|**Count**|  
|`SQLAOPMIN`|接続前/接続後|**Min**|  
|`SQLAOPMAX`|接続前/接続後|**Max**|  
|`SQLDATETIM4`|接続前/接続後|**smalldatetime**|  
|`SQLMONEY4`|接続前/接続後|**smallmoney**|  
|`SQLFLT4`|接続前/接続後|**本当の**|  
|`SQLUNIQUEID`|接続前/接続後|**uniqueidentifier**|  
|`SQLNCHAR`|いいえ|**nchar**|  
|`SQLNVARCHAR`|いいえ|**Nvarchar**|  
|`SQLNTEXT`|接続前/接続後|**ntext**|  
|`SQLVARIANT`|接続前/接続後|**sql_variant**|  
|`SQLINT8`|接続前/接続後|**Bigint**|  
|`SQLCHARACTER`|はい|**varchar(max)**|  
|`SQLBIGCHAR`|はい|**varchar(max)**|  
|`SQLBIGVARCHAR`|はい|**varchar(max)**|  
|`SQLVARCHAR`|はい|**varchar(max)**|  
|`SQLBINARY`|はい|**varbinary(max)**|  
|`SQLBIGBINARY`|はい|**varbinary(max)**|  
|`SQLBIGVARBINARY`|はい|**varbinary(max)**|  
|`SQLVARBINARY`|はい|**varbinary(max)**|  
|`SQLNCHAR`|はい|**nvarchar(max)**|  
|`SQLNVARCHAR`|はい|**nvarchar(max)**|  
|`SQLXML`|はい|**Xml**|  
|`SQLUDT`|接続前/接続後|**Udt**|  
  
## <a name="bcpgettypename-support-for-enhanced-date-and-time-features"></a>bcp_gettypename による機能強化された日付と時刻のサポート  
 内のテーブルの「sqlncli.h の型」列の日付/時刻型のトークンのパラメーターの値が説明されている[強化された日付と時刻型向けの一括コピーの変更&#40;OLE DB および ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)します。 返される値は、対応する行の "ファイル ストレージ型" 列に示されています。  
  
 詳細については、次を参照してください。[日付と時刻の強化&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)します。  
  
## <a name="see-also"></a>参照  
 [一括コピー関数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
