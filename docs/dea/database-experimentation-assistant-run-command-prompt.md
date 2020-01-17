---
title: コマンドプロンプトで Database Experimentation Assistant を実行する
description: コマンドプロンプトで Database Experimentation Assistant を実行する
ms.custom: seo-lt-2019
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: f5a0f7441dd17aec2587c772a678a3681fd3b423
ms.sourcegitcommit: 9e026cfd9f2300f106af929d88a9b43301f5edc2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74317720"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>コマンドプロンプトで Database Experimentation Assistant を実行する

この記事では、Database Experimentation Assistant (DEA) でトレースをキャプチャし、その結果をすべてコマンドプロンプトから分析する方法について説明します。

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>DEA コマンドを使用して、新しいワークロードキャプチャを開始します。

新しいワークロードのキャプチャを開始するには、コマンドプロンプトで次のコマンドを実行します。

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**よう**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload-capture"></a>ワークロードのキャプチャを再生する

1. 分散再生コントローラーコンピューターにログインします。
2. DEA コマンドを使用してキャプチャしたワークロードトレースを IRF ファイルに変換するには、コマンドプロンプトで次のコマンドを実行します。

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3. StartReplayCaptureTrace を使用して SQL Server を実行しているターゲットコンピューターでトレースキャプチャを開始します。

    」を参照します。  SQL Server Management Studio (SSMS) で、<Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.sql. を開きます。

    b.  を`Set @durationInMins=0`実行して、指定した時間が経過するとトレースキャプチャが自動的に停止しないようにします。

    c.  トレースファイルあたりの最大ファイルサイズを設定するに`Set @maxfilesize`は、を実行します。 推奨サイズは 200 (MB) です。

    d.  を`@Tracefile`編集して、トレースファイルの一意の名前を設定します。

    e.  ワーク`@dbname`ロードを特定のデータベースでのみキャプチャする必要がある場合は、データベース名を指定して編集します。 既定では、サーバー全体のワークロードがキャプチャされます。

4. ターゲット SQL Server インスタンスに対して IRF ファイルを再生するには、コマンドプロンプトで次のコマンドを実行します。

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`

    」を参照します。  ステータスを監視するには、コマンドプロンプトでを`DReplay status -f 1`実行します。

    b.  再生を停止するには (たとえば、パス% が予想より低い場合)、コマンドプロンプトでを実行`DReplay cancel`します。

5. ターゲット SQL Server インスタンスのトレースキャプチャを停止します。
6. SSMS でを開き`<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`ます。
7. SQL Server `@Tracefile`を実行しているターゲットコンピューター上のトレースファイルのパスと一致するように、を編集します。
8. SQL Server を実行しているターゲットコンピューターに対してスクリプトを実行します。

## <a name="analyze-traces-using-the-dea-command"></a>DEA コマンドを使用してトレースを分析する

新しいトレース分析を開始するには、コマンドプロンプトで次のコマンドを実行します。

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**よう**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="see-also"></a>参照

- DEA の使用方法の詳細については、「 [Database Experimentation Assistant の概要](database-experimentation-assistant-overview.md)」を参照してください。
