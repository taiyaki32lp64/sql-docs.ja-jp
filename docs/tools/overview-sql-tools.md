---
title: SQL Server 用の SQL クエリおよび管理ツール、Azure SQL (azure sql データベース、azure sql マネージインスタンス、SQL 仮想マシン)、Azure SQL data warehouse |Microsoft Docs
description: SQL Server 用の SQL クエリおよび管理ツール、Azure SQL (Azure sql database、azure sql マネージインスタンス、SQL 仮想マシン)、Azure SQL data warehouse
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ''
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 09/11/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 9c5262dfc610e62f0782b0cc6c8fe523d94d0730
ms.sourcegitcommit: c0fd28306a3b42895c2ab673734fbae2b56f9291
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2019
ms.locfileid: "71096880"
---
# <a name="sql-query-and-management-tools-for-sql-server"></a>SQL Server 用の SQL クエリおよび管理ツール

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

データベースの管理 (クエリ、監視など) を行うには、ツールが必要です。 データベースはクラウド、Windows、または[Linux](../linux/sql-server-linux-overview.md)で実行できますが、ツールをデータベースと同じプラットフォームで実行する必要はありません。

使用できるデータベースツールは多数あります。この記事では、SQL データベースを操作するために使用できるツールについて説明します。 必要なツールを決定する際には、[どのツールを使用すればよいでしょうか](#which-tool-should-i-choose)。

詳細については、ツールをダウンロードするには、次の表の「ツール」列のリンクを選択してください。 SQL Server をダウンロードするには、「 [SQL Server のインストール](../database-engine/install-windows/install-sql-server.md)」を参照してください。

## <a name="gui-tools-to-manage-databases"></a>データベースを管理するための GUI ツール

次のツールには、グラフィカルユーザーインターフェイス (GUI) が用意されています。

| ツール | [説明] | 実行 |
|:--|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)]は、実行されている任意の場所でデータベースを管理するための、無料の軽量ツールです。 このプレビューリリースでは、拡張された Transact-sql エディターや、データベースの運用状態に対するカスタマイズ可能な洞察など、データベース管理機能を利用できます。 | **[!INCLUDE[name-sos](../includes/name-sos-short.md)] は、Windows、macOS、Linux 上で実行されます**。|
| [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) | SQL Server Management Studio (SSMS) を使用して、SQL Server、Azure SQL Database、および Azure SQL Data Warehouse のクエリ、設計、管理を行います。 | **SSMS は Windows 上で実行**されます。|
| [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md) | SQL Server、Azure SQL Database、および Azure SQL Data Warehouse のために、Visual Studio を強力な開発環境にします。| **SSDT は Windows 上で実行されます**。|
| [Visual Studio Code](https://code.visualstudio.com/)| Visual Studio Code のインストール後、Microsoft SQL Server、Azure SQL Database、および SQL Data Warehouse を開発するための[mssql 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)をインストールします。| **Visual Studio Code は、Windows、macOS、Linux で実行**されます。|

## <a name="command-line-tools-to-manage-databases"></a>データベースを管理するためのコマンドラインツール

主なコマンドラインツールを次に示します。

| ツール | [説明] | 実行 |
|:--|:--|:--|
|[**mssql-cli (プレビュー)** ](mssql-cli.md)|**mssql-cli**は、SQL Server クエリを実行するための対話型コマンドラインツールです。 | Windows、macOS、Linux|
| [**sqlpackage**](sqlpackage.md) |**sqlpackage**は、いくつかのデータベース開発タスクを自動化するコマンドラインユーティリティです。 sqlpackage の macOS および Linux バージョンは、現在プレビューの段階です。 | Windows、macOS、Linux|
|[**SQL Server PowerShell**](../powershell/sql-server-powershell.md)| **SQL Server PowerShell**は、SQL を操作するためのコマンドレットを提供します。| Windows、macOS、Linux|
| [**sqlcmd**](sqlcmd-utility.md) |**sqlcmd**ユーティリティを使用すると、transact-sql ステートメント、システムプロシージャ、およびスクリプトファイルをコマンドプロンプトで入力できます。 | Windows、macOS、Linux|
|[**bcp**](https://docs.microsoft.com/sql/tools/bcp-utility?view=sql-server-2014)|**b**ulk **c**opy **p**rogram ユーティリティ (**bcp**) では、[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスと、ユーザー指定の形式のデータ ファイルとの間でデータの一括コピーを行います。|Windows、macOS、Linux|
|[**mssql-scripter (プレビュー)** ](https://github.com/Microsoft/mssql-scripter)|**scripter**は、SQL Server データベースをスクリプト化するためのマルチプラットフォームコマンドラインエクスペリエンスです。|Windows、macOS、Linux|
|[**mssql-conf**](../linux/sql-server-linux-configure-mssql-conf.md)|**mssql は、** Linux で実行されている SQL Server を構成します。|Linux|

## <a name="which-tool-should-i-choose"></a>どのツールを選択すればよいですか?

- Windows、Linux、または Mac で軽量エディターを使用して、SQL Server インスタンスまたはデータベースを管理しますか? [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) を選択します。
- 完全な GUI サポートを使用して、Windows 上の SQL Server インスタンスまたはデータベースを管理しますか? [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) を選択します。
- Windows でのコンパイル時の検証、リファクタリング、デザイナーのサポートなど、データベースコードを作成または管理しますか? [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md) を選択します。
- IntelliSense、高光灯などの機能を備えたコマンドラインツールを使用して SQL Server に対してクエリを実行しますか? [Mssql-cli の](mssql-cli.md)選択
- Windows、Linux、または Mac の軽量エディターで T-sql スクリプトを作成しますか? [Visual Studio Code](https://code.visualstudio.com/)と[mssql 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)を選択します。

## <a name="additional-tools"></a>その他のツール

| ツール | [説明] |
|:--|:--|
| [構成マネージャー](../tools/configuration-manager/sql-server-configuration-manager-help.md) | SQL Server 構成マネージャーを使用して SQL Server サービスを構成し、ネットワーク接続を構成します。 Windows での Configuration Manager の実行|
| [SQL Server Migration Assistant](../ssma/sql-server-migration-assistant.md) | SQL Server Migration Assistant を使用して、Microsoft Access、DB2、MySQL、Oracle、Sybase から SQL Server へのデータベースの移行を自動化します。|
| [Database Experimentation Assistant](../dea/database-experimentation-assistant-overview.md) | Database Experimentation Assistant を使用して、特定のワークロードの対象となる SQL のバージョンを評価します。 |
| [分散再生](../tools/distributed-replay/install-distributed-replay-overview.md) | 分散再生の機能を使用すると、今後の SQL Server アップグレードの影響を評価するのに役立ちます。 また、分散再生を使用して、ハードウェアとオペレーティングシステムのアップグレード、および SQL Server チューニングの影響を評価することもできます。 |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | Ssbdiagnose ユーティリティは、Service Broker メッセージ交換または Service Broker サービスの構成の問題を報告します。 |

このページに記載されていないその他のツールについては、「 [SQL コマンドプロンプトユーティリティ](command-prompt-utility-reference-database-engine.md)」を参照してください。