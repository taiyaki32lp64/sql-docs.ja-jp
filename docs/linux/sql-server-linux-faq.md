---
title: SQL Server on Linux に関する FAQ
description: この記事では、Linux で実行されている SQL Server に関してよく寄せられる質問への回答を提供します。
author: VanMSFT
ms.author: vanto
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 4fe5ea36b2e60a3a0531e247acc303b70e0db801
ms.sourcegitcommit: 39630fddc69141531eddca2a3c156ccf8536f49c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72929903"
---
# <a name="sql-server-on-linux-frequently-asked-questions-faq"></a>SQL Server on Linux に関してよく寄せられる質問 (FAQ)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

以下のセクションでは、Linux で実行されている SQL Server についてよく寄せられる質問と回答を提供します。

## <a name="general-questions"></a>一般的な質問

1. **どの Linux プラットフォームがサポートされていますか?**

   現在、SQL Server は Red Hat Enterprise Server、SUSE Linux Enterprise Server、および Ubuntu でサポートされています。 また、Docker を使用したコンテナーでの実行もサポートされています。 サポートされているバージョンの最新情報については、「[サポートされているプラットフォーム](sql-server-linux-setup.md#supportedplatforms)」を参照してください。

1. **SQL Server on Linux は他のプラットフォームで動作しますか?**

   前述のディストリビューションについては、Linux で SQL Server がテストおよびサポートされています。 その他の Linux ディストリビューションは密接に関連しており、SQL Server を実行できる場合があります (たとえば、CentOS は Red Hat Enterprise Server に密接に関連しています)。 しかし、サポートされていないオペレーティング システムに SQL Server をインストールすることを選択した場合は、サポートの影響を理解するために、「[Microsoft SQL Server のテクニカル サポート ポリシー](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)」の「**サポート ポリシー** 」セクションを確認してください。 また、コミュニティによって管理されるいくつかの Linux ディストリビューションには、基になるオペレーティング システムが問題である場合にサポートを受けるための正式な方法がないことに注意してください。

1. **SQL Server on Linux は Windows の場合と同じですか?**

   Linux 上の SQL Server のコア データベース エンジンは、Windows の場合と同じです。 しかし、一部の機能は現在、Linux ではサポートされていません。 Linux でサポートされていない機能のリストについては、「[サポートされていない機能 & サービス](sql-server-linux-editions-and-components-2019.md#Unsupported)」を参照してください。 また、「[既知の問題](sql-server-linux-release-notes.md#known-issues)」も確認してください。 これらのリストで指定されていない限り、Linux では他の SQL Server 機能やサービスがサポートされます。

1. **SQL Server のサポート ポリシーは何ですか?**

   サポート ポリシーを理解するには、[SQL Server のテクニカル サポート ポリシー](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)を確認してください。

1. **Windows SQL Server を使用してきました。SQL Server on Linux の使用方法を学習するのに役立つリソースはありますか?**

   [クイックスタート](sql-server-linux-setup.md#platforms)では、SQL Server on Linux をインストールし、Transact-SQL クエリを実行する詳細な方法が提供されています。 その他のチュートリアルでは、SQL Server on Linux の使用の追加の手順が提供されています。 サードパーティのヒントのリストについては、[SQL Server on Linux のヒントの MSSQLTIPS リスト](https://www.mssqltips.com/sql-server-tip-category/226/sql-server-on-linux/)に関するページを参照してください。

## <a name="licensing"></a>ライセンス

1. **Linux ではライセンスはどのように機能しますか?**

   SQL Server には、Windows と Linux の両方で同じ方法でライセンスが付与されます。 実際には、SQL Server にライセンスを付与してから、そのライセンスを任意のプラットフォームで使用するように選択できます。 詳細については、「[SQL Server のライセンス方法](https://www.microsoft.com/sql-server/sql-server-2017-pricing)」を参照してください。

1. **既に購入している場合は、どのエディションの SQL Server を選択する必要がありますか?**

   mssql-conf セットアップを実行すると、次のオプションが表示されます。
   
   ```
   Choose an edition of SQL Server:
      1. Evaluation (free, no production use rights, 180-day limit)
      2. Developer (free, no production use rights)
      3. Express (free)
      4. Web (PAID)
      5. Standard (PAID)
      6. Enterprise (PAID)
      7. Enterprise Core (PAID)
      8. I bought a license through a retail sales channel and have a product key to enter.
   ```
     
   マイクロソフト エンタープライズ契約の一部としてボリューム ライセンスを通じて、または MSDN サブスクリプションを通じて、ライセンスを取得した場合は、オプション 4 から 7 を選択する必要があります。 この手順ではライセンスを入力するように求めるメッセージは表示されませんが、構成に適したライセンスを事前に購入しておく必要があります。 小売チャネルを通じて Standard Edition を購入した場合は、オプション 8 を選択します。 このオプションでは、キーを入力するように求められます。 

1. **SQL Server on Linux のインストールされているバージョンとエディションはどのように確認すればよいですか?**

   **sqlcmd**、**mssql-cli**、Visual Studio Code などのクライアント ツールを使用して、SQL Server インスタンスに接続します。 その後、以下の Transact-SQL クエリを実行し、実行している SQL Server のバージョンとエディションを確認します。 

   ```sql
   SELECT @@VERSION
   SELECT SERVERPROPERTY('Edition')
   ```

## <a name="installation"></a>インストール

1. **Linux サーバーには SQL Server をどのようにインストールすればよいですか?**

   Microsoft では、SQL Server をインストールするためのパッケージ リポジトリを保持しており、yum、zypper、apt などのネイティブ パッケージ マネージャーを使用したインストールをサポートしています。 すばやくインストールするには、[クイックスタート](sql-server-linux-setup.md#platforms)のいずれかを参照してください。

1. **Linux Subsystem for Windows 10 に SQL Server をインストールできますか?**

   不可。 Windows 10 で実行されている Linux は、現在、SQL Server および関連ツールでサポートされているプラットフォームではありません。

1. **SQL Server では、データ ファイルに対してどの Linux ファイル システムを使用できますか?**

   現在、SQL Server on Linux では ext4 と XFS がサポートされています。 その他のファイル システムのサポートは、今後、必要に応じて追加されます。

1. **インストール パッケージをダウンロードして SQL Server をオフラインでインストールすることはできますか?**

   可能。 詳細については、[リリース ノート](sql-server-linux-release-notes.md)に関するページのパッケージ ダウンロード リンクを参照してください。 また、[オフライン インストールの手順](sql-server-linux-setup.md#offline)を確認してください。

1. **SQL Server on Linux の無人インストールを実行できますか?**

   可能。 無人インストールの詳細については、「[SQL Server on Linux のインストール ガイダンス](sql-server-linux-setup.md#unattended)」を参照してください。 [Red Hat](sample-unattended-install-redhat.md)、[SUSE Linux Enterprise Server](sample-unattended-install-suse.md)、[Ubuntu](sample-unattended-install-ubuntu.md) のサンプル スクリプトを参照してください。 SQL Server Customer Advisory Team によって作成された[このサンプル スクリプト](https://blogs.msdn.microsoft.com/sqlcat/2017/10/03/unattended-install-and-configuration-for-sql-server-2017-on-linux/)を確認することもできます。

## <a name="tools"></a>ツール

1. **Windows で SQL Server Management Studio クライアントを使用して SQL Server on Linux にアクセスすることはできますか?**

   はい。Windows で実行されているすべての既存のツールを使用して、SQL Server on Linux にアクセスできます。 これには、SQL Server Management Studio (SSMS)、SQL Server Data Tools (SSDT) などの Microsoft のツール、および OSS とサードパーティ製ツールが含まれます。

1. **Linux で実行される SSMS のようなツールはありますか?**

   新しい Azure Data Studio は、SQL Server を管理するためのクロスプラットフォーム ツールです。 詳細については、[Azure Data Studio とは何か](../azure-data-studio/what-is.md)に関するページを参照してください。

1. **sqlcmd や bcp のようなコマンドを Linux で使用できますか?**

   はい。[sqlcmd と bcp](sql-server-linux-setup-tools.md) は、Linux、macOS、および Windows でネイティブに使用できます。 また、Linux、macOS、または Windows 上で新しい [mssql-scripter](https://github.com/Microsoft/mssql-scripter) コマンドライン ツールを使用して、任意の場所で実行されている SQL データベース用の T-SQL スクリプトを生成します。 [mssql-cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/) のプレビュー リリースも参照してください。

1. **Linux で実行されているインスタンスのために Windows の SSMS を介して接続した場合、利用状況モニターを表示することはできますか?**

   はい。Windows の SSMS を使用してリモートで接続し、Linux インスタンスで利用状況モニター コマンドなどのツール/機能を使用することができます。

1. **Linux で SQL Server パフォーマンスを監視するために使用できるツールは何ですか?**

   [システム動的管理ビュー (DMV)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) を使用して、Linux プロセス情報を含む、SQL Server に関するさまざまな種類の情報を収集できます。 [クエリ ストア](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)を使用すると、クエリのパフォーマンスを向上させることができます。 組み込みの[パフォーマンス ダッシュボード](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/)などの他のツールは、Windows の SQL Server Management Studio (SSMS) でリモートで動作します。

   > [!TIP]
   > パフォーマンスを向上させる方法の 1 つは、Linux オペレーティング システムと SQL Server インスタンスを適切に構成することです。 詳細については、「[パフォーマンスのベスト プラクティスと SQL Server on Linux の構成ガイドライン](sql-server-linux-performance-best-practices.md)」を参照してください。

## <a name="administration"></a>管理

1. **Microsoft では、Linux 上の SQL Server 構成マネージャーのようなアプリが作成されていますか?**

   はい。[mssql-conf](sql-server-linux-configure-mssql-conf.md) という SQL Server on Linux 用の構成ツールがあります。

1. **SQL Server on Linux で同じホスト上の複数のインスタンスはサポートされますか?**

   複数の異なるインスタンスが含まれるように、ホスト上で複数のコンテナーを実行することをお勧めします。 これは docker を使用して簡単に実現されますが、各コンテナーでは別のポートでリッスンする必要があります。 詳細については、「[複数の SQL Server コンテナーを実行する](sql-server-linux-configure-docker.md#run-multiple-sql-server-containers)」を参照してください。

1. **Linux では Active Directory 認証がサポートされていますか?**

   可能。 詳細については、[SQL Server on Linux での Active Directory 認証](sql-server-linux-active-directory-authentication.md)に関するページを参照してください。

1. **Linux では Always On とクラスタリングがサポートされていますか?**

   Linux でのフェールオーバー クラスタリングと高可用性は、Linux の Pacemaker を使用して実現されます。 詳細については、「[ビジネス継続性とデータベース復旧 - SQL Server on Linux](sql-server-linux-business-continuity-dr.md)」を参照してください。

1. **Linux から Windows へ、またその逆のレプリケーションを構成することはできますか?**

   読み取りスケール レプリカは、一方向のデータ レプリケーションのために Windows と Linux の間で使用できます。

1. **以前のバージョンの SQL Server の既存のデータベースを Windows から Linux に移行することはできますか?**

   はい。これを実現する[いくつかの方法](sql-server-linux-migrate-overview.md)があります。

1. **Oracle や他のデータベース エンジンから SQL Server on Linux にデータを移行することはできますか?**

   可能。 SSMA では、次のいくつかの種類のデータベース エンジンからの移行がサポートされています:Microsoft Access、DB2、MySQL、Oracle、および SAP ASE (旧称: SAP Sybase ASE)。 SSMA の使用方法の例については、[SQL Server Migration Assistant を使用した SQL Server on Linux への Oracle スキーマの移行](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=/sql/toc/toc.json)に関するページを参照してください。

1. **SQL Server ファイルにはどのようなアクセス許可が必要ですか?**

   `/var/opt/mssql` ファイル フォルダー内のすべてのファイルは、**mssql** ユーザーが所有し、**mssql** グループに属している必要があります。 **mssql** ユーザーとグループの両方に、すべてのファイルとディレクトリの読み取り/書き込みアクセス許可がある必要があります。 ファイルとディレクトリのアクセス許可に関連する次のような特殊なシナリオに注意してください。

   * SQL Server ファイルの格納に使用されるマウントされたネットワーク共有には、mssql 所有者とグループのアクセス許可が必要です。
   * データベース ファイルまたはバックアップを既定以外のディレクトリに配置する場合は、そのディレクトリに対するアクセス許可も設定する必要があります。
   * 既定のルート umask を 0022 から変更した場合、インストール後の SQL Server の構成は失敗します。 その後、必要なアクセス許可を SQL Server 開始アカウントに手動で適用する必要があります。

1. **インストールされている mssql アカウントとグループから SQL Server ファイルとディレクトリの所有権を変更することはできますか?**

   既定のインストールからの SQL Server ディレクトリとファイルの所有権の変更はサポートされていません。 mssql アカウントとグループは特に SQL Server に使用され、対話型ログイン アクセス権はありません。

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
