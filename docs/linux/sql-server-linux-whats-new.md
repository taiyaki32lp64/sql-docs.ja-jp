---
title: SQL Server 2017 on Linux の新機能
description: この記事では、SQL Server 2017 on Linux の新機能について説明します。
author: VanMSFT
ms.author: vanto
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 6874c34c70b562ef726bda5abbda2aebe615cc08
ms.sourcegitcommit: bb56808dd81890df4f45636b600aaf3269c374f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72890546"
---
# <a name="whats-new-for-sql-server-2017-on-linux"></a>SQL Server 2017 on Linux の新機能

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、Linux 上で実行される SQL Server 2017 で使用できる主な機能とサービスについて説明します。

> [!NOTE]
> この記事に含まれているこれらの機能に加えて、累積的な更新プログラムが定期的にリリースされます。 これらの累積的な更新プログラムでは、多くの機能強化と修正が提供されます。 最新の CU リリースについて詳しくは、[https://aka.ms/sql2017cu](https://aka.ms/sql2017cu) を参照してください。 パッケージのダウンロードと既知の問題については、[リリース ノート](sql-server-linux-release-notes.md)のページをご覧ください。

## <a name="sql-server-database-engine"></a>SQL Server データベース エンジン

- コア SQL Server データベース エンジンの機能が有効になりました。
- ネイティブ Linux パスのサポート。
- IPv6 のサポート。
- NFS 上のデータベース ファイルのサポート。
- [トランスポート層セキュリティ](sql-server-linux-encrypted-connections.md) (TLS) の暗号化が有効になりました。
- [Active Directory 認証](sql-server-linux-active-directory-authentication.md)が有効になりました。
- 高可用性のための[可用性グループ機能](sql-server-linux-availability-group-overview.md)。
- [フルテキスト検索](sql-server-linux-setup-full-text-search.md)のサポート。

## <a name="sql-server-agent"></a>SQL Server エージェント

- 次のタスクに対する [SQL Server エージェント](sql-server-linux-setup-sql-agent.md)のサポートが有効になりました。
  - [Transact-SQL ジョブ](sql-server-linux-run-sql-server-agent-job.md)
  - [DB メール](sql-server-linux-db-mail-sql-agent.md)
  - [ログ配布](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- Linux 上で SSIS パッケージを実行する機能。 詳しくは、「[ssis-conf を使用して Linux で SQL Server Integration Services を構成する](sql-server-linux-configure-ssis.md)」をご覧ください。

## <a name="other-improvements"></a>その他の機能強化

- コマンドライン構成ツール、[mssql-confmssql-conf](sql-server-linux-configure-mssql-conf.md)。
- [環境変数](sql-server-linux-configure-environment-variables.md)での無人インストールのサポート。
- クロスプラットフォームの [Visual Studio Code mssql-server 拡張機能](sql-server-linux-develop-use-vscode.md)。
- クロスプラットフォームのスクリプト ジェネレーター、[mssql-scripter](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md)。
- クロスプラットフォームの動的管理ビュー (DMV) モニター、[DBFS ツール](https://github.com/Microsoft/dbfs)。

## <a name="next-steps"></a>次の手順

SQL Server on Linux をインストールするには、次のチュートリアルのいずれかを使用します。

- [Red Hat Enterprise Linux へのインストール](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server へのインストール](quickstart-install-connect-suse.md)
- [Ubuntu へのインストール](quickstart-install-connect-ubuntu.md)
- [Docker 上での実行](quickstart-install-connect-docker.md)
- [Azure での SQL VM プロビジョニング](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

よく寄せられる質問に対する回答については、「[SQL Server on Linux に関する FAQ](sql-server-linux-faq.md)」を参照してください。 SQL Server 2017 で導入されたその他の改善点については、「[SQL Server 2017 の新機能](../sql-server/what-s-new-in-sql-server-2017.md)」を参照してください。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
