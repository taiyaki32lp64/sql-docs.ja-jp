---
title: SQL Server on Linux 用のアプリケーションを開発する
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 11/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 758cb738-b018-465b-9ab0-59a24b892e66
ms.openlocfilehash: 584bf33201cab5d0f57205de0fed181725187d52
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077412"
---
# <a name="how-to-get-started-developing-applications-for-sql-server-on-linux"></a>SQL Server on Linux 用のアプリケーションの開発を開始する方法

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server on Linux に接続して使用するアプリケーションは、さまざまなプログラミング言語 (C#、Java、Node.js、PHP、Python、Ruby、C++ など) で作成できます。 一般的な Web フレームワークやオブジェクト リレーショナル マッピング (ORM) フレームワークを使用することもできます。

> [!VIDEO https://channel9.msdn.com/events/Connect/2017/T153/player]

> [!TIP]
> これらと同じ開発オプションを使用して、他のプラットフォームの SQL Server を対象にすることもできます。 アプリケーションは、オンプレミスまたはクラウドの、Linux、Windows、または macOS の Docker 上で実行されている SQL Server を対象にできます。 または、Azure SQL Database および Azure SQL Data Warehouse を対象にすることもできます。

## <a name="try-the-tutorials"></a>チュートリアルを試す

SQL Server に対するアプリケーションの構築を始める最適な方法は、自分で試してみることです。

- [開始用のチュートリアル](https://aka.ms/sqldev)を参照します。
- 言語と開発プラットフォームを選択します。
- コード サンプルを試します。

> [!TIP]
> Docker 上の SQL Server 向けに開発する場合は、**macOS** のチュートリアルを参照してください。

## <a name="create-new-applications"></a>新しいアプリケーションを作成する

新しいアプリケーションを作成している場合は、さまざまなプログラミング言語で使用できるコネクタや一般的なフレームワークの概要を、[接続ライブラリ](sql-server-linux-develop-connectivity-libraries.md)の一覧でご確認ください。

## <a name="use-existing-applications"></a>既存のアプリケーションを使用する

既存のデータベース アプリケーションがある場合は、接続文字列を変更するだけで SQL Server on Linux を対象にすることができます。 SQL Server on Linux に関する[既知の問題](sql-server-linux-release-notes.md)について必ずお読みください。

## <a name="use-existing-sql-tools-on-windows-with-sql-server-on-linux"></a>Windows の既存の SQL ツールを SQL Server on Linux で使用する

現在 Windows で実行されているツール (SSMS、SSDT、PowerShell など) は SQL Server on Linux でも動作します。 これらは Linux 上でネイティブに実行されませんが、Linux 上のリモート SQL Server インスタンスを管理することはできます。 

詳細については、次の各トピックを参照してください。

- [SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)
- [SQL Server Data Tools (SSDT)](sql-server-linux-develop-use-ssdt.md)
- [SQL PowerShell](sql-server-linux-manage-powershell.md)

> [!Note]
> 最適なエクスペリエンスを得るには、これらのツールの最新バージョンを使用してください。

## <a name="use-new-sql-tools-for-linux"></a>Linux 用の新しい SQL ツールを使用する

[Visual Studio Code](https://code.visualstudio.com) の新しい [mssql 拡張機能](https://aka.ms/mssql-marketplace)が Linux、macOS、および Windows で使用できるようになりました。 手順ごとの説明については、次のチュートリアルをご覧ください。

- [Visual Studio Code の使用](sql-server-linux-develop-use-vscode.md)

また、Linux のネイティブの新しいコマンドライン ツールを使用することもできます。 以下のツールが含まれています。

- [sqlcmd](../tools/sqlcmd-utility.md)
- [bcp](sql-server-linux-migrate-bcp.md)
- [mssql-conf](sql-server-linux-configure-mssql-conf.md)

## <a name="next-steps"></a>次の手順

開始するには、次のクイックスタートのいずれかを使用して SQL Server on Linux をインストールします。

- [Red Hat Enterprise Linux へのインストール](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server へのインストール](quickstart-install-connect-suse.md)
- [Ubuntu へのインストール](quickstart-install-connect-ubuntu.md)
- [Docker 上での実行](quickstart-install-connect-ubuntu.md)
