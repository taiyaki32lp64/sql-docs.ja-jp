---
title: テレメトリに関するフィードバック
description: 分析プラットフォームシステムのテレメトリに関するフィードバックを Microsoft に送信します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 639eb4e9e5c531e154b9eb7f91165af365bc519f
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400360"
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>分析プラットフォームシステムのテレメトリフィードバックを Microsoft に送信する
Analytics Platform System には、管理コンソールのデータを Microsoft に送信するオプションのテレメトリ機能があります。 
  
> [!NOTE]  
> このリリースでは、Microsoft はテレメトリデータを積極的に監視していません。 分析の目的でのみデータが収集されています。  
  
## <a name="privacy"></a>プライバシー  
最大限のプライバシー保護を提供するために、テレメトリを有効にせずに APS が付属しています。 この機能を有効にする前に、まず[Microsoft Analytics Platform System プライバシー](https://go.microsoft.com/fwlink/?LinkId=400902)に関する声明を確認してください。 オプトインするには、以下で説明する PowerShell スクリプトを実行します。  
  
## <a name="enable"></a>テレメトリを有効にする  
**DNS 転送:** テレメトリデータを Microsoft に送信するには、Analytics Platform System が DNS フォワーダーを介してインターネットに接続する必要があります。 この機能を有効にするには、すべてのホストとワークロード Vm で DNS 転送を有効にする必要があります。 DNS 転送`Enable-RemoteMonitoring`を適切に`SetupDnsForwarder`構成し、テレメトリを有効にするオプションを指定してコマンドを呼び出します。 DNS 転送`Enable-RemoteMonitoring`が既に`SetupDnsForwarder`構成されていて、ハートビート監視のみを有効にする場合は、オプションを指定せずにコマンドを呼び出します。  
  
> [!IMPORTANT]  
> DNS 転送を有効にすると、すべてのホストとワークロード Vm のインターネット接続が開きます。  
  
#### <a name="to-enable-feedback"></a>フィードバックを有効にするには  
  
1.  アプライアンスドメイン管理者アカウントを使用して、コントロールノード (<strong>*appliance_domain*CTL01</strong>) に接続し、Windows 管理者の資格情報を使用してコマンドプロンプトを開きます。  
  
2.  次のディレクトリに移動`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`します。  
  
3.  モジュールをインポートする`Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > インポートするには、コマンドで2つのピリオドを使用する必要があります。  
  
    **よう**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  コマンドを`Enable-RemoteMonitoring`呼び出します。  
  
    > [!NOTE]  
    > このスクリプトは、インターネット接続が正常に機能していることを前提としており、インターネット接続を検証しません。  
  
    1.  テレメトリを初めて有効にするときは、次のコマンドを使用して、すべての DNS フォワーダーが正しく構成されていることを確認します。 この例では、DNS によって`xx.xx.xx.xx`転送された ip アドレスを環境内の dns フォワーダーの ip アドレスに置き換えます。  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  以前に無効にしたテレメトリを再度有効にするなど、DNS フォワーダーが既に構成されている場合は、次のコマンドを使用して、DNS 転送を構成せずにテレメトリを有効にします。  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  AP がアプライアンスに関する情報を収集することを確認するメッセージが表示されます。 APS のプライバシーに関する声明へのリンクが表示されます。この声明をコピーして、任意のインターネットブラウザーに貼り付け、レビューを行うことができます。  
  
6.  「 **Y** 」を入力して同意し、フィードバックを選択するか、「 **N** 」と入力して同意しません。  
  
7.  「 **Y** 」と入力すると、一連のコマンドが実行されます。これにより、アプライアンスでテレメトリ (および必要に応じて DNS フォワーダー) 機能が有効になります。 コマンドが成功しなかったと思われるエラーや情報が表示された場合は、CSS に問い合わせてください。  
  
「 **N**」と入力した場合、コマンドは実行されず、機能は有効になりません。これ以上の操作はありません。  
  
`Enable-RemoteMonitoring`コマンドを複数回実行しても害はありません。 DNS フォワーダーが既に設定されている場合は、そのことを示す警告メッセージが表示されます。  
  
## <a name="disable"></a>テレメトリを無効にする  
テレメトリを無効にすると、アプライアンスの状態に関する情報をクラウド内の AP 監視サービスに伝えるすべての操作が停止されます。  
  
> [!IMPORTANT]  
> この操作を実行しても、アプライアンス内の他の機能で使用されている可能性がある DNS フォワーダーまたはインターネット接続は無効になりません。  
  
#### <a name="to-disable-telemetry"></a>テレメトリを無効にするには  
  
1.  アプライアンスドメイン管理者アカウントを使用して、コントロールノード (<strong>*appliance_domain*CTL01</strong>) に接続し、管理者特権で PowerShell ウィンドウを開きます。  
  
2.  次のディレクトリに移動`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`します。  
  
3.  モジュールをインポートする`Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > インポートするには、コマンドで2つのピリオドを使用する必要があります。  
  
    **よう**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  パラメーターを`Disable-RemoteMonitoring`指定せずにコマンドを呼び出します。 このコマンドは、フィードバックの送信を停止します。 (これはローカル監視には影響しません)。ただし、このコマンドでは、DNS フォワーダーを無効にしたり、インターネット接続を無効にしたりすることはできません。 この操作は、フィードバックを正常に無効にした後に手動で行う必要があります。  
  
    **よう**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
コマンドが成功しなかったと思われるエラーや情報が表示された場合は、CSS に問い合わせてください。  
  
`Disable-RemoteMonitoring`コマンドを複数回実行しても害はありません。  
  
## <a name="next-steps"></a>次の手順
詳細については、次のドキュメントを参照してください。
- [管理コンソール &#40;Analytics Platform System&#41;を使用してアプライアンスを監視する](monitor-the-appliance-by-using-the-admin-console.md)  
- [システムビュー &#40;Analytics Platform System&#41;を使用してアプライアンスを監視する](monitor-the-appliance-by-using-system-views.md)  
- [System Center Operations Manager &#40;Analytics Platform System&#41;を使用してアプライアンスを監視する](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [DNS フォワーダーを使用して、非アプライアンス DNS 名を解決する &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
