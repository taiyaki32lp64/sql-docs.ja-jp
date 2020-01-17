---
title: パラメーターと行セットのメタデータ |Microsoft Docs
description: パラメーターと行セットのメタデータ
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- metadata [OLE DB]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 641859e134a5f3c3201f239023f911b79de1c11e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67995097"
---
# <a name="metadata---parameter-and-rowset"></a>メタデータ - パラメーターと行セット
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  この記事では、OLE DB の日付および時刻の機能強化に関連する、次の型と型メンバーについて説明します。  
  
-   DBBINDING 構造体  
  
-   **ICommandWithParameters::GetParameterInfo**  
  
-   **ICommandWithParameters::SetParameterInfo**  
  
-   **IColumnsRowset::GetColumnsRowset**  
  
-   **IColumnsInfo::GetColumnInfo**  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 *prgParamInfo* を使用して DBPARAMINFO 構造体に次の情報が返されます。  
  
|パラメーターの型|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|-------------------|------------------|--------------|-----------------------------------------------------|  
|date|DBTYPE_DBDATE|6|10|0|Clear|  
|time|DBTYPE_DBTIME2|10|8、10..16|0..7|オン|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19、21..27|0..7|オン|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26、28..34|0..7|オン|  
  
 場合によっては、値の範囲が連続していないことに注意してください。 有効桁数が 0 より大きい場合は、小数点が追加されるためです。  
  
 DBPARAMFLAGS_SS_ISVARIABLESCALE は、[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 以降のサーバーに接続されている場合にのみ有効です。 下位レベルのサーバーに接続されている場合は、DBPARAMFLAGS_SS_ISVARIABLESCALE は設定されません。  
  
## <a name="icommandwithparameterssetparameterinfo-and-implied-parameter-types"></a>ICommandWithParameters::SetParameterInfo と暗黙のパラメーターの型  
 DBPARAMBINDINFO 構造体で提供される情報は、次の表に準拠する必要があります。  
  
|*pwszDataSourceType*<br /><br /> (プロバイダー固有)|*pwszDataSourceType*<br /><br /> (OLE DB 汎用)|*ulParamSize*|*bScale*|  
|----------------------------------------------------|-------------------------------------------------|-------------------|--------------|  
||DBTYPE_DATE|6|無視|  
|date|DBTYPE_DBDATE|6|無視|  
||DBTYPE_DBTIME|10|無視|  
|time|DBTYPE_DBTIME2|10|0..7|  
|smalldatetime||16|無視|  
|DATETIME||16|無視|  
|datetime2 または DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|16|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|0..7|  
  
 *Bprecision*パラメーターは無視されます。  
  
 データをサーバーに送信する場合、"DBPARAMFLAGS_SS_ISVARIABLESCALE" は無視されます。 アプリケーションでは、プロバイダー固有の型名 "**datetime**" および "**smalldatetime**" を使用して、従来の表形式のデータ ストリーム (TDS) の型を強制的に使用することができます。 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (以降の) サーバーに接続されている場合、"**datetime2**" 形式が使用され、型名が "**datetime2**" または "DBTYPE_DBTIMESTAMP" の場合は、必要に応じて、暗黙的なサーバー変換が発生します。 プロバイダー固有の型名 "**datetime**" または "**smalldatetime**" が使用されている場合、 *bscale*は無視されます。 それ以外の場合、アプリケーションは*Bscale*が正しく設定されていることを確認する必要があります。 "DBTYPE_DBTIMESTAMP" を使用している MDAC および[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] OLE DB Driver for SQL Server からアップグレードされたアプリケーションは、 *bscale*を正しく設定しないと失敗します。 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] より前のサーバー インスタンスに接続されている場合は、"DBTYPE_DBTIMESTAMP" で 0 または 3 以外に設定された *bScale* の値はエラーになり、E_FAIL が返されます。  
  
 ICommandWithParameters:: SetParameterInfo が呼び出されない場合、プロバイダーは、次のように IAccessor:: CreateAccessor で指定されているように、バインドの種類からサーバーの種類を示します。  
  
|バインドの種類|*pwszDataSourceType*<br /><br /> (プロバイダー固有)|  
|------------------|----------------------------------------------------|  
|DBTYPE_DATE|datetime2(0)|  
|DBTYPE_DBDATE|date|  
|DBTYPE_DBTIME|time(0)|  
|DBTYPE_DBTIME2|time(7)|  
|DBTYPE_DBTIMESTAMP|datetime2(7)|  
|DBTYPE_DBTIMESTAMPOFFSET|datetimeoffset(7)|  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 **IColumnsRowset:: GetColumnsRowset**は、次の列を返します。  
  
|列の型|DBCOLUMN_TYPE|DBCOLUM_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE、DBCOLUMN_DATETIMEPRECISION|DBCOLUMN_FLAGS、DBCOLUMNFLAGS_SS_ISVARIABLESCALE|  
|-----------------|--------------------|-------------------------|-------------------------|--------------------------------------------------|---------------------------------------------------------|  
|date|DBTYPE_DBDATE|6|10|0|Clear|  
|time|DBTYPE_DBTIME2|10|8、10..16|0..7|オン|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19、21..27|0..7|オン|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26、28..34|0..7|オン|  
  
 DBCOLUMN_FLAGS では、DBCOLUMNFLAGS_ISFIXEDLENGTH は日付/時刻型に対して常に true になり、次のフラグは常に false になります。  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 その他のフラグ (DBCOLUMNFLAGS_ISNULLABLE、DBCOLUMNFLAGS_MAYBENULL、DBCOLUMNFLAGS_WRITE、および DBCOLUMNFLAGS_WRITEUNKNOWN) は、列の定義方法と実際のクエリに応じて設定できます。  
  
 DBCOLUMN_FLAGS に用意されている新しいフラグ DBCOLUMNFLAGS_SS_ISVARIABLESCALE を使用すると、アプリケーションは、DBCOLUMN_TYPE が DBTYPE_DBTIMESTAMP である列のサーバーの種類を判断できます。 サーバーの種類を識別するには、DBCOLUMN_SCALE または DBCOLUMN_DATETIMEPRECISION も使用する必要があります。  
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE は [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 以降のサーバーに接続されている場合にのみ有効です。 下位レベルのサーバーに接続されている場合、DBCOLUMNFLAGS_SS_ISVARIABLESCALE は未定義となります。  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 DBCOLUMNINFO 構造体から次の情報が返されます。  
  
|パラメーターの型|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------------------|  
|date|DBTYPE_DBDATE|6|10|0|Clear|  
|time(1..7)|DBTYPE_DBTIME2|10|8、10..16|0..7|オン|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19、21..27|0..7|オン|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26、28..34|0..7|オン|  
  
 *dwFlags* では、DBCOLUMNFLAGS_ISFIXEDLENGTH は日付/時刻型に対して常に true になり、次のフラグは常に false になります。  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER、MAYDEFER  
  
 その他のフラグ (DBCOLUMNFLAGS_ISNULLABLE、DBCOLUMNFLAGS_MAYBENULL、DBCOLUMNFLAGS_WRITE、および DBCOLUMNFLAGS_WRITEUNKNOWN) は、設定することができます。  
  
 *dwFlags* に用意されている新しいフラグ DBCOLUMNFLAGS_SS_ISVARIABLESCALE を使用すると、アプリケーションは、*wType* が DBTYPE_DBTIMESTAMP である列のサーバーの種類を判断できます。 サーバーの種類を識別するには、*bScale* も使用する必要があります。  
  
## <a name="see-also"></a>参照  
 [OLE DB の日付/時刻の強化に対するデータ型のサポート](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
  
  
