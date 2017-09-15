---
title: "サーバー ネットワーク プロトコルの有効化または無効化 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- network protocols [SQL Server], disabling
- remote connections [SQL Server], enabling using Configuration Manager
- protocols [SQL Server], enabling using Configuration Manager
- protocols [SQL Server], disabling using Configuration Manager
- disabling network protocols, Configuration Manager
- network protocols [SQL Server], enabling
- enabling network protocols, Configuration Manager
- surface area configuration [SQL Server], connection protocols
- connections [SQL Server], enabling remote using Configuration Manager
ms.assetid: ec5ccb69-61c9-4576-8843-014b976fd46e
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7bb0a9abeba4730bd2d5d4e57cd7b02b2b93b55c
ms.contentlocale: ja-jp
ms.lasthandoff: 08/02/2017

---
# サーバー ネットワーク プロトコルの有効化または無効化
  すべてのネットワーク プロトコルは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップによってインストールされますが、必ずしも有効になっているとは限りません。 このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーまたは PowerShell を使用してサーバー ネットワーク プロトコルを有効または無効にする方法について説明します。 変更を有効にするために [!INCLUDE[ssDE](../../includes/ssde-md.md)] を停止し、再起動する必要があります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] のセットアップ時に、ログインは BUILTIN\Users グループに追加されます。 これにより、コンピューターの認証されたすべてのユーザーが public ロールのメンバーとして [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] のインスタンスにアクセスできるようになります。 BUILTIN\Users ログインを安全に削除して、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] アクセスを、個別のログインを持つコンピューター ユーザーまたはログインを持つ他の Windows グループのメンバーに制限できます。  
  
> [!WARNING]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[msCoName](../../includes/msconame-md.md)] 向けの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ プロバイダーでは、SSL 3.0、TLS 1.0 がサポートされています。 オペレーティング システムの SChannel 層を変更して別のプロトコル (TLS 1.1、TLS 1.2 など) を適用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続に失敗する可能性があります。  
  
 **このトピックの内容**  
  
-   **サーバー ネットワーク プロトコルを有効または無効にするための方法:**  
  
     [SQL Server 構成マネージャー](#SSMSProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server 構成マネージャーの使用  
  
#### サーバー ネットワーク プロトコルを有効にするには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーのコンソール ペインで、 **[SQL Server ネットワークの構成]**を展開します。  
  
2.  コンソール ペインで、**[***\<インスタンス名> のプロトコル]* をクリックします。  
  
3.  詳細ペインで、変更するプロトコルを右クリックし、 **[有効化]** または **[無効化]**をクリックします。  
  
4.  コンソール ペインで、 **[SQL Server のサービス]**をクリックします。  
  
5.  詳細ペインで **[SQL Server (***\<インスタンス名>***)]** を右クリックします。次に、**[再起動]** をクリックして、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを停止し、再起動します。  
  
##  <a name="PowerShellProcedure"></a> SQL Server PowerShell の使用  
  
#### PowerShell を使用してサーバー ネットワーク プロトコルを有効にするには  
  
1.  管理者権限を使用してコマンド プロンプトを開きます。  
  
2.  タスク バーから Windows PowerShell を起動するか、[スタート] ボタンをクリックし、[すべてのプログラム]、[アクセサリ]、[Windows PowerShell]、[Windows PowerShell] の順にクリックします。  
  
3.  「 **Import-Module "sqlps"** 」と入力して、 **Import-Module “Import-Module "sqlps"”**モジュールをインポートします。  
  
4.  次のステートメントを実行して TCP プロトコルおよび名前付きパイプ プロトコルの両方を有効にします。 `<computer_name>` を、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を実行しているコンピューターの名前に置き換えます。 名前付きインスタンスを構成する場合は、 `MSSQLSERVER` をインスタンス名に置き換えます。  
  
     プロトコルを無効にするには、 `IsEnabled` プロパティを `$false`に設定します。  
  
    ```  
    $smo = 'Microsoft.SqlServer.Management.Smo.'  
    $wmi = new-object ($smo + 'Wmi.ManagedComputer').  
  
    # List the object properties, including the instance names.  
    $Wmi  
  
    # Enable the TCP protocol on the default instance.  
    $uri = "ManagedComputer[@Name='<computer_name>']/ ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
    $Tcp = $wmi.GetSmoObject($uri)  
    $Tcp.IsEnabled = $true  
    $Tcp.Alter()  
    $Tcp  
  
    # Enable the named pipes protocol for the default instance.  
    $uri = "ManagedComputer[@Name='<computer_name>']/ ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Np']"  
    $Np = $wmi.GetSmoObject($uri)  
    $Np.IsEnabled = $true  
    $Np.Alter()  
    $Np  
    ```  
  
#### ローカル コンピューターのプロトコルを構成するには  
  
-   スクリプトをローカルで実行してローカル コンピューターを構成する場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell ではローカル コンピューター名を動的に判断でき、スクリプトの柔軟性が向上します。 ローカル コンピューター名を取得するには、 `$uri` 変数の行の設定を次の行に置き換えます。  
  
    ```  
    $uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
    ```  
  
#### SQL Server PowerShell を使用してデータベース エンジンを再起動するには  
  
-   プロトコルを有効または無効にした後は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] を停止してから再起動して、変更を有効にする必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell で既定のインスタンスを停止してから起動するには、次のステートメントを実行します。 名前付きインスタンスを停止してから起動するには、 `'MSSQLSERVER'` を `'MSSQL$<instance_name>'`に置き換えます。  
  
    ```  
    # Get a reference to the ManagedComputer class.  
    CD SQLSERVER:\SQL\<computer_name>  
    $Wmi = (get-item .).ManagedComputer  
    # Get a reference to the default instance of the Database Engine.  
    $DfltInstance = $Wmi.Services['MSSQLSERVER']  
    # Display the state of the service.  
    $DfltInstance  
    # Stop the service.  
    $DfltInstance.Stop();  
    # Wait until the service has time to stop.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    # Start the service again.  
    $DfltInstance.Start();  
    # Wait until the service has time to start.  
    # Refresh the cache and display the state of the service.  
    $DfltInstance.Refresh(); $DfltInstance  
    ```  
  
  