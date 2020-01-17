---
title: ssis-conf を使用して Linux で SSIS を構成する
description: この記事では、ssis-conf ユーティリティを使用して Linux で SQL Server Integration Services (SSIS) を構成する方法について説明します。
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 51dc2ba27e346dea75f1bd347491d4932695fd43
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077532"
---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>ssis-conf を使用して Linux で SQL Server Integration Services を構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Red Hat Enterprise Linux および Ubuntu 用の SQL Server Integration Services (SSIS) をインストールするときは、`ssis-conf` 構成スクリプトを実行します。 SSIS のインストールについて詳しくは、「[SQL Server Integration Services (SSIS) を Linux にインストールする](sql-server-linux-setup-ssis.md)」をご覧ください。

`ssis-conf` ユーティリティを使用して、次のプロパティを構成することもできます。

| コマンド | [説明] |
|-------------|---------------------------------------------------------------------|
| set-edition | SQL Server のエディションを設定します。                                       |
| telemetry   | SQL Server Integration Services のテレメトリ サービスを有効または無効にします。 |
| セットアップ       | Microsoft SQL Server Integration Services を初期化して設定します。      |
|||

## <a name="run-ssis-conf"></a>ssis-conf を実行する

この記事の例では、完全なパス `/opt/ssis/bin/ssis-conf` を指定して `ssis-conf` を実行します。 その場所に異動してから `ssis-conf` を実行する場合は、このユーティリティを現在のディレクトリのコンテキストで実行できます (`./ssis-conf`)。

この記事で説明されているコマンドは必ずルート特権を付けて使用してください。 たとえば、`/opt/ssis/bin/ssis-conf setup` ではなく、`sudo /opt/ssis/bin/ssis-conf setup` を実行します。

希望の言語のプロンプトでこれらのコマンドを実行するには、ロケールを指定できます。 たとえば、中国語のプロンプトを受け取るには、コマンド `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup` を実行します。

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>set-edition を使用して SQL Server Integration Services のエディションを設定する

SSIS のエディションは SQL Server のエディションに合わせられます。

コマンド `$ sudo /opt/ssis/bin/ssis-conf set-edition` を入力します。

コマンドを入力すると、次のプロンプトが表示されます。

```
Choose an edition of SQL Server:

1) Evaluation (free, no production use rights, 180-day limit)

2) Developer (free, no production use rights)

3) Express (free)

4) Web (PAID)

5) Standard (PAID)

6) Enterprise (PAID)

7) Enterprise Core (PAID)

8) I bought a license through a retail sales channel and have a product key to enter.

Details about editions can be found at https://go.microsoft.com/fwlink/?LinkId=852748&clcid=0x409.

Use of PAID editions of this software requires separate licensing through a Microsoft Volume Licensing program.

By choosing a PAID edition, you are verifying that you have the appropriate number of licenses in place to install and run this software.

Enter your edition (1-8):
```

1 から 7 までの値を入力すると、無償版または有償版がシステムによって構成されます。 8 と入力すると、購入したプロダクト キーの入力を求められます。

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>telemetry を使用してカスタマー フィードバックを構成する

`telemetry` コマンドは、SSIS が Microsoft にフィードバックを送信するかどうかを決定します。

無償版 (Express、Developer、および Evaluation Edition) の場合、テレメトリ サービスは常に有効になります。 無償版を使用する場合、`telemetry` コマンドを使用してテレメトリを無効にすることはできません。

コマンド `$ sudo /opt/ssis/bin/ssis-conf telemetry` を入力します。

有償版の場合、コマンドを入力すると、次のプロンプトが表示されます。

```
Send feature usage data to Microsoft. Feature usage data includes information about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

**Yes** を選択すると、テレメトリ サービスが有効になり、実行が開始します。 サービスは起動のたびに自動的に開始します。 **No** を選択すると、テレメトリ サービスが停止し、無効になります。

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>setup を使用して Microsoft SQL Server Integration Services を初期化および設定する

SSIS をインストールするたびに `setup` コマンドを使用します。

コマンド `sudo /opt/ssis/bin/ssis-conf setup` を入力します。

ユーティリティによって、次の項目の値を確認または指定するように求められます。
-   製品ライセンス
-   使用許諾契約
-   テレメトリ サービス
-   Integration Services で使用される言語

希望の言語のプロンプトで `setup` コマンドを実行するには、ロケールを指定できます。 たとえば、中国語のプロンプトを受け取るには、コマンド `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup` を実行します。

## <a name="ssisconf-format"></a>ssis.conf の形式

次の `/var/opt/ssis/ssis.conf` ファイルで各設定の例を示します。

SQL Server では、`mssql.conf` ファイルの値を変更することによってシステム設定を変更できます。 SSIS では、`ssis.conf` ファイルの値を変更してシステム設定を変更 "*できません*"。 `ssis.conf` ファイルには、セットアップの結果のみが表示されます。 SSIS の設定を変更する場合は、`ssis.conf` ファイルを削除し、`setup` コマンドを再度実行します。

次に、サンプルの `ssis.conf` ファイルを示します。 各フィールドが 1 つのセットアップ手順の結果に対応しています。

```
[LICENSE]
                       
registered = Y        
                       
pid = enterprisecore  
                       
[EULA]
                       
accepteula = Y        
                       
[TELEMETRY]
                       
enabled = Y           
                       
[language]
                       
lcid = 2052
```

## <a name="related-content-about-ssis-on-linux"></a>Linux 上の SSIS の関連コンテンツ
-   [SSIS で Linux 上のデータの抽出、変換、読み込みを行う](sql-server-linux-migrate-ssis.md)
-   [Linux に SQL Server Integration Services (SSIS) をインストールする](sql-server-linux-setup-ssis.md)
-   [Linux の SSIS の制限事項と既知の問題](sql-server-linux-ssis-known-issues.md)
-   [cron を利用して Linux で SQL Server Integration Services パッケージのスケジュールを設定する](sql-server-linux-schedule-ssis-packages.md)
