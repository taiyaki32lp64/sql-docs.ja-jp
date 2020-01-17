---
title: チュートリアル:SQL Server Integration Services Scale Out を設定する | Microsoft Docs
description: この記事では、SSIS Scale Out のセットアップと構成について説明します
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
author: HaoQian-MS
ms.author: haoqian
ms.openlocfilehash: d3b6ea9f53a54b7f02042b85781bc8fe24028a69
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67896133"
---
# <a name="walkthrough-set-up-integration-services-ssis-scale-out"></a>チュートリアル:Integration Services (SSIS) Scale Out を設定する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


以下のタスクを実行して、[!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] (SSIS) Scale Out をセットアップします。 

> [!TIP]
> Scale Out を 1 台のコンピューターにインストールする場合は、Scale Out Master 機能と Scale Out Worker 機能を同時にインストールします。 そうすると、Scale Out Master に接続するためのエンドポイントが自動的に生成されます。 

* [Scale Out Master をインストールする](#InstallMaster)

* [Scale Out Worker をインストールする](#InstallWorker)

* [Scale Out Worker クライアント証明書をインストールする](#InstallCert)

* [ファイアウォールのポートを開く](#Firewall)

* [SQL Server Scale Out Master および Worker サービスを開始する](#Start)

* [Scale Out Master を有効にする](#EnableMaster)

* [SQL Server 認証モードを有効にする](#EnableAuth)

* [Scale Out Worker を有効にする](#EnableWorker)

## <a name="InstallMaster"></a> Scale Out Master をインストールする

Scale Out Master をセットアップするには、[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] をセットアップするときに、データベース エンジン サービス、[!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)]、および SSIS の Scale Out Master 機能をインストールする必要があります。 

データベース エンジンと [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] のセットアップの方法については、「[SQL Server データベース エンジンのインストール](../../database-engine/install-windows/install-sql-server-database-engine.md)」および「[Integration Services のインストール](../install-windows/install-integration-services.md)」をご覧ください。

> [!NOTE]
> Scale Out ログの既定の SQL Server 認証アカウントを使用するには、データベース エンジンのインストール時に **[データベース エンジンの構成]** ページの [認証モード] で [混合モード] を選択します。 詳細については、「[Scale Out ログのアカウントの変更](change-logdb-account.md)」を参照してください。

Scale Out Master 機能をインストールするには、[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] インストール ウィザードまたはコマンド プロンプトを使用します。

### <a name="install-scale-out-master-with-the-sql-server-installation-wizard"></a>SQL Server インストール ウィザードによる Scale Out Master のインストール
1.  **[機能の選択]** ページで、[[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]] の下に一覧表示される **[Scale Out Master]** を選択します。   
  
    ![Master 機能の選択](media/feature-select-master.PNG)
  
2.  **[サーバーの構成]** ページで、 **[SQL Server Integration Services Scale Out Master service]** (SQL Server Integration Services Scale Out Master サービス) を実行するアカウントを選び、 **[スタートアップの種類]** を選びます。  
    ![サーバーの構成](media/server-config.PNG)

3.  **[Integration Services Scale Out Master Configuration]** (Integration Services Scale Out Master の構成) ページで、Scale Out Master が Scale Out Worker との通信に使うポート番号を指定します。 既定のポート番号は 8391 です。  

    ![マスターの構成](media/master-config.PNG "マスターの構成")

4.  次のいずれかを行って、Scale Out Master と Scale Out Worker の間の通信の保護に使用する SSL 証明書を指定します。
    * **[新しい SSL 証明書の作成]** をクリックして、セットアップ プロセスで既定の自己署名 SSL 証明書を作成します。  既定の証明書は、ローカル コンピューターの信頼されたルート証明機関にインストールされます。 この証明書で CN を指定できます。 マスター エンドポイントのホスト名は、CN に含める必要があります。 既定では、マスター ノードのコンピューター名と IP が含まれます。
    * **[既存の SSL 証明書を使用する]** をクリックしてから **[参照]** をクリックして証明書を選択し、ローカル コンピューターで既存の SSL 証明書を選択します。 証明書のサムプリントがテキスト ボックスに表示されます。 **[Browse]** (参照) をクリックすると、ローカル コンピューターの信頼されたルート証明機関に格納されている証明書が表示されます。 選択する証明書はここに格納されている必要があります。       

    ![マスターの構成 2](media/master-config-2.PNG "マスターの構成 2")
  
5.  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] インストール ウィザードを最後まで実行します。

### <a name="install-scale-out-master-from-the-command-prompt"></a>コマンド プロンプトからの Scale Out Master のインストール

「 [コマンド プロンプトからの SQL Server のインストール](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)」の手順に従います。 次の手順を実行して、Scale Out Master のパラメーターを設定します。
 
1.  パラメーター `/FEATURES` に `IS_Master` を追加します。

2.  次のパラメーターとその値を指定することによって、Scale Out Master を構成します。
    -   `/ISMASTERSVCACCOUNT`
    -   `/ISMASTERSVCPASSWORD`
    -   `/ISMASTERSVCSTARTUPTYPE`
    -   `/ISMASTERSVCPORT`
    -   `/ISMasterSVCSSLCertCN` (省略可)
    -   `/ISMASTERSVCTHUMBPRINT` (省略可)

    > [!NOTE]
    > Scale Out Master が Microsoft SQL Server データベース エンジンと共にインストールされず、そのデータベース エンジン インスタンスが名前付きインスタンスである場合は、インストール後に Scale Out Master サービス構成ファイルで `SqlServerName` を構成する必要があります。 詳細については、[Scale Out Master](integration-services-ssis-scale-out-master.md) に関するページを参照してください。

## <a name="InstallWorker"></a> Scale Out Worker をインストールする
 
Scale Out Worker をセットアップするには、[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] のセットアップで [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] とその Scale Out Worker 機能をインストールする必要があります。

Scale Out Worker 機能をインストールするには、[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] インストール ウィザードまたはコマンド プロンプトを使用します。

### <a name="install-scale-out-worker-with-the-sql-server-installation-wizard"></a>SQL Server インストール ウィザードによる Scale Out Worker のインストール

1.  **[機能の選択]** ページで、[[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]] の下に一覧表示される **[Scale Out Worker]** を選択します。

    ![Worker 機能の選択](media/feature-select-worker.PNG)

2.  **[サーバーの構成]** ページで、 **[SQL Server Integration Services Scale Out Worker service]** (SQL Server Integration Services Scale Out Worker サービス) を実行するアカウントを選び、 **[スタートアップの種類]** を選びます。

    ![サーバーの構成 2](media/server-config-2.PNG "サーバーの構成 2")

3.  **[Integration Services Scale Out Worker Configuration]** (Integration Services Scale Out Worker の構成) ページで、Scale Out Master に接続するエンドポイントを指定します。 

    - **1 台のコンピューター**環境では、Scale Out Master と Scale Out Worker を同時にインストールすると、エンドポイントが自動的に生成されます。 

    - **複数コンピューター**環境では、エンドポイントは、Scale Out Master がインストールされているコンピューターの名前または IP と、Scale Out Master のインストール時に指定したポート番号で構成されます。
   
    ![ワーカーの構成 1](media/worker-config.PNG "ワーカーの構成 1")    

    > [!NOTE]
    > ここで Worker 構成を省略し、インストール後に [Scale Out Manager](integration-services-ssis-scale-out-manager.md) を使用して Scale Out Worker を Scale Out Master に関連付けることができます。

4. **複数コンピューター**環境の場合は、Scale Out Master の検証に使用されるクライアント SSL 証明書を指定します。 **1 台のコンピューター**環境では、クライアント SSL 証明書を指定する必要がありません。 
  
    **[Browse]** (参照) をクリックして、証明書ファイル (*.cer) を指定します。 既定の SSL 証明書を使用するには、Scale Out Master がインストールされているコンピューター上の `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn` に置かれている `SSISScaleOutMaster.cer` ファイルを選択します。   

    ![ワーカーの構成 2](media/worker-config-2.PNG "ワーカーの構成 2")

    > [!NOTE]
    > Scale Out Master で使用される SSL 証明書が自己署名されている場合は、Scale Out Worker のコンピューターに対応するクライアント SSL 証明書をインストールする必要があります。 **[Integration Services スケール アウト ワーカーの構成]** ページでクライアント SSL 証明書のファイル パスを指定した場合、証明書は自動的にインストールされます。それ以外の場合は、後で証明書を手動でインストールする必要があります。 
     
5. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] インストール ウィザードを最後まで実行します。

### <a name="install-scale-out-worker-from-the-command-prompt"></a>コマンド プロンプトからの Scale Out Worker のインストール

「 [コマンド プロンプトからの SQL Server のインストール](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)」の手順に従います。 次の手順を実行して、Scale Out Worker のパラメーターを設定します。

1.  パラメーター `/FEATURES` に IS_Worker を追加します。

2. 次のパラメーターとその値を指定することによって、Scale Out Worker を構成します。
    -   `/ISWORKERSVCACCOUNT`
    -   `/ISWORKERSVCPASSWORD`
    -   `/ISWORKERSVCSTARTUPTYPE`
    -   `/ISWORKERSVCMASTER` (省略可)
    -   `/ISWORKERSVCCERT` (省略可)
 
## <a name="InstallCert"></a> Scale Out Worker クライアント証明書をインストールする

Scale Out Worker のインストール時に、ワーカー証明書が自動的に作成され、コンピューターにインストールされます。 また、対応するクライアント証明書 SSISScaleOutWorker.cer が `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn` にインストールされます。 Scale Out Master で Scale Out Worker を認証するには、このクライアント証明書を Scale Out Master のローカル コンピューターのルート ストアに追加する必要があります。
  
ルート ストアにクライアント証明書を追加するには、.cer ファイルをダブルクリックし、[証明書] ダイアログ ボックスで **[証明書のインストール]** をクリックします。 **証明書のインポート ウィザード**が開きます。  

## <a name="Firewall"></a> ファイアウォールのポートを開く

Scale Out Master コンピューターの Windows ファイアウォールで、Scale Out Master のインストール時に指定したポートと、SQL Server のポート (既定では 1433) を開きます。

> [!Note]
> ファイアウォールのポートを開いた後に、Scale Out Worker サービスを再開する必要もあります。
    
## <a name="Start"></a> SQL Server Scale Out Master および Worker サービスを開始する

インストール時にサービスのスタートアップの種類を **[自動]** に設定していない場合は、次のサービスを開始してください。

-   SQL Server Integration Services Scale Out Master 14.0 (SSISScaleOutMaster140)

-   SQL Server Integration Services Scale Out Worker 14.0 (SSISScaleOutWorker140)

## <a name="EnableMaster"></a> Scale Out Master を有効にする

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../../includes/ssmanstudio-md.md)] で SSISDB カタログを作成するときに、 **[カタログの作成]** ダイアログ ボックスで **[SSIS スケール アウト マスターとしてこのサーバーを有効にする]** をクリックします。

カタログの作成後は、[[Scale Out Manager]](integration-services-ssis-scale-out-manager.md) を使用して Scale Out Master を有効にすることができます。

## <a name="EnableAuth"></a> SQL Server 認証モードを有効にする
データベース エンジンをインストールするときに [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 認証を有効にしなかった場合は、SSISDB カタログをホストする [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] インスタンスで SQL Server 認証モードを有効にします。 

SQL Server 認証を無効にすると、パッケージの実行はブロックされません。 ただし、実行ログを SSISDB データベースに書き込むことはできません。

## <a name="EnableWorker"></a> Scale Out Worker を有効にする

Scale Out Worker は [Scale Out Manager](integration-services-ssis-scale-out-manager.md) (グラフィカル ユーザー インターフェイスを利用可能) またはストアド プロシージャを使用して有効にすることができます。

ストアド プロシージャを使用して Scale Out Worker を有効にするには、パラメーターとして **WorkerAgentId** を指定して `[catalog].[enable_worker_agent]` ストアド プロシージャを実行します。 

**WorkerAgentId** の値は、Scale Out Worker を Scale Out Master に登録した後で SSISDB の `[catalog].[worker_agents]` ビューから取得します。 Scale Out Master サービスおよび Scale Out Worker サービスを開始した後、登録には数分かかります。

#### <a name="example"></a>例
次の例では、`computerA` で Scale Out Worker を有効にします。

```sql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName  --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    computerA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```

## <a name="next-steps"></a>次の手順
-   [Integration Services (SSIS) Scale Out でパッケージを実行する](run-packages-in-integration-services-ssis-scale-out.md)
