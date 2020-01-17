---
title: SQL Server on Linux の使用状況と診断データの収集を構成する
description: Linux 上で SQL Server の顧客の使用状況と診断データがどのように収集および構成されるかについて説明します。
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: d7fc5a14a9da000b69db804a5439fb62985f59b8
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558560"
---
# <a name="configure-usage--diagnostic-data-collection-for-sql-server-on-linux"></a>SQL Server on Linux の使用状況と診断データの収集を構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Microsoft SQL Server は既定で、お客様のアプリケーションの使用状態に関する情報を収集します。 具体的には、SQL Server はインストール エクスペリエンス、利用状況、およびパフォーマンスに関する情報を収集します。 この情報は、Microsoft が製品の向上を図り、お客様のニーズをさらに満たすのに役立ちます。 たとえば Microsoft では、お客様が受け取るエラー コードの種類に関する情報を収集して、関連するバグの修正、SQL Server の使用方法に関するドキュメントの改善、より良いサービスのために製品に機能を追加すべきかどうかの判断を行います。

このドキュメントでは、収集される情報の種類と、収集した情報を Microsoft に送信するように Microsoft SQL Server on Linux を構成する方法について詳しく説明します。 SQL Server 2017 にはプライバシーに関する声明が含まれています。この声明では、ユーザーから収集される情報と収集されない情報について説明します。 詳しくは、[プライバシーに関する声明](https://go.microsoft.com/fwlink/?LinkID=868444)をご覧ください。

具体的には、Microsoft はこのメカニズムでは次の種類の情報は送信しません。

- ユーザー テーブル内からのすべての値
- すべてのログオン資格情報またはその他の認証情報
- 個人を特定できる情報 (PII)

SQL Server 2017 は、インストール エクスペリエンスに関する情報をセットアップ時点から常に収集および送信して、お客様側で発生しているインストールの問題をすばやく発見し修正できるようにします。 SQL Server 2017 は、**mssql-conf** によって、Microsoft に (サーバー インスタンスごとに) 情報を送信しないように構成できます。 mssql-conf は、Red Hat Enterprise Linux、SUSE Linux Enterprise Server、Ubuntu 用に SQL Server 2017 と共にインストールされる構成スクリプトです。

> [!NOTE]
> Microsoft への情報送信を無効にできるのは、有料版の SQL Server のみです。

## <a name="disable-usage-and-diagnostic-data-collection"></a>使用状況と診断データの収集を無効にする

このオプションを使用すると、SQL Server によって使用状況と診断データの収集が Microsoft に送信されるかどうかを変更できます。 既定では、この値は true に設定されます。 値を変更するには、次のコマンドを実行します。

> [!IMPORTANT]
> SQL Server、Express、Developer の無償エディションに関する使用状況と診断データの収集をオフにすることはできません。

### <a name="on-red-hat-suse-and-ubuntu"></a>Red Hat、SUSE、Ubuntu の場合

1. **telemetry.customerfeedback** の **set** コマンドを使用して、mssql-conf スクリプトを root として実行します。 次の例では、**false** を指定することによって、使用状況と診断データの収集をオフにします。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. SQL Server サービスを再起動します。

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>Docker の場合
Docker 上で使用状況と診断データの収集を無効にするには、Docker によって[データが保持される](sql-server-linux-configure-docker.md)必要があります。 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. `[telemetry]` および `customerfeedback = false` という行を含む `mssql.conf` ファイルをホスト ディレクトリに追加します。
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. コンテナー イメージを実行します

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. `[telemetry]` および `customerfeedback = false` という行を含む `mssql.conf` ファイルをホスト ディレクトリに追加します。

   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. コンテナー イメージを実行します

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

::: moniker-end

## <a name="local-audit-for-sql-server-on-linux-usage-and-diagnostic-data-collection"></a>SQL Server on Linux の使用状況と診断データの収集の Local Audit

Microsoft SQL Server 2017 は、お客様のコンピューターまたはデバイスに関する情報 (以下「標準的なコンピューター情報」といいます) を収集してマイクロソフトに送信するインターネット対応の機能を備えています。 SQL Server の使用状況と診断データの収集の Local Audit コンポーネントでは、サービスによって収集されたデータを指定されたフォルダーに書き込むことができます。このデータは、Microsoft に送信されるデータ (ログ) です。 Local Audit の目的は、Microsoft がこの機能で収集するすべてのデータをユーザーがコンプライアンス、法規制、またはプライバシーの検証目的で確認できるようにすることです。

SQL Server on Linux では、Local Audit は SQL Server Database Engine のインスタンス レベルで構成可能です。 その他の SQL Server コンポーネントおよび SQL Server ツールには、使用状況と診断データの収集のための Local Audit 機能がありません。

### <a name="enable-local-audit"></a>Local Audit を有効にする

このオプションを使用すると、Local Audit を有効にし、Local Audit ログが作成されるディレクトリを設定できます。

1. 新しい Local Audit ログのターゲット ディレクトリを作成します。 次の例では、新しい **/tmp/audit** ディレクトリを作成します。

   ```bash
   sudo mkdir /tmp/audit
   ```

2. ディレクトリの所有者とグループを **mssql** ユーザーに変更します。

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

3. **telemetry.userrequestedlocalauditdirectory** の **set** コマンドを使用して、mssql-conf スクリプトを root として実行します。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

4. SQL Server サービスを再起動します。

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>Docker の場合
Docker 上で Local Audit を有効にするには、Docker で[データを保持](sql-server-linux-configure-docker.md)する必要があります。 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 新しい Local Audit ログのターゲット ディレクトリは、コンテナーに格納されます。 マシン上のホスト ディレクトリに新しい Local Audit ログのターゲット ディレクトリを作成します。 次の例では、新しい **/audit** ディレクトリを作成します。

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. `[telemetry]` および `userrequestedlocalauditdirectory = <host directory>/audit` という行を含む `mssql.conf` ファイルをホスト ディレクトリに追加します。
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```

1. コンテナー イメージを実行します

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. 新しい Local Audit ログのターゲット ディレクトリは、コンテナーに格納されます。 マシン上のホスト ディレクトリに新しい Local Audit ログのターゲット ディレクトリを作成します。 次の例では、新しい **/audit** ディレクトリを作成します。

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. `[telemetry]` および `userrequestedlocalauditdirectory = <host directory>/audit` という行を含む `mssql.conf` ファイルをホスト ディレクトリに追加します。
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```

1. コンテナー イメージを実行します

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

::: moniker-end

## <a name="next-steps"></a>次のステップ

Linux 上の SQL Server の詳細については、[Linux 上の SQL Server の概要](sql-server-linux-overview.md)に関する記事をご覧ください。
