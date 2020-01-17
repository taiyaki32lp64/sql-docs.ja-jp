---
title: SSIS で Linux 上のデータの抽出、変換、読み込みを行う
description: この記事では、Linux コンピューターの SQL Server Integration Services (SSIS) について説明します。
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: e6230ee4efebc4b1af873a61e9f2ebfc191df171
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "67943817"
---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>SSIS で Linux 上のデータの抽出、変換、読み込みを行う

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、Linux で SQL Server Integration Services (SSIS) パッケージを実行する方法について説明します。 SSIS では、複数のソースやフォーマットからデータを抽出し、データを変換し、クレンジングし、データを複数の宛先に読み込むことで複雑なデータ統合問題を解決します。 

Linux で実行されている SSIS パッケージは、Windows オンプレミス、クラウド、Linux、または Docker で実行されている Microsoft SQL Server に接続できます。 Azure SQL Database、Azure SQL Data Warehouse、ODBC データ ソース、フラット ファイル、その他のデータ ソース (ADO.NET ソース、XML ファイル、OData サービス) にも接続できます。

SSIS の機能に関する詳細は、「[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)」を参照してください。

## <a name="prerequisites"></a>Prerequisites

Linux コンピューターで SSIS パッケージを実行するには、最初に SQL Server Integration Services をインストールする必要があります。 SSIS は、Linux コンピューターの SQL Server のインストールには含まれていません。 インストール手順については、「[SQL Server Integration Services のインストール](sql-server-linux-setup-ssis.md)」を参照してください。

また、パッケージを作成し、保守管理するには Windows コンピューターが必要です。 SSIS の設計と管理のためのツールは、Linux コンピューターでは現在使用できない Windows アプリケーションです。 

## <a name="run-an-ssis-package"></a>SSIS パッケージを実行する

Linux コンピューターで SSIS パッケージを実行するには、次の操作を行います。

1.  SSIS パッケージを Linux コンピューターにコピーします。
2.  次のコマンドを実行します。
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="run-an-encrypted-password-protected-package"></a>暗号化された (パスワードで保護された) パッケージを実行する
パスワードで暗号化された SSIS パッケージを実行するには、次の 3 つの方法があります。

1.  次の例に示すように、環境変数 `SSIS_PACKAGE_DECRYPT` の値を設定します。

    ```
    SSIS_PACKAGE_DECRYPT=test /opt/ssis/bin/dtexec /f package.dtsx
    ```

2.  次の例に示すように、パスワードを対話方式で入力するには `/de[crypt]` オプションを指定します。

    ```
    /opt/ssis/bin/dtexec /f package.dtsx /de
    
    Enter decryption password:
    ```

3.  次の例に示すように、パスワードをコマンド ラインで指定するには `/de` オプションを指定します。 コマンド履歴にコマンドの解読パスワードが保存されるため、この方法は推奨されません。

    ```
    opt/ssis/bin/dtexec /f package.dtsx /de test
    
    Warning: Using /De[crypt] <password> may store decryption password in command history.
    
    You can use /De[crypt] instead to enter interactive mode,
    or use environment variable SSIS_PACKAGE_DECRYPT to set decryption password.
    ```

## <a name="design-packages"></a>パッケージの設計

**ODBC データ ソースに接続する** Linux CTP 2.1 Refresh 以降の SSIS の場合、SSIS パッケージでは、Linux で ODBC 接続を使用できます。 この機能は SQL Server ドライバーと MySQL ODBC ドライバーでテストされていますが、ODBC 仕様に準拠するあらゆる Unicode ODBC ドライバーでも動作することが予想されます。 デザイン時、DSN または接続文字列を指定し、ODBC データに接続できます。Windows 認証を使用することもできます。 詳細については、[Linux での ODBC サポートの告知ブログ投稿](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)を参照してください。

**パス**。 SSIS パッケージで Windows スタイルのパスを提供します。 Linux の SSIS では Linux スタイルのパスがサポートされていませんが、実行時、Windows スタイルのパスが Linux スタイルのパスにマッピングされます。 その後、たとえば、Linux の SSIS で Windows スタイルのパス `C:\test` が Linux スタイルのパス `/test` にマッピングされます。

## <a name="deploy-packages"></a>パッケージの配置
このリリースでは、Linux のファイル システムにのみパッケージを保管できます。 SSIS カタログ データベースとレガシー SSIS サービスは、Linux では、パッケージの配置と保存のために使用できません。

## <a name="schedule-packages"></a>パッケージのスケジュール設定
`cron` など、Linux システム スケジューリング ツールを利用し、パッケージをスケジューリングできます。 このリリースでは、Linux 上の SQL エージェントを使用してパッケージ実行をスケジューリングすることはできません。 詳細については、「[cron を利用して Linux で SSIS パッケージのスケジュールを設定する](sql-server-linux-schedule-ssis-packages.md)」を参照してください。

## <a name="limitations-and-known-issues"></a>制限事項と既知の問題

Linux の SSIS の制限事項と既知の問題の詳細については、「[Linux の SSIS の制限事項と既知の問題](sql-server-linux-ssis-known-issues.md)」を参照してください。

## <a name="more-info-about-ssis-on-linux"></a>Linux の SSIS に関する詳細情報

Linux の SSIS の詳細については、次のブログ投稿を参照してください。

-   [Linux の SSIS が SQL Server CTP2.1 で使用可能に](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [Linux の SSIS で ODBC がサポートされる (SQL Server CTP 2.1 Refresh)](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-info-about-ssis"></a>SSIS に関する詳細情報

Microsoft SQL Server Integration Services (SSIS) は、データ ウェアハウスの ETL (抽出、変換、読み込み) パッケージなど、パフォーマンスの高いデータ統合ソリューションを構築するためのプラットフォームです。 詳細については、「 [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services)」を参照してください。

SSIS には次の機能があります。
- Windows でパッケージをビルドし、デバッグするためのグラフィカル ツールとウィザード
- FTP 操作、SQL ステートメントの実行、電子メールメッセージの送信などのワークフロー機能を実行するためのさまざまなタスク
- データの抽出と読み込みを行うためのさまざまなデータ ソースと宛先
- データのクリーニング、集計、結合、コピーを行うためのさまざまな変換
- 独自のカスタム スクリプトとコンポーネントで SSIS を拡張するためのアプリケーション プログラミング インターフェイス (API)

SSIS を始めるには、[SQL Server Data Tools (SSDT)](../integration-services/ssis-how-to-create-an-etl-package.md) の最新版をダウンロードします。

SSIS の詳細については、次の記事を参照してください。
- [SQL Server Integration Services の詳細情報](../integration-services/sql-server-integration-services.md)
- [SQL Server Integration Services (SSIS) の開発ツールと管理ツール](../integration-services/integration-services-ssis-development-and-management-tools.md)
- [SQL Server Integration Services チュートリアル](../integration-services/integration-services-tutorials.md)

## <a name="related-content-about-ssis-on-linux"></a>Linux 上の SSIS の関連コンテンツ
-   [Linux に SQL Server Integration Services (SSIS) をインストールする](sql-server-linux-setup-ssis.md)
-   [ssis-conf を使用して Linux で SQL Server Integration Services を構成する](sql-server-linux-configure-ssis.md)
-   [Linux の SSIS の制限事項と既知の問題](sql-server-linux-ssis-known-issues.md)
-   [cron を利用して Linux で SQL Server Integration Services パッケージのスケジュールを設定する](sql-server-linux-schedule-ssis-packages.md)
