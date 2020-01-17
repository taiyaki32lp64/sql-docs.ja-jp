---
title: Azure にデプロイされた SSIS パッケージの検証 | Microsoft Docs
description: Azure で期待どおりにパッケージが実行されない可能性のある既知の問題について、SSIS のパッケージの配置ウィザードでパッケージを確認する方法について説明します。
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: fd6c55f439b9d95473c5e36ea88cc7c5e1fb555e
ms.sourcegitcommit: e7c3c4877798c264a98ae8d51d51cb678baf5ee9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72915993"
---
# <a name="validate-sql-server-integration-services-ssis-packages-deployed-to-azure"></a>Azure にデプロイされた SQL Server Integration Services (SSIS) パッケージを検証する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



SQL Server Integration Services (SSIS) プロジェクトを Azure サーバーの SSIS カタログ (SSISDB) にデプロイすると、パッケージの配置ウィザードにより、 **[確認]** ページの後に検証手順が追加されます。 この検証手順では、Azure SSIS Integration Runtime で予定されているパッケージ実行を妨げる既知の問題がないか、プロジェクトのパッケージが調べられます。 その後、 **[検証]** ページに該当する警告が表示されます。

> [!IMPORTANT]
> この記事で説明する検証は、SQL Server Data Tools (SSDT) バージョン 17.4 以降でプロジェクトをデプロイするときに行われます。 最新版の SSDT を入手する方法については、「[SQL Server Data Tools (SSDT) のダウンロード](../../ssdt/download-sql-server-data-tools-ssdt.md)」をご覧ください。

パッケージの配置ウィザードの詳細については、「[Integration Services (SSIS) プロジェクトとパッケージの配置](../packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。

## <a name="validate-connection-managers"></a>接続マネージャーを検証する

ウィザードでは、接続を失敗させる可能性がある次の問題がないか、特定の接続マネージャーが確認されます。
- **Windows 認証**。 接続文字列で Windows 認証を使用する場合、検証で警告が表示されます。 Windows 認証は、追加の構成手順を要求します。 詳細については、「[Windows 認証でデータとファイル共有に接続する](ssis-azure-connect-with-windows-auth.md)」を参照してください。
- **ファイル パス**。 接続文字列に `C:\\...` のようなハードコーディングされたローカル ファイル パスが含まれる場合、検証で警告が表示されます。 絶対パスを含むパッケージは失敗することがあります。
- **UNC パス**。 接続文字列に UNC パスが含まれる場合、検証で警告が表示されます。 UNC パスを含むパッケージは失敗することがあります。一般的に、UNC パスはアクセスに Windows 認証を要求するためです。
- **ホスト名**。 サーバー プロパティに IP アドレスではなくホスト名が含まれる場合、検証で警告が表示されます。 ホスト名を含むパッケージは失敗することがあります。一般的に、Azure 仮想ネットワークは DNS 名前解決のために正しい DNS 構成を必要とするためです。
- **プロバイダーまたはドライバー**。 プロバイダーまたはドライバーがサポートされていない場合、検証で警告が表示されます。 現時点では、ごく少数の組み込みプロバイダー/ドライバーがサポートされています。

このウィザードでは、一覧の接続マネージャーに対して次の検証が行われます。

| 接続マネージャー | Windows 認証 | [ファイル パス] | UNC パス | ホスト名 | プロバイダーまたはドライバー |
|--------------------|----------|-----------|-----|-----------|-------------------|
| Ado                | âœ“        |           |     | âœ“         | âœ“                 |
| AdoNet             | âœ“        |           |     | âœ“         | âœ“                 |
| Cache              |          | âœ“         | âœ“   |           |                   |
| [エクスポート]              |          | âœ“         | âœ“   |           |                   |
| ファイル               |          | âœ“         | âœ“   |           |                   |
| FlatFile           |          | âœ“         | âœ“   |           |                   |
| Ftp                |          |           |     | âœ“         |                   |
| MsOLAP100          |          |           |     | âœ“         | âœ“                 |
| MultiFile          |          | âœ“         | âœ“   |           |                   |
| MultiFlatFile      |          | âœ“         | âœ“   |           |                   |
| OData              | âœ“        |           |     | âœ“         |                   |
| Odbc               | âœ“        |           |     | âœ“         | âœ“                 |
| OleDb              | âœ“        |           |     | âœ“         | âœ“                 |
| SmoServer          | âœ“        |           |     | âœ“         |                   |
| Smtp               | âœ“        |           |     | âœ“         |                   |
| SqlMobile          |          | âœ“         | âœ“   |           |                   |
| Wmi                | âœ“        |           |     |           |                   |
|||||||

## <a name="validate-sources-and-destinations"></a>ソースとターゲットの検証
次のサードパーティ ソース/ターゲットはサポートされていません。

-   Attunity Oracle ソース/ターゲット
-   Attunity Teradata ソース/ターゲット
-   SAP BI ソース/ターゲット

## <a name="validate-tasks-and-components"></a>タスクとコンポーネントの検証

### <a name="execute-process-task"></a>プロセス実行タスク

絶対パスを持つローカル ファイルか UNC パスを持つファイルをコマンドが指す場合、検証で警告が表示されます。 このようなパスでは、Azure 上の実行が失敗することがあります。

### <a name="script-task-and-script-component"></a>スクリプト タスクとスクリプト コンポーネント

サポートされていないアセンブリを参照したり、呼び出したりする可能性があるスクリプト タスクまたはスクリプト コンポーネントがパッケージに含まれる場合、検証で警告が表示されます。 このような参照や呼び出しが原因で実行に失敗することがあります。

### <a name="other-components"></a>その他のコンポーネント

Orc 形式は HDFS ターゲットと Azure Data Lake Store ターゲットでサポートされていません。

## <a name="next-steps"></a>次の手順
Azure でパッケージ実行をスケジュールする方法については、「[Azure で SSIS パッケージのスケジュールを設定する](ssis-azure-schedule-packages.md)」を参照してください。
