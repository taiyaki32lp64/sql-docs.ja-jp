---
title: SQL Server on Linux の概要
description: この記事では、Linux 上で SQL Server を実行する方法を説明し、詳細を学習する方法について詳細情報を提供します。
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.openlocfilehash: 31904a43dba642c73620a66bcf4abaa066b5ef82
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531279"
---
# <a name="sql-server-on-linux"></a>Linux 上の SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: moniker range="= sql-server-2017 || = sqlallproducts-allversions"
SQL Server 2017 から、SQL Server は Linux 上で動作するようになりました。 これは同じ SQL Server データベース エンジンであり、オペレーティング システムに関係なく、多くの似た機能とサービスを備えています。
::: moniker-end

::: moniker range=">= sql-server-ver15 || >= sql-server-linux-ver15"
SQL Server 2019 は Linux で動作します。 これは同じ SQL Server データベース エンジンであり、オペレーティング システムに関係なく、多くの似た機能とサービスを備えています。 このリリースの詳細については、[Linux 用 SQL Server 2019 の新機能](sql-server-linux-whats-new-2019.md)に関するページを参照してください。
::: moniker-end

::: moniker range="= sql-server-2017"
> [!TIP]
> [SQL Server 2019](sql-server-linux-overview.md?view=sql-server-ver15) が使用できるようになりました。 最新リリースの Linux の新機能については、[Linux 用 SQL Server 2019 の新機能](sql-server-linux-whats-new-2019.md?view=sql-server-ver15)に関するページを参照してください。
::: moniker-end

::: moniker range="= sql-server-linux-2017"
> [!TIP]
> [SQL Server 2019](sql-server-linux-overview.md?view=sql-server-linux-ver15) が使用できるようになりました。 最新リリースの Linux の新機能については、[Linux 用 SQL Server 2019 の新機能](sql-server-linux-whats-new-2019.md?view=sql-server-linux-ver15)に関するページを参照してください。
::: moniker-end

::: moniker range="= sqlallproducts-allversions"
> [!TIP]
> SQL Server 2019 が使用できるようになりました。 最新リリースの Linux の新機能については、[Linux 用 SQL Server 2019 の新機能](sql-server-linux-whats-new-2019.md)に関するページを参照してください。
::: moniker-end

## <a name="install"></a>インストール

開始するには、次のクイックスタートのいずれかを使用して SQL Server on Linux をインストールします。

- [Red Hat Enterprise Linux へのインストール](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server へのインストール](quickstart-install-connect-suse.md)
- [Ubuntu へのインストール](quickstart-install-connect-ubuntu.md)
- [Docker 上での実行](quickstart-install-connect-docker.md)
- [Azure での SQL VM プロビジョニング](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

> [!NOTE]
> Docker 自体は複数のプラットフォームで動作します。つまり、Linux、Mac、Windows 上で Docker イメージを実行できます。

## <a name="connect"></a>接続する

インストールが完了したら、Linux マシン上で SQL Server インスタンスに接続します。 ローカルでもリモートでも、さまざまなツールやドライバーを使用して接続できます。 このクイックスタートでは、[sqlcmd](sql-server-linux-setup-tools.md) コマンドライン ツールの使用方法を示します。 他に次のようなツールがあります。

| ツール | チュートリアル |
|-----|-----|
| Visual Studio Code (VS Code) | [SQL Server on Linux で VS Code を使用する](sql-server-linux-develop-use-vscode.md) |
| SQL Server Management Studio (SSMS) | [Windows 上の SSMS を使用して SQL Server on Linux に接続する](sql-server-linux-manage-ssms.md) |
| SQL Server Data Tools (SSDT) | [SQL Server on Linux で SSDT を使用する](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>探索

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

SQL Server 2017 は、Linux を含むすべてのサポートされているプラットフォームで、基になるデータベース エンジンが同じです。 そのため、既存の多くの特徴と機能が Linux でも同じように動作します。 ドキュメントのこの領域では、Linux の観点から、これらの機能の一部を紹介します。 また、Linux 上では独自の要件がある領域に関する注意も示します。

既に SQL Server について理解している場合は、[リリース ノート](sql-server-linux-release-notes.md)で、このリリースの一般的なガイドラインと既知の問題を参照してください。 次に、[SQL Server on Linux の新機能](sql-server-linux-whats-new.md)と [SQL Server 2017 全体の新機能](../sql-server/what-s-new-in-sql-server-2017.md)を参照してください。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15"

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] は、Linux を含むすべてのサポートされているプラットフォームで、基になるデータベース エンジンが同じです。 そのため、既存の多くの特徴と機能が Linux でも同じように動作します。 ドキュメントのこの領域では、Linux の観点から、これらの機能の一部を紹介します。 また、Linux 上では独自の要件がある領域に関する注意も示します。

既に SQL Server on Linux について理解している場合は、[リリース ノート](sql-server-linux-release-notes-2019.md)で、このリリースの一般的なガイドラインと既知の問題を参照してください。 次に、[SQL Server on Linux 2019 の新機能](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15)を確認します。

::: moniker-end

<!--SQL Server All Versions-->
::: moniker range="=sqlallproducts-allversions"

SQL Server 2017 と [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] は、Linux を含むすべてのサポートされているプラットフォームで、基になるデータベース エンジンが同じです。 そのため、既存の多くの特徴と機能が Linux でも同じように動作します。 ドキュメントのこの領域では、Linux の観点から、これらの機能の一部を紹介します。 また、Linux 上では独自の要件がある領域に関する注意も示します。

既に SQL Server on Linux について理解している場合は、リリース ノートを参照してください。

- [SQL Server 2017 リリース ノート](sql-server-linux-release-notes.md)
- [SQL Server 2019 リリース ノート](sql-server-linux-release-notes-2019.md)

次に、新機能についてを参照してください。

- [SQL Server 2017 の新機能](sql-server-linux-whats-new.md)
- [SQL Server 2019 on Linux の新機能](../sql-server/what-s-new-in-sql-server-ver15.md#sql-server-on-linux)

::: moniker-end

> [!TIP]
> よく寄せられる質問に対する回答については、「[SQL Server on Linux に関する FAQ](sql-server-linux-faq.md)」を参照してください。

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
