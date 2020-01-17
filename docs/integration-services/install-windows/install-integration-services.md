---
title: SQL Server Integration Services (SSIS) をインストールする | Microsoft Docs
description: Microsoft SQL Server Integration Services (SSIS) をインストールする方法と、SSIS の他のダウンロードを取得する方法について説明します
ms.custom: ''
ms.date: 09/19/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, installing
- SSIS, installing
- installing Integration Services, about installing Integration Services
- SQL Server Integration Services, installing
- Setup [Integration Services], about installing Integration Services
- installing Integration Services
- Setup [Integration Services]
ms.assetid: bd20fd3a-414b-4581-959d-ebba4ddf5a55
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0478e345f388b3f4246bf33fdaba29a47a6ec0f6
ms.sourcegitcommit: a26cb217adfbbfb3636dff43fb19a46462e2e994
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74491956"
---
# <a name="install-integration-services-ssis"></a>Integration Services (SSIS) のインストール

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] を含む任意またはすべてのコンポーネントを 1 つのセットアップ プログラムでインストールできます。 他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントと共にまたは単独で、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] を 1 台のコンピューターにインストールするには、セットアップを使います。

 この記事では、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールする前に知っておく必要がある重要な注意点について説明します。 この記事の情報を参考にして各インストール オプションを評価することにより、インストール時に適切な選択を行うことができます。

![Integration Services のインストール](install-integration-services/install-integration-services-sql-setup.png)

## <a name="get-ready-to-install-integration-services"></a>Integration Services のインストールを準備する

[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールする前に、次の情報を確認してください。

- [SQL Server のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)

- [SQL Server インストールにおけるセキュリティの考慮事項](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)

## <a name="install-standalone-or-side-by-side"></a>スタンドアロンまたはサイド バイ サイドでインストールする

次の構成で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールできます。

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の以前のインスタンスが存在しないコンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールできます。

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の既存のインスタンスとサイド バイ サイドでインストールできます。

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の以前のバージョンが既にインストールされているコンピューターで [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の最新バージョンにアップグレードすると、現在のバージョンは以前のバージョンとサイド バイ サイドでインストールされます。

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のアップグレードについて詳しくは、「[Integration Services のアップグレード](../../integration-services/install-windows/upgrade-integration-services.md)」をご覧ください。

## <a name="get-sql-server-with-integration-services"></a>Integration Services で SQL Server を取得する

Microsoft SQL Server がまだない場合は、無料の Evaluation Edition または無料の Developer Edition を、[SQL Server のダウンロード](https://www.microsoft.com/sql-server/sql-server-downloads) ページからダウンロードします。 SQL Server の Express Edition には SSIS は含まれません。

## <a name="install-integration-services"></a>Integration Services のインストール

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール要件を検討し、コンピューターがそれらの要件を満たしていることを確認したら、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のインストールの準備は完了です。

セットアップ ウィザードを使って [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールする場合は、一連のページを使ってコンポーネントとオプションを指定します。

- **[機能の選択]** ページの **[共有機能]**で**[Integration Services]** を選びます。

- SSIS パッケージを格納、管理、実行、監視するために SSIS カタログ データベース `SSISDB` をホストするには、 **[インスタンス機能]** で必要に応じて **[データベース エンジン サービス]** を選びます。

- [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プログラミング用にマネージド アセンブリをインストールするには、 **[共有機能]** で **[クライアント ツール SDK]** も選びます。

> [!NOTE]
> セットアップ ウィザードの **[機能の選択]** ページでインストールを選ぶことができる一部の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントで、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントのサブセットの一部がインストールされます。 これらのコンポーネントを使って一部のタスクを実行することは可能ですが、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のすべての機能を使うことはできません。 たとえば、 **[データベース エンジン サービス]** オプションを選択すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] インポートおよびエクスポート ウィザードに必要な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントがインストールされます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]を完全にインストールするには、 **[機能の選択]** ページで **[Integration Services]** を選択する必要があります。

### <a name="installing-a-dedicated-server-for-etl-processes"></a>ETL プロセス専用サーバーのインストール

ETL (抽出、変換、読み込み) プロセス専用のサーバーを使うには、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のインストール時に [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のローカル インスタンスをインストールします。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、通常、パッケージを [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに格納し、このパッケージのスケジュールを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントに依存して設定します。 ETL サーバーに [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスが存在しない場合は、[!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスが存在するサーバーからパッケージをスケジュール設定したり実行したりする必要があります。 結果として、パッケージは、ETL サーバーではなく、パッケージが開始されたサーバーで実行されます。 その結果、専用の ETL サーバーのリソースは意図したとおりに使用されません。 さらに、他のサーバーのリソースが実行中の ETL プロセスによって使用される場合もあります。

### <a name="configuring-ssis-event-logging"></a>SSIS イベント ログの構成

既定では、新規インストールで、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] はパッケージの実行に関連するイベントをアプリケーション イベント ログに記録しないように構成されます。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のデータ コレクター機能を使用すると、この設定により、大量のイベント ログ エントリは生成されません。 ログに記録されないイベントは、EventID 12288 の "パッケージが起動されました。" や EventID 12289 の "パッケージが正常に完了しました。" です。 これらのイベントをアプリケーション イベント ログに記録するには、レジストリを編集用に開きます。 次に、レジストリ内で HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS ノードを見つけ、LogPackageExecutionToEventLog 設定の DWORD 値を 0 から 1 に変更します。

## <a name="install-additional-components-for-integration-services"></a>Integration Services の追加コンポーネントをインストールする

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の完全なインストールの場合は、次の一覧から必要なコンポーネントを選びます。

- **Integration Services (SSIS)** 。 SQL Server セットアップ ウィザードで SSIS をインストールします。 SSIS を選ぶと、次のものがインストールされます。

  - SQL Server データベース エンジンでの SSIS カタログのサポート。

  - 必要に応じて、マスターとワーカーで構成される [Scale Out 機能](../scale-out/walkthrough-set-up-integration-services-scale-out.md)。

  - 32 ビットおよび 64 ビットの SSIS コンポーネント。

  - SSIS をインストールしても、SSIS パッケージの設計と開発に必要なツールはインストール**されません**。

- **SQL Server データベース エンジン**。 SQL Server セットアップ ウィザードでデータベース エンジンをインストールします。 データベース エンジンを選ぶと、SSIS パッケージを格納、管理、実行、監視するための SSIS カタログ データベース `SSISDB` を作成してホストできます。

- **SQL Server Data Tools (SSDT)** 。 SSDT をダウンロードしてインストールするには、「[SQL Server Data Tools (SSDT) のダウンロード](../../ssdt/download-sql-server-data-tools-ssdt.md)」をご覧ください。 SSDT をインストールすると、SSIS パッケージを設計して展開できます。 SSDT では次のものがインストールされます。

  - SSIS パッケージの設計および開発ツール (SSIS デザイナーなど)。

  - 32 ビットの SSIS コンポーネントのみ。

  - Visual Studio の限定バージョン (Visual Studio のエディションがまだインストールされていない場合)。

  - Visual Studio Tools for Applications (VSTA)。SSIS スクリプト タスクおよびスクリプト コンポーネントで使われるスクリプト エディターです。

  - 展開ウィザードとパッケージ アップグレード ウィザードを含む SSIS ウィザード。

  - SQL Server インポートおよびエクスポート ウィザード。

- **SQL Server Data Tools (SSDT)** 。 Visual Studio 2019 向け SSDT スタンドアロン インストーラーは廃止となりました。 Visual Studio 2019 に関しては、今後、[VS マーケット プレース](https://marketplace.visualstudio.com/items?itemName=SSIS.SqlServerIntegrationServicesProjects&ssr=false#overview)から SSIS デザイナー拡張機能を入手できます。

- **Integration Services Feature Pack for Azure**。 Feature Pack のダウンロードとインストールについて詳しくは、「[Microsoft SQL Server 2017 Integration Services Feature Pack for Azure](https://docs.microsoft.com/sql/integration-services/azure-feature-pack-for-integration-services-ssis?view=sql-server-2017)」をご覧ください。 Feature Pack をインストールすると、パッケージは、次のサービスを含む Azure クラウドのストレージ サービスと分析サービスに接続できます。

  - Azure Blob Storage です。

  - Azure HDInsight。

  - Azure Data Lake Store。

  - Azure SQL Data Warehouse。

  - Azure Data Lake Storage (Gen2)。

- **オプションの追加コンポーネント**。 必要に応じて、SQL Server Feature Package から追加のサードパーティ コンポーネントをダウンロードできます。

  - Microsoft SQL Server® 用 Microsoft® Connector for SAP BW。 これらのコンポーネントを入手するには、「[Microsoft® SQL Server® 2017 Feature Pack](https://www.microsoft.com/download/details.aspx?id=55992)」をご覧ください。

  - Microsoft Connector Version 5.0 for Oracle by Attunity および Microsoft Connector Version 5.0 for Teradata by Attunity。 これらのコンポーネントを入手するには、「[Microsoft Connectors v5.0 for Oracle and Teradata](https://www.microsoft.com/download/details.aspx?id=55179)」をご覧ください。

## <a name="next-steps"></a>次のステップ

- [Integration Services バージョンのサイド バイ サイド インストール](installing-integration-services-versions-side-by-side.md)

- [SQL Server 2016 の Integration Services の新機能](../what-s-new-in-integration-services-in-sql-server-2016.md)

- [SQL Server 2017 の Integration Services の新機能](../what-s-new-in-integration-services-in-sql-server-2017.md)
