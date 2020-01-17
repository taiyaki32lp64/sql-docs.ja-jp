---
title: DNS フォワーダーを使用する
description: DNS フォワーダーを使用して、Analytics Platform System のアプライアンス以外の DNS 名を解決します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3d1d0d9428138da615fad7ff5745c758d9fcd3b8
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399433"
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names-in-analytics-platform-system"></a>DNS フォワーダーを使用して、Analytics Platform System のアプライアンス以外の DNS 名を解決する
スクリプトおよびソフトウェアアプリケーションが外部サーバーにアクセスできるようにするには、Analytics Platform システムアプライアンスの Active Directory Domain Services ノード (**_アプライアンス\_ドメイン_-AD01**および**_アプライアンス\_ドメイン_-AD02**) で DNS フォワーダーを構成することができます。  
  
## <a name="ResolveDNS"></a>DNS フォワーダーの使用  
Analytics Platform System アプライアンスは、アプライアンスにないサーバーの DNS 名を解決しないように構成されています。 Windows ソフトウェア更新サービス (WSUS) などの一部のプロセスでは、アプライアンスの外部のサーバーにアクセスする必要があります。 この使用シナリオをサポートするために、Analytics platform system の DNS を構成して、Analytics Platform システムホストと Virtual Machines (Vm) が外部 DNS サーバーを使用してアプライアンスの外部にある名前を解決できるようにすることができます。 DNS サフィックスのカスタム構成はサポートされていません。つまり、アプライアンス以外のサーバー名を解決するには完全修飾ドメイン名を使用する必要があります。  
  
**Dns GUI を使用して DNS フォワーダーを作成するには**  
  
1.  **_アプライアンス\_のドメイン_-AD01**ノードにログオンします。  
  
2.  DNS マネージャー (**dnsmgmt.msc**) を開きます。  
  
3.  サーバーの名前を右クリックし、[**プロパティ**] をクリックします。  
  
4.  [**詳細設定**] タブで、[**再帰を無効にする (フォワーダーも無効にする)** ] オプションを選択解除し、[**適用**] をクリックします)。  
  
5.  [**フォワーダー** ] タブをクリックし、[**編集**] をクリックします。  
  
6.  名前解決を提供する外部 DNS サーバーの IP アドレスを入力します。 アプライアンス内の Vm とサーバー (ホスト) は、完全修飾ドメイン名を使用して外部サーバーに接続します。  
  
7.  **_アプライアンス\_ドメイン_-AD02**ノードで手順 1-6 を繰り返します。  
  
**Windows PowerShell を使用して DNS フォワーダーを作成するには**  
  
1.  **_アプライアンス\_のドメイン_-AD01**ノードにログオンします。  
  
2.  **_アプライアンス\_のドメイン_-AD01**ノードから、次の Windows PowerShell スクリプトを実行します。 Windows PowerShell スクリプトを実行する前に、IP アドレスをアプライアンス以外の DNS サーバーの IP アドレスに置き換えます。  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  **_アプライアンス\_のドメイン_-AD02**ノードで同じコマンドを実行します。  
  
## <a name="configuring-dns-resolution-for-wsus"></a>WSUS の DNS 解決の構成  
SQL Server PDW 2012 は、統合されたサービスと修正プログラムの適用機能を提供します。 SQL Server PDW は、Microsoft Update とその他の Microsoft サービステクノロジを使用します。 更新を有効にするには、アプライアンスが企業の WSUS リポジトリまたは Microsoft パブリック WSUS リポジトリに接続できる必要があります。  
  
Microsoft パブリック WSUS リポジトリで更新プログラムを検索するようにアプライアンスを構成することを選択した場合は、次の手順に従ってアプライアンスの適切な構成の詳細を設定します。  
  
> [!NOTE]  
> 顧客のネットワーク管理者は、 **Microsoft.com**で名前を解決できる企業 DNS サーバーの IP アドレスを指定する必要があります。  
  
1.  リモートデスクトップを使用して、ファブリックドメイン管理<fabric domain>者アカウントを使用して vmm VM (-vmm) にログオンします。  
  
2.  コントロールパネルを開き、[**ネットワークとインターネット**] をクリックして、[**ネットワークと共有センター**] をクリックします。  
  
3.  [接続] ボックスの一覧の [ **Vmseruncommand**] をクリックし、[**プロパティ**] をクリックします。  
  
4.  
  **[インターネット プロトコル バージョン 4 (TCP/IPv4)]** を選択し、**[プロパティ]** をクリックします。  
  
5.  [**代替 DNS サーバー** ] ボックスに、顧客のネットワーク管理者から提供された IP アドレスを追加します。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
