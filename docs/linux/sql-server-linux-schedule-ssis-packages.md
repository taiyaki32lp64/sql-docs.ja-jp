---
title: cron を使用して Linux 上で SSIS パッケージのスケジュールを設定する
description: この記事では、cron を使用して Linux 上で SQL Server Integration Services (SSIS) パッケージのスケジュールを設定する方法について説明します。
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: ac7648287b4e4b609f4dd4f25b1b07a512065364
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68065161"
---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>cron を使用して Linux 上で SQL Server Integration Services パッケージの実行スケジュールを設定する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Windows 上で SQL Server Integration Services (SSIS) と SQL Server を実行するときは、SQL Server エージェントを使用して SSIS パッケージの実行を自動化できます。 ただし、Linux 上で SQL Server と SSIS を実行する場合、SQL Server エージェント ユーティリティを使用して Linux 上でジョブをスケジュールすることはできません。 代わりに、パッケージの実行を自動化するために Linux プラットフォームで広く使用されている cron サービスが使用されます。

この記事では、SSIS パッケージの実行を自動化する方法を示す例を紹介します。 これらの例は、Red Hat Enterprise で実行するように記述されています。 このコードは、Ubuntu などの他の Linux ディストリビューションでも同様です。

## <a name="prerequisites"></a>Prerequisites

cron サービスを使用してジョブを実行する前に、そのサービスがお使いのコンピューター上で実行されているかどうかを確認します。

cron サービスの状態を確認するには、`systemctl status crond.service` コマンドを使用します。

サービスがアクティブでない場合 (つまり、サービスが実行されていない場合) は、管理者に連絡して cron サービスを適切に設定して構成してください。

## <a name="create-jobs"></a>ジョブを作成する

cron ジョブは、指定された間隔で定期的に実行されるように構成できるタスクです。 ジョブは、通常、コンソールに直接入力するか、シェル スクリプトとして実行するコマンドと同じようにシンプルにすることができます。

管理と保守を容易にするために、わかりやすい名前を含むスクリプトにパッケージ実行コマンドを配置することをお勧めします。

パッケージを実行するためのシンプルなシェル スクリプトの例を次に示します。 それには 1 つのコマンドだけが含まれていますが、必要に応じてさらにコマンドを追加できます。

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>cron サービスを使用してジョブのスケジュールを設定する

ジョブを定義したら、cron サービスを使用して、ジョブが自動的に実行されるようにスケジュールできます。

cron で実行するジョブを追加するには、crontab ファイルにジョブを追加します。 ジョブを追加または更新する crontab ファイルをエディターで開くには、`crontab -e` コマンドを使用します。

前に記述したジョブを毎日午前 2 時 10 分に実行するようにスケジュールするには、次の行を crontab ファイルに追加します。

```
# run <SSIS package name> at 2:10 AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

crontab ファイルを保存し、エディターを終了します。

サンプル コマンドの形式を理解するには、次のセクションの情報を確認してください。
 
## <a name="format-of-a-crontab-file"></a>crontab ファイルの形式

次の図に、crontab ファイルに追加されるジョブ行の形式の説明を示します。

![crontab ファイル内のエントリの形式の説明](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

crontab ファイルの形式の詳細な説明を取得するには、`man 5 crontab` コマンドを使用します。

この記事の例を説明するのに役立つ出力例の一部を次に示します。

![crontab 形式の詳細な説明の一部](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

## <a name="related-content-about-ssis-on-linux"></a>SSIS on Linux の関連コンテンツ
-   [SSIS を使用して Linux 上でデータの抽出、変換、読み込みを行う](sql-server-linux-migrate-ssis.md)
-   [SQL Server Integration Services (SSIS) on Linux をインストールする](sql-server-linux-setup-ssis.md)
-   [ssis-conf を使用して SQL Server Integration Services on Linux を構成する](sql-server-linux-configure-ssis.md)
-   [SSIS on Linux の制限事項と既知の問題](sql-server-linux-ssis-known-issues.md)
