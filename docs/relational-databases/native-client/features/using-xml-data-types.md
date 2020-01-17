---
title: XML データ型の使用 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- IRowsetChange interface
- IRowsetUpdate interface
- data access [SQL Server Native Client], xml data type
- SQL Server Native Client OLE DB schema rowsets
- PROVIDER_TYPES rowset
- IColumnsInfo interface
- IRowsetFind interface
- IColumnsRowset interface
- PROCEDURE_PARAMETERS rowset
- SQLNCLI, XML
- xml data type [SQL Server], SQL Server Native Client
- SQL Server Native Client, XML
- IRowset interface
- ISequentialStream interface
- ISSCommandWithParameters interface
- SS_XMLSCHEMA rowset
- SQL Server Native Client OLE DB interfaces
- XML [SQL Server], SQL Server Native Client
- COLUMNS rowset
ms.assetid: a7af5b72-c5c2-418d-a636-ae4ac6270ee5
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 05fbec5afe8083bb6c428e496933ca38092a9a9d
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761280"
---
# <a name="using-xml-data-types"></a>XML データ型の使用
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] には **xml** データ型が導入されています。このデータ型を使用すると XML ドキュメントや XML フラグメントを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースに格納できます。 **xml** データ型は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] での組み込みデータ型の 1 つであり、**int** や **varchar** などの他の組み込みデータ型といくつかの点で似ています。 **xml** データ型は、他の組み込みデータ型と同様に、テーブル作成時の列の型、変数の型、パラメーターの型、または関数の戻り値の型として使用したり、CAST 関数や CONVERT 関数でも使用できます。  
  
## <a name="programming-considerations"></a>プログラミングの考慮事項  
 XML は自己記述型で、必要に応じて、次のようにドキュメントのエンコードを指定する XML ヘッダーを含めることができます。  
  
 `<?xml version="1.0" encoding="windows-1252"?><doc/>`  
  
 XML 標準では、ドキュメントの先頭の数バイトを調べることで、ドキュメントで使用しているエンコードを XML プロセッサで検出する方法が説明されています。 アプリケーションで指定するエンコードとドキュメントで指定されているエンコードが競合する場合があります。 バインドされたパラメーターとして渡されるドキュメントの場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では XML がバイナリ データとして扱われるので、データ変換は行われず、XML パーサーはドキュメントに指定されたエンコードを問題なく使用することができます。 ただし、WSTR としてバインドされた XML データの場合、そのドキュメントが Unicode でエンコードされていることをアプリケーションで確認する必要があります。 この場合、必然的にドキュメントが DOM に読み込まれることになり、エンコードが Unicode に変更され、ドキュメントはシリアル化されます。 この処理が行われないと、データ変換が行われ、結果として無効なまたは破損した XML になります。  
  
 また、XML がリテラルで指定された場合も競合が発生する可能性があります。 たとえば、次に示すステートメントは無効です。  
  
 `INSERT INTO xmltable(xmlcol) VALUES('<?xml version="1.0" encoding="UTF-16"?><doc/>')`  
  
 `INSERT INTO xmltable(xmlcol) VALUES(N'<?xml version="1.0" encoding="UTF-8"?><doc/>')`  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB プロバイダー  
 DBTYPE_XML は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの新しい XML 固有のデータ型です。 また、既存の OLE DB 型である DBTYPE_BYTES、DBTYPE_WSTR、DBTYPE_BSTR、DBTYPE_XML、DBTYPE_STR、DBTYPE_VARIANT、および DBTYPE_IUNKNOWN を使用して、XML データにアクセスできます。 XML 型の列に格納されたデータ型は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの行セット内の列から、次の形式で取得できます。  
  
-   テキスト文字列  
  
-   **ISequentialStream**  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーには、SAX リーダーは含まれていませんが、MSXML では**ISequentialStream**を SAX および DOM オブジェクトに簡単に渡すことができます。  
  
 **ISequentialStream**は、大きな XML ドキュメントを取得するために使用する必要があります。 他の大きな値の型で使用される方法と同じ方法を XML でも使用できます。 詳細については、「[大きな値の型の使用](../../../relational-databases/native-client/features/using-large-value-types.md)」を参照してください。  
  
 行セットの XML 型の列に格納されているデータは、アプリケーションで **IRow::GetColumns**、**IRowChange::SetColumns**、**ICommand::Execute** などの通常のインターフェイスを使用することにより、取得、挿入、または更新することもできます。 検索の場合と同様に、アプリケーションプログラムは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーにテキスト文字列または**ISequentialStream**を渡すことができます。  
  
> [!NOTE]  
>  **ISequentialStream** インターフェイスを使用して XML データを文字列形式で送信するには、DBTYPE_IUNKNOWN を指定して **ISequentialStream** を取得し、その *pObject* 引数をバインドの際に NULL に設定する必要があります。  
  
 コンシューマーのバッファーが小さすぎて取得した XML データが切り捨てられるときは、データ長が 0xffffffff で返されます。この値は、長さが不明であることを意味します。 この動作は、実際のデータの前に長さの情報を送信しないでクライアントにストリーム送信されるデータ型の実装と一貫性を持たせています。 場合によっては、プロバイダーが**IRowset:: GetData**などの値全体をバッファーに格納し、データ変換が実行されるときに、実際の長さが返されることがあります。  
  
 SQL Server に送信される XML データは、サーバーではバイナリ データとして扱われます。 その結果、変換が行われず、XML パーサーが XML エンコードを自動検出できます。 これにより、広範な XML ドキュメント (UTF-8 でエンコードされた XML ドキュメントなど) を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] への入力として受け取ることができます。  
  
 入力 XML が DBTYPE_WSTR にバインドされる場合、不要なデータ変換によってデータが破損しないようにするために、アプリケーションでは入力 XML が Unicode でエンコードされていることを確認する必要があります。  
  
### <a name="data-bindings-and-coercions"></a>データ バインドと強制型変換  
 次の表に、特定のデータ型を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の **xml** データ型と共に使用した場合に行われるバインドおよび強制型変換を示します。  
  
|データ型|SQL Server の<br /><br /> **XML**|SQL Server の<br /><br /> **XML 以外へ**|サーバーから<br /><br /> **XML**|サーバーから<br /><br /> **XML 以外へ**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_XML|パス スルー<sup>6、7</sup>|エラー<sup>1</sup>|OK<sup>11、6</sup>|エラー<sup>8</sup>|  
|DBTYPE_BYTES|パス スルー<sup>6、7</sup>|N/A<sup>2</sup>|可 <sup>11、6</sup>|該当なし <sup>2</sup>|  
|DBTYPE_WSTR|パス スルー<sup>6、10</sup>|該当なし <sup>2</sup>|OK<sup>4、6、12</sup>|該当なし <sup>2</sup>|  
|DBTYPE_BSTR|パス スルー<sup>6、10</sup>|該当なし <sup>2</sup>|可 <sup>3</sup>|該当なし <sup>2</sup>|  
|DBTYPE_STR|OK<sup>6、9、10</sup>|該当なし <sup>2</sup>|可<sup>5、6、12</sup>|該当なし <sup>2</sup>|  
|DBTYPE_IUNKNOWN|**ISequentialStream** 経由のバイト ストリーム<sup>7</sup>|該当なし <sup>2</sup>|**ISequentialStream** 経由のバイト ストリーム<sup>11</sup>|該当なし <sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|パス スルー<sup>6、7</sup>|該当なし <sup>2</sup>|なし|該当なし <sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|パス スルー<sup>6、10</sup>|該当なし <sup>2</sup>|可<sup>3</sup>|該当なし <sup>2</sup>|  
  
 <sup>1</sup>DBTYPE_XML 以外のサーバー型が **ICommandWithParameters::SetParameterInfo** で指定され、アクセサー型が DBTYPE_XML の場合、ステートメントの実行時にエラーが発生します (DB_E_ERRORSOCCURRED、パラメーターの状態は DBSTATUS_E_BADACCESSOR)。それ以外の場合は、データがサーバーに送信されますが、XML 型からパラメーターのデータ型への暗黙の変換が行われないことを示すエラーがサーバーから返されます。  
  
 <sup>2</sup>このトピックでは扱いません。  
  
 <sup>3</sup>形式は UTF-16 です。バイト順マーク (BOM)、エンコード仕様、および終端を示す NULL は付加されません。  
  
 <sup>4</sup>形式は UTF-16 です。BOM とエンコード仕様は付加されず、NULL で終端が示されます。  
  
 <sup>5</sup>クライアントのコード ページでエンコードされ、NULL で終端が示される、マルチバイト文字列形式です。 Unicode を使用できるサーバーから変換するとデータが破損する場合があるので、このバインドはお勧めしません。  
  
 <sup>6</sup>BY_REF を使用できます。  
  
 <sup>7</sup>UTF-16 データは BOM で始まる必要があります。 BOM で始まらない場合は、サーバーでエンコードが正しく認識されないことがあります。  
  
 <sup>8</sup>検証は、アクセサーの作成時、またはフェッチ時に行われます。 エラーは DB_E_ERRORSOCCURRED です。その場合、バインドの状態は DBBINDSTATUS_UNSUPPORTEDCONVERSION に設定されます。  
  
 <sup>9</sup>データは、サーバーに送信される前にクライアントのコード ページを使用して Unicode に変換されます。 ドキュメントのエンコードがクライアントのコード ページと一致しない場合、変換によってデータが破損することがあるので、このバインドはお勧めしません。  
  
 <sup>10</sup>サーバーに送信されるデータには必ず BOM が追加されます。 既にデータが BOM で始まる場合、この動作により、バッファーの先頭に 2 つの BOM が存在することになります。 サーバーでは、1 つ目の BOM からエンコードを UTF-16 と認識した後、その BOM を破棄します。 2 つ目の BOM は、幅が 0 の改行を行わない空白文字として解釈されます。  
  
 <sup>11</sup>形式は UTF-16 です。エンコード仕様は付加されません。サーバーから受け取ったデータに BOM が追加されます。 サーバーから空文字列が返されても、アプリケーションには BOM が返されます。 バッファー長が奇数バイトの場合、データは適切に切り捨てられます。 1 つの値が複数のチャンクで返される場合、それぞれを連結して正しい値を再構成できます。  
  
 <sup>12</sup>バッファーの長さが2文字未満の場合 (つまり、null 終了に十分な領域がない場合)、オーバーフローエラーが報告されます。  
  
> [!NOTE]  
>  NULL の XML 値の場合は、データは返されません。  
  
 XML 標準では、UTF-16 でエンコードされた XML をバイト順マーク (BOM) で始める必要があります。BOM は UTF-16 の文字コードでは 0xFEFF です。 WSTR と BSTR バインドを使用する場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、バインドによってエンコードが暗黙的に示されるため、BOM が必要でも追加されません。 BYTES バインド、XML バインド、または IUNKNOWN バインドを使用する場合、その目的は他の XML プロセッサや XML ストレージ システムでの処理を簡単にすることです。 この場合、BOM は UTF-16 でエンコードされた XML を示し、SQL Server を含め XML プロセッサの多くは値の先頭の数バイトを調べてエンコードを推定するので、アプリケーションで実際のエンコードを考慮する必要はありません。 バイト、XML、または IUNKNOWN バインドを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client から受信した XML データは、常に、BOM 付きで UTF-16 でエンコードされ、エンコード宣言は埋め込まれません。  
  
 OLE DB Core Services で提供されるデータ変換 (**IDataConvert**) は、DBTYPE_XML 型には適用できません。  
  
 検証はデータがサーバーに送信されたときに行われます。 クライアント側の検証とエンコードの変更はアプリケーションで処理する必要がありますが、直接処理するのではなく、DOM リーダーや SAX リーダーを使用して XML データを処理することを強くお勧めします。  
  
 DBTYPE_NULL と DBTYPE_EMPTY は入力パラメーターにバインドできますが、出力パラメーターや結果にはバインドできません。 入力パラメーターにバインドした場合、状態を DBSTATUS_S_ISNULL または DBSTATUS_S_DEFAULT に設定する必要があります。  
  
 DBTYPE_XML は DBTYPE_EMPTY および DBTYPE_NULL に変換でき、DBTYPE_EMPTY は DBTYPE_XML に変換できますが、DBTYPE_NULL を DBTYPE_XML に変換することはできません。 この動作は、DBTYPE_WSTR と一貫性があります。  
  
 DBTYPE_IUNKNOWN は上記の表に示したようにサポート済みのバインドですが、DBTYPE_XML と DBTYPE_IUNKNOWN との間では変換は行われません。 DBTYPE_IUNKNOWN は、DBTYPE_BYREF と共に使用することはできません。  
  
### <a name="ole-db-rowset-additions-and-changes"></a>OLE DB 行セットに関する追加事項と変更事項  
 Native Client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、新しい値または多くの主要な OLE DB スキーマ行セットへの変更を追加します。  
  
#### <a name="the-columns-and-procedure_parameters-schema-rowsets"></a>COLUMNS スキーマ行セットと PARAMETERS スキーマ行セット  
 COLUMNS スキーマ行セットと PROCEDURE_PARAMETERS スキーマ行セットに次の列が追加されました。  
  
|列名|[型]|[説明]|  
|-----------------|----------|-----------------|  
|SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML スキーマ コレクションを定義しているカタログの名前。 XML 型以外の列または型指定されていない XML 列の場合は NULL です。|  
|SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|XML スキーマ コレクションを定義しているスキーマの名前。 XML 型以外の列または型指定されていない XML 列の場合は NULL です。|  
|SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|XML スキーマ コレクションの名前。 XML 型以外の列または型指定されていない XML 列の場合は NULL です。|  
  
#### <a name="the-provider_types-schema-rowset"></a>PROVIDER_TYPES スキーマ行セット  
 PROVIDER_TYPES スキーマ行では、**xml** データ型の COLUMN_SIZE の値は 0 で、DATA_TYPE は DBTYPE_XML です。  
  
#### <a name="the-ss_xmlschema-schema-rowset"></a>SS_XMLSCHEMA スキーマ行セット  
 クライアントで XML スキーマ情報を取得できるように、新しいスキーマ行セット SS_XMLSCHEMA が導入されました。 SS_XMLSCHEMA 行セットには、次の列が含まれています。  
  
|列名|[型]|[説明]|  
|-----------------|----------|-----------------|  
|SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML コレクションが属するカタログ。|  
|SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|XML コレクションが属するスキーマ。|  
|SCHEMACOLLECTIONNAME|DBTYPE_WSTR|型指定された XML 列の場合は、XML スキーマ コレクションの名前です。それ以外の場合は、NULL です。|  
|TARGETNAMESPACEURI|DBTYPE_WSTR|XML スキーマの対象名前空間。|  
|SCHEMACONTENT|DBTYPE_WSTR|XML スキーマのコンテンツ。|  
  
 各 XML スキーマのスコープは、カタログ名、スキーマ名、スキーマ コレクション名、および対象名前空間を識別する Uniform Resource Identifier (URI) 別に設定されます。 また、DBSCHEMA_XML_COLLECTIONS という名前の新しい GUID も定義されます。 SS_XMLSCHEMA スキーマ行セットの制限数と制限列は、次のように定義されます。  
  
|GUID|制限数|制限列|  
|----------|----------------------------|------------------------|  
|DBSCHEMA_XML_COLLECTIONS|4|SCHEMACOLLECTION_CATALOGNAME<br /><br /> SCHEMACOLLECTION_SCHEMANAME<br /><br /> SCHEMACOLLECTIONNAME<br /><br /> TARGETNAMESPACEURI|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>OLE DB プロパティ セットに関する追加事項と変更事項  
 Native Client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、主要な OLE DB プロパティセットの多くに新しい値または変更を追加します。  
  
#### <a name="the-dbpropset_sqlserverparameter-property-set"></a>DBPROPSET_SQLSERVERPARAMETER プロパティ セット  
 OLE DB で**xml**データ型をサポートするために、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は、次の値を含む新しい DBPROPSET_SQLSERVERPARAMETER プロパティセットを実装します。  
  
|[オブジェクト名]|[型]|[説明]|  
|----------|----------|-----------------|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML スキーマ コレクションを定義しているカタログ (データベース) の名前。 SQL の 3 部構成による名前の識別子の一部になります。|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|スキーマ コレクションに含まれている XML スキーマの名前。 SQL の 3 部構成による名前の識別子の一部になります。|  
|SSPROP_PARAM_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|カタログに含まれている XML スキーマ コレクションの名前。SQL の 3 部構成による名前の識別子の一部になります。|  
  
#### <a name="the-dbpropset_sqlservercolumn-property-set"></a>DBPROPSET_SQLSERVERCOLUMN プロパティ セット  
 **Itabledefinition**インターフェイスでのテーブルの作成をサポートするために、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は、DBPROPSET_SQLSERVERCOLUMN のプロパティセットに3つの新しい列を追加します。  
  
|[オブジェクト名]|[型]|[説明]|  
|----------|----------|-----------------|  
|SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME|VT_BSTR|型指定された XML 列の場合、このプロパティは XML スキーマが格納されているカタログ名を指定する文字列です。 他のデータ型の列の場合、このプロパティでは空文字列が返されます。|  
|SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME|VT_BSTR|型指定された XML 列の場合、このプロパティはこの列を定義している XML スキーマ名を指定する文字列です。|  
|SSPROP_COL_XML_SCHEMACOLLECTIONNAME|VT_BSTR|型指定された XML 列の場合、このプロパティは値を定義している XML スキーマ コレクション名を指定する文字列です。|  
  
 SSPROP_PARAM 値と同様に、これらのプロパティはすべて省略可能なプロパティで、既定値は空です。 SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME と SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME は、SSPROP_COL_XML_SCHEMACOLLECTIONNAME が指定されている場合のみ指定できます。 XML をサーバーに渡すときにこれらの値が含まれていると、これらの値が妥当かどうかが現在のデータベースとの比較によりチェックされ、インスタンス データがスキーマとの比較によりチェックされます。 どの場合でも、これらはすべて空かすべて設定されている場合に妥当と判断されます。  
  
### <a name="ole-db-interface-additions-and-changes"></a>OLE DB インターフェイスに関する追加事項と変更事項  
 Native Client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、コア OLE DB インターフェイスの多くに新しい値または変更を追加します。  
  
#### <a name="the-isscommandwithparameters-interface"></a>ISSCommandWithParameters インターフェイス  
 OLE DB で**xml**データ型をサポートするために、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、 [Isscommandwithparameters](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)インターフェイスの追加など、多数の変更が実装されています。 この新しいインターフェイスは、主要な OLE DB インターフェイス **ICommandWithParameters** から継承されます。 **ICommandWithParameters**から継承された3つのメソッドに加えて、**Getparameterinfo**、 **Mapparameternames**、および**setparameterinfo**;**Isscommandwithparameters**には、サーバー固有のデータ型を処理するために使用される[getparameterproperties](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)メソッドと[setparameterproperties](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)メソッドが用意されています。  
  
> [!NOTE]  
>  **ISSCommandWithParameters** インターフェイスでは、新しい SSPARAMPROPS 構造体も使用されます。  
  
#### <a name="the-icolumnsrowset-interface"></a>IColumnsRowset インターフェイス  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、 **IColumnRowset:: GetColumnsRowset**メソッドによって返される行セットに、次の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]固有の列が追加されます。 これらの列には、XML スキーマ コレクションの 3 部構成の名前が含まれます。 XML 以外の列または型指定されていない XML 列の場合、これら 3 列の既定値はすべて NULL になります。  
  
|列名|[型]|[説明]|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML スキーマ コレクションが属するカタログ。<br /><br /> それ以外の場合は、NULL です。|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|XML スキーマ コレクションが属するスキーマ。 それ以外の場合は、NULL です。|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|型指定された XML 列の場合は、XML スキーマ コレクションの名前です。それ以外の場合は、NULL です。|  
  
#### <a name="the-irowset-interface"></a>IRowset インターフェイス  
 XML 列内の XML インスタンスは **IRowset::GetData** メソッドを使用して取得されます。 クライアントで指定されているバインドによって異なりますが、XML インスタンスは DBTYPE_BSTR、DBTYPE_WSTR、DBTYPE_VARIANT、DBTYPE_XML、DBTYPE_STR、DBTYPE_BYTES として、または DBTYPE_IUNKNOWN 経由のインターフェイスとして取得できます。 コンシューマーが DBTYPE_BSTR、DBTYPE_WSTR、または DBTYPE_VARIANT を指定すると、プロバイダーで XML インスタンスの型がユーザーが要求した型に変換され、対応するバインドで指定した場所に格納されます。  
  
 コンシューマーが DBTYPE_IUNKNOWN を指定し、*pObject* 引数に NULL を設定した場合、または *pObject* 引数に IID_ISequentialStream を設定した場合、プロバイダーから **ISequentialStream** インターフェイスが返されるので、列の XML データをストリーム出力できます。 その後、**ISequentialStream** から XML データが Unicode 文字のストリームとして返されます。  
  
 プロバイダーは DBTYPE_IUNKNOWN にバインドされた XML 値を返すときに、`sizeof (IUnknown *)` でサイズ値を報告します。 この動作は、列が DBTYPE_IUnknown または DBTYPE_IDISPATCH としてバインドされる場合行われる動作、および正確な列のサイズを特定できない場合に DBTYPE_IUNKNOWN や ISequentialStream で行われる動作と同じです。  
  
#### <a name="the-irowsetchange-interface"></a>IRowsetChange インターフェイス  
 コンシューマーは、列の XML インスタンスを 2 とおりの方法で更新できます。 1 つ目の方法では、プロバイダーで作成されるストレージ オブジェクト **ISequentialStream** を使用します。 コンシューマーは **ISequentialStream::Write** メソッドを呼び出して、プロバイダーから返された XML インスタンスを直接更新できます。  
  
 2 つ目の方法では、**IRowsetChange::SetData** メソッドまたは **IRowsetChange::InsertRow** メソッドを使用します。 この方法では、コンシューマーのバッファーにある XML インスタンスを DBTYPE_BSTR、DBTYPE_WSTR、DBTYPE_VARIANT、DBTYPE_XML、または DBTYPE_IUNKNOWN 型のバインドで指定できます。  
  
 DBTYPE_BSTR、DBTYPE_WSTR、または DBTYPE_VARIANT の場合、コンシューマーのバッファーに存在する XML インスタンスがプロバイダーによって適切な列に格納されます。  
  
 DBTYPE_IUNKNOWN/ISequentialStream の場合、コンシューマーがストレージオブジェクトを指定していない場合は、コンシューマーが**ISequentialStream**オブジェクトを事前に作成し、XML ドキュメントをオブジェクトにバインドしてから、 **IRowsetChange:: SetData**メソッドを使用してそのオブジェクトをプロバイダーに渡す必要があります。 また、ストレージ オブジェクトを作成して pObject 引数に IID_ISequentialStream を設定し、**ISequentialStream** オブジェクトを作成してから、その **ISequentialStream** オブジェクトを **IRowsetChange::SetData** メソッドに渡すこともできます。 どちらの場合も、プロバイダーは **ISequentialStream** オブジェクトを使用して XML オブジェクトを取得し、それを適切な列に挿入できます。  
  
#### <a name="the-irowsetupdate-interface"></a>IRowsetUpdate インターフェイス  
 **IRowsetUpdate** インターフェイスには遅延更新のための機能が用意されています。 行セットで使用できるデータは、コンシューマーが**IRowsetUpdate: Update**メソッドを呼び出すまで、他のトランザクションでは使用できません。  
  
#### <a name="the-irowsetfind-interface"></a>IRowsetFind インターフェイス  
 **IRowsetFind::FindNextRow** メソッドでは、**xml** データ型を処理できません。 **hAccessor** 引数に DBTYPE_XML の列を指定して *IRowsetFind::FindNextRow* を呼び出すと、DB_E_BADBINDINFO が返されます。 この動作は、検索対象の列の型とは無関係に行われます。 その他のバインドの型では、検索対象の列が **xml** データ型の場合、**FindNextRow** が DB_E_BADCOMPAREOP を返して失敗します。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC ドライバー  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、 **xml**データ型をサポートするために、さまざまな関数にいくつかの変更が加えられています。  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 [Sqlcolattribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md)関数には、SQL_CA_SS_XML_SCHEMACOLLECTION_CATALOG_NAME、SQL_CA_SS_XML_SCHEMACOLLECTION_SCHEMA_NAME、SQL_CA_SS _XML_SCHEMACOLLECTION_NAME を含む3つの新しいフィールド識別子があります。  
  
 Native Client ODBC ドライバー [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、SQL_DESC_DISPLAY_SIZE および SQL_DESC_LENGTH 列の SQL_SS_LENGTH_UNLIMITED を報告します。  
  
### <a name="sqlcolumns"></a>SQLColumns  
 [Sqlcolumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)関数には、SS_XML_SCHEMACOLLECTION_CATALOG_NAME、SS_XML_SCHEMACOLLECTION_SCHEMA_NAME、SS_XML_SCHEMACOLLECTION_NAME を含む3つの新しい列があります。 既存の TYPE_NAME 列を使用して XML 型の名前が示されます。XML 型の列または XML 型のパラメーターの DATA_TYPE は SQL_SS_XML になります。  
  
 Native Client ODBC ドライバー [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、COLUMN_SIZE と CHAR_OCTET_LENGTH の値について SQL_SS_LENGTH_UNLIMITED を報告します。  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、列のサイズを[SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md)関数で特定できない場合に SQL_SS_LENGTH_UNLIMITED を報告します。  
  
### <a name="sqlgettypeinfo"></a>SQLGetTypeInfo  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、 [SQLGetTypeInfo](../../../relational-databases/native-client-odbc-api/sqlgettypeinfo.md)関数の**xml**データ型の最大 COLUMN_SIZE として SQL_SS_LENGTH_UNLIMITED を報告します。  
  
### <a name="sqlprocedurecolumns"></a>SQLProcedureColumns  
 [SQLProcedureColumns](../../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md)関数には、 **sqlcolumns**関数と同じ列が追加されています。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、 **xml**データ型の最大 COLUMN_SIZE として SQL_SS_LENGTH_UNLIMITED を報告します。  
  
### <a name="supported-conversions"></a>サポートされる変換  
 SQL データ型から C データ型に変換する際、SQL_C_WCHAR、SQL_C_BINARY、および SQL_C_CHAR は、次の条件下ですべて SQL_SS_XML に変換できます。  
  
-   SQL_C_WCHAR: 形式は UTF-16 で、バイト順マーク (BOM) は付加されず、NULL で終端が示されます。  
  
-   SQL_C_BINARY: 形式は UTF-16 で、NULL で終端は示されません。 サーバーから受け取ったデータに BOM が追加されます。 サーバーから空文字列が返されても、アプリケーションには BOM が返されます。 バッファー長が奇数バイトの場合、データは適切に切り捨てられます。 1 つの値が複数のチャンクで返される場合、それぞれを連結して正しい値を再構成できます。  
  
-   SQL_C_CHAR: クライアント コード ページでエンコードされ、NULL で終端が示される、マルチバイト文字列形式です。 UTF-16 を使用できるサーバーから変換するとデータが破損する場合があるので、このバインドはお勧めしません。  
  
 C データ型から SQL データ型に変換する際、SQL_C_WCHAR、SQL_C_BINARY、および SQL_C_CHAR は、次の条件下ですべて SQL_SS_XML に変換できます。  
  
-   SQL_C_WCHAR: サーバーに送信されるデータには必ず BOM が追加されます。 既にデータが BOM で始まる場合、この動作により、バッファーの先頭に 2 つの BOM が存在することになります。 サーバーでは、1 つ目の BOM からエンコードを UTF-16 と認識した後、その BOM を破棄します。 2 つ目の BOM は、幅が 0 の改行を行わない空白文字として解釈されます。  
  
-   SQL_C_BINARY: 変換が行われないので、データはそのままの状態でサーバーに渡されます。 UTF-16 データは BOM で始まる必要があります。BOM で始まらない場合、エンコードがサーバーで適切に認識されません。  
  
-   SQL_C_CHAR: データはクライアント上で UTF-16 に変換され、サーバーにそのまま SQL_C_WCHAR として送信されます (ただし、BOM が追加されます)。 XML がクライアントのコード ページでエンコードされない場合、この変換が原因でデータが破損することがあります。  
  
 XML 標準では、UTF-16 でエンコードされた XML をバイト順マーク (BOM) で始める必要があります。BOM は UTF-16 の文字コードでは 0xFEFF です。 バインドによってエンコードが暗黙的に使用されるため、SQL_C_BINARY バインドを使用する場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は BOM を必要としないか追加します。 SQL_C_BINARY バインドを使用する目的は、その他の XML プロセッサや XML ストレージ システムでの処理を簡単にすることです。 この場合、BOM は UTF-16 でエンコードされた XML を示し、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を含め XML プロセッサの多くは値の先頭の数バイトを調べてエンコードを推定するので、アプリケーションで実際のエンコードを考慮する必要はありません。 SQL_C_BINARY バインディングを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client から受信した XML データは、常に、BOM を持つ UTF-16 でエンコードされ、エンコード宣言は埋め込まれません。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client の機能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
