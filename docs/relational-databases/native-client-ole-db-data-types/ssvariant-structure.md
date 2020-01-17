---
title: SSVARIANT 構造体 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
ms.assetid: d13c6aa6-bd49-467a-9093-495df8f1e2d9
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2298bbbfcdb4c0245d9b932152c21f39d7e884f0
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73770747"
---
# <a name="ssvariant-structure"></a>SSVARIANT 構造体
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Sqlncli で定義されている**Ssvariant**構造体は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client OLEDB プロバイダーの DBTYPE_SQLVARIANT 値に対応します。  
  
 **Ssvariant**は識別 union です。 vt メンバーの値に応じて、コンシューマーは読み取るメンバーを決めることができます。 vt 値は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型に対応します。 したがって、**SSVARIANT** 構造体には、任意の SQL Server 型を格納できます。 標準 OLE DB 型のデータ構造の詳細については、「[型インジケーター](https://go.microsoft.com/fwlink/?LinkId=122171)」を参照してください。  
  
## <a name="remarks"></a>解説  
 DataTypeCompat==80 の場合、いくつかの **SSVARIANT** サブタイプが文字列になります。 たとえば、次の vt 値は **SSVARIANT** では VT_SS_WVARSTRING として表されます。  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 DateTypeCompat == 0 の場合、これらの型はネイティブ形式で表されます。  
  
 SSPROP_INIT_DATATYPECOMPATIBILITY の詳細については、「 [SQL Server Native Client での接続文字列キーワードの使用](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
 Sqlncli ファイルには、 **ssvariant**構造体内のメンバー型の逆参照を簡略化するバリアントアクセスマクロが含まれています。 たとえば、V_SS_DATETIMEOFFSET を次のように使用できます。  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 **Ssvariant**構造体の各メンバーの access マクロの完全なセットについては、sqlncli ファイルを参照してください。  
  
 次の表で、**SSVARIANT** 構造体のメンバーについて説明します。  
  
|メンバー|OLE DB 型インジケーター|OLE DB C データ型|vt の値|コメント|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||**SSVARIANT** 構造体に格納される値の型を指定します。|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|**Tinyint**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型をサポートします。|  
|sShortIntVal|DBTYPE_I2|**SHORT**|**VT_SS_I2**|では、 **smallint**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。|  
|lIntVal|DBTYPE_I4|**LONG**|**VT_SS_I4**|**Int**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型をサポートします。|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|では、 **bigint**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|では、**実際**の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|**Float**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型をサポートします。|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|では、 **money**および**smallmoney**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|では、**ビット**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|では、 **uniqueidentifier**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|**数値**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型をサポートします。|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|**date**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型をサポートします。|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|では、 **smalldatetime**、 **datetime**、および**datetime2**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|では、 **time**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型をサポートしています。<br /><br /> 次のメンバーを含みます。<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bscale* (**BYTE**) *tTime2Val*値の小数点以下桁数を指定します。|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|では、 **datetime2**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。<br /><br /> 次のメンバーを含みます。<br /><br /> *tsDataTimeVal* (dbtimestamp)<br /><br /> *bscale* (**BYTE**) *tsDataTimeVal*値の小数点以下桁数を指定します。|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|では、 **datetimeoffset**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型をサポートしています。<br /><br /> 次のメンバーを含みます。<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bscale* (**BYTE**) *tsoDateTimeOffsetVal*値の小数点以下桁数を指定します。|  
|NCharVal|対応する OLE DB 型インジケーターはありません。|**構造体の _NCharVal**|**VT_SS_WVARSTRING、**<br /><br /> **VT_SS_WSTRING**|では、 **nchar**および**nvarchar**の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。<br /><br /> 次のメンバーを含みます。<br /><br /> *sActualLength* (**SHORT**) *pwchNCharVal*が指す文字列の実際の長さを指定します。 末尾の 0 は含まれません。<br /><br /> *Smaxlength* (**SHORT**) *pwchNCharVal*が指す文字列の最大長を指定します。<br /><br /> *pwchNCharVal* (**WCHAR** \*) 文字列へのポインター。<br /><br /> 使用されていないメンバー: *rgbReserved*、 *dwreserved*、および*pwchReserved*。|  
|CharVal|対応する OLE DB 型インジケーターはありません。|**構造体の _CharVal**|**VT_SS_STRING、**<br /><br /> **VT_SS_VARSTRING**|では、 **char**および**varchar**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。<br /><br /> 次のメンバーを含みます。<br /><br /> *sActualLength* (**SHORT**) *pchcharval*が指す文字列の実際の長さを指定します。 末尾の 0 は含まれません。<br /><br /> *Smaxlength* (**SHORT**) は、 *pchcharval*が指す文字列の最大長を指定します。<br /><br /> 文字列への*Pchcharval* (**CHAR** \*) ポインター。<br /><br /> 使用されないメンバー :<br /><br /> *rgbReserved*、 *dwreserved*、および*pwchReserved*。|  
|BinaryVal|対応する OLE DB 型インジケーターはありません。|**構造体の _BinaryVal**|**VT_SS_VARBINARY、**<br /><br /> **VT_SS_BINARY**|では、 **binary**および**varbinary**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型がサポートされています。<br /><br /> 次のメンバーを含みます。<br /><br /> *sActualLength* (**SHORT**) *prgbbinaryval*が指すデータの実際の長さを指定します。<br /><br /> *Smaxlength* (**SHORT**) は、 *prgbbinaryval*が指すデータの最大長を指定します。<br /><br /> *Prgbbinaryval* (**バイト**\*) バイナリデータへのポインター。<br /><br /> 未使用のメンバー: *Dwreserved*。|  
|UnknownType|未使用|未使用|未使用|未使用|  
|BLOBType|未使用|未使用|未使用|未使用|  
  
## <a name="see-also"></a>参照  
 [データ型&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
