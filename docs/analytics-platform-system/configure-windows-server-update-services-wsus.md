---
title: WSUS の構成
description: ここでは、Windows Server Update Services (WSUS) 構成ウィザードを使用して、Analytics Platform System 用に WSUS を構成する手順について説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2fef7b88514357deb6cf0a009d12272cc3cf79a2
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401401"
---
# <a name="configure-windows-server-update-services-wsus-in-analytics-platform-system"></a>Analytics Platform System での Windows Server Update Services (WSUS) の構成
ここでは、Windows Server Update Services (WSUS) 構成ウィザードを使用して、Analytics Platform System 用に WSUS を構成する手順について説明します。 ソフトウェア更新プログラムをアプライアンスに適用する前に、WSUS を構成する必要があります。 WSUS はアプライアンスの VMM 仮想マシンに既にインストールされています。  
  
WSUS の構成の詳細については、wsus の web サイトの「[ステップバイステップインストールガイド](https://go.microsoft.com/fwlink/?LinkId=202417)」を参照してください。 WSUS を構成した後、更新プログラムを開始するには、 [Microsoft 更新プログラムのダウンロードと適用 &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)に関する情報を参照してください。  
  
> [!WARNING]  
> この構成プロセス中にエラーが発生した場合は、を停止し、サポートにお問い合わせください。 エラーを無視したり、エラーを受信した後にプロセスを続行したりしないでください。  
  
## <a name="before-you-begin"></a>開始する前に  
WSUS を構成するには、次のことを行う必要があります。  
  
-   Analytics Platform System アプライアンスのドメイン管理者アカウントのログイン情報を取得します。  
  
-   **管理コンソール**にアクセスし、アプライアンスの状態情報を表示するためのアクセス許可を持つ Analytics Platform システムログインが必要です。  
  
-   Microsoft Update から直接更新を同期するのではなく、アップストリーム WSUS サーバーから更新プログラムを同期する予定がある場合は、アップストリーム WSUS サーバーの IP アドレスを確認します。 アップストリーム WSUS サーバーが匿名接続を許可し、SSL をサポートするように設定されていることを確認します。  
  
-   アプライアンスが上流サーバーまたは Microsoft Update にアクセスするためにプロキシサーバーを使用する場合は、プロキシサーバーの IP アドレスを確認します。  
  
-   ほとんどの場合、WSUS はアプライアンスの外部のサーバーにアクセスする必要があります。 この使用シナリオをサポートするには、分析プラットフォームシステムのホストと Virtual Machines (Vm) が外部 DNS サーバーを使用して外部 DNS サーバーを使用して外部の名前を解決できるようにする外部名フォワーダーをサポートするように、Analytics Platform システム DNS を構成します。nas. 詳細については、「 [Dns フォワーダーを使用してアプライアンス以外の Dns 名を解決する」 &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)」を参照してください。  
  
## <a name="to-configure-windows-server-update-services-wsus"></a>Windows Server Update Services を構成するには (WSUS)  
  
1.  **管理コンソール**にログインします。 [**アプライアンスの状態**] タブで、[**クラスター** ] および [**ネットワーク**] 列がすべてのノードに対して緑色 (または**n**) で表示されていることを確認します。 **アプライアンスの状態**にあるすべてのノードの状態インジケーターを確認します。  
  
    -   緑色または NA インジケーターで続行することは安全です。  
  
    -   重大でない (黄色の) 警告エラーを評価します。 場合によっては、警告メッセージによって更新プログラムがブロックされないことがあります。 C:\ にない、重大でないディスクボリュームのエラーがある場合ディスクボリュームのエラーを解決する前に、次の手順に進むことができます。  
  
    -   続行する前に、最も赤色のインジケーターを解決する必要があります。 ディスクエラーが発生した場合は、**管理コンソール**の [アラート] ページを使用して、各サーバーまたは SAN アレイ内に1つ以上のディスク障害が発生していないことを確認します。 各サーバーまたは SAN アレイ内に1つ以上のディスク障害が発生していない場合は、次の手順に進み、ディスクの障害を修正することができます。 できるだけ早くディスクの障害を修正するには、Microsoft サポートにお問い合わせください。  
  
2.  アプライアンスドメイン管理者として VMM バーチャルマシンにログオンします。  
  
3.  構成ウィザードを起動します。  
  
    #### <a name="to-launch-the-configuration-wizard"></a>構成ウィザードを起動するには  
  
    1.  **サーバーマネージャーダッシュボード**で、[**ツール**] メニューの [ **Windows Server Update Services**] をクリックします。  
  
    2.  [ **Update Services** ] ウィンドウの左側のウィンドウで、仮想マシンの管理ノードサーバー (**_appliance_domain_**) をクリックして展開し、[**オプション**] をクリックします。  
  
    3.  [**オプション**] ウィンドウで、[ **WSUS サーバー構成ウィザード**] をクリックして構成ウィザードを起動します。  
  
        ![サーバー マネージャーのダッシュボードのメニュー](./media/configure-windows-server-update-services-wsus/WSUS_Wiz0.png "WSUS_Wiz0")  
  
    4.  WSUS ウィザードを初めて実行する場合は、更新プログラムを保存するディレクトリを構成するように求められることがあります。 `C:\wsus`は適切な場所です。ただし、別のパスを指定することもできます。  
  
        ![WSUS パス](./media/configure-windows-server-update-services-wsus/WSUS_Wiz1.png "WSUS_Wiz1")  
  
    5.  ウィザードを完了する前に、完了する項目の一覧の [**開始する前に**] を確認します。  
  
        ![WSUS: 作業を開始する準備](./media/configure-windows-server-update-services-wsus/WSUS_Wiz2.png "WSUS_Wiz2")  
  
    6.  [ **Microsoft Update 向上プログラムに参加**します] ページで、[**はい、Microsoft Update 向上プログラムに参加**します] を選択し、[**次へ**] をクリックします。  
  
        ![WSUS: 向上プログラム](./media/configure-windows-server-update-services-wsus/WSUS_Wiz3.png "WSUS_Wiz3")  
  
    **[アップストリームサーバーの選択**] ページが表示されます。 次のスクリーンショットは、構成ウィザードの開始点です。  
  
    ![WSUS: 上流サーバーの同期](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
4.  アップストリームサーバーを選択します。  
  
    WSUS 構成ウィザードの [**アップストリームサーバーの選択**] ページで、ソフトウェア更新プログラムを取得するために、[仮想マシンの管理] ノードの WSUS がアップストリームサーバーに接続する方法を選択します。 2つの選択肢は、アップストリームサーバーを[Microsoft Update](https://go.microsoft.com/fwlink/?LinkId=133349)と同期するか、更新を別の Windows Server Update Services サーバーと同期させることです。  
  
    #### <a name="to-update-by-using-microsoft-update"></a>Microsoft Update を使用して更新するには  
  
    1.  Microsoft Update と同期することを選択した場合は、 **[アップストリームサーバーの選択**] ページに変更を加える必要はありません。 
  **[次へ]** をクリックします。  
  
        ![WSUS: 上流サーバーの同期](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
    #### <a name="to-update-from-another-wsus-server"></a>別の WSUS サーバーから更新するには  
  
    1.  Microsoft Update (アップストリームサーバー) 以外のソースと同期する場合は、サーバー (IP アドレスを入力) と、このサーバーが上流サーバーと通信するポートを指定します。  
  
        ![WSUS: WSUS からの上流サーバーの同期](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4b.png "WSUS_Wiz4b")  
  
    2.  Secure Sockets Layer (SSL) を使用するには、[**更新情報の同期時に ssl を使用**する] チェックボックスをオンにします。 この場合、サーバーは同期にポート443を使用します。  
  
        ![WSUS: WSUS SSL からの上流サーバーの同期](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4c.png "WSUS_Wiz4c")  
  
    3.  これがレプリカ サーバーの場合は、**[これはアップストリーム サーバーのレプリカです]** チェック ボックスをオンにします。 [**更新情報の同期時に SSL を使用**する] と [**アップストリームサーバーのレプリカ] の**両方を選択できます。  
  
        ![WSUS: 上流サーバーのレプリカ](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4d.png "WSUS_Wiz4d")  
  
    4.  この時点で、上流サーバーの構成が完了しました。 [**次へ**] をクリックするか、左側のナビゲーションウィンドウで [**プロキシサーバーの指定**] を選択します。  
  
5.  プロキシサーバーを指定します。  
  
    このサーバーが Microsoft Update または別のアップストリームサーバーにアクセスするためにプロキシサーバーを必要とする場合は、ここでプロキシサーバーの設定を構成できます。それ以外の場合は、[**次へ**] をクリックします。  
  
    ![WSUS: プロキシ](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5a.png "WSUS_Wiz5a")  
  
    #### <a name="to-configure-proxy-server-settings"></a>プロキシサーバーの設定を構成するには  
  
    1.  構成ウィザードの [**プロキシサーバーの指定**] ページで、[**同期時にプロキシサーバーを使用**する] チェックボックスをオンにし、対応するボックスにプロキシサーバーの IP アドレス (名前以外) とポート番号 (既定ではポート 80) を入力します。  
  
    2.  特定のユーザー資格情報を使用してプロキシ サーバーに接続する場合は、**[ユーザーの資格情報を使用して、プロキシ サーバーに接続する]** チェック ボックスをオンにし、対応するボックスにユーザーの名前、ドメイン、およびパスワードを入力します。 プロキシサーバーに接続しているユーザーの基本認証を有効にする場合は、[**基本認証を許可する (クリアテキストでパスワードを送信する)** ] チェックボックスをオンにします。  
  
        ![WSUS: プロキシの資格情報](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5b.png "WSUS_Wiz5b")  
  
    3.  この時点で、プロキシサーバーの構成が完了しました。 
  **[次へ]** をクリックして次のページに進むと、同期プロセスの設定を開始できます。  
  
6.  接続を開始します。  
  
    ![WSUS: プロキシの接続の開始](./media/configure-windows-server-update-services-wsus/WSUS_Wiz6.png "WSUS_Wiz6")  
  
    [**接続の開始**] をクリックします。  
  
    接続が正常に完了したら、[**次**へ] をクリックして次のページに移動します。ここでは、言語を選択できます。  
  
7.  言語を選択します。  
  
    [**次の言語でのみ更新プログラムをダウンロード**する] を選択します。  
  
    [**英語**] を選択し、[**次へ**] をクリックします。  
  
    ![言語の選択](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseLanguages.png "SQL_Server_PDW_WSUSChooseLanguages")  
  
8.  [製品] を選択します。  
  
    > [!NOTE]  
    > アップストリームサーバーを使用している場合は、製品を選択できないことがあります。 このオプションが使用できない場合は、この手順をスキップします。  
  
    選択した更新プログラムをすべて選択解除します。  
  
    [ **Windows Server 2012 r2**] および [ **System Center 2012 r2-Virtual Machine Manager**] を選択し、[**次へ**] をクリックします。  
  
9. [分類] を選択します。  
  
    > [!NOTE]  
    > アップストリームサーバーを使用している場合は、分類を選択できないことがあります。  このオプションが使用できない場合は、この手順をスキップします。  
  
    以前に選択したすべての更新プログラムを選択解除します。  
  
    分析プラットフォームシステムアプライアンス用に同期する更新プログラムの [**重要な更新**プログラムと**セキュリティ更新プログラム**] を選択し、[**次へ**] をクリックします。  
  
    ![分類の選択](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseClassifications.png "SQL_Server_PDW_WSUSChooseClassifications")  
  
10. 同期スケジュールを構成します。  
  
    [**手動で同期**] を選択し、[**次へ**] をクリックします。  
  
    ![同期スケジュールの設定](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSyncSchedule.png "SQL_Server_PDW_WSUSSyncSchedule")  
  
11. 初期同期を開始します。  
  
    [**初期同期を開始**します] を選択し、[**次へ**] をクリックします。  
  
12. 完了。  
  
    
  **[完了]** をクリックします。  
  
## <a name="bkmk_WSUSGroup"></a>WSUS でアプライアンスサーバーをグループ化する  
Analytics Platform System の WSUS を構成した後、次の手順ではアプライアンスサーバーをグループ化します。 すべてのアプライアンスサーバーをグループに追加することで、WSUS はアプライアンス内のすべてのサーバーにソフトウェアの更新を適用できるようになります。  
  
> [!NOTE]  
> WSUS システムは、非同期的に実行するように設計されています。 アクティビティを開始しても、常に直ちに更新されるとは限りません。 そのため、WSUS のダイアログボックスにコンピューターが表示されるまで、しばらく待つ必要がある場合があります。 トピックの`setup.exe /action=ReportMicrosoftUpdateClientStatus /DomainAdminPassword="<password>"`最後に記載されているコマンドを実行します。「 [Microsoft 更新プログラムのダウンロードと適用 &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)は、ダイアログボックスの更新に役立ちます。  
  
#### <a name="to-group-the-appliance-servers"></a>アプライアンスサーバーをグループ化するには  
  
1.  WSUS コンソールを開き、[すべての**コンピューター** ] を右クリックし、[**コンピューターグループの追加**] をクリックします。  
  
    ![コンピューター グループを追加します。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSAddComputerGroup.png "SQL_Server_PDW_WSUSAddComputerGroup")  
  
2.  コンピューターグループの名前として「APS」を入力し、[**追加**] をクリックします。  
  
    ![新しいコンピューター グループの名前を入力します。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSpecifyGroupName.png "SQL_Server_PDW_WSUSSpecifyGroupName")  
  
3.  [**すべてのコンピューター** ] を再度クリックし、 **[状態**] ドロップダウンメニューの状態を [**任意**] に変更して、[最新の情報に**更新**] をクリックします。 追加したばかりの新しいグループを表示するには、左側のツリーコントロールで [**すべてのコンピューター** ] をクリックして展開する必要があります。  
  
    ![[状態] を [任意] に変更して [更新] をクリックします。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusToAny.png "SQL_Server_PDW_WSUSChangeStatusToAny")  
  
4.  アプライアンスの一部であるすべてのコンピュータを選択し、右クリックして、[**メンバーシップの変更**] をクリックします。  
  
    ![すべての PDW コンピューターのメンバーシップを変更します。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeMembership.png "SQL_Server_PDW_WSUSChangeMembership")  
  
5.  チェックボックスをオンにして [ **OK]** をクリックし、作成した新しいコンピューターグループを選択します。  
  
    ![コンピューターのグループ メンバーシップの設定](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSetComputerGroupMembership.png "SQL_Server_PDW_WSUSSetComputerGroupMembership")  
  
6.  新しいコンピューターグループを選択し、その**状態**を [**任意**] に変更して、[最新の情報に**更新**] をクリックします。 これで、すべてのコンピューターがこのグループに割り当てられ、右側のウィンドウに表示されます。 **このノードがまだステータスを報告していない**などの警告がノードに表示されると、通常は安全です。  
  
    ![[状態] を [任意] に変更し、[更新] をクリックします。](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusAnyRefresh.png "SQL_Server_PDW_WSUSChangeStatusAnyRefresh")  
  
