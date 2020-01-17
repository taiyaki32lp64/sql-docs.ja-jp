---
title: XML データ型の使用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 9e640f495d216495141131519e0b9aa51d48de4d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63136664"
---
# <a name="using-xml-data-types"></a>XML データ型の使用
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
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、SAX リーダーは含まれませんが、 **ISequentialStream** msxml SAX、DOM オブジェクトに簡単に渡すことができます。  
  
 **ISequentialStream**大きな XML ドキュメントの取得のために使用をする必要があります。 他の大きな値の型で使用される方法と同じ方法を XML でも使用できます。 詳細については、次を参照してください。[大きな値の型を使用して](using-large-value-types.md)します。  
  
 行セットの XML 型の列に格納されているデータは、アプリケーションで **IRow::GetColumns**、**IRowChange::SetColumns**、**ICommand::Execute** などの通常のインターフェイスを使用することにより、取得、挿入、または更新することもできます。 同様に取得の場合に、アプリケーション プログラムを渡すことができます、テキスト文字列または**ISequentialStream**を[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB プロバイダー。  
  
> [!NOTE]  
>  **ISequentialStream** インターフェイスを使用して XML データを文字列形式で送信するには、DBTYPE_IUNKNOWN を指定して **ISequentialStream** を取得し、その *pObject* 引数をバインドの際に NULL に設定する必要があります。  
  
 コンシューマーのバッファーが小さすぎて取得した XML データが切り捨てられるときは、データ長が 0xffffffff で返されます。この値は、長さが不明であることを意味します。 この動作は、実際のデータの前に長さの情報を送信しないでクライアントにストリーム送信されるデータ型の実装と一貫性を持たせています。 場合によっては、実際の長さは、プロバイダーがなど、値全体をバッファーがときに返される**irowset::getdata**データ変換が実行されます。  
  
 SQL Server に送信される XML データは、サーバーではバイナリ データとして扱われます。 その結果、変換が行われず、XML パーサーが XML エンコードを自動検出できます。 これにより、広範な XML ドキュメント (UTF-8 でエンコードされた XML ドキュメントなど) を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] への入力として受け取ることができます。  
  
 入力 XML が DBTYPE_WSTR にバインドされる場合、不要なデータ変換によってデータが破損しないようにするために、アプリケーションでは入力 XML が Unicode でエンコードされていることを確認する必要があります。  
  
### <a name="data-bindings-and-coercions"></a>データ バインドと強制型変換  
 次の表に、特定のデータ型を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の **xml** データ型と共に使用した場合に行われるバインドおよび強制型変換を示します。  
  
|データ型|SQL Server の<br /><br /> **XML**|SQL Server の<br /><br /> **XML 以外から**|サーバーから<br /><br /> **XML**|サーバーから<br /><br /> **XML 以外から**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_XML|パス スルー<sup>6、7</sup>|エラー<sup>1</sup>|[OK]<sup>11、6</sup>|エラー<sup>8</sup>|  
|DBTYPE_BYTES|パス スルー<sup>6、7</sup>|該当なし<sup>2</sup>|可 <sup>11、6</sup>|該当なし <sup>2</sup>|  
|DBTYPE_WSTR|パス スルー<sup>6、10</sup>|該当なし <sup>2</sup>|[OK]<sup>4、6、12</sup>|該当なし <sup>2</sup>|  
|DBTYPE_BSTR|パス スルー<sup>6、10</sup>|該当なし <sup>2</sup>|可 <sup>3</sup>|該当なし <sup>2</sup>|  
|DBTYPE_STR|[OK]<sup>6、9、10</sup>|該当なし <sup>2</sup>|可<sup>5、6、12</sup>|該当なし <sup>2</sup>|  
|DBTYPE_IUNKNOWN|**ISequentialStream** 経由のバイト ストリーム<sup>7</sup>|該当なし <sup>2</sup>|**ISequentialStream** 経由のバイト ストリーム<sup>11</sup>|該当なし <sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|パス スルー<sup>6、7</sup>|該当なし <sup>2</sup>|なし|該当なし <sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|パス スルー<sup>6、10</sup>|該当なし <sup>2</sup>|可<sup>3</sup>|該当なし <sup>2</sup>|  
  
 <sup>1</sup>サーバー以外の型に dbtype_xml 型が指定されて場合**icommandwithparameters::setparameterinfo**アクセサーの型が dbtype_xml 型、およびステートメントが実行されたときにエラーが発生した (DB_E_ERRORSOCCURRED、パラメーターの状態は dbstatus_e_badaccessor になります) です。サーバーにデータが送信されるそれ以外の場合がサーバーには、XML からパラメーターのデータ型への暗黙的な変換がないことを示すエラーが返されます。  
  
 <sup>2</sup>このトピックの範囲を超えています。  
  
 <sup>3</sup>形式は UTF-16 です。バイト順マーク (BOM)、エンコード仕様、および終端を示す NULL は付加されません。  
  
 <sup>4</sup>形式は UTF-16 です。BOM とエンコード仕様は付加されず、NULL で終端が示されます。  
  
 <sup>5</sup>クライアントのコード ページでエンコードされ、NULL で終端が示される、マルチバイト文字列形式です。 Unicode を使用できるサーバーから変換するとデータが破損する場合があるので、このバインドはお勧めしません。  
  
 <sup>6</sup>BY_REF を使用できます。  
  
 <sup>7</sup>UTF-16 データは BOM で始まる必要があります。 BOM で始まらない場合は、サーバーでエンコードが正しく認識されないことがあります。  
  
 <sup>8</sup>検証は、アクセサーの作成時、またはフェッチ時に行われます。 エラーは DB_E_ERRORSOCCURRED です。その場合、バインドの状態は DBBINDSTATUS_UNSUPPORTEDCONVERSION に設定されます。  
  
 <sup>9</sup>データは、サーバーに送信される前にクライアントのコード ページを使用して Unicode に変換されます。 ドキュメントのエンコードがクライアントのコード ページと一致しない場合、変換によってデータが破損することがあるので、このバインドはお勧めしません。  
  
 <sup>10</sup>サーバーに送信されるデータには必ず BOM が追加されます。 既にデータが BOM で始まる場合、この動作により、バッファーの先頭に 2 つの BOM が存在することになります。 サーバーでは、1 つ目の BOM からエンコードを UTF-16 と認識した後、その BOM を破棄します。 2 つ目の BOM は、幅が 0 の改行を行わない空白文字として解釈されます。  
  
 <sup>11</sup>形式は UTF-16 です。エンコード仕様は付加されません。サーバーから受け取ったデータに BOM が追加されます。 サーバーから空文字列が返されても、アプリケーションには BOM が返されます。 バッファー長が奇数バイトの場合、データは適切に切り捨てられます。 1 つの値が複数のチャンクで返される場合、それぞれを連結して正しい値を再構成できます。  
  
 <sup>12</sup>バッファー長が 2 未満である文字、null で終端--の領域が不足している場合、オーバーフロー エラーが報告されます。  
  
> [!NOTE]  
>  NULL の XML 値の場合は、データは返されません。  
  
 XML 標準では、UTF-16 でエンコードされた XML をバイト順マーク (BOM) で始める必要があります。BOM は UTF-16 の文字コードでは 0xFEFF です。 WSTR と BSTR のバインディングを使用する場合[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client が必要がありますまたはバインドによってエンコードが暗黙的に BOM を追加していません。 BYTES バインド、XML バインド、または IUNKNOWN バインドを使用する場合、その目的は他の XML プロセッサや XML ストレージ システムでの処理を簡単にすることです。 この場合、BOM は UTF-16 でエンコードされた XML を示し、SQL Server を含め XML プロセッサの多くは値の先頭の数バイトを調べてエンコードを推定するので、アプリケーションで実際のエンコードを考慮する必要はありません。 受信した XML データ[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client (バイト)、XML、または IUNKNOWN を使用してバインドは常にでエンコードされた utf-16 BOM とエンコード宣言は埋め込まれません。  
  
 OLE DB Core Services で提供されるデータ変換 (**IDataConvert**) は、DBTYPE_XML 型には適用できません。  
  
 検証はデータがサーバーに送信されたときに行われます。 クライアント側の検証とエンコードの変更はアプリケーションで処理する必要がありますが、直接処理するのではなく、DOM リーダーや SAX リーダーを使用して XML データを処理することを強くお勧めします。  
  
 DBTYPE_NULL と DBTYPE_EMPTY は入力パラメーターにバインドできますが、出力パラメーターや結果にはバインドできません。 入力パラメーターにバインドした場合、状態を DBSTATUS_S_ISNULL または DBSTATUS_S_DEFAULT に設定する必要があります。  
  
 DBTYPE_XML は DBTYPE_EMPTY および DBTYPE_NULL に変換でき、DBTYPE_EMPTY は DBTYPE_XML に変換できますが、DBTYPE_NULL を DBTYPE_XML に変換することはできません。 この動作は、DBTYPE_WSTR と一貫性があります。  
  
 DBTYPE_IUNKNOWN は上記の表に示したようにサポート済みのバインドですが、DBTYPE_XML と DBTYPE_IUNKNOWN との間では変換は行われません。 DBTYPE_IUNKNOWN は、DBTYPE_BYREF と共に使用することはできません。  
  
### <a name="ole-db-rowset-additions-and-changes"></a>OLE DB 行セットに関する追加事項と変更事項  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、新しい値が追加され、多くの主要な OLE DB スキーマ行セットへの変更します。  
  
#### <a name="the-columns-and-procedureparameters-schema-rowsets"></a>COLUMNS スキーマ行セットと PARAMETERS スキーマ行セット  
 COLUMNS スキーマ行セットと PROCEDURE_PARAMETERS スキーマ行セットに次の列が追加されました。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML スキーマ コレクションを定義しているカタログの名前。 XML 型以外の列または型指定されていない XML 列の場合は NULL です。|  
|SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|XML スキーマ コレクションを定義しているスキーマの名前。 XML 型以外の列または型指定されていない XML 列の場合は NULL です。|  
|SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|XML スキーマ コレクションの名前。 XML 型以外の列または型指定されていない XML 列の場合は NULL です。|  
  
#### <a name="the-providertypes-schema-rowset"></a>PROVIDER_TYPES スキーマ行セット  
 PROVIDER_TYPES スキーマ行では、**xml** データ型の COLUMN_SIZE の値は 0 で、DATA_TYPE は DBTYPE_XML です。  
  
#### <a name="the-ssxmlschema-schema-rowset"></a>SS_XMLSCHEMA スキーマ行セット  
 クライアントで XML スキーマ情報を取得できるように、新しいスキーマ行セット SS_XMLSCHEMA が導入されました。 SS_XMLSCHEMA 行セットには、次の列が含まれています。  
  
|列名|型|説明|  
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
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、新しい値を追加します。 またはに多くの主要な OLE DB プロパティ セットを変更します。  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>DBPROPSET_SQLSERVERPARAMETER プロパティ セット  
 サポートするために、 **xml** OLE DB でのデータ型[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client では、次の値を含む新しい DBPROPSET_SQLSERVERPARAMETER プロパティ セット。  
  
|名前|型|説明|  
|----------|----------|-----------------|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML スキーマ コレクションを定義しているカタログ (データベース) の名前。 SQL の 3 部構成による名前の識別子の一部になります。|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|スキーマ コレクションに含まれている XML スキーマの名前。 SQL の 3 部構成による名前の識別子の一部になります。|  
|SSPROP_PARAM_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|カタログに含まれている XML スキーマ コレクションの名前。SQL の 3 部構成による名前の識別子の一部になります。|  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>DBPROPSET_SQLSERVERCOLUMN プロパティ セット  
 内のテーブルの作成をサポートするために、 **ITableDefinition**インターフェイス、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は、DBPROPSET_SQLSERVERCOLUMN プロパティ セットに 3 つの新しい列を追加します。  
  
|名前|型|説明|  
|----------|----------|-----------------|  
|SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME|VT_BSTR|型指定された XML 列の場合、このプロパティは XML スキーマが格納されているカタログ名を指定する文字列です。 他のデータ型の列の場合、このプロパティでは空文字列が返されます。|  
|SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME|VT_BSTR|型指定された XML 列の場合、このプロパティはこの列を定義している XML スキーマ名を指定する文字列です。|  
|SSPROP_COL_XML_SCHEMACOLLECTIONNAME|VT_BSTR|型指定された XML 列の場合、このプロパティは値を定義している XML スキーマ コレクション名を指定する文字列です。|  
  
 SSPROP_PARAM 値と同様に、これらのプロパティはすべて省略可能なプロパティで、既定値は空です。 SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME と SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME は、SSPROP_COL_XML_SCHEMACOLLECTIONNAME が指定されている場合のみ指定できます。 XML をサーバーに渡すときにこれらの値が含まれていると、これらの値が妥当かどうかが現在のデータベースとの比較によりチェックされ、インスタンス データがスキーマとの比較によりチェックされます。 どの場合でも、これらはすべて空かすべて設定されている場合に妥当と判断されます。  
  
### <a name="ole-db-interface-additions-and-changes"></a>OLE DB インターフェイスに関する追加事項と変更事項  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、新しい値が追加または多くの主要な OLE DB インターフェイスに変更します。  
  
#### <a name="the-isscommandwithparameters-interface"></a>ISSCommandWithParameters インターフェイス  
 サポートするために、 **xml** OLE DB でのデータ型[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client では、多数の変更の追加など、 [ISSCommandWithParameters](../../native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)インターフェイス。 この新しいインターフェイスは、主要な OLE DB インターフェイス **ICommandWithParameters** から継承されます。 継承した次の 3 つのメソッドだけでなく**ICommandWithParameters**;**GetParameterInfo**、 **MapParameterNames**、および**SetParameterInfo**;**ISSCommandWithParameters**提供、 [GetParameterProperties](../../native-client-ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)と[SetParameterProperties](../../native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)サーバー固有の処理に使用されるメソッドデータ型。  
  
> [!NOTE]  
>  **ISSCommandWithParameters** インターフェイスでは、新しい SSPARAMPROPS 構造体も使用されます。  
  
#### <a name="the-icolumnsrowset-interface"></a>IColumnsRowset インターフェイス  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は、以下を追加します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-特定の列によって返される行セットに、 **:getcolumnsrowset**メソッド。 これらの列には、XML スキーマ コレクションの 3 部構成の名前が含まれます。 XML 以外の列または型指定されていない XML 列の場合、これら 3 列の既定値はすべて NULL になります。  
  
|列名|型|説明|  
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
  
 2 つ目の方法では、**IRowsetChange::SetData** メソッドまたは **IRowsetChange::InsertRow** メソッドを使用します。 この方法では、コンシューマーのバッファー内の XML インスタンスは DBTYPE_BSTR、DBTYPE_WSTR、DBTYPE_VARIANT、DBTYPE_XML と DBTYPE_IUNKNOWN 型のバインドで指定できます。  
  
 DBTYPE_BSTR、DBTYPE_WSTR、または DBTYPE_VARIANT の場合、コンシューマーのバッファーに存在する XML インスタンスがプロバイダーによって適切な列に格納されます。  
  
 DBTYPE_IUNKNOWN と isequentialstream をコンシューマーが、任意のストレージ オブジェクトを指定しない場合、コンシューマー作成する必要があります、 **ISequentialStream**オブジェクトをあらかじめ、オブジェクト、XML ドキュメントをバインドし、オブジェクトを渡します使用して、プロバイダー、 **irowsetchange::setdata**メソッド。 また、ストレージ オブジェクトを作成して pObject 引数に IID_ISequentialStream を設定し、**ISequentialStream** オブジェクトを作成してから、その **ISequentialStream** オブジェクトを **IRowsetChange::SetData** メソッドに渡すこともできます。 どちらの場合も、プロバイダーは **ISequentialStream** オブジェクトを使用して XML オブジェクトを取得し、それを適切な列に挿入できます。  
  
#### <a name="the-irowsetupdate-interface"></a>IRowsetUpdate インターフェイス  
 **IRowsetUpdate** インターフェイスには遅延更新のための機能が用意されています。 行セットで使用できるデータがコンシューマー呼び出されるまでは他のトランザクションから使用できない、 **IRowsetUpdate:Update**メソッド。  
  
#### <a name="the-irowsetfind-interface"></a>IRowsetFind インターフェイス  
 **IRowsetFind::FindNextRow** メソッドでは、**xml** データ型を処理できません。 *hAccessor* 引数に DBTYPE_XML の列を指定して **IRowsetFind::FindNextRow** を呼び出すと、DB_E_BADBINDINFO が返されます。 この動作は、検索対象の列の型とは無関係に行われます。 その他のバインドの型では、検索対象の列が **xml** データ型の場合、**FindNextRow** が DB_E_BADCOMPAREOP を返して失敗します。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC ドライバー  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、変更の数に加えさまざまな機能をサポートする、 **xml**データ型。  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 [SQLColAttribute](../../native-client-odbc-api/sqlcolattribute.md)関数には、SQL_CA_SS_XML_SCHEMACOLLECTION_CATALOG_NAME、SQL_CA_SS_XML_SCHEMACOLLECTION_SCHEMA_NAME、sql_ca_ss _XML_SCHEMACOLLECTION_NAME を含む、3 つの新しいフィールド識別子。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーが、SQL_DESC_DISPLAY_SIZE 列と SQL_DESC_LENGTH 列に関して SQL_SS_LENGTH_UNLIMITED を報告します。  
  
### <a name="sqlcolumns"></a>SQLColumns  
 [SQLColumns](../../native-client-odbc-api/sqlcolumns.md)関数には、次の 3 つの新しい列を含むという、SS_XML_SCHEMACOLLECTION_SCHEMA_NAME、および追加されました。 既存の TYPE_NAME 列を使用して XML 型の名前が示されます。XML 型の列または XML 型のパラメーターの DATA_TYPE は SQL_SS_XML になります。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、column_size 値と CHAR_OCTET_LENGTH 値に関して SQL_SS_LENGTH_UNLIMITED を報告します。  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]で、列のサイズを特定できない場合、Native Client ODBC ドライバーは SQL_SS_LENGTH_UNLIMITED を報告、 [SQLDescribeCol](../../native-client-odbc-api/sqldescribecol.md)関数。  
  
### <a name="sqlgettypeinfo"></a>SQLGetTypeInfo  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、column_size の最大の値として SQL_SS_LENGTH_UNLIMITED を報告、 **xml**のデータ型の[SQLGetTypeInfo](../../native-client-odbc-api/sqlgettypeinfo.md)関数。  
  
### <a name="sqlprocedurecolumns"></a>SQLProcedureColumns  
 [SQLProcedureColumns](../../native-client-odbc-api/sqlprocedurecolumns.md)関数が同じ列の追加として、 **SQLColumns**関数。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、column_size の最大の値として SQL_SS_LENGTH_UNLIMITED を報告、 **xml**データ型。  
  
### <a name="supported-conversions"></a>サポートされる変換  
 SQL データ型から C データ型に変換する際、SQL_C_WCHAR、SQL_C_BINARY、および SQL_C_CHAR は、次の条件下ですべて SQL_SS_XML に変換できます。  
  
-   SQL_C_WCHAR:形式は、null で終端 utf-16 バイト順マーク (BOM) なし。  
  
-   SQL_C_BINARY:形式では、utf-16 はない null で終端します。 サーバーから受け取ったデータに BOM が追加されます。 サーバーから空文字列が返されても、アプリケーションには BOM が返されます。 バッファー長が奇数バイトの場合、データは適切に切り捨てられます。 1 つの値が複数のチャンクで返される場合、それぞれを連結して正しい値を再構成できます。  
  
-   SQL_C_CHAR:形式は、null で終端のクライアント コード ページでエンコードされたマルチバイト文字です。 UTF-16 を使用できるサーバーから変換するとデータが破損する場合があるので、このバインドはお勧めしません。  
  
 C データ型から SQL データ型に変換する際、SQL_C_WCHAR、SQL_C_BINARY、および SQL_C_CHAR は、次の条件下ですべて SQL_SS_XML に変換できます。  
  
-   SQL_C_WCHAR:BOM は、サーバーに送信されるデータに常に追加されます。 既にデータが BOM で始まる場合、この動作により、バッファーの先頭に 2 つの BOM が存在することになります。 サーバーでは、1 つ目の BOM からエンコードを UTF-16 と認識した後、その BOM を破棄します。 2 つ目の BOM は、幅が 0 の改行を行わない空白文字として解釈されます。  
  
-   SQL_C_BINARY:変換は行われません、および"です」と、サーバーにデータが渡される UTF-16 データは BOM で始まる必要があります。BOM で始まらない場合、エンコードがサーバーで適切に認識されません。  
  
-   SQL_C_CHAR:データでは、クライアントで utf-16 に変換され、SQL_C_WCHAR (、BOM が追加を含む) と同様に、サーバーに送信します。 XML がクライアントのコード ページでエンコードされない場合、この変換が原因でデータが破損することがあります。  
  
 XML 標準では、UTF-16 でエンコードされた XML をバイト順マーク (BOM) で始める必要があります。BOM は UTF-16 の文字コードでは 0xFEFF です。 SQL_C_BINARY バインドを使用する場合[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client が必要がありますまたはバインドによってエンコードが暗黙的に、BOM を追加していません。 SQL_C_BINARY バインドを使用する目的は、その他の XML プロセッサや XML ストレージ システムでの処理を簡単にすることです。 この場合、BOM は UTF-16 でエンコードされた XML を示し、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を含め XML プロセッサの多くは値の先頭の数バイトを調べてエンコードを推定するので、アプリケーションで実際のエンコードを考慮する必要はありません。 受信した XML データ[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client SQL_C_BINARY を使用してバインドは常にでエンコードされた utf-16 BOM とエンコード宣言は埋め込まれません。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client の機能](sql-server-native-client-features.md)   
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
