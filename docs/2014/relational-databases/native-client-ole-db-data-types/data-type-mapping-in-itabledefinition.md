---
title: ITableDefinition でのデータ型マッピング |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- SQL Server Native Client OLE DB provider, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
ms.assetid: 13292d1f-c17e-4d11-bf98-3460a10cbb18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e561742406c173b69bfb5040c2f2f51efdf5ed64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63201215"
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition でのデータ型のマッピング
  使用してテーブルを作成するときに、 **itabledefinition::createtable**関数の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのコンシューマーが指定できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型、 *pwszTypeName*渡される DBCOLUMNDESC 配列のメンバーです。 コンシューマーが列のデータ型を名前で指定する場合、DBCOLUMNDESC 構造体の *wType* メンバーで示される OLE DB データ型のマッピングは無視されます。  
  
 DBCOLUMNDESC 構造体を使用して OLE DB データ型を持つ新しい列のデータ型を指定するときに*wType* 、メンバー、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーが OLE DB データ型を次のようにマップされます。  
  
|OLE DB データ型|SQL Server<br /><br /> データ型 (data type)|関連情報|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**、**varbinary**、**image**、**varbinary(max)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって、 *ulColumnSize* DBCOLUMNDESC 構造体のメンバー。 値、およびのバージョンに基づいて、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンス、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーにマップする型**イメージ**します。<br /><br /> 場合の値*ulColumnSize*の最大長よりも小さい、**バイナリ**データ型の列、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって、DBCOLUMNDESC *rgPropertySets*メンバー。 DBPROP_COL_FIXEDLENGTH が VARIANT_TRUE の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーにマップする型**バイナリ**します。 プロパティの値が VARIANT_FALSE の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーにマップする型**varbinary**します。 いずれの場合も、DBCOLUMNDESC の *ulColumnSize* メンバーによって、作成される SQL Server の列の幅が決まります。|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの検査、DBCOLUMDESC *bPrecision*と*bScale*メンバーには、有効桁数を決定し、拡張、**数値**列です。|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**、**varchar**、**text**、**varchar(max)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって、 *ulColumnSize* DBCOLUMNDESC 構造体のメンバー。 値とのバージョンに基づいて、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンス、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーにマップする型**テキスト**します。<br /><br /> 場合の値*ulColumnSize*マルチバイト文字データ型の列の最大長よりも小さい、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって、DBCOLUMNDESC *rgPropertySets*メンバー。 DBPROP_COL_FIXEDLENGTH が VARIANT_TRUE の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーにマップする型**char**します。 プロパティの値が VARIANT_FALSE の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーにマップする型**varchar**します。 いずれの場合も、DBCOLUMNDESC の *ulColumnSize* メンバーによって、作成される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の列の幅が決まります。|  
|DBTYPE_UDT|**UDT**|次の情報が使用される`DBCOLUMNDESC`構造体**itabledefinition::createtable** UDT 列が必要な場合。<br /><br /> -   *pwSzTypeName*は無視されます。<br />-   *rgPropertySets*含める必要があります、`DBPROPSET_SQLSERVERCOLUMN`プロパティに関するセクションで説明したように設定`DBPROPSET_SQLSERVERCOLUMN`の[ユーザー種類](../native-client/features/using-user-defined-types.md)します。|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**、**nvarchar**、**ntext**、**nvarchar(max)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって、 *ulColumnSize* DBCOLUMNDESC 構造体のメンバー。 値に基づいて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーにマップする型**ntext**します。<br /><br /> 場合の値*ulColumnSize* Unicode 文字データ型列の最大長よりも小さい、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって、DBCOLUMNDESC *rgPropertySets*メンバー。 DBPROP_COL_FIXEDLENGTH が VARIANT_TRUE の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーにマップする型**nchar**します。 プロパティの値が VARIANT_FALSE の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーにマップする型**nvarchar**します。 いずれの場合も、DBCOLUMNDESC の *ulColumnSize* メンバーによって、作成される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の列の幅が決まります。|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  新しいテーブルの作成時には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって上記の表に示した OLE DB データ型の列挙値のみがマップされます。 それ以外の OLE DB データ型の列が含まれたテーブルを作成すると、エラーが発生します。  
  
## <a name="see-also"></a>関連項目  
 [データ型&#40;OLE DB&#41;](data-types-ole-db.md)  
  
  
