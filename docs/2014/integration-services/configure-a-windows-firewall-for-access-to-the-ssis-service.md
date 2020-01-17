---
title: SSIS サービスにアクセスするための Windows ファイアウォールの構成 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- security [Integration Services], firewalls
- Windows Firewall [Integration Services]
- unauthorized access [Integration Services]
- Integration Services service, firewalls
- firewall systems [Integration Services]
- SQL Server Integration Services, firewalls
- SSIS, firewalls
ms.assetid: 39975cf2-c351-4205-8c39-27a0fadfb010
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b2c6a19eb44b1d53fe87bef0183bdafbb3ec105b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060852"
---
# <a name="configure-a-windows-firewall-for-access-to-the-ssis-service"></a>SSIS サービスにアクセスするように Windows ファイアウォールを構成する
    
> [!IMPORTANT]  
>  このトピックでは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを管理するための Windows サービスである [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスについて説明します。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] では、以前のリリースの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]との互換性を維持するために、このサービスをサポートしています。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]以降では、Integration Services サーバー上のパッケージなどのオブジェクトを管理できます。  
  
 Windows ファイアウォール システムは、ネットワーク接続経由でコンピューター リソースに不正なアクセスが行われるのを防ぐのに役立ちます。 このファイアウォールを経由して [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] にアクセスするには、アクセスを有効にするようにファイアウォールを構成する必要があります。  
  
> [!IMPORTANT]  
>  リモート サーバーに格納されるパッケージを管理するために、そのリモート サーバー上の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスのインスタンスに接続する必要はありません。 代わりに、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスの構成ファイルを編集し、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] でリモート サーバーに格納されているパッケージが表示されるようにします。 詳細については、「 [Integration Services サービスの構成 (SSIS サービス)](configuring-the-integration-services-service-ssis-service.md)との互換性を維持するために、このサービスをサポートしています。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスは、DCOM プロトコルを使用しています。 ファイアウォールを介した DCOM プロトコルのしくみの詳細については、情報の記事を参照してください。"[ファイアウォールで分散 COM を使用して](https://manualzz.com/doc/19762578/using-distributed-com-with-firewalls-by-michael-nelson-in...)"。  
  
 多くのファイアウォール システムが市販されています。 Windows ファイアウォール以外のファイアウォールを実行している場合、使用しているシステム固有の情報については、そのファイアウォールのマニュアルを参照してください。  
  
 ファイアウォールでアプリケーション レベルのフィルター処理がサポートされている場合は、Windows によって提供されるユーザー インターフェイスを使用して、プログラムやサービスなどの例外を指定し、ファイアウォールを通過することを許可できます。 それ以外の場合は、限定された TCP ポートのセットを使用するように DCOM を構成する必要があります。 上記の Microsoft Web サイト リンクには、使用する TCP ポートを指定する方法が紹介されています。  
  
 Integration Services サービスでは、ポート 135 を使用します。このポートは変更できません。 サービス コントロール マネージャー (SCM) のアクセスのためには、TCP ポート 135 を開く必要があります。 SCM は、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスの起動と停止、実行中のサービスに対する制御要求の転送などのタスクを実行します。  
  
 以下のセクションに記載されている情報は、Windows ファイアウォールに固有の情報です。 Windows ファイアウォール システムを構成する方法には、コマンド プロンプトでコマンドを実行する方法と、[Windows ファイアウォール] ダイアログ ボックスでプロパティを設定する方法があります。  
  
 Windows ファイアウォールの既定の設定の詳細と、データベース エンジン、Analysis Services、Reporting Services、および Integration Services に影響する TCP ポートの説明については、「 [SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」を参照してください。  
  
## <a name="configuring-a-windowsfirewall"></a>Windows ファイアウォールの構成  
 次のコマンドを使用すると、TCP ポート 135 を開き、MsDtsSrvr.exe を例外リストに追加し、ファイアウォールのブロックを解除するスコープを指定できます。  
  
#### <a name="to-configure-a-windowsfirewall-using-the-command-prompt-window"></a>コマンド プロンプト ウィンドウを使用して Windows ファイアウォールを構成するには  
  
1.  次のコマンドを実行します。 `netsh firewall add portopening protocol=TCP port=135 name="RPC (TCP/135)" mode=ENABLE scope=SUBNET`  
  
2.  次のコマンドを実行します。 `netsh firewall add allowedprogram program="%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.exe" name="SSIS Service" scope=SUBNET`  
  
    > [!NOTE]  
    >  すべてのコンピューターおよびインターネット上のコンピューターに対してファイアウォールを開くには、scope=SUBNET を scope=ALL に変更します。  
  
 次の手順では、Windows のユーザー インターフェイスを使用して、TCP ポート 135 を開き、MsDtsSrvr.exe を例外リストに追加して、ファイアウォールのブロックを解除するスコープを指定する方法について説明します。  
  
#### <a name="to-configure-a-firewall-using-the-windowsfirewall-dialog-box"></a>[Windows ファイアウォール] ダイアログ ボックスを使用してファイアウォールを構成するには  
  
1.  コントロール パネルの **[Windows ファイアウォール]** をダブルクリックします。  
  
2.  **[Windows ファイアウォール]** ダイアログ ボックスで、 **[例外]** タブをクリックし、 **[プログラムの追加]** をクリックします。  
  
3.  **[プログラムの追加]** ダイアログ ボックスで、 **[参照]** をクリックし、Program Files\Microsoft SQL Server\100\DTS\Binn フォルダーに移動します。次に MsDtsSrvr.exe をクリックし、 **[開く]** をクリックします。 **[OK]** をクリックして、 **[プログラムの追加]** ダイアログ ボックスを閉じます。  
  
4.  **[例外]** タブで、 **[ポートの追加]** をクリックします。  
  
5.  **[ポートの追加]** ダイアログ ボックスの **[名前]** ボックスに、「 **RPC(TCP/135)** 」またはその他のわかりやすい名前を入力します。次に、 **[ポート番号]** ボックスに「 **135** 」と入力し、 **[TCP]** をクリックにします。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスは常にポート 135 を使用します。 別のポートを指定することはできません。  
  
6.  **[ポートの追加]** ダイアログ ボックスで、必要に応じて **[スコープの変更]** をクリックし、既定のスコープを変更できます。  
  
7.  **[スコープの変更]** ダイアログ ボックスで、 **[ユーザーのネットワーク (サブネット) のみ]** を選択するか、カスタムの一覧を入力し、 **[OK]** をクリックします。  
  
8.  **[OK]** をクリックして **[ポートの追加]** ダイアログ ボックスを閉じます。  
  
9. **[OK]** をクリックして **[Windows ファイアウォール]** ダイアログ ボックスを閉じます。  
  
    > [!NOTE]  
    >  Windows ファイアウォールを構成するために、この手順では、コントロール パネルの **[Windows ファイアウォール]** を使用します。 **[Windows ファイアウォール]** では、現在のネットワークの場所のプロファイルに対してのみファイアウォールを構成できます。 ただし、Windows ファイアウォールは、 **netsh** コマンド ライン ツール、またはセキュリティが強化された Windows ファイアウォールの [!INCLUDE[msCoName](../includes/msconame-md.md)] 管理コンソール (MMC) スナップインを使用して構成することもできます。 これらのツールの詳細については、「 [SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services サービスの構成 (SSIS サービス)](service/integration-services-service-ssis-service.md)   
 [Integration Services サービス (SSIS サービス)](service/integration-services-service-ssis-service.md)  
  
  
