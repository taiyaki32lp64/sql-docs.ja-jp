---
title: 大きな CLR ユーザー定義型 (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types [OLE DB]
ms.assetid: 4bf12058-0534-42ca-a5ba-b1c23b24d90f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1aea946703b9ebe06c32fcc25044a3b68326625e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199255"
---
# <a name="large-clr-user-defined-types-ole-db"></a>大きな CLR ユーザー定義型 (OLE DB)
  このトピックでは、大きな共通言語ランタイム (CLR) ユーザー定義型 (UDT) をサポートするための、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の OLE DB に対する変更について説明します。  
  
 における大きな CLR Udt のサポートの詳細については[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client を参照してください[Large CLR User-Defined 型](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)します。 サンプルについては、次を参照してください。[大きな CLR Udt を使用して&#40;OLE DB&#41;](../../native-client-ole-db-how-to/use-large-clr-udts-ole-db.md)します。  
  
## <a name="data-format"></a>データ形式  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、大きなオブジェクト (LOB) の型についてサイズが無制限である値の長さを表す場合に、~0 が使用されます。 8,000 バイトを超える CLR UDT のサイズも ~0 で表されます。  
  
 次の表に、パラメーターおよび行セットでのデータ型のマッピングを示します。  
  
|SQL Server データ型|OLE DB データ型|メモリ レイアウト|値|  
|--------------------------|----------------------|-------------------|-----------|  
|CLR UDT|DBTYPE_UDT|BYTE[](バイト配列\)|132 (oledb.h)|  
  
 UDT 値はバイト配列として表されます。 16 進文字列との間の変換がサポートされています。 リテラル値は、"0x" で始まる 16 進文字列として表されます。 16 進文字列は、ベース 16 のバイナリ データをテキストで表現したものです。 一例として、サーバー型 `varbinary(10)` から DBTYPE_STR への変換が挙げられます。この変換では、1 対の文字が 1 バイトを表す 20 文字の 16 進表記が生成されます。  
  
## <a name="parameter-properties"></a>パラメーターのプロパティ  
 DBPROPSET_SQLSERVERPARAMETER プロパティ セットは、OLE DB を介して UDT をサポートします。 詳細については、「[ユーザー定義型の使用](../features/using-user-defined-types.md)」を参照してください。  
  
## <a name="column-properties"></a>列のプロパティ  
 DBPROPSET_SQLSERVERCOLUMN プロパティ セットは、OLE DB を介してテーブルの作成をサポートします。 詳細については、「[ユーザー定義型の使用](../features/using-user-defined-types.md)」を参照してください。  
  
## <a name="data-type-mapping-in-itabledefinitioncreatetable"></a>ITableDefinition::CreateTable でのデータ型マッピング  
 次の情報が使用される`DBCOLUMNDESC`itabledefinition::createtable で UDT 列が必要な場合に使用される構造。  
  
|OLE DB データ型 (*wType*)|*pwszTypeName*|SQL Server データ型|*rgPropertySets*|  
|----------------------------------|--------------------|--------------------------|----------------------|  
|DBTYPE_UDT|無視|UDT (UDT)|DBPROPSET_SQLSERVERCOLUMN プロパティ セットを含める必要があります。|  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 **prgParamInfo** を介して DBPARAMINFO 構造体に返される情報は、次のとおりです。  
  
|パラメーターの型|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags* DBPARAMFLAGS_ISLONG|  
|--------------------|-------------|-------------------|------------------|--------------|------------------------------------|  
|DBTYPE_UDT<br /><br /> (8,000 バイト以下の長さ)|"DBTYPE_UDT"|*n*|未定義|未定義|クリア|  
|DBTYPE_UDT<br /><br /> (8,000 バイトを超える長さ)|"DBTYPE_UDT"|~0|未定義|未定義|セット (set)|  
  
## <a name="icommandwithparameterssetparameterinfo"></a>ICommandWithParameters::SetParameterInfo  
 DBPARAMBINDINFO 構造体で提供される情報は、次の表に準拠する必要があります。  
  
|パラメーターの型|*pwszDataSourceType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags* DBPARAMFLAGS_ISLONG|  
|--------------------|--------------------------|-------------------|------------------|--------------|------------------------------------|  
|DBTYPE_UDT<br /><br /> (8,000 バイト以下の長さ)|DBTYPE_UDT|*n*|無視|無視|パラメーターが DBTYPE_IUNKNOWN を使用して渡される場合に設定する必要があります。|  
|DBTYPE_UDT<br /><br /> (8,000 バイトを超える長さ)|DBTYPE_UDT|~0|無視|無視|無視|  
  
## <a name="isscommandwithparameters"></a>ISSCommandWithParameters  
 アプリケーションでは、**ISSCommandWithParameters** を使用して、「パラメーターのプロパティ」セクションで定義されているパラメーターのプロパティを取得または設定します。  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 返される列は次のとおりです。  
  
|列の型|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE|DBCOLUMN_FLAGS_ISLONG|DBCOLUMNS_ISSEARCHABLE|DBCOLUMN_OCTETLENGTH|  
|-----------------|--------------------|--------------------------|-------------------------|---------------------|-----------------------------|-----------------------------|---------------------------|  
|DBTYPE_UDT<br /><br /> (8,000 バイト以下の長さ)|DBTYPE_UDT|*n*|NULL|NULL|Clear|DB_ALL_EXCEPT_LIKE|n|  
|DBTYPE_UDT<br /><br /> (8,000 バイトを超える長さ)|DBTYPE_UDT|~0|NULL|NULL|Set|DB_ALL_EXCEPT_LIKE|0|  
  
 UDT には次の列も定義されています。  
  
|列識別子|型|説明|  
|-----------------------|----------|-----------------|  
|DBCOLUMN_UDT_CATALOGNAME|DBTYPE_WSTR|UDT 列の場合は、UDT が定義されているカタログの名前。|  
|DBCOLUMN_UDT_SCHEMANAME|DBTYPE_WSTR|UDT 列の場合は、UDT が定義されているスキーマの名前。|  
|DBCOLUMN_UDT_NAME|DBTYPE_WSTR|UDT 列の場合は、UDT の 1 部構成の名前。|  
|DBCOLUMN_ASSEMBLY_TYPENAME|DBTYPE_WSTR|UDT 列の場合は、UDT の完全な型名。 アセンブリ型の完全修飾名を使用することで、Type.GetType メソッドを使用してその型のオブジェクトのインスタンスを作成できます。|  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 DBCOLUMNINFO 構造体で返される情報は次のとおりです。  
  
|パラメーターの型|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBCOLUMNFLAGS_ISLONG|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------|  
|DBTYPE_UDT<br /><br /> (8,000 バイト以下の長さ)|DBTYPE_UDT|*n*|~0|~0|Clear|  
|DBTYPE_UDT<br /><br /> (8,000 バイトを超える長さ)|DBTYPE_UDT|~0|~0|~0|Set|  
  
## <a name="columns-rowset-schema-rowsets"></a>COLUMNS 行セット (スキーマ行セット)  
 UDT 型に対して返される列値を次に示します。  
  
|列の型|DATA_TYPE|COLUMN_FLAGS、DBCOLUMFLAGS_ISLONG|CHARACTER_OCTET_LENGTH|  
|-----------------|----------------|-----------------------------------------|------------------------------|  
|DBTYPE_UDT<br /><br /> (8,000 バイト以下の長さ)|DBTYPE_UDT|Clear|*n*|  
|DBTYPE_UDT<br /><br /> (8,000 バイトを超える長さ)|DBTYPE_UDT|Set|0|  
  
 UDT には、次の追加の列が定義されています。  
  
|列識別子|型|説明|  
|-----------------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|UDT 列の場合は、UDT が定義されているカタログの名前。|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|UDT 列の場合は、UDT が定義されているスキーマの名前。|  
|SS_UDT_NAME|DBTYPE_WSTR|UDT 列の場合は、UDT の 1 部構成の名前。|  
|SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|UDT 列の場合は、UDT の完全な型名。 アセンブリ型の完全修飾名を使用することで、Type.GetType メソッドを使用してその型のオブジェクトのインスタンスを作成できます。|  
  
 PROCEDURE_PARAMETERS 行セットに関しては、DATA_TYPE に COLUMNS スキーマ行セットと同じ値が格納され、TYPE_NAME に UDT が格納されます。 同じ追加の列も定義されています。  
  
 PROVIDER_TYPES スキーマ行セットには、ユーザー定義型が表示されません。  
  
## <a name="bindings-and-conversions"></a>バインドと変換  
  
|Binding データ型|UDT からサーバー|UDT 以外からサーバー|サーバーから UDT|サーバーから UDT 以外|  
|----------------------|-------------------|------------------------|---------------------|--------------------------|  
|DBTYPE_UDT|サポート (5)|エラー (1)|サポート (5)|エラー (4)|  
|DBTYPE_BYTES|サポート (5)|なし|サポート (5)|なし|  
|DBTYPE_WSTR|サポート (2)、(5)|なし|サポート (3)、(5)、(6)|なし|  
|DBTYPE_BSTR|サポート (2)、(5)|なし|サポート (3)、(5)|なし|  
|DBTYPE_STR|サポート (2)、(5)|なし|サポート (3)、(5)|なし|  
|DBTYPE_IUNKNOWN|サポート (6)|なし|サポート (6)|なし|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|サポート (5)|なし|サポート (3)、(5)|なし|  
|DBTYPE_VARIANT (VT_BSTR)|サポート (2)、(5)|なし|なし|なし|  
  
### <a name="key-to-symbols"></a>記号の説明  
  
|シンボル|説明|  
|------------|-------------|  
|1|**ICommandWithParameters::SetParameterInfo** で DBTYPE_UDT 以外のサーバーの型が指定され、アクセサーの型が DBTYPE_UDT の場合は、ステートメントの実行時にエラーが発生します。  発生するエラーは DB_E_ERRORSOCCURRED、パラメーターの状態は DBSTATUS_E_BADACCESSOR です。<br /><br /> UDT ではないサーバー パラメーターに UDT 型のパラメーターを指定すると、エラーになります。|  
|2|データが 16 進数文字列からバイナリ データに変換されます。|  
|3|データがバイナリ データから 16 進文字列に変換されます。|  
|4|**CreateAccessor** または **GetNextRows** を使用したときに、検証が行われる場合があります。 このエラーは DB_E_ERRORSOCCURRED です。 バインドの状態は、DBBINDSTATUS_UNSUPPORTEDCONVERSION に設定されます。|  
|5|BY_REF を使用できます。|  
|6|UDT パラメーターを、DBBINDING で DBTYPE_IUNKNOWN としてバインドできます。 DBTYPE_IUNKNOWN へのバインドは、アプリケーションで ISequentialStream インターフェイスを使用してデータをストリームとして処理する必要があることを示します。 コンシューマーを示す*wType*ストアド プロシージャのパラメーターは、UDT を DBTYPE_IUNKNOWN 型としてバインドし、対応する列または出力で、SQL Server Native Client には ISequentialStream が返されます。 クエリは、入力パラメーターでは、SQL Server Native Client、ISequentialStream インターフェイス。<br /><br /> UDT が大きい場合は、DBTYPE_IUNKNOWN バインドを使用しながら UDT データの長さをバインドしないようにすることができます。 ただし、小さな UDT の場合は長さをバインドする必要があります。 次の条件が 1 つ以上当てはまる場合は、DBTYPE_UDT パラメーターを大きな UDT として指定できます。<br /><br /> -   *ulParamParamSize*は ~ 0。<br />で DBPARAMBINDINFO 構造体 DBPARAMFLAGS_ISLONG が設定されています。<br /><br /> 行データの場合は、DBTYPE_IUNKNOWN バインドを大きな UDT だけに使用できます。 コマンド オブジェクトの IColumnsInfo インターフェイスまたは列が行セットに対して icolumnsinfo::getcolumninfo メソッドを使用して、大きな UDT 型がかどうかを確認できます。 次の条件が 1 つ以上当てはまる場合、DBTYPE_UDT 列は大きな UDT 列です。<br /><br /> DBCOLUMNFLAGS_ISLONG フラグが設定されて*dwFlags* DBCOLUMNINFO 構造体のメンバー<br />-   *ulColumnSize* DBCOLUMNINFO のメンバーが ~ 0。|  
  
 DBTYPE_NULL と DBTYPE_EMPTY は入力パラメーターにバインドできますが、出力パラメーターや結果にはバインドできません。 入力パラメーターにバインドした場合は、状態を DBSTATUS_S_ISNULL (DBTYPE_NULL の場合) または DBSTATUS_S_DEFAULT (DBTYPE_EMPTY の場合) に設定する必要があります。 DBTYPE_BYREF を、DBTYPE_NULL または DBTYPE_EMPTY と共に使用することはできません。  
  
 DBTYPE_UDT は、DBTYPE_EMPTY および DBTYPE_NULL に変換することもできます。 ただし、DBTYPE_NULL および DBTYPE_EMPTY を DBTYPE_UDT に変換することはできません。 この動作は、DBTYPE_BYTES 型と一貫性があります。 UDT をパラメーターとして処理する場合には、**ISSCommandWithParameters** が使用されます。  
  
 OLE DB Core Services で提供されるデータ変換 (**IDataConvert**) は、DBTYPE_UDT 型には適用できません。  
  
 また、その他のバインドもサポートされません。  
  
## <a name="comparability-for-irowsetfind"></a>IRowsetFind での比較  
 UDT 型については、次の比較のみがサポートされています。  
  
-   EQ  
  
-   NE  
  
-   IGNORE  
  
 その他の比較を試みると、DB_E_BADCOMPAREOP が返されます。  
  
## <a name="bcp-support-for-udts"></a>BCP による UDT のサポート  
 UDT 値は、文字値またはバイナリ値としてのみインポートおよびエクスポートできます。  
  
## <a name="down-level-client-behavior-for-udts"></a>UDT に対する下位クライアントの動作  
 UDT に対しては、下位クライアントで次のように型マッピングが行われます。  
  
|クライアントのバージョン|DBTYPE_UDT<br /><br /> (8,000 バイト以下の長さ)|DBTYPE_UDT<br /><br /> (8,000 バイトを超える長さ)|  
|--------------------|------------------------------------------------------------------|---------------------------------------------------------|  
|SQL Server 2005|UDT (UDT)|varbinary(max)|  
|SQL Server 2008 以降|UDT (UDT)|UDT (UDT)|  
  
 `DataTypeCompatibility` (SSPROP_INIT_DATATYPECOMPATIBILITY) を "80" に設定すると、大きな UDT 型が、下位クライアントで表示されるときと同じようにクライアントで表示されます。  
  
## <a name="see-also"></a>参照  
 [大きな CLR ユーザー定義型](../features/large-clr-user-defined-types.md)  
  
  
