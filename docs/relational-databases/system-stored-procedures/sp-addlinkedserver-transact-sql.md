---
title: sp_addlinkedserver (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addlinkedserver_TSQL
- sp_addlinkedserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlinkedserver
ms.assetid: fed3adb0-4c15-4a1a-8acd-1b184aff558f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ad01313933cb2e04bf22257bcdd0eb93a1a755e9
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313747"
---
# <a name="sp_addlinkedserver-transact-sql"></a>sp_addlinkedserver (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  リンク サーバーを作成します。 リンク サーバーを使用すると、OLE DB データ ソースに対する異種の分散クエリの利用が可能になります。 **Sp_addlinkedserver**を使用してリンクサーバーを作成した後は、このサーバーに対して分散クエリを実行できます。 リンク サーバーを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスとして定義した場合は、リモート ストアド プロシージャを実行できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_addlinkedserver [ @server= ] 'server' [ , [ @srvproduct= ] 'product_name' ]   
     [ , [ @provider= ] 'provider_name' ]  
     [ , [ @datasrc= ] 'data_source' ]   
     [ , [ @location= ] 'location' ]   
     [ , [ @provstr= ] 'provider_string' ]   
     [ , [ @catalog= ] 'catalog' ]   
```  
  
## <a name="arguments"></a>引数  
[@server =] *\'server\'*           
作成するリンク サーバーの名前を指定します。 *server* のデータ型は **sysname**で、既定値はありません。  
  
[@srvproduct =] *\'product_name\'*           
リンクサーバーとして追加する OLE DB データソースの製品名を指定します。 *product_name*は**nvarchar (** 128 **)** ,、既定値は NULL です。 **SQL Server**の場合、 *provider_name*、 *data_source*、*場所*、 *provider_string*、および*カタログ*を指定する必要はありません。  
  
[@provider =] *\'provider_name\'*           
このデータ ソースに対応する OLE DB プロバイダーの一意なプログラム識別子 (PROGID) を指定します。 *provider_name*は、現在のコンピューターにインストールされている指定された OLE DB プロバイダーに対して一意である必要があります。 *provider_name*は**nvarchar (128)** ,、既定値は NULL です。ただし、 *provider_name*を省略した場合、SQLNCLI が使用されます。 

> [!NOTE]
> SQLNCLI を使用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの最新バージョンにリダイレクトされます。 OLE DB プロバイダーは、指定の PROGID を使用してレジストリに登録されることが想定されています。

> [!IMPORTANT] 
> 以前の Microsoft OLE DB Provider for SQL Server (SQLOLEDB) と SQL Server Native Client OLE DB プロバイダー (SQLNCLI) は非推奨のままであり、新しい開発作業にはどちらの使用もお勧めできません。 代わりに、新しい [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) を使用します。これは、最新のサーバー機能で更新されます。
  
[@datasrc =] *\'data_source\'*           
 OLE DB プロバイダーによって解釈されるデータソースの名前を指定します。 *data_source*は**nvarchar (** 4000 **)** です。 OLE DB プロバイダーを初期化するために、DBPROP_INIT_DATASOURCE プロパティとして*data_source*が渡されます。  
  
[@location =] *\'の場所\'*           
 OLE DB プロバイダーで認識されるデータベースの場所を指定します。 *場所*は**nvarchar (** 4000 **)** ,、既定値は NULL です。 *location*は、OLE DB プロバイダーを初期化するために DBPROP_INIT_LOCATION プロパティとして渡されます。  
  
[@provstr =] *\'provider_string\'*           
 一意なデータ ソースを識別する、OLE DB プロバイダー固有の接続文字列を指定します。 *provider_string*は**nvarchar (** 4000 **)** ,、既定値は NULL です。 *provstr*は、IDataInitialize に渡されるか、DBPROP_INIT_PROVIDERSTRING プロパティとして設定され、OLE DB プロバイダーを初期化します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーに対してリンクサーバーを作成する場合は、server キーワードを server =*servername*\\*instancename*として使用してインスタンスを指定し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の特定のインスタンスを指定できます。 *servername*は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行されているコンピューターの名前です。 *instancename*は、ユーザーが接続される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の特定のインスタンスの名前です。  
  
> [!NOTE]
> ミラー化されたデータベースにアクセスするには、接続文字列にデータベース名を含める必要があります。 この名前は、データ アクセス プロバイダーがフェールオーバーを試行できるようにするために必要です。 データベースは **\@provstr**または **\@catalog**パラメーターで指定できます。 必要に応じて、接続文字列でフェールオーバーパートナー名を指定することもできます。  
  
[@catalog =] *\'カタログ\'*        
 OLE DB プロバイダーへの接続が確立されるときに使用するカタログを指定します。 *catalog*の**sysname**,、既定値は NULL です。 *カタログ*は、OLE DB プロバイダーを初期化するために DBPROP_INIT_CATALOG プロパティとして渡されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに対してリンクサーバーが定義されている場合、catalog は、リンクサーバーがマップされている既定のデータベースを参照します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし。  
  
## <a name="remarks"></a>Remarks  
 次の表に、OLE DB を使用してアクセスできるデータソース用にリンクサーバーを設定する方法を示します。 リンクサーバーは、特定のデータソースに対して複数の方法で設定できます。1つのデータソースの種類に対して複数の行を指定できます。 このテーブルには、リンクサーバーの設定に使用される**sp_addlinkedserver**パラメーター値も表示されます。  
  
|リモート OLE DB データ ソース|OLE DB プロバイダー|product_name|provider_name|data_source|location|provider_string|カタログ|  
|-------------------------------|---------------------|-------------------|--------------------|------------------|--------------|----------------------|-------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <sup>1</sup> (既定値)||||||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー||**SQLNCLI**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のネットワーク名 (既定のインスタンスの場合)|||データベース名 (省略可能)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー||**SQLNCLI**|*servername*\\*instancename* (特定のインスタンス用)|||データベース名 (省略可能)|  
|Oracle、バージョン 8 以降|Oracle Provider for OLE DB|Any|**OraOLEDB.Oracle**|Oracle データベースに対する別名||||  
|Access/Jet|Microsoft OLE DB Provider for Jet|Any|**Microsoft. OLEDB. 4.0**|Jet データベースファイルの完全なパス||||  
|ODBC データ ソース (ODBC data source)|Microsoft OLE DB Provider for ODBC|Any|**MSDASQL**|ODBC データソースのシステム DSN||||  
|ODBC データ ソース (ODBC data source)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for ODBC|Any|**MSDASQL**|||ODBC 接続文字列||  
|ファイル システム|インデックスサービスの OLE DB プロバイダーの [!INCLUDE[msCoName](../../includes/msconame-md.md)]|Any|**MSIDXS**|インデックスサービスのカタログ名||||  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel ワークシート|Jet 用 OLE DB プロバイダーの [!INCLUDE[msCoName](../../includes/msconame-md.md)]|Any|**Microsoft. OLEDB. 4.0**|Excel ファイルのフル パス||Excel 5.0||  
|IBM DB2 データベース|DB2 の [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB プロバイダー|Any|**DB2OLEDB**|||[!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for DB2 のドキュメントを参照してください。|DB2 データベースのカタログ名|  
  
 <sup>1</sup>この方法でリンクサーバーを設定すると、リンクサーバーの名前が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のリモートインスタンスのネットワーク名と同じになります。 *Data_source*を使用してサーバーを指定します。  
  
 <sup>2</sup> "任意" は、製品名を任意の名前にすることを示します。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、プロバイダー名が指定されていない場合、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が製品名として指定されている場合に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用されるプロバイダーです。 以前のプロバイダー名を指定した場合でも、SQLOLEDB は、カタログに永続化するときに SQLNCLI に変更されます。  
  
 *Data_source*、 *location*、 *provider_string*、および*catalog*パラメーターは、リンクサーバーが指すデータベースを識別します。 これらのいずれかのパラメーターが NULL に設定されると、対応する OLE DB 初期化プロパティは設定されません。  
  
 クラスター環境では OLE DB データソースを指すようにファイル名を指定する場合は、汎用名前付け規則名 (UNC) または共有ドライブを使用して場所を指定します。  
  
 **sp_addlinkedserver**は、ユーザー定義のトランザクション内では実行できません。  
  
> [!IMPORTANT]
> **Sp_addlinkedserver**を使用してリンクサーバーを作成すると、すべてのローカルログインに対して既定の自己マッピングが追加されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のプロバイダーの場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証されたログインは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスアカウントでプロバイダーにアクセスできる可能性があります。 管理者は、`sp_droplinkedsrvlogin <linkedserver_name>, NULL` を使用してグローバルマッピングを削除することを検討する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 `sp_addlinkedserver` ステートメントには、`ALTER ANY LINKED SERVER` アクセス許可が必要です。 ([**新しいリンクサーバー**の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]] ダイアログボックスは、`sysadmin` 固定サーバーロールのメンバーシップを必要とする方法で実装されます)。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-the-microsoft-sql-server-ole-db-provider"></a>A. Microsoft SQL Server OLE DB プロバイダーの使用  
 次の例では、`SEATTLESales` というリンク サーバーを作成します。 製品名は `SQL Server` で、プロバイダー名は使用されません。  
  
```sql  
USE master;  
GO  
EXEC sp_addlinkedserver   
   N'SEATTLESales',  
   N'SQL Server';  
GO  
```  

 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB ドライバーを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにリンクサーバー `S1_instance1` を作成します。  

```sql  
EXEC sp_addlinkedserver     
   @server=N'S1_instance1',   
   @srvproduct=N'',  
   @provider=N'MSOLEDBSQL',   
   @datasrc=N'S1\instance1';  
```  

 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにリンクサーバー `S1_instance1` を作成します。  
 
> [!IMPORTANT] 
> SQL Server Native Client OLE DB プロバイダー (SQLNCLI) は非推奨のままであり、新しい開発作業での使用はお勧めできません。 代わりに、新しい [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) を使用します。これは、最新のサーバー機能で更新されます。
  
```sql  
EXEC sp_addlinkedserver     
   @server=N'S1_instance1',   
   @srvproduct=N'',  
   @provider=N'SQLNCLI',   
   @datasrc=N'S1\instance1';  
```  
  
### <a name="b-using-the-microsoft-ole-db-provider-for-microsoft-access"></a>b. Microsoft OLE DB Provider for Microsoft Access を使用する  
 Microsoft Jet OLEDB プロバイダーは、2002-2003 形式を使用する Microsoft Access データベースに接続します。 次の例では、`SEATTLE Mktg` というリンク サーバーを作成します。  
  
> [!NOTE]  
> この例では、[!INCLUDE[msCoName](../../includes/msconame-md.md)] アクセスとサンプル**northwind**データベースの両方がインストールされており、 **northwind**データベースが c:\msoffice\access\samples に存在することを前提としています。  
  
```sql  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Mktg',   
   @provider = N'Microsoft.Jet.OLEDB.4.0',   
   @srvproduct = N'OLE DB Provider for Jet',  
   @datasrc = N'C:\MSOffice\Access\Samples\Northwind.mdb';  
GO  
```  
  
 Microsoft.ACE.OLEDB.12.0 プロバイダーは、2007 形式を使用する Microsoft Access データベースに接続します。 次の例では、`SEATTLE Mktg` というリンク サーバーを作成します。  
  
> [!NOTE]  
> この例では、[!INCLUDE[msCoName](../../includes/msconame-md.md)] アクセスとサンプル**northwind**データベースの両方がインストールされており、 **northwind**データベースが c:\msoffice\access\samples に存在することを前提としています。  
  
```sql  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Mktg',   
   @provider = N'Microsoft.ACE.OLEDB.12.0',   
   @srvproduct = N'OLE DB Provider for ACE',  
   @datasrc = N'C:\MSOffice\Access\Samples\Northwind.accdb';  
GO  
```  
  
### <a name="c-using-the-microsoft-ole-db-provider-for-odbc-with-the-data_source-parameter"></a>C. Data_source パラメーターを使用して Microsoft OLE DB Provider for ODBC を使用する  
 次の例では、[!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for ODBC (`MSDASQL`) と*data_source*パラメーターを使用する `SEATTLE Payroll` という名前のリンクサーバーを作成します。  
  
> [!NOTE]  
> リンク サーバーを使用する前には、指定した ODBC データ ソース名をサーバーのシステム DSN として定義する必要があります。  
  
```sql  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Payroll',   
   @srvproduct = N'',  
   @provider = N'MSDASQL',   
   @datasrc = N'LocalServer';  
GO  
```  
  
### <a name="d-using-the-microsoft-ole-db-provider-for-excel-spreadsheet"></a>D. Microsoft OLE DB Provider for Excel スプレッドシートの使用  
 Jet 用の [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider を使用して 1997-2003 形式の Excel スプレッドシートにアクセスするリンクサーバー定義を作成するには、まず、選択する Excel ワークシートの列と行を指定して、Excel で名前付き範囲を作成します。 こうすると、分散クエリで範囲の名前をテーブル名として参照できるようになります。  
  
```sql  
EXEC sp_addlinkedserver 'ExcelSource',  
   'Jet 4.0',  
   'Microsoft.Jet.OLEDB.4.0',  
   'c:\MyData\DistExcl.xls',  
   NULL,  
   'Excel 5.0';  
GO  
```  
  
 Excel スプレッドシートのデータにアクセスするには、セルの範囲を名前に関連付けます。 先に設定したリンク サーバーを使って、テーブルとして指定されている名前付き範囲 `SalesData` にアクセスするときには、次のクエリを使用できます。  
  
```sql  
SELECT *  
   FROM ExcelSource...SalesData;  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がリモート共有へのアクセス権を持つドメインアカウントで実行されている場合は、マップされたドライブの代わりに UNC パスを使用できます。  
  
```sql  
EXEC sp_addlinkedserver 'ExcelShare',  
   'Jet 4.0',  
   'Microsoft.Jet.OLEDB.4.0',  
   '\\MyServer\MyShare\Spreadsheets\DistExcl.xls',  
   NULL,  
   'Excel 5.0';  
```  
  
 Excel 2007 形式の Excel スプレッドシートに接続するには、ACE プロバイダーを使用します。  
  
```sql  
EXEC sp_addlinkedserver @server = N'ExcelDataSource',   
@srvproduct=N'ExcelData', @provider=N'Microsoft.ACE.OLEDB.12.0',   
@datasrc=N'C:\DataFolder\People.xlsx',  
@provstr=N'EXCEL 12.0' ;  
  
```  
  
### <a name="e-using-the-microsoft-ole-db-provider-for-jet-to-access-a-text-file"></a>E. Microsoft OLE DB Provider for Jet を使用してテキストファイルにアクセスする  
 次の例では、Access .mdb ファイル内のテーブルとしてテキスト ファイルにリンクするのではなく、直接テキスト ファイルにアクセスするリンク サーバーを作成します。 プロバイダーが `Microsoft.Jet.OLEDB.4.0`、プロバイダー文字列が `Text`。  
  
 データソースは、テキストファイルが格納されているディレクトリの完全なパスです。 テキストファイルの構造を記述する schema.ini ファイルは、テキストファイルと同じディレクトリに存在する必要があります。 Schema.ini ファイルの作成方法の詳細については、Jet Database Engine のマニュアルを参照してください。  
  
```sql  
--Create a linked server.  
EXEC sp_addlinkedserver txtsrv, N'Jet 4.0',   
   N'Microsoft.Jet.OLEDB.4.0',  
   N'c:\data\distqry',  
   NULL,  
   N'Text';  
GO  
  
--Set up login mappings.  
EXEC sp_addlinkedsrvlogin txtsrv, FALSE, Admin, NULL;  
GO  
  
--List the tables in the linked server.  
EXEC sp_tables_ex txtsrv;  
GO  
  
--Query one of the tables: file1#txt  
--using a four-part name.   
SELECT *   
FROM txtsrv...[file1#txt];  
```  
  
### <a name="f-using-the-microsoft-ole-db-provider-for-db2"></a>F. Microsoft OLE DB Provider for DB2 の使用  
 次の例では、`Microsoft OLE DB Provider for DB2`を使用する `DB2` という名前のリンクサーバーを作成します。  
  
```sql  
EXEC sp_addlinkedserver  
   @server=N'DB2',  
   @srvproduct=N'Microsoft OLE DB Provider for DB2',  
   @catalog=N'DB2',  
   @provider=N'DB2OLEDB',  
   @provstr=N'Initial Catalog=PUBS;  
       Data Source=DB2;  
       HostCCSID=1252;  
       Network Address=XYZ;  
       Network Port=50000;  
       Package Collection=admin;  
       Default Schema=admin;';  
```  
  
### <a name="g-add-a-includesssdsfullincludessssdsfull-mdmd-as-a-linked-server-for-use-with-distributed-queries-on-cloud-and-on-premises-databases"></a>G. クラウドとオンプレミスのデータベースで分散クエリを使用するために、リンクサーバーとして [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] を追加する  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] をリンク サーバーとして追加し、内部設置型データベースとクラウド データベースにまたがる分散クエリでそのサーバーを使用することができます。 これは、オンプレミスの企業ネットワークと Azure クラウドにまたがるデータベースハイブリッドソリューションのコンポーネントです。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] box 製品には、分散クエリ機能が含まれています。この機能を使用すると、リンクサーバーとして定義されているリモートソース ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のデータソースのデータを含む) からローカルデータソースとデータのデータを結合するクエリを作成できます。 すべての [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (仮想マスターを除く) を個々のリンクサーバーとして追加し、データベースアプリケーションで他のデータベースとして直接使用することができます。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] を使用する利点としては、管理性、高可用性、スケーラビリティ、使い慣れた開発モデルの使用、リレーショナルデータモデルなどがあります。 データベースアプリケーションの要件によって、クラウドでの [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] の使用方法が決まります。 すべてのデータを一度に移動して [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]することも、データの一部を段階的に移動して、残りのデータをオンプレミスに保持することもできます。 このようなハイブリッドデータベースアプリケーションでは、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] をリンクサーバーとして追加できるようになりました。また、データベースアプリケーションは分散クエリを発行して、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] とオンプレミスのデータソースのデータを結合することができます。  
  
 分散クエリを使用して [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] に接続する方法を説明する簡単な例を次に示します。  
  
```sql  
-- Configure the linked server  
-- Add one Azure SQL DB as Linked Server  
EXEC sp_addlinkedserver  
  @server='myLinkedServer', -- here you can specify the name of the linked server  
  @srvproduct='',       
  @provider='sqlncli', -- using SQL Server Native Client  
  @datasrc='myServer.database.windows.net',   -- add here your server name  
  @location='',  
  @provstr='',  
  @catalog='myDatabase'  -- add here your database name as initial catalog (you cannot connect to the master database)  

-- Add credentials and options to this linked server  
EXEC sp_addlinkedsrvlogin  
  @rmtsrvname = 'myLinkedServer',  
  @useself = 'false',  
  @rmtuser = 'myLogin',             -- add here your login on Azure DB  
  @rmtpassword = 'myPassword' -- add here your password on Azure DB  

EXEC sp_serveroption 'myLinkedServer', 'rpc out', true;  

-- Now you can use the linked server to execute 4-part queries  
-- You can create a new table in the Azure DB  
EXEC ('CREATE TABLE t1tutut2(col1 int not null CONSTRAINT PK_col1 PRIMARY KEY CLUSTERED (col1) )') at myLinkedServer  
-- Insert data from your local SQL Server  
EXEC ('INSERT INTO t1tutut2 VALUES(1),(2),(3)') at myLinkedServer  
  
-- Query the data using 4-part names  
SELECT * FROM myLinkedServer.myDatabase.dbo.myTable  
```  
  
## <a name="see-also"></a>参照  
 [分散クエリストアドプロシージャ&#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [transact-sql &#40;  の&#41; sp_addlinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_addserver](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_dropserver](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)  
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [transact-sql &#40;  の&#41; sp_setnetname](../../relational-databases/system-stored-procedures/sp-setnetname-transact-sql.md)  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [システム テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
