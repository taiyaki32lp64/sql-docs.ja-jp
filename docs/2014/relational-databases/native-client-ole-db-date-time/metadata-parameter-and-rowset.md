---
title: パラメーターと行セットのメタデータ |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- metadata [OLE DB]
ms.assetid: 31b318a4-20e7-4db0-b367-eb9938859029
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b96876a050f9ba46363792eec22d76640ee6fc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62655628"
---
# <a name="parameter-and-rowset-metadata"></a>パラメーターと行セットのメタデータ
  このトピックでは、OLE DB の日付および時刻の機能強化に関連する、次の型と型メンバーについて説明します。  
  
-   DBBINDING 構造体  
  
-   `ICommandWithParameters::GetParameterInfo`  
  
-   `ICommandWithParameters::SetParameterInfo`  
  
-   `IColumnsRowset::GetColumnsRowset`  
  
-   `IColumnsInfo::GetColumnInfo`  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 *prgParamInfo* を使用して DBPARAMINFO 構造体に次の情報が返されます。  
  
|パラメーターの型|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|-------------------|------------------|--------------|-----------------------------------------------------|  
|日付|DBTYPE_DBDATE|6|10|0|Clear|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|Set|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19,21..27|0..7|Set|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26,28..34|0..7|Set|  
  
 場合によっては、値の範囲が連続していないことに注意してください。 有効桁数が 0 より大きい場合は、小数点が追加されるためです。  
  
 DBPARAMFLAGS_SS_ISVARIABLESCALE は、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のサーバーに接続されている場合にのみ有効です。 下位レベルのサーバーに接続されている場合は、DBPARAMFLAGS_SS_ISVARIABLESCALE は設定されません。  
  
## <a name="icommandwithparameterssetparameterinfo-and-implied-parameter-types"></a>ICommandWithParameters::SetParameterInfo と暗黙のパラメーターの型  
 DBPARAMBINDINFO 構造体で提供される情報は、次の表に準拠する必要があります。  
  
|*pwszDataSourceType*<br /><br /> (プロバイダー固有)|*pwszDataSourceType*<br /><br /> (OLE DB 汎用)|*ulParamSize*|*bScale*|  
|----------------------------------------------------|-------------------------------------------------|-------------------|--------------|  
||DBTYPE_DATE|6|無視|  
|日付|DBTYPE_DBDATE|6|無視|  
||DBTYPE_DBTIME|10|無視|  
|time|DBTYPE_DBTIME2|10|0..7|  
|smalldatetime||16|無視|  
|DATETIME||16|無視|  
|datetime2 または DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|16|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|0..7|  
  
 *BPrecision*パラメーターは無視されます。  
  
 データをサーバーに送信する場合、"DBPARAMFLAGS_SS_ISVARIABLESCALE" は無視されます。 アプリケーションでは、プロバイダー固有の型名 "`datetime`" および "`smalldatetime`" を使用して、従来の表形式のデータ ストリーム (TDS) の型を強制的に使用することができます。 接続されているときに[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)](またはそれ以降)、サーバー"`datetime2`"形式が使用して、暗黙的なサーバー変換が発生、必要に応じて、型名が"`datetime2`"または"DBTYPE_DBTIMESTAMP"。 *bScale*プロバイダー固有の型名の場合は無視されます"`datetime`「または」`smalldatetime`"ために使用されます。 それ以外の場合、アプリケーションである必要がありますように*bScale*が正しく設定されています。 MDAC からアップグレードされたアプリケーションと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client から[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]"DBTYPE_DBTIMESTAMP"が設定されない場合は失敗を使用して*bScale*正しくします。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] より前のサーバー インスタンスに接続されている場合は、"DBTYPE_DBTIMESTAMP" で 0 または 3 以外に設定された *bScale* の値はエラーになり、E_FAIL が返されます。  
  
 Icommandwithparameters::setparameterinfo が呼び出されていない場合プロバイダー基、サーバーに iaccessor::createaccessor で指定されたバインドの種類から次のように入力します。  
  
|バインドの種類|*pwszDataSourceType*<br /><br /> (プロバイダー固有)|  
|------------------|----------------------------------------------------|  
|DBTYPE_DATE|datetime2(0)|  
|DBTYPE_DBDATE|日付|  
|DBTYPE_DBTIME|time(0)|  
|DBTYPE_DBTIME2|time(7)|  
|DBTYPE_DBTIMESTAMP|datetime2(7)|  
|DBTYPE_DBTIMESTAMPOFFSET|datetimeoffset(7)|  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 `IColumnsRowset::GetColumnsRowset` は次の列を返します。  
  
|列の型|DBCOLUMN_TYPE|DBCOLUM_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE、DBCOLUMN_DATETIMEPRECISION|DBCOLUMN_FLAGS、DBCOLUMNFLAGS_SS_ISVARIABLESCALE|  
|-----------------|--------------------|-------------------------|-------------------------|--------------------------------------------------|---------------------------------------------------------|  
|日付|DBTYPE_DBDATE|6|10|0|Clear|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|Set|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Set|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Set|  
  
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
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE は [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のサーバーに接続されている場合にのみ有効です。 下位レベルのサーバーに接続されている場合、DBCOLUMNFLAGS_SS_ISVARIABLESCALE は未定義となります。  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 DBCOLUMNINFO 構造体から次の情報が返されます。  
  
|パラメーターの型|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------------------|  
|日付|DBTYPE_DBDATE|6|10|0|Clear|  
|time(1..7)|DBTYPE_DBTIME2|10|8, 10..16|0..7|Set|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Set|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Set|  
  
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
 [メタデータ&#40;OLE DB&#41;](../../database-engine/dev-guide/metadata-ole-db.md)  
  
  
