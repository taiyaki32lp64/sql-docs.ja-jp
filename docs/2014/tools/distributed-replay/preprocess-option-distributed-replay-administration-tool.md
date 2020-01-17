---
title: 前処理オプション (分散再生管理ツール) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 9b5012fd-233e-4a25-a2e1-585c63b70502
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6f5f4492dc18a93ab1fea9d34287eb90703bc3d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149906"
---
# <a name="preprocess-option-distributed-replay-administration-tool"></a>前処理オプション (Distributed Replay 管理ツール)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 管理ツール、 `DReplay.exe`、分散再生コント ローラーとの通信に使用できるコマンド ライン ツールです。 このトピックでは、 **preprocess** コマンド ライン オプションとそれに対応する構文について説明します。  
  
 **preprocess** オプションは、前処理段階を開始します。 この段階では、ターゲット サーバーに対して、コントローラーが入力トレース データの再生の準備を行います。  
  
 ![トピック リンク アイコン](../../database-engine/media/topic-link.gif "トピック リンク アイコン") 管理ツールの構文で使用される構文表記規則の詳細については、「[Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
      dreplay preprocess [-mcontroller] -iinput_trace_file  
    -dcontroller_working_dir [-cconfig_file] [-fstatus_interval]  
```  
  
#### <a name="parameters"></a>パラメーター  
 **-m** *controller*  
 コントローラーのコンピューターの名前を指定します。 "`localhost`" または "`.`" を使用してローカル コンピューターを参照できます。  
  
 **-m** パラメーターが指定されていない場合、ローカル コンピューターが使用されます。  
  
 **-i** *input_trace_file*  
 `D:\Mytrace.trc`などの形式で、コントローラー上の入力トレース ファイルの完全なパスを指定します。 **-i** パラメーターは必須です。  
  
 同じディレクトリにロールオーバー ファイルがある場合は、自動的に読み込まれて使用されます。 ファイルは、ファイル ロールオーバー名前付け規則に準拠する必要があります (例: `Mytrace.trc`、`Mytrace_1.trc`、`Mytrace_2.trc`、`Mytrace_3.trc`、... `Mytrace_n.trc`)。  
  
> [!NOTE]  
>  コントローラーとは別のコンピューターで管理ツールを使用している場合は、このパラメーターにローカル パスを使用できるように、コントローラーに入力トレース ファイルをコピーする必要があります。  
  
 **-d** *controller_working_dir*  
 中間ファイルが格納される、コントローラー上のディレクトリを指定します。 **-d** パラメーターは必須です。  
  
 これには次の要件があります。  
  
-   ディレクトリはコントローラー上に置く必要があります。  
  
-   ドライブ文字で始まる完全なパスを指定する必要があります (たとえば、 `c:\WorkingDir`)。  
  
-   パスはバックスラッシュ "`\`" で終了することはできません。  
  
-   UNC パスはサポートされません。  
  
 **-c** *config_file*  
 前処理構成ファイルのフル パスです。別の場所に保存されている前処理構成ファイルの場所を指定するために使用します。 このパラメーターは UNC パスにするか、または管理ツールを実行するコンピューター上にローカルに置くことができます。  
  
 **-c** パラメーターは、フィルターが必要ない場合または最大アイドル時間を変更しない場合は、必要ありません。  
  
 **-c** パラメーターが指定されない場合は、既定の前処理構成ファイル `DReplay.exe.preprocess.config`が使用されます。  
  
 **-f** *status_interval*  
 ステータス メッセージを表示する頻度 (秒単位) を指定します。  
  
 **-f** を指定しない場合は、既定の間隔は 30 秒です。  
  
## <a name="examples"></a>使用例  
 この例では、すべての既定の設定で前処理段階が開始されます。 値 `localhost` は、コントローラー サービスが管理ツールと同じコンピューターで実行されていることを示します。 *input_trace_file* パラメーターは、入力トレース データ `c:\mytrace.trc`の場所を指定します。 トレース ファイルのフィルターがないため、 **-c** パラメーターを指定する必要はありません。  
  
```  
dreplay preprocess -m localhost -i c:\mytrace.trc -d c:\WorkingDir  
```  
  
 この例では、前処理段階が開始され、変更した前処理構成ファイルが指定されます。 前の例とは異なり、 **-c** パラメーターを使用して、別の場所に格納されている変更された構成ファイルを指定しています。 以下に例を示します。  
  
```  
dreplay preprocess -m localhost -i c:\mytrace.trc -d c:\WorkingDir -c c:\DReplay.exe.preprocess.config  
```  
  
 変更された前処理構成ファイルでは、分散再生中にシステム セッションを除外するフィルター条件が追加されます。 `<PreprocessModifiers>` 要素を前処理構成ファイル `DReplay.exe.preprocess.config`で変更することで、フィルターが追加されます。  
  
 変更された構成ファイルの例を次に示します。  
  
```  
<?xml version='1.0'?>  
<Options>  
    <PreprocessModifiers>  
        <IncSystemSession>No</IncSystemSession>  
        <MaxIdleTime>-1</MaxIdleTime>  
    </PreprocessModifiers>  
</Options>  
```  
  
## <a name="permissions"></a>アクセス許可  
 対話ユーザー (ローカル ユーザーまたはドメイン ユーザー アカウント) として、管理ツールを実行する必要があります。 ローカル ユーザー アカウントを使用するには、管理ツールとコントローラーが同じコンピューター上で実行されている必要があります。  
  
 詳細については、「 [Distributed Replay Security](distributed-replay-security.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [入力トレース データの準備](prepare-the-input-trace-data.md)   
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)   
 [分散再生の構成](configure-distributed-replay.md)  
  
  
