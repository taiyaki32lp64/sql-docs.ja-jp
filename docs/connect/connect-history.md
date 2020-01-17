---
title: Microsoft SQL Server のドライバー履歴 |Microsoft Docs
ms.custom: ''
ms.date: 05/04/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a0eb869cf19f128515951421efddc229aa785cdd
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451837"
---
# <a name="driver-history-for-microsoft-sql-server"></a>Microsoft SQL Server のドライバー履歴

このページでは、SQL Server に接続するための Microsoft の履歴データ接続テクノロジについて説明します。

## <a name="odbc"></a>ODBC

SQL Server 用 Microsoft ODBC ドライバーには 3 つの異なる世代があります。 最初の "SQL Server" ODBC ドライバーは、引き続き[Windows Data Access コンポーネント](#microsoft-or-windows-data-access-components)の一部として出荷されます。 新しい開発では、このドライバーを使用しないことをお勧めします。 SQL Server 2005 以降、 [SQL Server Native Client](#sql-server-native-client)には odbc インターフェイスが含まれており、SQL Server 2005 から SQL Server 2012 までに付属する odbc ドライバーです。 新しい開発では、このドライバーを使用しないことをお勧めします。 2012 SQL Server 後、 [Microsoft ODBC Driver for SQL Server](#microsoft-odbc-driver-for-sql-server)は最新のサーバー機能で更新されたドライバーになります。

### <a name="sql-server-native-client"></a>SQL Server Native Client

SQL Server Native Client は、OLE DB と ODBC の両方に使用されるスタンドアロンライブラリです。 SQL Server Native Client (多くの場合、省略形の SNAC) が SQL Server 2005 から2012に含まれていました。 SQL Server Native Client は SQL Server 2012 から SQL Server 2005 で導入された新機能を利用する必要があるアプリケーションに使用できます。 (Microsoft/Windows Data Access Components は、SQL Server の新機能については更新されません)。SQL Server 2012 を超える新機能の場合、SQL Server Native Client は更新されません。 今後新しい SQL Server 機能を利用する場合は、Microsoft ODBC Driver for SQL Server または Microsoft OLE DB Driver for SQL Server に切り替えてください。

SQL Server Native Client の詳細なドキュメントについては、 [SQL Server Native Client のドキュメント](../relational-databases/native-client/sql-server-native-client-programming.md)を参照してください。

### <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft SQL Server 用 ODBC Driver

2012 SQL Server 後、SQL Server のプライマリ ODBC ドライバーは Microsoft ODBC Driver for SQL Server として開発およびリリースされました。 詳細については、 [Microsoft ODBC Driver for SQL Server のドキュメント](./odbc/microsoft-odbc-driver-for-sql-server.md)を参照してください。

## <a name="ole-db"></a>OLE DB (OLE DB)

SQL Server 向けの Microsoft OLE DB プロバイダーには 3 つの世代があります。 最初の "Microsoft OLE DB Provider for SQL Server" (SQLOLEDB) は、現在でも [Windows Data Access Components](#microsoft-or-windows-data-access-components) の一部として同梱されています。 このプロバイダーは新しい機能では更新されません。新しい開発にこのドライバーを使用することはお勧めしません。 SQL Server 2005 以降では、 [SQL Server Native Client](#sql-server-native-client)に OLE DB provider インターフェイス (SQLNCLI) が含まれており、SQL Server 2005 から SQL Server 2017 までに出荷された OLE DB プロバイダーです。 [2011 年に非推奨として発表済み](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)であり、新規開発にこのドライバーを使用することはお勧めしません。 2017では、OLE DB データアクセステクノロジは今後[非推奨とされており](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/)、2018について新しい計画リリースが発表されました。 新しい OLE DB プロバイダーは、"Microsoft OLE DB Driver for SQL Server" (MSOLEDBSQL) と呼ばれ、現在は保守およびサポートされています。

## <a name="adonet"></a>ADO.NET

ADO.NET は Microsoft .NET Framework で導入されたものであり、引き続き改善され、維持されます。 これは、Microsoft .NET Framework の中核となるコンポーネントです。 詳細については、「 [Microsoft ADO.NET for SQL Server](ado-net/microsoft-ado-net-sql-server.md)」を参照してください。

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>Microsoft SQL Server 用 JDBC Driver

2000で導入された SQL Server の Microsoft JDBC Driver は、引き続き改善され、維持されます。 2016でオープンソースでした。 ドライバーのダウンロード方法など、最新の情報については、「 [JDBC ドライバーの概要](./jdbc/overview-of-the-jdbc-driver.md)」を参照してください。

## <a name="php"></a>PHP (PHP)

### <a name="microsoft-drivers-for-php-for-sql-server"></a>Microsoft SQL Server 用 Drivers for PHP

2009で導入されたオープンソースプロジェクトとして、Microsoft Drivers for PHP for SQL Server が引き続き改善され、維持されます。 PHP ドライバーのダウンロード方法など、最新の情報については、「 [Microsoft Drivers FOR php for SQL Server](./php/microsoft-php-driver-for-sql-server.md)」を参照してください。

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>Microsoft Driver for node.js for SQL Server

Microsoft Driver for node.js for SQL Server を使用すると、Microsoft Windows および Microsoft Azure の node.js アプリケーションは Microsoft SQL Server および Microsoft Azure SQL Database にアクセスできます。 開発作業は、このドライバーに焦点が当てられていません。 SQL Server 用の Microsoft Driver for node.js を使用して新しいアプリケーションを作成することはお勧めしません。

SQL Server 用 Microsoft Driver for node.js の詳細については、「 [windowsazure.servicebus/node-sqlserver](https://github.com/Azure/node-sqlserver)」を参照してください。

### <a name="tedious"></a>退屈

Microsoft は、現在、JavaScript を使用した SQL Server への接続のために、node.js のオープンソースの面倒なモジュールに貢献し、サポートしています。 詳細については、「 [SQL Server 用の Node.js ドライバー](./node-js/node-js-driver-for-sql-server.md)」を参照してください。

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft または Windows のデータアクセスコンポーネント

Microsoft/Windows Data Access Components (MDAC/WDAC) は、アプリケーションの下位互換性を確保するために Windows に付属していてサポートされており、現在の SQL Server テクノロジスタックには含まれていません。 新しい機能は、MDAC/WDAC のコンポーネントに追加されることはなく、新しいアプリケーションの開発には使用しないことをお勧めします。

このドキュメントでは、テクノロジと製品に基づいて、MDAC/WDAC スタックを次のコンポーネントに分割できます。

* **ADO** (ADOMD および ADOX を含む)
* **OLE DB** (OLE DB コアサービス、SQL Server OLE DB プロバイダー、Oracle OLE DB プロバイダー、ODBC ドライバーの OLE DB プロバイダー、データシェイププロバイダー、およびリモート Data Provider を含む)
* **Odbc** (Odbc ドライバーマネージャー、SQL odbc ドライバー、および Oracle odbc ドライバーを含む)

### <a name="mdacwdac-components"></a>MDAC/WDAC コンポーネント

MDAC/WDAC には、次のコンポーネントが含まれています。

* **ODBC:** Microsoft Open Database Connectivity (ODBC) インターフェイスは、アプリケーションがさまざまなデータベース管理システム (DBMS) のデータにアクセスできるようにする C プログラミング言語のインターフェイスです。 この API を使用するアプリケーションには、リレーショナルデータソースのみへのアクセスが制限されます。
* **OLE DB:** OLE DB は、さまざまなデータストアのデータにアクセスするための一連の COM インターフェイスです。 OLE DB プロバイダーは、データベース、ファイルシステム、メッセージストア、ディレクトリサービス、ワークフロー、およびドキュメントストアのデータにアクセスするために存在します。
* **ADO:** ActiveX データオブジェクト (ADO) は、高レベルのプログラミングモデルを提供します。 OLE DB または ODBC を直接コーディングするよりも、パフォーマンスがわずかに低下しますが、ADO は簡単に学習して使用することができます。 これは、Microsoft Visual Basic Scripting Edition (VBScript) や Microsoft JScript などのスクリプト言語から使用できます。
* **ADOMD:** .ADO 多次元 (ADOMD) では、Microsoft Analysis Services プロバイダーとも呼ばれる Microsoft OLAP プロバイダーなどの多次元データ プロバイダーで使用します。 MDAC 2.0 以降、機能に関する主な機能強化は行われていません。
* **ADOX:** ADO Extensions for DDL and Security (ADOX) を使用すると、データベース、テーブル、インデックス、またはストアドプロシージャの定義を作成および変更できます。 すべてのプロバイダーで ADOX を使用できます。 Microsoft Jet OLE DB プロバイダーは ADOX を完全にサポートしていますが、Microsoft SQL Server OLE DB プロバイダーは限られたサポートを提供しています。
* **Microsoft SQL Server ネットワークライブラリ:** SQL Server ネットワークライブラリを使用すると、SQLOLEDB と SQLODBC が SQL Server データベースと通信できるようになります。 Banyan Vines、AppleTalk、ServerNet、IPX/SPX、Giganet、および RPC では、次の SQL Server ネットワークライブラリが非推奨とされます。 TCP/IP と名前付きパイプは引き続きサポートされ、64ビットの Windows オペレーティングシステムで使用できます。
* **MSDASQL:** Microsoft OLE DB Provider for ODBC (MSDASQL) は、ODBC ドライバーを通じてデータ ソースのアクセスを OLE DB と ADO (内部的に OLEDB を使用) する上で構築されるアプリケーションをできます。 MSDASQL は、データベースではなく ODBC に接続する OLEDB プロバイダーです。 データソース用の直接 OLE DB プロバイダーが存在しない場合は、OLE DB から ODBC ドライバーへのブリッジとして使用されます。 MSDASQL は、windows オペレーティングシステムに付属しています。 Windows Server 2008 と Vista SP1 は、64ビット版のテクノロジを含む最初の Windows リリースでした。

### <a name="deprecated-mdacwdac-components"></a>非推奨の MDAC/WDAC コンポーネント

これらのコンポーネントは、現在のリリースの MDAC/WDAC でもサポートされていますが、今後のリリースでは削除される可能性があります。 新しいアプリケーションを開発するときは、これらのコンポーネントを使用しないことをお勧めします。 また、既存のアプリケーションをアップグレードまたは変更する場合は、これらのコンポーネントの依存関係を削除します。

* **SQLOLEDB:** Microsoft OLE DB Provider for SQL Server (SQLOLEDB)、Microsoft SQL Server へのアクセスをサポートするには、これは非推奨とされました。 将来のバージョンの SQL Server への接続がサポートされていない可能性があります。 SQL Server 7 より前のバージョンに接続する機能は、Windows 7 以降のオペレーティングシステムから削除されます。 新しいアプリケーションでは、Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL) を使用する必要があります。これにより、新しい SQL Server 機能がサポートされます。 既存のアプリケーションは、パフォーマンス、信頼性、およびサポート性を向上させるために、Microsoft OLE DB Driver for SQL Server にも移行する必要があります。 詳細については、「 [MDAC から OLE DB Driver for SQL Server にアプリケーションを更新する](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)」を参照してください。
* **SQLODBC:** Microsoft SQL Server へのアクセスをサポートする Microsoft SQL Server ODBC ドライバー (SQLODBC) は非推奨とされました。 将来のバージョンの SQL Server への接続がサポートされていない可能性があります。 SQL Server 7 より前のバージョンに接続する機能は、Windows 7 以降のオペレーティングシステムから削除されます。 新しいアプリケーションでは、新しい SQL Server 機能をサポートする Windows 上の Microsoft ODBC Driver for SQL Server を使用する必要があります。 既存のアプリケーションは、パフォーマンス、信頼性、およびサポート性を向上させるために、Microsoft ODBC Driver for SQL Server にも移行する必要があります。 関連情報については、「 [MDAC から SQL Server Native Client するようにアプリケーションを更新する](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)」を参照してください。
* **Microsoft Jet データベースエンジン 4.0:** バージョン2.6 以降では、MDAC に Jet コンポーネントが含まれなくなりました。 つまり、MDAC 2.6、2.7、および2.8 には、Microsoft Jet、Microsoft Jet OLE DB プロバイダー、ODBC Desktop データベースドライバー、または Jet データアクセスオブジェクト (DAO) は含まれていません。 

  Jet データベースエンジンの64ビットバージョン、Jet OLEDB ドライバー、Jet ODBC ドライバー、または Jet DAO が使用できません。 詳細については、[サポート技術情報の記事 957570](https://support.microsoft.com/kb/957570) を参照してください。 Windows の64ビットバージョンでは、32ビット Jet は Windows WOW64 サブシステムで実行されます。 WOW64 の詳細については、 [MSDN wow64 のドキュメント](/windows/desktop/WinProg64/wow64-implementation-details)を参照してください。 ネイティブの64ビットアプリケーションは、WOW64 で実行されている32ビットの Jet ドライバーと通信できません。

  Microsoft Jet の代わりに、microsoft では、リレーショナルデータストアを必要とする、Microsoft 以外の新しい Access アプリケーションを開発する際に[Microsoft SQL Server Express エディション](https://www.microsoft.com/sql-server/sql-server-editions-express)を使用することをお勧めします。 これらの新しいまたは変換された Jet アプリケーションは、プライマリ以外のデータストレージに Microsoft Office 2003 以前のファイル (.mdb および .xls) を使用することを目的として、引き続き Jet を使用できます。 ただし、これらのアプリケーションでは、Jet から Microsoft Access データベースエンジンに移行することを計画する必要があります。 [Microsoft access データベースエンジンをダウンロード](https://www.microsoft.com/download/details.aspx?id=54920)することができます。これにより、office 2003 (.mdb および .xls) または office 2007 (* .accdb, * .xlsm, * .xlsb) ファイル形式の既存のファイルに対して読み取りと書き込みを行うことができます。

  > [!IMPORTANT]
  > 特定の使用制限については、2007の Office システム使用許諾契約書をお読みください。

  > [!NOTE]
  > また SQL Server アプリケーションは、2007 Office システムドライバーを使用して、異種データ接続と integration Services 機能 SQL Server から、2007の Office システム、およびそれ以前のファイルにアクセスすることもできます。 さらに、64ビットの SQL Server アプリケーションは、64ビットの Windows で32ビット SQL Server Integration Services (SSIS) を使用して、32ビットの Jet および 2007 Office システムファイルにアクセスできます。

* **MSDADS:** Microsoft OLE DB Provider for Data 整形 (MSDADS) を使用すると、アプリケーション内のキー、フィールド、または行セットの間に階層リレーションシップを作成できます。 MDAC 2.1 以降、機能に関する主な機能強化は行われていません。 このプロバイダーは非推奨とされます。 Microsoft では、MSDADS の代わりに XML を使用することをお勧めします。
* **ORACLE ODBC および oracle OLE DB:** Microsoft Oracle ODBC Driver (Oracle ODBC) および Microsoft OLE DB Provider for Oracle (Oracle OLE DB) を使用すると、Oracle データベースサーバーにアクセスできます。 これらは、Oracle Call Interface (OCI) バージョン7を使用して構築され、Oracle 7 の完全なサポートを提供します。 また、oracle 7 エミュレーションを使用して、Oracle 8 データベースの制限付きサポートを提供しています。 Oracle では、OCI バージョン7の呼び出しを使用するアプリケーションはサポートされなくなりました。 これらのテクノロジは非推奨とされます。 Oracle データソースを使用している場合は、Oracle によって提供されるドライバーおよびプロバイダーに移行する必要があります。
* **RDS:** リモート データ サービス (RDS) は、インターネットまたはイントラネットの間でリモートの ADO レコード セット オブジェクトにアクセスするための独自の Microsoft メカニズムです。 RDS は非推奨とされます。MDAC 2.1 以降、RDS には、機能に関する主な機能強化は加えられていません。 Microsoft は、広範な SOAP 機能を備え、RDS コンポーネントを置き換える .NET Framework をリリースしました。 すべての RDS サーバーコンポーネントは、Windows 7 以降のオペレーティングシステムから削除されます。
* **JRO:** Jet レプリケーションオブジェクト (JRO) は非推奨とされます。 JRO は、jet データベース (.mdb) を作成および圧縮し、jet レプリケーション管理を実行するために、Jet ( *.mdb) データベースと共に ADO 内で使用されます。MDAC 2.7 は、最新のリリースになります。64ビットの Windows オペレーティングシステムでは、JRO は使用できません。Microsoft Access 2007 ファイル形式 (* .accdb) では、JRO はサポートされていません。
* **16 ビット ODBC のサポート:** 16ビットアプリケーションを使用している場合は、32ビットアプリケーションに移行する必要があります。 16ビットの機能は非推奨となり、64ビットのオペレーティングシステムから削除されます。 詳細については、[サポート技術情報の記事 896458](https://support.microsoft.com/kb/896458) を参照してください。
* **OLEDB Simple Provider (MSDAOSP):** OLEDB Simple Provider は、単純なデータを介して OLE DB プロバイダーをすばやく構築するためのフレームワークを提供します。 MSDAOSP は非推奨とされます。
* **ODBC カーソルライブラリ:** ODBC Cursor Library (ODBCCR32) では、クライアント側のデータカーソルが制限されています。 ODBC カーソルライブラリの使用は非推奨とされました。アプリケーションでは、代替としてサーバー側のカーソル実装を使用できます。
* **OLE DB アウトプロセスインターフェイスリモート処理:** OLEDB インターフェイスリモート処理 (msdaps) は、OLE DB プロバイダーのプロセスが不足することを許可しようとしました。 OLEDB アウトプロセスインターフェイスリモート処理は非推奨とされます。
* **AppleTalk および Banyan VINES SQL ネットワークライブラリ:** Banyan Vines、AppleTalk、ServerNet、IPX/SPX、Giganet、および RPC SQL ネットワークライブラリは非推奨とされます。 これらのテクノロジのいずれかを使用している場合は、TCP/IP や名前付きパイプなどの他のネットワークライブラリのいずれかを使用するようにアプリケーションを変更する必要があります。

### <a name="mdacwdac-releases"></a>MDAC/WDAC リリース

以前の MDAC/WDAC リリースのサポートシナリオの一覧を次に示します。

* **Mdac 1.5、mdac 2.0、および mdac 2.1:** これらのバージョンの MDAC は、Microsoft Windows NT オプションパック、Microsoft Windows プラットフォーム SDK、または MDAC Web サイトからリリースされた独立したリリースでした。 これらのバージョンの MDAC はサポートされなくなりました。
* **MDAC 2.5:** このバージョンの MDAC は、Windows 2000 オペレーティングシステムに含まれていました。 MDAC 2.5 の service pack は、対応する Windows 2000 service pack に含まれていました。
* **MDAC 2.6:** MDAC 2.6 RTM、SP1、および SP2 は、それぞれ Microsoft SQL Server 2000 RTM、SP1、SP2 に含まれていました。 また、これらの MDAC service pack は、Microsoft SQL Server 2000 service pack のリリーススケジュールに従って、MDAC Web サイトにリリースされました。 このバージョンの MDAC とそのサービスパックは、Windows 2000、Windows Millennium Edition、Windows NT、Windows 95、および Windows 98 プラットフォームにインストールできます。 このバージョンの MDAC はサポートされなくなりました。
* **MDAC 2.7:** このバージョンの MDAC は、Microsoft Windows XP RTM および SP1 オペレーティングシステムに含まれていました。 このバージョンの MDAC とそのサービスパックは、Windows 2000、Windows Millennium、Windows NT、および Windows 98 プラットフォームにインストールできます。 このバージョンは、オペレーティングシステムまたはそのサービスパックを使用してのみ、Windows XP プラットフォームにインストールできます。 このバージョンの MDAC はサポートされなくなりました。
* **MDAC 2.8:** このバージョンの MDAC は、Windows Server 2003 および Windows XP SP2 以降に含まれていました。 このバージョンの MDAC とそのサービスパックは、Windows 2000 にもインストールできます。

  * MDAC 2.8 の32ビットバージョンは、Windows Server 2003 が顧客にリリースされたときと同時に MDAC Web サイトにもリリースされました。
  * 64ビット版の MDAC 2.8 は、Windows Server 2003 および Windows XP の64ビットバージョンでリリースされました。

* **Windows Data Access Components (WDAC):** MDAC は、Windows Vista および Windows Server 2008 以降では、名前が WDAC-"Windows Data Access Components" に変更されました。 WDAC はオペレーティングシステムの一部として含まれており、再配布用に個別に使用することはできません。 WDAC のサービス性には、オペレーティングシステムのライフサイクルが適用されます。

  32ビットおよび64ビットバージョンの WDAC は、それぞれ32ビットバージョンと64ビットバージョンの Windows オペレーティングシステムでリリースされます。

## <a name="obsolete-data-access-technologies"></a>互換性のために残されているデータアクセステクノロジ

互換性のために残されているテクノロジは、いくつかの製品リリースで強化または更新されていないテクノロジで、今後の製品リリースからは除外されます。 新しいアプリケーションを作成するときは、これらのテクノロジを使用しないでください。 これらのテクノロジを使用して作成された既存のアプリケーションを変更する場合は、それらのアプリケーションを ADO.NET または他の現在のテクノロジに移行することを検討してください。

次のコンポーネントは、互換性のために残されていると見なされます。

* **DB-Library:** DB ライブラリは、C Api を含む SQL Server に固有のプログラミング モデルです。 SQL Server 6.5 以降、DB-LIBRARY に機能強化は加えられていません。 最終的なリリースは SQL Server 2000 であり、64ビットの Windows オペレーティングシステムには移植されません。
* **EMBEDDED SQL (E sql):** SQL は、Transact-sql ステートメントを Visual C コードに埋め込むことができる、SQL Server 固有のプログラミングモデルです。 SQL Server 6.5 以降、E SQL に機能の機能強化は行われていません。 最終的なリリースは SQL Server 2000 であり、64ビットの Windows オペレーティングシステムには移植されません。
* **データアクセスオブジェクト (DAO):** DAO は、JET (Access) データベースへのアクセスを提供します。 この API は、Microsoft Visual Basic、Microsoft Visual C++、およびスクリプト言語から使用できます。 Microsoft Office 2000 および Office XP に含まれていました。 DAO 3.6 は、このテクノロジの最終バージョンです。 これは、64ビットの Windows オペレーティングシステムでは使用できません。
* **リモートデータオブジェクト (RDO):** RDO は、特にリモート ODBC リレーショナルデータソースにアクセスするように設計されており、複雑なアプリケーションコードを使用せずに ODBC を使いやすくしました。 これは、Microsoft Visual Basic バージョン4、5、および6に含まれていました。 RDO バージョン2.0 は、このテクノロジの最終バージョンです。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
