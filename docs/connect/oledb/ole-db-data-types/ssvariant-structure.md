---
title: SSVARIANT 構造体 |Microsoft Docs
description: OLE DB Driver for SQL Server の SSVARIANT 構造
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 09ff4af7026ce75a8668db22910e550dc0c72857
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67995170"
---
# <a name="ssvariant-structure"></a>SSVARIANT 構造体
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Msoledbsql で定義されている**Ssvariant**構造体は、SQL Server の OLE DB ドライバーの DBTYPE_SQLVARIANT 値に対応しています。  
  
 **Ssvariant**は識別 union です。 vt メンバーの値に応じて、コンシューマーは読み取るメンバーを決めることができます。 vt 値は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型に対応します。 したがって、**SSVARIANT** 構造体には、任意の SQL Server 型を格納できます。 標準 OLE DB 型のデータ構造の詳細については、「[型インジケーター](https://go.microsoft.com/fwlink/?LinkId=122171)」を参照してください。  
  
## <a name="remarks"></a>Remarks  
 DataTypeCompat==80 の場合、いくつかの **SSVARIANT** サブタイプが文字列になります。 たとえば、次の vt 値は **SSVARIANT** では VT_SS_WVARSTRING として表されます。  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 DateTypeCompat == 0 の場合、これらの型はネイティブ形式で表されます。  
  
 SSPROP_INIT_DATATYPECOMPATIBILITY の詳細については、「 [OLE DB Driver for SQL Server」の「接続文字列キーワードの使用](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)」を参照してください。  
  
 msoledbsql.h ファイルには、**SSVARIANT** 構造体のメンバー型の逆参照を単純化するバリアント アクセス マクロが格納されています。 たとえば、V_SS_DATETIMEOFFSET を次のように使用できます。  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 **Ssvariant**構造体の各メンバーの access マクロの完全なセットについては、msoledbsql ファイルを参照してください。  
  
 次の表で、**SSVARIANT** 構造体のメンバーについて説明します。  
  
|メンバー|OLE DB 型インジケーター|OLE DB C データ型|vt の値|コメント|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||**SSVARIANT** 構造体に格納される値の型を指定します。|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|**Tinyint**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型をサポートします。|  
|sShortIntVal|DBTYPE_I2|**SHORT**|**VT_SS_I2**|では、 **smallint** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型がサポートされています。|  
|lIntVal|DBTYPE_I4|**LONG**|**VT_SS_I4**|**Int**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型をサポートします。|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|では、 **bigint** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型がサポートされています。|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|では、 **real** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型がサポートされています。|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|**Float**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型をサポートします。|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|では、 **money**データ型と**smallmoney** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型がサポートされています。|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|では、 **bit** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型がサポートされています。|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|では、 **uniqueidentifier** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型がサポートされています。|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|**数値**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型をサポートします。|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|**date**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型をサポートします。|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|では、 **smalldatetime**、 **datetime**、および**datetime2** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型がサポートされています。|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|では、 **time** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型がサポートされています。<br /><br /> 次のメンバーを含みます。<br /><br /> *tTime2Val*(**DBTIME2**)<br /><br /> *Bscale*(**バイト**)*TTime2Val*値の小数点以下桁数を指定します。|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|では、 **datetime2** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型がサポートされています。<br /><br /> 次のメンバーを含みます。<br /><br /> *tsDataTimeVal*DBTIMESTAMP<br /><br /> *Bscale*(**バイト**)*TsDataTimeVal*値の小数点以下桁数を指定します。|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|では、 **datetimeoffset** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型がサポートされています。<br /><br /> 次のメンバーを含みます。<br /><br /> *tsoDateTimeOffsetVal*(**DBTIMESTAMPOFFSET**)<br /><br /> *Bscale*(**バイト**)*TsoDateTimeOffsetVal*値の小数点以下桁数を指定します。|  
|NCharVal|対応する OLE DB 型インジケーターはありません。|**構造体 Ncharval**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|では、 **nchar**および**nvarchar** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型がサポートされています。<br /><br /> 次のメンバーを含みます。<br /><br /> *sActualLength*(**短い**)*PwchNCharVal*が指す文字列の実際の長さを指定します。 末尾の 0 は含まれません。<br /><br /> *Smaxlength*(**短い**)*PwchNCharVal*が指す文字列の最大長を指定します。<br /><br /> *pwchNCharVal*(**WCHAR** \*) 文字列へのポインター。<br /><br /> 使用されていないメンバー: *rgbReserved*、 *dwreserved*、および*pwchReserved*。|  
|CharVal|対応する OLE DB 型インジケーターはありません。|**構造体 Charval**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|では、 **char**および**varchar** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型がサポートされています。<br /><br /> 次のメンバーを含みます。<br /><br /> *sActualLength*(**短い**)*Pchcharval*が指す文字列の実際の長さを指定します。 末尾の 0 は含まれません。<br /><br /> *Smaxlength*(**短い**)*Pchcharval*が指す文字列の最大長を指定します。<br /><br /> *Pchcharval*(**CHAR** \*) 文字列へのポインター。<br /><br /> 使用されないメンバー :<br /><br /> *rgbReserved*、 *dwreserved*、および*pwchReserved*。|  
|BinaryVal|対応する OLE DB 型インジケーターはありません。|**構造体 Binaryval (_t)**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|では、 **binary**および**varbinary** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型がサポートされています。<br /><br /> 次のメンバーを含みます。<br /><br /> *sActualLength*(**短い**)*Prgbbinaryval*が指すデータの実際の長さを指定します。<br /><br /> *Smaxlength*(**短い**)*Prgbbinaryval*が指すデータの最大長を指定します。<br /><br /> *Prgbbinaryval*(**BYTE** \*) バイナリデータへのポインター。<br /><br /> 未使用のメンバー: *Dwreserved*。|  
|UnknownType|未使用|未使用|未使用|未使用|  
|BLOBType|未使用|未使用|未使用|未使用|  
  
## <a name="see-also"></a>参照  
 [データ型&#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
