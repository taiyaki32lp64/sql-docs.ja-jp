---
title: ユーザー定義型の使用 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_DATASOURCEINFO property set
- UDTs [SQL Server Native Client]
- user-defined types [SQL Server], SQL Server Native Client
- SQL Server Native Client OLE DB provider, user-defined types
- DBPROPSET_SQLSERVERPARAMETER property set
- IColumnsRowset interface
- SQLNCLI, user-defined types
- SQL Server Native Client, user-defined types
- data access [SQL Server Native Client], user-defined types
- ISSCommandWithParameters interface
ms.assetid: e15d8169-3517-4323-9c9e-0f5c34aff7df
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2adbf40b3fe0b0e079198087a47f525d464a41b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206612"
---
# <a name="using-user-defined-types"></a>ユーザー定義型の使用
  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] では、ユーザー定義型 (UDT) が導入されました。 これにより、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースにオブジェクトやカスタム データ構造を格納できるようになり、SQL の型システムが拡張されます。 UDT は複数のデータ型を持つことができ、動作を定義できます。この点は、1 つの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] システム データ型から構成される従来の別名データ型と異なります。 UDT は、検証可能なコードを生成する .NET 共通言語ランタイム (CLR) でサポートされる任意の言語を使用して定義されます。 これにより、Microsoft Visual が含まれます。 C#<sup>いますか。</sup> および Visual Basic<sup>??</sup> .NET。 データは、.NET のクラスまたは構造体のフィールドやプロパティとして公開され、動作はクラスまたは構造体のメソッドによって定義されます。  
  
 UDT は、テーブルの列定義、[!INCLUDE[tsql](../../../includes/tsql-md.md)] バッチの変数、または [!INCLUDE[tsql](../../../includes/tsql-md.md)] 関数やストアド プロシージャの引数として使用することができます。  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB プロバイダー  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのメタデータについては、オブジェクトとしての Udt を管理することができますを持つバイナリ型としての Udt をサポートしています。 UDT 列は、DBTYPE_UDT 型として公開され、この列のメタデータは主要な OLE DB インターフェイスの **IColumnRowset** と新しいインターフェイスの [ISSCommandWithParameters](../../native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md) により公開されます。  
  
> [!NOTE]  
>  **IRowsetFind::FindNextRow** メソッドでは、UDT データ型を処理できません。 UDT が検索列の型として使用されると、DB_E_BADCOMPAREOP が返されます。  
  
### <a name="data-bindings-and-coercions"></a>データ バインドと強制型変換  
 次の表に、特定のデータ型を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の UDT と共に使用した場合に行われるバインドおよび強制型変換を示します。 UDT 列がを介して公開される、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーにより dbtype_udt 型として。 この列のメタデータは、適切なスキーマ行セットを使用して取得できるので、独自に定義した型をオブジェクトとして管理できます。  
  
|データの種類|SQL Server の<br /><br /> **UDT**|SQL Server の<br /><br /> **UDT 以外から**|サーバーから<br /><br /> **UDT**|サーバーから<br /><br /> **UDT 以外から**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_UDT|サポートされている<sup>6</sup>|エラー<sup>1</sup>|サポートされている<sup>6</sup>|エラー<sup>5</sup>|  
|DBTYPE_BYTES|サポートされている<sup>6</sup>|該当なし<sup>2</sup>|サポートされている<sup>6</sup>|該当なし<sup>2</sup>|  
|DBTYPE_WSTR|サポートされている<sup>3、6</sup>|該当なし<sup>2</sup>|サポートされている<sup>4、6</sup>|該当なし<sup>2</sup>|  
|DBTYPE_BSTR|サポートされている<sup>3、6</sup>|該当なし<sup>2</sup>|サポートされている<sup>4</sup>|該当なし<sup>2</sup>|  
|DBTYPE_STR|サポートされている<sup>3、6</sup>|該当なし<sup>2</sup>|サポートされている<sup>4、6</sup>|該当なし<sup>2</sup>|  
|DBTYPE_IUNKNOWN|サポートされていません|該当なし<sup>2</sup>|サポートされていません|該当なし<sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|サポートされている<sup>6</sup>|該当なし<sup>2</sup>|サポートされている<sup>4</sup>|該当なし<sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|サポートされている<sup>3、6</sup>|該当なし<sup>2</sup>|なし|該当なし<sup>2</sup>|  
  
 <sup>1</sup>**ICommandWithParameters::SetParameterInfo** で DBTYPE_UDT 以外のサーバーの型が指定され、アクセサーの型が DBTYPE_UDT の場合、ステートメントの実行時にエラー (DB_E_ERRORSOCCURRED) が発生します (パラメーターの状態は DBSTATUS_E_BADACCESSOR になります)。 それ以外の場合、データはサーバーに送信されますが、サーバーからは、UDT からパラメーターのデータ型への暗黙的な変換がないことを示すエラーが返されます。  
  
 <sup>2</sup>このトピックの範囲を超えています。  
  
 <sup>3</sup> 16 進文字列からバイナリ データへのデータ変換が行われます。  
  
 <sup>4</sup> バイナリ データから 16 進文字列へのデータ変換が行われます。  
  
 <sup>5</sup>アクセサーの作成時またはフェッチ時に検証が行われることがあります。エラー DB_E_ERRORSOCCURRED が返され、バインドの状態は DBBINDSTATUS_UNSUPPORTEDCONVERSION になります。  
  
 <sup>6</sup>BY_REF を使用できます。  
  
 DBTYPE_NULL と DBTYPE_EMPTY は入力パラメーターにバインドできますが、出力パラメーターや結果にはバインドできません。 入力パラメーターにバインドした場合、状態を DBSTATUS_S_ISNULL または DBSTATUS_S_DEFAULT に設定する必要があります。  
  
 DBTYPE_UDT 型は、DBTYPE_EMPTY と DBTYPE_NULL に変換できますが、DBTYPE_EMPTY と DBTYPE_NULL は DBTYPE_UDT に変換できません。 この動作は、DBTYPE_BYTES 型と一貫性があります。  
  
> [!NOTE]  
>  UDT をパラメーターとして処理するための新しいインターフェイス **ISSCommandWithParameters** が導入されました。これは、**ICommandWithParameters** インターフェイスから継承されます。 アプリケーションでは、少なくとも UDT パラメーターの SSPROP_PARAM_UDT_NAME プロパティ セットの DBPROPSET_SQLSERVERPARAMETER プロパティの設定に、このインターフェイスを使用する必要があります。 これを行わないと、**ICommand::Execute** から DB_E_ERRORSOCCURRED が返されます。 このインターフェイスとプロパティ セットについては、このトピックの後半で説明します。  
  
 データをすべて格納できる大きさがない列にユーザー定義型を挿入した場合、**ICommand::Execute** は状態が DB_E_ERRORSOCCURRED の S_OK を返します。  
  
 OLE DB Core Services で提供されるデータ変換 (**IDataConvert**) は、DBTYPE_UDT 型には適用できません。 また、その他のバインドもサポートされません。  
  
### <a name="ole-db-rowset-additions-and-changes"></a>OLE DB 行セットに関する追加事項と変更事項  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、新しい値が追加され、多くの主要な OLE DB スキーマ行セットへの変更します。  
  
#### <a name="the-procedureparameters-schema-rowset"></a>PROCEDURE_PARAMETERS スキーマ行セット  
 PROCEDURE_PARAMETERS スキーマ行セットには、次の列が追加されました。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|3 部構成の名前の識別子。|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|3 部構成の名前の識別子。|  
|SS_UDT_NAME|DBTYPE_WSTR|3 部構成の名前の識別子。|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|型名と、CLR での参照に必要なすべてのアセンブリ ID を含むアセンブリ修飾名。|  
  
#### <a name="the-sqlassemblies-schema-rowset"></a>SQL_ASSEMBLIES スキーマ行セット  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、新しいプロバイダー固有のスキーマ行セットを登録済み Udt を記述するを公開します。 ASSEMBLY_SERVER を DBTYPE_WSTR 型として指定することはできますが、行セットには格納されません。 指定しない場合、行セットでは既定で現在のサーバーが使用されます。 次の表に、SQL_ASSEMBLIES スキーマ行セットの定義を示します。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|このデータ型を含むアセンブリのカタログ名。|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|このデータ型を含むアセンブリのスキーマ名 (所有者の名前)。 アセンブリのスコープはスキーマではなくデータベースによって決まりますが、アセンブリには依然として所有者が存在します。|  
|ASSEMBLY_NAME|DBTYPE_WSTR|このデータ型を含むアセンブリの名前。|  
|ASSEMBLY_ID|DBTYPE_UI4|このデータ型を含むアセンブリのオブジェクト ID。|  
|PERMISSION_SET|DBTYPE_WSTR|アセンブリのアクセスのスコープを示す値。 スコープを示す値には、"SAFE"、"EXTERNAL_ACCESS"、および "UNSAFE" があります。|  
|ASSEMBLY_BINARY|DBTYPE_BYTES|アセンブリのバイナリ表記。|  
  
#### <a name="the-sqlassemblies-dependencies-schema-rowset"></a>SQL_ASSEMBLIES_ DEPENDENCIES スキーマ行セット  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、指定されたサーバーのアセンブリの依存関係を説明する新しいプロバイダーに固有のスキーマ行セットを公開します。 ASSEMBLY_SERVER は呼び出し元により DBTYPE_WSTR 型として指定することができますが、行セットには格納されません。 指定しない場合、行セットでは既定で現在のサーバーが使用されます。 次の表に、SQL_ASSEMBLY_DEPENDENCIES スキーマ行セットの定義を示します。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|このデータ型を含むアセンブリのカタログ名。|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|このデータ型を含むアセンブリのスキーマ名 (所有者の名前)。 アセンブリのスコープはスキーマではなくデータベースによって決まりますが、アセンブリには依然として所有者が存在します。|  
|ASSEMBLY_ID|DBTYPE_UI4|アセンブリのオブジェクト ID。|  
|REFERENCED_ASSEMBLY_ID|DBTYPE_UI4|参照されるアセンブリのオブジェクト ID。|  
  
#### <a name="the-sqlusertypes-schema-rowset"></a>SQL_USER_TYPES スキーマ行セット  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、新しいスキーマ行セット SQL_USER_TYPES を場合を公開します。 指定されたサーバーの登録済み Udt が追加されます。 UDT_SERVER は、呼び出し元により DBTYPE_WSTR 型として指定される必要がありますが、行セットには格納されません。 次の表に、SQL_USER_TYPES スキーマ行セットの定義を示します。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|UDT_CATALOGNAME|DBTYPE_WSTR|UDT 列の場合、このプロパティは、UDT が定義されているカタログ名を指定する文字列です。|  
|UDT_SCHEMANAME|DBTYPE_WSTR|UDT 列の場合、このプロパティは、UDT が定義されているスキーマ名を指定する文字列です。|  
|UDT_NAME|DBTYPE_WSTR|UDT を含むアセンブリの名前。|  
|UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|型名の前に名前空間を付けた完全な型名 (AQN) (該当する場合)。|  
  
#### <a name="the-columns-schema-rowset"></a>COLUMNS スキーマ行セット  
 COLUMNS スキーマ行セットには、次の列が追加されました。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|UDT 列の場合、このプロパティは、UDT が定義されているカタログ名を指定する文字列です。|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|UDT 列の場合、このプロパティは、UDT が定義されているスキーマ名を指定する文字列です。|  
|SS_UDT_NAME|DBTYPE_WSTR|UDT の名前。|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|型名の前に名前空間を付けた完全な型名 (AQN) (該当する場合)。|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>OLE DB プロパティ セットに関する追加事項と変更事項  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、新しい値を追加します。 またはに多くの主要な OLE DB プロパティ セットを変更します。  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>DBPROPSET_SQLSERVERPARAMETER プロパティ セット  
 OLE DB で Udt をサポートするために[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client では、次の値を含む新しい DBPROPSET_SQLSERVERPARAMETER プロパティ セット。  
  
|名前|型|説明|  
|----------|----------|-----------------|  
|SSPROP_PARAM_UDT_CATALOGNAME|DBTYPE_WSTR|3 部構成の名前の識別子。<br /><br /> UDT パラメーターの場合、このプロパティは、ユーザー定義型が定義されているカタログ名を指定する文字列です。|  
|SSPROP_PARAM_UDT_SCHEMANAME|DBTYPE_WSTR|3 部構成の名前の識別子。<br /><br /> UDT パラメーターの場合、このプロパティは、ユーザー定義型が定義されているスキーマ名を指定する文字列です。|  
|SSPROP_PARAM_UDT_NAME|DBTYPE_WSTR|3 部構成の名前の識別子。<br /><br /> UDT 列の場合、このプロパティは、ユーザー定義型の 1 部構成の名前を指定する文字列です。|  
  
 SSPROP_PARAM_UDT_NAME は必須です。 SSPROP_PARAM_UDT_CATALOGNAME と SSPROP_PARAM_UDT_SCHEMANAME は省略可能です。 いずれかのプロパティが適切に指定されていない場合、DB_E_ERRORSINCOMMAND が返されます。 SSPROP_PARAM_UDT_CATALOGNAME プロパティと SSPROP_PARAM_UDT_SCHEMANAME プロパティがどちらも指定されていない場合、UDT は、テーブルと同じデータベースおよびスキーマ内に定義する必要があります。 UDT の定義が、テーブルと同じデータベース内にあって、同じスキーマ内にない場合、SSPROP_PARAM_UDT_SCHEMANAME プロパティを指定する必要があります。 UDT の定義がテーブルと異なるデータベースにある場合、SSPROP_PARAM_UDT_CATALOGNAME プロパティと SSPROP_PARAM_UDT_SCHEMANAME プロパティの両方を指定する必要があります。  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>DBPROPSET_SQLSERVERCOLUMN プロパティ セット  
 内のテーブルの作成をサポートするために、 **ITableDefinition**インターフェイス、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は、DBPROPSET_SQLSERVERCOLUMN プロパティ セットに次の 3 つの新しい列を追加します。  
  
|名前|説明|種類|説明|  
|----------|-----------------|----------|-----------------|  
|SSPROP_COL_UDT_CATALOGNAME|UDT_CATALOGNAME|VT_BSTR|DBTYPE_UDT 型の列の場合、このプロパティは、UDT が定義されているカタログ名を指定する文字列です。|  
|SSPROP_COL_UDT_SCHEMANAME|UDT_SCHEMANAME|VT_BSTR|DBTYPE_UDT 型の列の場合、このプロパティは、UDT が定義されているスキーマ名を指定する文字列です。|  
|SSPROP_COL_UDT_NAME|UDT_NAME|VT_BSTR|DBTYPE_UDT 型の列の場合、このプロパティは、UDT の 1 部構成の名前を指定する文字列です。 他の列の型の場合、このプロパティでは空文字列が返されます。|  
  
> [!NOTE]  
>  UDT は PROVIDER_TYPES スキーマ行セットには表示されません。 すべての列は読み取り/書き込みアクセスです。  
  
 ADO では、"説明" 列の対応するエントリを使用してこれらのプロパティを参照します。  
  
 SSPROP_COL_UDTNAME は必須です。 SSPROP_COL_UDT_CATALOGNAME と SSPROP_COL_UDT_SCHEMANAME は省略可能です。 いずれかのプロパティが適切に指定されていない場合、`DB_E_ERRORSINCOMMAND` が返されます。  
  
 SSPROP_COL_UDT_CATALOGNAME プロパティと SSPROP_COL_UDT_SCHEMANAME プロパティがどちらも指定されていない場合、UDT は、テーブルと同じデータベースおよびスキーマ内に定義する必要があります。  
  
 UDT の定義が、テーブルと同じデータベース内にあって、同じスキーマ内にない場合、SSPROP_COL_UDT_SCHEMANAME プロパティを指定する必要があります。  
  
 UDT の定義がテーブルと異なるデータベースにある場合、SSPROP_COL_UDT_CATALOGNAME プロパティと SSPROP_COL_UDT_SCHEMANAME プロパティの両方を指定する必要があります。  
  
### <a name="ole-db-interface-additions-and-changes"></a>OLE DB インターフェイスに関する追加事項と変更事項  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、新しい値が追加または多くの主要な OLE DB インターフェイスに変更します。  
  
#### <a name="the-isscommandwithparameters-interface"></a>ISSCommandWithParameters インターフェイス  
 OLE DB を介して Udt をサポートする[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client では、多数の変更の追加など、 **ISSCommandWithParameters**インターフェイス。 この新しいインターフェイスは、主要な OLE DB インターフェイス **ICommandWithParameters** から継承されます。 継承した次の 3 つのメソッドだけでなく**ICommandWithParameters**;**GetParameterInfo**、 **MapParameterNames**、および**SetParameterInfo**;**ISSCommandWithParameters**提供、 **GetParameterProperties**と**SetParameterProperties**サーバー固有の処理に使用されるメソッドデータ型。  
  
> [!NOTE]  
>  **ISSCommandWithParameters** インターフェイスでは、新しい SSPARAMPROPS 構造体も使用されます。  
  
#### <a name="the-icolumnsrowset-interface"></a>IColumnsRowset インターフェイス  
 加え、 **ISSCommandWithParameters**インターフェイス、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は、呼び出しから返される行セットに新しい値を追加することも、 **icolumnsrowset::getcolumnrowset**メソッド次のようにします。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_UDT_CATALOGNAME|DBTYPE_WSTR|UDT カタログ名の識別子。|  
|DBCOLUMN_SS_UDT_SCHEMANAME|DBTYPE_WSTR|UDT スキーマ名の識別子。|  
|DBCOLUMN_SS_UDT_NAME|DBTYPE_WSTR|UDT 名の識別子。|  
|DBCOLUMN_SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|型名と、CLR での参照に必要なすべてのアセンブリ ID を含むアセンブリ修飾名。|  
  
 DBCOLUMN_TYPE を DBTYPE_UDT に設定すると、上記の新しく追加された UDT メタデータを参照することにより、サーバーの UDT 列と他のバイナリ型列とを区別することができます。 そのデータが部分的に完成している場合、サーバーのデータ型は UDT になります。 サーバーのデータ型が UDT 以外の場合、これらの列は、常に NULL として返されます。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC ドライバー  
 多数の変更を加え、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Udt をサポートするために Native Client ODBC ドライバー。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのマップ、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQL_SS_UDT ドライバー固有の SQL データを UDT は、識別子を入力します。 UDT 列は SQL_SS_UDT 型としてマップされます。 マップした場合、UDT 列に明示的に SQL ステートメントで別の型を使用して、 **ToString**または**ToXMLString**またはを使用して、UDT のメソッド、 **CAST/CONVERT**関数、型結果内の列のセットには、実際の型に変換された列が反映されます。  
  
### <a name="sqlcolattribute-sqldescribeparam-sqlgetdescfield"></a>SQLColAttribute、SQLDescribeParam、SQLGetDescField  
 結果セットの UDT 列または UDT パラメーターを使用して取得するストアド プロシージャやパラメーター化クエリのいずれかの追加情報を提供する 4 つの新しいドライバー固有の記述子フィールドが追加されて、 [SQLColAttribute](../../native-client-odbc-api/sqlcolattribute.md)、 [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md)、および[SQLGetDescField](../../native-client-odbc-api/sqlgetdescfield.md)関数。  
  
 新しく追加された記述子フィールドは、SQL_CA_SS_UDT_CATALOG_NAME、SQL_CA_SS_UDT_SCHEMA_NAME、SQL_CA_SS_UDT_TYPE_NAME、および SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME です。  
  
### <a name="sqlcolumns-sqlprocedurecolumns"></a>SQLColumns、SQLProcedureColumns  
 さらに、3 つの新しいドライバー特定列が結果から返されるセットに追加、 [SQLColumns](../../native-client-odbc-api/sqlcolumns.md)と[SQLProcedureColumns](../../native-client-odbc-api/sqlprocedurecolumns.md) UDT 結果のいずれかに関する追加情報を提供する関数列または UDT パラメーターを設定します。 新しく追加された 3 つの列は、SS_UDT_CATALOG_NAME、SS_UDT_SCHEMA_NAME、および SS_UDT_ASSEMBLY_TYPE_NAME です。  
  
### <a name="supported-conversions"></a>サポートされる変換  
 SQL データ型から C データ型に変換する際、SQL_C_WCHAR、SQL_C_BINARY、および SQL_C_CHAR は、すべて SQL_SS_UDT に変換できます。 ただし、SQL_C_WCHAR と SQL_C_CHAR SQL から変換した場合、バイナリ データは 16 進文字列に変換されることに注意してください。  
  
 C データ型から SQL データ型に変換する際、SQL_C_WCHAR、SQL_C_BINARY、および SQL_C_CHAR は、すべて SQL_SS_UDT に変換できます。 ただし、SQL_C_WCHAR と SQL_C_CHAR SQL データ型から変換するときに、16 進文字列にバイナリ データを変換することに注意してください。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Native Client の機能](sql-server-native-client-features.md)   
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
