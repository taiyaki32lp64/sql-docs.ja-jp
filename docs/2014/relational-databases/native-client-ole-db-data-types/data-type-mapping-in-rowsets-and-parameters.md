---
title: 行セット、およびパラメーター内のデータ型マッピング |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- DBTYPE_SQLVARIANT data type
- SQL Server Native Client OLE DB provider, data types
- rowsets [OLE DB], data type mapping
- data types [OLE DB]
- GetColumnInfo function
- parameters [OLE DB]
- SSPROP_ALLOWNATIVEVARIANT property
- GetParameterInfo function
- OLE DB, data types
ms.assetid: 3d831ff8-3b79-4698-b2c1-2b5dd2f8235c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0979892b6770b9a9c2d0d9c4e8a0d734d873c085
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63062201"
---
# <a name="data-type-mapping-in-rowsets-and-parameters"></a>行セットとパラメーターでのデータ型マッピング
  行セットでは、パラメーター値として、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーを表す[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]次 OLE DB を使用してデータには、関数で報告された、データ型が定義されている**icolumnsinfo::getcolumninfo**と**Icommandwithparameters::getparameterinfo**します。  
  
|SQL Server データ型|OLE DB データ型|  
|--------------------------|----------------------|  
|**bigint**|DBTYPE_I8|  
|**[バイナリ]**|DBTYPE_BYTES|  
|**bit**|DBTYPE_BOOL|  
|**char**|DBTYPE_STR|  
|**datetime**|DBTYPE_DBTIMESTAMP|  
|**datetime2**|DBTYPE_DBTIME2|  
|**decimal**|DBTYPE_NUMERIC|  
|**float**|DBTYPE_R8|  
|**image**|DBTYPE_BYTES|  
|**int**|DBTYPE_I4|  
|**money**|DBTYPE_CY|  
|**nchar**|DBTYPE_WSTR|  
|**ntext**|DBTYPE_WSTR|  
|**numeric**|DBTYPE_NUMERIC|  
|**nvarchar**|DBTYPE_WSTR|  
|**real**|DBTYPE_R4|  
|**smalldatetime**|DBTYPE_DBTIMESTAMP|  
|**smallint**|DBTYPE_I2|  
|**smallmoney**|DBTYPE_CY|  
|**sql_variant**|DBTYPE_VARIANT、DBTYPE_SQLVARIANT|  
|**sysname**|DBTYPE_WSTR|  
|**text**|DBTYPE_STR|  
|**timestamp**|DBTYPE_BYTES|  
|**tinyint**|DBTYPE_UI1|  
|**UDT**|DBTYPE_UDT|  
|**uniqueidentifier**|DBTYPE_GUID|  
|**varbinary**|DBTYPE_BYTES|  
|**varchar**|DBTYPE_STR|  
|**XML**|DBTYPE_XML|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、図に示すように、コンシューマーから要求されたデータの変換をサポートしています。  
  
 **sql_variant** オブジェクトは、text、ntext、image、varchar(max)、nvarchar(max)、varbinary(max)、xml、timestamp、および Microsoft .NET Framework 共通言語ランタイム (CLR) のユーザー定義型を除く、任意の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型のデータを保持できます。 また、sql_variant データのインスタンスは、その基になる基本データ型として sql_variant を保持できません。 たとえば、一部の行の列に **smallint** 型の値を格納し、他の行の列に **float** 型の値を格納して、残りの行の列に **char**/**nchar** 型の値を格納できます。  
  
> [!NOTE]  
>  **Sql_variant**データ型はバリアント データ型では、Microsoft Visual Basic に似ています。 DBTYPE_VARIANT、DBTYPE_SQLVARIANT します。  
  
 **sql_variant** 型のデータを DBTYPE_VARIANT としてフェッチすると、このデータはバッファーの VARIANT 構造体内に格納されます。 ただし、VARIANT 構造体内のサブタイプは、**sql_variant** データ型で定義されているサブタイプにマップされない場合があります。 このため、すべてのサブタイプを一致させるには、**sql_variant** 型のデータを DBTYPE_SQLVARIANT としてフェッチする必要があります。  
  
## <a name="dbtypesqlvariant-data-type"></a>DBTYPE_SQLVARIANT データ型  
 サポートするために、 **sql_variant**データ型、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、DBTYPE_SQLVARIANT と呼ばれるプロバイダー固有のデータ型を公開します。 **sql_variant** 型のデータを DBTYPE_SQLVARIANT としてフェッチすると、データはプロバイダー固有の SSVARIANT 構造体内に格納されます。 SSVARIANT 構造体には、**sql_variant** データ型のサブタイプに一致するすべてのサブタイプが含まれています。  
  
 また、セッション プロパティ SSPROP_ALLOWNATIVEVARIANT を TRUE に設定する必要もあります。  
  
## <a name="provider-specific-property-sspropallownativevariant"></a>プロバイダー固有のプロパティ SSPROP_ALLOWNATIVEVARIANT  
 データをフェッチするときに、列またはパラメーターに返すデータ型を明示的に指定できます。 また、**IColumnsInfo** を使用して列情報を取得し、その情報をバインドに使用することもできます。 **IColumnsInfo** を使用してバインド用の列情報を取得するときに、SSPROP_ALLOWNATIVEVARIANT セッション プロパティが FALSE (既定値) の場合、**sql_variant** 型の列には DBTYPE_VARIANT が返されます。 SSPROP_ALLOWNATIVEVARIANT プロパティが FALSE の場合、DBTYPE_SQLVARIANT はサポートされません。 SSPROP_ALLOWNATIVEVARIANT プロパティを TRUE に設定すると、列の型は DBTYPE_SQLVARIANT として返されます。この場合、バッファーには SSVARIANT 構造体が保持されます。 **sql_variant** 型のデータを DBTYPE_SQLVARIANT としてフェッチするときは、セッション プロパティ SSPROP_ALLOWNATIVEVARIANT が TRUE に設定されている必要があります。  
  
 SSPROP_ALLOWNATIVEVARIANT プロパティはプロバイダー固有の DBPROPSET_SQLSERVERSESSION プロパティ セットの一部であり、セッション プロパティです。  
  
 DBTYPE_VARIANT は、他のすべての OLE DB プロバイダーに適用されます。  
  
## <a name="sspropallownativevariant"></a>SSPROP_ALLOWNATIVEVARIANT  
 SSPROP_ALLOWNATIVEVARIANT はセッション プロパティで、DBPROPSET_SQLSERVERSESSION プロパティ セットの一部です。  
  
|||  
|-|-|  
|SSPROP_ALLOWNATIVEVARIANT|型:VT_BOOL<br /><br /> R/W[読み取り/書き込み]<br /><br /> 既定値:VARIANT_FALSE<br /><br /> 説明:フェッチされるデータを DBTYPE_VARIANT と dbtype_sqlvariant のどちらとしてかどうかを判断します。<br /><br /> VARIANT_TRUE:列の型は、SSVARIANT 構造体をバッファーが保持されます DBTYPE_SQLVARIANT として返されます。<br /><br /> VARIANT_FALSE:列の型は DBTYPE_VARIANT として返されます、バッファーは VARIANT 構造体に必要があります。|  
  
## <a name="see-also"></a>関連項目  
 [データ型&#40;OLE DB&#41;](data-types-ole-db.md)  
  
  
