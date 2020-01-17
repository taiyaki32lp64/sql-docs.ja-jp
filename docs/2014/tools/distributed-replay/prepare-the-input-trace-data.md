---
title: 入力トレース データの準備 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: c14fd3d2-5770-47c2-a851-cc13ddbc9bf5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7af5d166ec3bc059bc2628512564d92fd4cc6cad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149995"
---
# <a name="prepare-the-input-trace-data"></a>入力トレース データの準備
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Distributed Replay 機能を使用して分散再生を開始する前に、分散再生管理ツールから前処理段階を開始することで、入力トレース データを準備する必要があります。 前処理段階で、Distributed Replay Controller がトレース データを処理し、中間ファイルを生成します。  
  
 ![分散再生の前処理段階](../../database-engine/media/preprocess.gif "分散再生の前処理段階")  
  
 前処理段階の詳細については、「 [SQL Server Distributed Replay](sql-server-distributed-replay.md)」を参照してください。  
  
> [!NOTE]  
>  入力トレース データは、Distributed Replay と互換性があるバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でキャプチャする必要があります。 また、入力トレース データは、トレース データを再生するターゲット サーバーと互換性がある必要があります。 バージョンの要件の詳細については、「 [Distributed Replay Requirements](distributed-replay-requirements.md)」を参照してください。  
  
### <a name="to-prepare-the-input-trace-data"></a>入力トレース データを準備するには  
  
1.  **(省略可能)変更の構成設定を前処理**:変更する必要がありますシステム セッションのフィルター処理する最大のアイドル時間を構成するかなど、前処理構成設定を変更する場合、`<PreprocessModifiers>`要素、XML ベースの前処理構成ファイルの`DReplay.exe.preprocess.config`します。 前処理構成ファイルを変更する場合は、元のファイルではなく、コピーを変更することをお勧めします。 設定を変更するには、次の手順に従います。  
  
    1.  既定の前処理構成ファイル `DReplay.exe.preprocess.config`のコピーを作成し、新しいファイルの名前を変更します。 既定の前処理構成ファイルは管理ツールのインストール フォルダーにあります。  
  
    2.  新しい構成ファイル内の前処理構成設定を変更します。  
  
    3.  前処理段階 (次の手順) を開始するときに、 *前処理* オプションの **config_file** パラメーターを使用して、変更した構成ファイルの場所を指定します。  
  
     前処理構成ファイルの詳細については、「 [Distributed Replay の構成](configure-distributed-replay.md)」を参照してください。  
  
2.  **前処理段階を開始**:入力トレース データを準備するには、使用して、管理ツールを実行する必要があります、**前処理**オプション。 詳細については、「[前処理オプション &#40;Distributed Replay 管理ツール&#41;](preprocess-option-distributed-replay-administration-tool.md)」を参照してください。  
  
    1.  Windows のコマンド プロンプト ユーティリティ (`CMD.exe`) を開き、Distributed Replay 管理ツール (`DReplay.exe`) のインストール場所に移動します。  
  
    2.  (省略可能) 管理ツールを実行するコンピューターとは別のコンピューター上でコントローラー サービスが実行されている場合、 *controller* パラメーター **-m**を使用して、コントローラーを指定します。  
  
    3.  *input_trace_file* パラメーター **-i**を使用して、入力トレース ファイルの場所と名前を指定します。  
  
    4.  *controller_working_directory* パラメーター **-d**を使用して、コントローラーで中間ファイルを保存する場所を指定します。  
  
    5.  (省略可能) *config_file* パラメーター **-c**を使用して、前処理構成ファイルの場所を指定します。 既定の前処理構成ファイルのコピーを変更した場合は、このパラメーターを使用して、新しい構成ファイルを指定します。  
  
    6.  (省略可能) *status_interval* パラメーター **-f**を使用して、30 秒以外の周期で状態メッセージを管理ツールで表示させるかどうかを指定します。  
  
     たとえば、 `c:\trace1.trc`にあるトレース ファイルに対して、コントローラー サービスと同じコンピューターで前処理段階を開始し、コントローラー作業ディレクトリが `c:\WorkingDir` にあり、既定の 30 秒で状態メッセージが表示される場合、 `dreplay preprocess -i c:\trace1.trc -d c:\WorkingDir`  
  
3.  前処理段階が完了したら、コントローラー作業ディレクトリに中間ファイルが格納されます。 イベント再生段階を開始するには、 **再生** オプションを使用して、管理ツールを実行する必要があります。 詳細については、「 [トレース データの再生](replay-trace-data.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)   
 [分散再生の要件](distributed-replay-requirements.md)   
 [管理ツール コマンド ライン オプション &#40;Distributed Replay Utility&#41;](administration-tool-command-line-options-distributed-replay-utility.md)   
 [Distributed Replay の構成](configure-distributed-replay.md)  
  
  
