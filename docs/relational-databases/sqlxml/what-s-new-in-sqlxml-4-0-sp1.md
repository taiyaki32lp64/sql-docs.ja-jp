---
title: SQLXML 4.0 SP1 の新機能&#39;
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- registry keys [SQLXML]
- SQLNCLI, SQLXML
- what's new [SQLXML]
- SQLXML, what's new
- migrating SQLXML applications
- redistributing SQLXML
- SQL Server Native Client, SQLXML
- side-by-side installations [SQLXML]
ms.assetid: 48f7720b-1705-402d-93ce-097ff1737877
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 64d531dc8eeee5a55cb0bcabbee14c06e1e5db93
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252155"
---
# <a name="what39s-new-in-sqlxml-40-sp1"></a>SQLXML 4.0 SP1 の新機能&#39;
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 SP1 では、多くの更新と拡張が行われています。 ここでは、更新内容についてまとめ、詳細情報がある場合はそのリンクを提供します。 SQLXML 4.0 SP1 では、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] で導入された新しいデータ型をサポートするための追加の拡張が行われています。 このトピックの項目は次のとおりです。  
  
-   SQLXML 4.0 SP1 のインストール  
  
-   サイド バイ サイド インストールに関する問題  
  
-   SQLXML 4.0 と MSXML  
  
-   SQLXML 4.0 の再配布  
  
-   Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のサポート  
  
-   
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] で導入されたデータ型のサポート  
  
-   SQLXML 4.0 での XML 一括読み込みの変更点  
  
-   SQLXML 4.0 でのレジストリ キーの変更点  
  
-   移行の問題  
  
## <a name="installing-sqlxml-40-sp1"></a>SQLXML 4.0 SP1 のインストール  
 
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] より前のバージョンでは、SQLXML 4.0 は SQL Server に付属してリリースされ、SQL Server のすべてのバージョン (SQL Server Express を除く) の既定のインストールに含まれていました。 
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降の SQL Server には、SQLXML の最新バージョン (SQLXML 4.0 SP1) が含まれないようになりました。 SQLXML 4.0 SP1 をインストールするには、 [sqlxml 4.0 sp1 のインストール場所](https://www.microsoft.com/download/details.aspx?id=30403)からダウンロードします。  
  
 SQLXML 4.0 SP1 のファイルは次の場所にインストールされます。  
  
 `%PROGRAMFILES%\SQLXML 4.0\`  
  
> [!NOTE]  
>  SQLXML 4.0 に必要なレジストリ設定はすべて、インストール処理の一部として行われます。  
  
 32 ビットの SQLXML アプリケーションを 64 ビット Windows オペレーティング システム上の Windows on Windows (WOW64) で実行できるようにするには、64 ビットの SQLXML 4.0 SP1 パッケージ (sqlxml4.msi) を実行してください。このパッケージは、ダウンロード センターで入手できます。  
  
#### <a name="uninstalling-sqlxml-40-sp1"></a>SQLXML 4.0 SP1 のアンインストール  
 SQLXML 3.0 SP3、SQLXML 4.0、および SQLXML 4.0 SP1 には、共有のレジストリ キーがあります。 SQLXML 3.0 SP3 があるコンピューター上で SQLXML のより新しいバージョンをアンインストールすると、SQLXML 3.0 SP3 を再インストールする必要が生じる場合もあります。  
  
## <a name="side-by-side-installation-issues"></a>サイド バイ サイド インストールに関する問題  
 SQLXML 4.0 のインストール処理では、以前のバージョンの SQLXML でインストールされたファイルは削除されません。 したがって、コンピューターに、バージョンの異なる SQLXML の DLL を複数インストールして、 同時に実行することができます。 SQLXML 4.0 には、バージョン固有ではない PROGID とバージョン固有の PROGID の両方が含まれています。 すべての製品アプリケーションでは、バージョン固有の PROGID を使用する必要があります。  
  
## <a name="sqlxml-40-sp1-and-msxml"></a>SQLXML 4.0 SP1 と MSXML  
 SQLXML 4.0 では、MSXML はインストールされません。 SQLXML 4.0 では MSXML 6.0 が使用されますが、これは [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のインストール時にその一部としてインストールされます。  
  
## <a name="redistributing-sqlxml-40-sp1"></a>SQLXML 4.0 SP1 の再配布  
 SQLXML 4.0 SP1 は、再配布可能インストーラー パッケージを使って再配布できます。 チェイナーとブートストラップのテクノロジを使用すると、ユーザーが 1 回のインストール手順に従うだけで複数のパッケージをまとめてインストールできるようになります。 詳細については、「Visual Studio 2005 用のカスタム ブートストラップ パッケージの作成」および「カスタムの必須コンポーネントの追加」をご覧ください。  
  
 アプリケーションが、開発時に使用したものとは異なるプラットフォームを対象としている場合、Microsoft ダウンロード センターから x64、Itanium、および x86 用のバージョンの sqlncli.msi をダウンロードできます。  
  
 MSXML 6.0 には、個別の再配布インストール プログラム (msxml6.msi) もあります。 これらのプログラムは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール CD の次の場所にあります。  
  
 `%CD%\Setup\`  
  
 これらのインストール ファイルを使用すると、MSXML 6.0 を CD から直接インストールできます。 インストール ファイルは、独自に作成したアプリケーションと共に MSXML 6.0 と SQLXML 4.0 SP1 を再配布するときにも自由に使用できます。  
  
 独自のアプリケーションでデータ プロバイダーとして使用する場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client も再配布する必要があります。 詳細については、「 [SQL Server Native Client のインストール](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)」を参照してください。  
  
## <a name="support-for-sql-server-native-client"></a>SQL Server Native Client のサポート  
 SQLXML 4.0 では、SQLOLEDB と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client プロバイダーの両方がサポートされています。 Native client は、native client の**日付、時刻**、 **DateTime2**、および[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **dateTimeOffset**データ型[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]など、サーバーに出荷される新しいデータ型をサポートするように開発されているため、同じバージョンの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client プロバイダーとを使用することをお勧めします。  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client は、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] で導入されたデータ アクセス テクノロジです。 これは SQLOLEDB プロバイダーと SQLODBC ドライバーを組み合わせて 1 つのネイティブ ダイナミック リンク ライブラリ (DLL) にしたものです。Microsoft Data Access Components (MDAC) とは独立した新しい機能も提供されます。  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で導入された機能のうち、MDAC および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows において SQLOLEDB と SQLODBC でサポートされていない機能を利用する必要がある場合は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Native Client を使用して、新しいアプリケーションを作成したり既存のアプリケーションを拡張したりすることができます。 たとえば、FOR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] xml などのクライアント側の SQLXML 機能で**xml**データ型を使用するには、Native Client が必要です。 詳細については、「[クライアント側の XML 書式設定 &#40;sqlxml 4.0&#41;](../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)」、「 [ADO を使用して sqlxml 4.0 クエリを実行する](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」、および「[プログラミング SQL Server Native Client](../../relational-databases/native-client/sql-server-native-client-programming.md)」を参照してください。  
  
> [!NOTE]  
>  SQLXML 4.0 には、下位の SQLXML 3.0 との完全な互換性はありません。 SQLXML 4.0 では不具合の修正とその他の機能変更が行われており、特に SQLXML ISAPI のサポートが削除されているため、IIS 仮想ディレクトリは使用できなくなりました。 大半のアプリケーションは少し変更すれば使用できますが、SQLXML 4.0 で運用する前には必ずテストを行ってください。  
  
## <a name="support-for-data-types-introduced-in-sql-server-2005-and-sql-server-2008"></a>SQL Server 2005 および SQL Server 2008 で導入されたデータ型のサポート  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]では**xml**データ型が導入され、SQLXML 4.0 では**xml**データ型がサポートされています。 詳細については、「 [SQLXML 4.0 での Xml データ型のサポート](../../relational-databases/sqlxml/xml-data-type-support-in-sqlxml-4-0.md)」を参照してください。  
  
 Xml ビューのマッピング、xml の一括読み込み、または XML アップデートグラムの実行時に SQLXML で**xml**データ型を使用する方法の例については、次のトピックに記載されている例を参照してください。  
  
-   [XSD の要素と属性からテーブルと列への既定のマッピング](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
  
-   [XML アップデートグラムを使用したデータの挿入](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)  
  
-   [XML ドキュメントの一括読み込みの例](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]**Date、Time**、 **DateTime2**、および**DateTimeOffset**データ型が導入されました。 SQLXML 4.0 SP1 を、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 付属の [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client OLE DB プロバイダー (SQLNCLI11) と共に使用した場合、これらの 4 つの新しいデータ型は組み込みスカラー型として有効になります。  
  
## <a name="xml-bulk-load-changes-for-sqlxml-40-sp1"></a>SQLXML 4.0 SP1 での XML 一括読み込みの変更点  
  
-   SQLXML 4.0 では、SchemaGen overflow フィールドは**xml**データ型を使用して作成されます。 詳細については、「 [SQL SERVER XML 一括読み込みオブジェクトモデル](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/sql-server-xml-bulk-load-object-model-sqlxml-4-0.md)」を参照してください。  
  
-   以前に [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic アプリケーションを作成済みで、SQLXML 4.0 を使用する場合は、Xblkld4.dll を参照するようアプリケーションを再コンパイルする必要があります。  
  
-   Visual Basic Scripting Edition のアプリケーションについては、使用する DLL を登録する必要があります。 次の例で、バージョン固有でない PROGID を指定した場合、アプリケーションは最後に登録された DLL に従って動作します。  
  
    ```  
    set objBulkLoad = CreateObject("SQLXMLBulkLoad.SQLXMLBulkLoad")   
    ```  
  
    > [!NOTE]  
    >  バージョン固有の PROGID は、SQLXMLBulkLoad.SQLXMLBulkLoad.4.0 です。  
  
## <a name="registry-key-changes-for-sqlxml-40"></a>SQLXML 4.0 でのレジストリ キーの変更点  
 SQLXML 4.0 では、以前のリリースと比べてレジストリ キーが次のように変更されています。  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\SchemaCacheSize  
  
 SQLXML 4.0 でこれらのキーを有効にするには、設定を変更する必要があります。  
  
 また、SQLXML 4.0 では次のレジストリ キーが導入されています。  
  
-   `HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\ReportErrorsWithSQLInfo`  
  
     SQLXML 4.0 の既定では、以前のバージョンの SQLXML と違って高いレベルの SQLXML エラーは返されず、代わりに OLE DB と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のネイティブ エラー情報が返されます。 この動作を変更する場合は、DWORD 型のこのレジストリ キーの値を 0 に設定する必要があります (既定値は 1)。  
  
-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\FORXML_GenerateGUIDBraces  
  
     既定で SQLXML では、SQL Server GUID がかっこで囲まずに返されます。 GUID 値が中かっこで返されるようにする場合は ({*SOME GUID*} など)、このレジストリキーの値を1に設定する必要があります (既定値は 0)。  
  
-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\SQL2000CompatMode  
  
     既定では、XML パーサーでデータが読み込まれるとき、空白文字は XML 1.0 規則に従って正規化されます。 この結果、データの空白文字の一部が失われることがあります。 これによってデータの意味が変わることはありませんが、データのテキストは解析後に同じでなくなります。  
  
     新しく導入されたこのキーを使用すると、データの空白文字を保持するよう指定できます。 このレジストリ キーを追加し、値を 0 に設定すると、XML の空白文字 (LF、CR、タブ) は、属性値の場合はエンコードされて返され、 要素値の場合は CR だけがエンコードされて返されます。  
  
     例:  
  
    ```  
    CREATE TABLE T( Col1 int, Col2 nvarchar(100));  
    GO  
    -- Insert data with tab, line feed and carriage return).  
    INSERT INTO T VALUES (1, 'This is a tab    . This is a line feed and CR   
     more text');  
    GO  
    -- Test this query (without the registry key).  
    SELECT * FROM T   
    FOR XML AUTO;  
    -- This is the result (no encoding of special characters).  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
      <T Col1="1"   
         Col2="This is a tab    . This is a line feed and CR   
     more text"/>  
    </r>  
    -- Now add registry key with value 0 and execute the query again.  
    -- Note the encoding for carriage return, line-feed and tab in the attribute value.  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
      <T Col1="1"   
         Col2="This is a tab    . This is a line feed and CR   
     more text"/>  
    </r>  
  
    -- Update the query and specify ELEMENTS directive  
    SELECT * FROM T  
    FOR XML AUTO, ELEMENTS  
    -- Only the carriage return is returned encoded.  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
       <T>  
          <Col1>1</Col1>  
          <Col2>This is a tab    . This is a line feed and CR   
     more text</Col2>  
       </T>  
    </r>  
    ```  
  
## <a name="migration-issues"></a>移行の問題  
 SQLXML のレガシ アプリケーションから SQLXML 4.0 への移行に影響を与える可能性のある問題を次に示します。  
  
### <a name="ado-and-sqlxml-40-queries"></a>ADO と SQLXML 4.0 のクエリ  
 以前のバージョンの SQLXML では、IIS 仮想ディレクトリを使用した URL ベースのクエリ実行と、SQLXML ISAPI フィルターがサポートされていました。 SQLXML 4.0 を使用するアプリケーションで、このサポートは使用できなくなりました。  
  
 代わりに、Microsoft Data Access Components (MDAC) 2.6 以降で最初に導入された ADO (ActiveX Data Objects) の SQLXML 拡張を使用して、SQLXML クエリ、テンプレート、アップデートグラムを実行できます。  
  
 詳細については、「ADO を使用した[SQLXML 4.0 クエリの実行](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)」を参照してください。  
  
### <a name="supportability-for-sqlxml-30-isapi-and-data-types-introduced-in-sql-server-2005"></a>SQLXML 3.0 ISAPI のサポートと SQL Server 2005 で導入されたデータ型  
 ISAPI サポートが SQLXML 4.0 から削除されているため、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [xml データ型](../../t-sql/xml/xml-transact-sql.md)、[ユーザー定義データ型 (udt)](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) 、Web ベースのアクセスなど、で導入された拡張データ型機能が必要な場合は、 [sqlxml マネージクラス](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-4-0-net-framework-support-managed-classes.md)などの別の種類の HTTP ハンドラー (SQL Server 2005 用のネイティブ xml Web サービスなど) を使用する必要があります。  
  
 または、これらの型の拡張機能が必要ない場合は、SQLXML 3.0 を使用して[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]に接続し、をインストールすることもできます。 SQLXML 3.0 ISAPI サポートは、これらの新しいバージョンに対して機能しますが、 **** で[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]導入された xml データ型または UDT 型サポートをサポートしたり認識したりすることはありません。  
  
### <a name="xml-bulk-load-security-changes-for-temporary-files"></a>一時ファイルに関する XML 一括読み込みのセキュリティの変更点  
 SQLXML 4.0 および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、XML 一括読み込みの権限は、一括読み込み操作を実行するユーザーに許可されます。 読み取りと書き込みの権限は、ファイル システムから継承されます。 以前のリリースの SQLXML および SQL Server では、SQLXML での XML 一括読み込みで作成される一時ファイルは保護されず、だれにでも読み取りが可能でした。  
  
### <a name="migration-issues-for-client-side-for-xml"></a>クライアント側の FOR XML の移行に関する問題  
 実行エンジンが変更されたため[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、は、で for XML クエリを実行した場合とは異なり、ベーステーブルのメタデータに異なる[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]値を返すことがあります。 この場合、クライアント側の FOR XML クエリ結果の形式は、クエリの実行対象となるバージョンによって異なります。  
  
 **Xml**データ型の列に対して SQLXML 3.0 を使用して FOR xml クエリを実行すると、結果のデータは完全にエンティティ文字列として返されます。 SQLXML 4.0 で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) がプロバイダーとして指定されている場合、データは XML として返されます。  
  
  
