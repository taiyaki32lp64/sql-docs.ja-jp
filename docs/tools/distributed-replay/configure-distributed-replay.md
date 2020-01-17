---
title: 分散再生の構成 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: aee11dde-daad-439b-b594-9f4aeac94335
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 092b08697580d79f800dcc539ed90559262ff44f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023768"
---
# <a name="configure-distributed-replay"></a>Configure Distributed Replay
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Distributed Replay Controller、クライアント、および管理ツールのインストール場所に関する [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay の構成の詳細は、XML ファイルで指定されます。 このようなファイルには、次のファイルが含まれます。  
  
-   [コントローラー構成ファイル](#DReplayController)  
  
-   [クライアント構成ファイル](#DReplayClient)  
  
-   [前処理構成ファイル](#PreprocessConfig)  
  
-   [再生構成ファイル](#ReplayConfig)  
  
##  <a name="DReplayController"></a> コントローラー構成ファイル: DReplayController.config  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller サービスを開始すると、コントローラー構成ファイル `DReplayController.config`からログ記録レベルが読み込まれます。 このファイルは、Distributed Replay Controller サービスをインストールしたフォルダーにあります。  
  
 **\<コントローラーのインストール パス>\DReplayController.config**  
  
 コントローラー構成ファイルによって指定されるログ記録レベルには、次の内容が含まれます。  
  
|設定|XML 要素|[説明]|指定できる値|Required|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|ログ記録レベル|`<LoggingLevel>`|コントローラー サービスのログ記録レベルを指定します。|`INFORMATION` &#124; `WARNING` &#124; `CRITICAL`|不可。 既定値は `CRITICAL`です。|  
  
### <a name="example"></a>例  
 この例は、 `INFORMATION` および `WARNING` ログのエントリを非表示にするように変更されたコントローラー構成ファイルを示しています。  
  
```  
<?xml version='1.0'?>  
<Options>  
<LoggingLevel>CRITICAL</LoggingLevel>  
</Options>  
```  
  
##  <a name="DReplayClient"></a> クライアント構成ファイル: DReplayClient.config  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client サービスを開始すると、クライアント構成ファイル `DReplayClient.config`から構成設定が読み込まれます。 このファイルは、各クライアントの Distributed Replay Client サービスをインストールしたフォルダーにあります。  
  
 **\<クライアントのインストール パス>\DReplayClient.config**  
  
 クライアント構成ファイルによって指定される設定には、次の内容が含まれます。  
  
|設定|XML 要素|[説明]|指定できる値|Required|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|コントローラー|`<Controller>`|コントローラーのコンピューターの名前を指定します。 クライアントは、コントローラーにアクセスすることによって、Distributed Replay 環境での登録を試みます。|"`localhost`" または "`.`" を使用してローカル コンピューターを参照できます。|不可。 既定では、クライアントはローカル ("`.`") で実行しているコントローラー インスタンスの登録を試みます (存在する場合)。|  
|クライアントの作業ディレクトリ|`<WorkingDirectory>`|ディスパッチ ファイルが保存されるクライアント上のローカル パス。<br /><br /> このディレクトリ内のファイルは、次の再生時に上書きされます。|ドライブ文字で始まる完全なディレクトリ名。|不可。 値が指定されない場合は、ディスパッチ ファイルは既定のクライアント構成ファイルと同じ場所に保存されます。 値が指定されており、そのフォルダーがクライアントに存在しない場合は、クライアント サービスは開始されません。|  
|クライアントの結果ディレクトリ|`<ResultDirectory>`|クライアントの再生アクティビティによって生成される結果トレース ファイルが保存される、クライアント上のローカル パス。<br /><br /> このディレクトリ内のファイルは、次の再生時に上書きされます。|ドライブ文字で始まる完全なディレクトリ名。|不可。 値が指定されない場合は、結果トレース ファイルは既定のクライアント構成ファイルと同じ場所に保存されます。 値が指定されており、そのフォルダーがクライアントに存在しない場合は、クライアント サービスは開始されません。|  
|ログ記録レベル|`<LoggingLevel>`|クライアント サービスのログ記録レベル。|`INFORMATION` &#124; `WARNING` &#124; `CRITICAL`|不可。 既定値は `CRITICAL`です。|  
  
### <a name="example"></a>例  
 この例は、 `Controller1`という名前の別のコンピューターでコントローラー サービスが実行されるように指定したクライアント構成ファイルを示しています。 `WorkingDirectory` および `ResultDirectory` 要素は、フォルダー `c:\ClientWorkingDir` および `c:\ResultTraceDir`をそれぞれ使用するように構成されています。 ログ記録レベルは `INFORMATION` および `WARNING` ログ エントリを非表示にするように既定値から変更されています。  
  
```  
<?xml version='1.0'?>  
<Options>  
    <Controller>Controller1</Controller>  
    <WorkingDirectory>c:\ClientWorkingDir</WorkingDirectory>  
    <ResultDirectory>c:\ResultTraceDir</ResultDirectory>  
    <LoggingLevel>CRITICAL</LoggingLevel>  
</Options>  
```  
  
##  <a name="PreprocessConfig"></a> 前処理構成ファイル : DReplay.exe.preprocess.config  
 前処理段階を開始するために管理ツールを使用すると、管理ツールは前処理構成ファイル `DReplay.exe.preprocess.config` から前処理設定を読み込みます。  
  
 既定の構成ファイルまたは管理ツール **-c** パラメーターを使用して、変更された前処理構成ファイルの場所を指定します。 管理ツールの前処理オプションの使用の詳細については、「[前処理オプション &#40;Distributed Replay 管理ツール&#41;](../../tools/distributed-replay/preprocess-option-distributed-replay-administration-tool.md)」を参照してください。  
  
 既定の前処理構成ファイルは管理ツールのインストール フォルダーにあります。  
  
 **\<管理ツールのインストール パス>\DReplayAdmin\DReplay.exe.preprocess.config**  
  
 前処理構成の設定は、前処理構成ファイル内の `<PreprocessModifiers>` 要素の子である XML 要素で指定されています。 これらの設定は次のとおりです。  
  
|設定|XML 要素|[説明]|指定できる値|Required|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|システム セッション アクティビティを含む|`<IncSystemSession>`|キャプチャ中のシステム セッション アクティビティが再生中に含まれるかどうかを示します。|`Yes` &#124; `No`|不可。 既定値は `No`です。|  
|最大アイドル時間|`<MaxIdleTime>`|アイドル時間を絶対数 (単位は秒) で指定します。|>= -1 の整数です。<br /><br /> `-1` は、元のトレース ファイルの元の値から変更されていないことを示します。<br /><br /> `0` は、指定された時刻に何らかのアクティビティが行われていることを示します。|不可。 既定値は `-1`です。|  
  
### <a name="example"></a>例  
 既定の前処理構成ファイルは、次のとおりです。  
  
```  
<?xml version='1.0'?>  
<Options>  
    <PreprocessModifiers>  
        <IncSystemSession>No</IncSystemSession>  
        <MaxIdleTime>-1</MaxIdleTime>  
    </PreprocessModifiers>  
</Options>  
```  
  
##  <a name="ReplayConfig"></a> 再生構成ファイル : DReplay.exe.replay.config  
 イベント再生段階を開始するために管理ツールを使用すると、管理ツールは再生構成ファイル `DReplay.exe.replay.config`から再生設定を読み込みます。  
  
 既定の構成ファイルまたは管理ツール **-c** パラメーターを使用して、変更された再生構成ファイルの場所を指定します。 管理ツールの再生オプションの使用の詳細については、「[replay オプション &#40;Distributed Replay 管理ツール&#41;](../../tools/distributed-replay/replay-option-distributed-replay-administration-tool.md)」を参照してください。  
  
 既定の再生構成ファイルは管理ツールのインストール フォルダーにあります。  
  
 **\<管理ツールのインストール パス>\DReplayAdmin\DReplay.exe.replay.config**  
  
 再生構成の設定は、再生構成ファイルの `<ReplayOptions>` 要素および `<OutputOptions>` 要素の子である XML 要素で指定されています。  
  
### <a name="replayoptions-element"></a>\<ReplayOptions > 要素  
 再生構成ファイルの `<ReplayOptions>` 要素によって指定される設定には、次の内容が含まれます。  
  
|設定|XML 要素|[説明]|指定できる値|Required|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の対象インスタンス (テスト サーバー)|`<Server>`|接続先となる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサーバーとインスタンスの名前を指定します。|*server_name*[\\*instance_name*]<br /><br /> "`localhost`" または "`.`" を使用してローカル ホストを表すことはできません。|いいえ (管理ツールの **replay** オプションで、サーバー名が既に **-s**_target server_ パラメーターを使用して指定されている場合)。|  
|シーケンス モード|`<SequencingMode>`|イベント スケジュールに使用されるモードを指定します。|`synchronization` &#124; `stress`|不可。 既定値は `stress`です。|  
|ストレス スケールの粒度|`<StressScaleGranularity>`|ストレス モードで、Service Profile ID (SPID) のすべての接続をまとめて測定するのか (SPID)、個別に測定するのか (Connection) を指定します。|SPID &#124; Connection|可能。 既定値は `SPID`です。|  
|接続タイム スケール|`<ConnectTimeScale>`|ストレス モードで接続時間を測定するのに使用されます。|`1` ～ `100`の整数値です。|不可。 既定値は `100`です。|  
|待ち時間タイム スケール|`<ThinkTimeScale>`|ストレス モードで待ち時間を測定するのに使用されます。|`0` ～ `100`の整数値です。|不可。 既定値は `100`です。|  
|接続プールの使用|`<UseConnectionPooling>`|各 Distributed Replay Client で接続プールを有効にするかどうかを指定します。|Yes &#124; No|可能。 既定値は `Yes`です。|  
|ヘルス モニターの間隔|`<HealthmonInterval>`|ヘルス モニターを実行する頻度 (秒) を示します。<br /><br /> この値は、同期モードでのみ使用されます。|>= 1 の整数<br /><br /> (無効にする場合は`-1` )|不可。 既定値は `60` です。|  
|クエリのタイムアウト|`<QueryTimeout>`|クエリのタイムアウト時間を秒単位で指定します。 この値は、最初の行が返されるまで有効です。|>= 1 の整数<br /><br /> (無効にする場合は`-1` )|不可。 既定値は `3600`です。|  
|クライアントごとのスレッド|`<ThreadsPerClient>`|それぞれの再生クライアントで使用する再生スレッドの数を指定します。|`1` ～ `512`の整数値です。|不可。 指定されない場合、Distributed Replay は値として `255`を使用します。|  
  
### <a name="outputoptions-element"></a>\<OutputOptions > 要素  
 再生構成ファイルの `<OutputOptions>` 要素によって指定される設定には、次の内容が含まれます。  
  
|設定|XML 要素|[説明]|指定できる値|Required|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|行数の記録|`<RecordRowCount>`|それぞれの結果セットで行数を記録するかどうかを示します。|`Yes` &#124; `No`|不可。 既定値は `Yes`です。|  
|結果セットの記録|`<RecordResultSet>`|すべての結果セットの内容を記録するかどうかを示します。|`Yes` &#124; `No`|不可。 既定値は `No`です。|  
  
### <a name="example"></a>例  
 既定の再生構成ファイルは、次のとおりです。  
  
```  
<?xml version='1.0'?>  
<Options>  
    <ReplayOptions>  
        <Server></Server>  
        <SequencingMode>stress</SequencingMode>  
        <ConnectTimeScale></ConnectTimeScale>  
        <ThinkTimeScale></ThinkTimeScale>  
        <HealthmonInterval>60</HealthmonInterval>  
        <QueryTimeout>3600</QueryTimeout>  
        <ThreadsPerClient></ThreadsPerClient>  
    </ReplayOptions>  
    <OutputOptions>  
        <ResultTrace>  
            <RecordRowCount>Yes</RecordRowCount>  
            <RecordResultSet>No</RecordResultSet>  
        </ResultTrace>  
    </OutputOptions>  
</Options>  
```  

### <a name="possible-issue-when-running-with-synchronization-sequencing-mode"></a>同期シーケンスモードで実行するときに発生する可能性のある問題
 再生機能が "停止" と表示されたり、イベントの再生が非常に遅くなったりする症状が発生する可能性があります。 この現象は、再生中のトレースが、復元されたターゲットデータベースに存在しないデータやイベントに依存している場合に発生する可能性があります。 
 
 1つの例として、Service Broker の WAITFOR RECEIVE ステートメントなど、WAITFOR を使用するキャプチャされたワークロードがあります。 同期シーケンスモードを使用する場合、バッチは直列に再生されます。 データベースのバックアップ後、再生キャプチャトレースが開始される前にソースデータベースに対して挿入が行われた場合、再生中に実行された WAITFOR RECEIVE は WAITFOR の全期間を待機する必要があります。 WAITFOR RECEIVE が停滞した後に再生されるように設定されたイベント。 これにより、replay データベースターゲットに対する Batch Requests/sec パフォーマンスモニターカウンターが、WAITFOR が完了するまで0に削除される可能性があります。 
 
 同期モードを使用する必要があり、この動作を回避する必要がある場合は、次の操作を行う必要があります。
 
1.  再生ターゲットとして使用するデータベースを停止します。

2.  すべての保留中のアクティビティの完了を許可します。

3.  データベースをバックアップし、バックアップを完了できるようにします。

4.  分散再生トレースのキャプチャを開始し、通常のワークロードを再開します。 
 
 
## <a name="see-also"></a>参照  
 [管理ツール コマンド ライン オプション &#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [SQL Server Distributed Replay フォーラム](https://social.technet.microsoft.com/Forums/sl/sqldru/)   
 [分散再生を使用した SQL Server のロード テスト – パート 1](https://blogs.msdn.com/b/mspfe/archive/2012/11/14/using-distributed-replay-to-load-test-your-sql-server-part-2.aspx)   
 [分散再生を使用した SQL Server のロード テスト – パート 1](https://blogs.msdn.com/b/mspfe/archive/2012/11/08/using-distributed-replay-to-load-test-your-sql-server-part-1.aspx)  
  
  
