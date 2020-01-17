---
title: Microsoft 更新プログラムのダウンロード
description: このトピックでは、Microsoft Update カタログから Windows Server Update Services (WSUS) に更新プログラムをダウンロードし、それらの更新プログラムを Analytics Platform System appliance サーバーに適用する方法について説明します。 Microsoft Update によって、Windows および SQL Server の適用可能なすべての更新プログラムがインストールされます。 WSUS は、アプライアンスの VMM バーチャルマシンにインストールされます。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2b24d55720d6db5997bfa85c2621f0e8d58c5f95
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401192"
---
# <a name="download-and-apply-microsoft-updates-for-analytics-platform-system"></a>Analytics Platform System の Microsoft 更新プログラムをダウンロードして適用する
このトピックでは、Microsoft Update カタログから Windows Server Update Services (WSUS) に更新プログラムをダウンロードし、それらの更新プログラムを Analytics Platform System appliance サーバーに適用する方法について説明します。 Microsoft Update によって、Windows および SQL Server の適用可能なすべての更新プログラムがインストールされます。 WSUS は、アプライアンスの VMM バーチャルマシンにインストールされます。  
  
## <a name="TOP"></a>開始する前に  
  
> [!WARNING]  
> アプライアンスまたはアプライアンスコンポーネントが停止しているか、またはフェールオーバー状態になっている場合は、更新プログラムの適用を試行しないでください。 その場合は、サポートにお問い合わせください。  
>   
> アプライアンスの使用中は、Microsoft 更新プログラムを適用しないでください。 更新プログラムを適用すると、アプライアンスノードが再起動される場合があります。 アプライアンスが使用されていない場合は、メンテナンス期間中に更新プログラムを適用する必要があります。  
  
### <a name="prerequisites"></a>前提条件  
これらの手順を実行する前に、次の操作を行う必要があります。  
  
-   「 [Configure Windows Server Update Services &#40;wsus&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)」の手順に従って、アプライアンスで wsus を構成します。  
  
-   ファブリックドメイン管理者アカウントのログイン情報に関する知識。  
  
-   Analytics Platform System 管理コンソールにアクセスし、アプライアンスの状態情報を表示するためのアクセス許可を持つログインがあること。  
  
-   ほとんどの場合、WSUS はアプライアンスの外部のサーバーにアクセスする必要があります。 この使用シナリオをサポートするには、分析プラットフォームシステムのホストと Virtual Machines (Vm) が外部 DNS サーバーを使用して外部 DNS サーバーを使用して外部の名前を解決できるようにする外部名フォワーダーをサポートするように、Analytics Platform システム DNS を構成します。nas. 詳細については、「 [Dns フォワーダーを使用してアプライアンス以外の Dns 名を解決する」 &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)」を参照してください。  
  
## <a name="bkmk_ImportUpdates"></a>Microsoft 更新プログラムをダウンロードして適用するには  
  
#### <a name="verify-the-appliance-state-indicators"></a>アプライアンスの状態インジケーターを確認する  
  
1.  管理コンソールを開き、[アプライアンスの状態] ページに移動します。 詳細については、「[管理コンソールを使用したアプライアンスの監視 &#40;Analytics Platform System](monitor-the-appliance-by-using-the-admin-console.md) 」を参照してください&#41;  
  
2.  アプライアンスの状態にあるすべてのノードの状態インジケーターを確認します。  
  
    -   緑色または NA インジケーターで続行することは安全です。  
  
    -   重大でない (黄色の) 警告エラーを評価します。 場合によっては、警告メッセージによって更新プログラムがブロックされないことがあります。 C:\ にない、重大でないディスクボリュームのエラーがある場合ディスクボリュームのエラーを解決する前に、次の手順に進むことができます。  
  
    -   続行する前に、最も赤色のインジケーターを解決する必要があります。 ディスクエラーが発生した場合は、管理コンソールの [アラート] ページを使用して、各サーバーまたは SAN アレイ内に1つ以上のディスク障害が発生していないことを確認します。 各サーバーまたは SAN アレイ内に1つ以上のディスク障害が発生していない場合は、次の手順に進み、ディスクの障害を修正することができます。 できるだけ早くディスクの障害を修正するには、Microsoft サポートにお問い合わせください。  
  
#### <a name="synchronize-the-wsus-server"></a>WSUS サーバーを同期する  
  
1.  ドメイン管理者として VMM 仮想マシンにログオンします。  
  
2.  **サーバーマネージャーダッシュボード**の [**ツール**] メニューで、[ **Windows Server Update Services** (**wsus**)] をクリックします。  
  
3.  WSUS 管理コンソールで、[**同期**] をクリックします。  
  
4.  同期が実行されていない場合は、右側のウィンドウで [**今すぐ同期**] をクリックします。 下部のウィンドウには、同期の状態が表示されます。 同期が完了するまで待ちます。  
  
#### <a name="approve-microsoft-updates-in-wsus"></a>WSUS での Microsoft 更新プログラムの承認  
  
1.  WSUS コンソールの左側のウィンドウで、[すべての**更新プログラム**] をクリックします。  
  
2.  [**すべての更新プログラム**] ウィンドウで、[**承認**] ドロップダウンメニューをクリックし、[**拒否] 以外**の [**承認**] を設定します。 [**状態**] ドロップダウンメニューをクリックし、[**状態**] を [**任意**] に設定します。 [**更新**] をクリックします。  
  
    [**タイトル**] 列を右クリックし、[**ファイルの状態**] を選択して、ダウンロードの完了後にファイルの状態を確認します。  
  
    左側のウィンドウで [**重要な更新**プログラム] または [**セキュリティ更新プログラム**] を選択して、これらのカテゴリの利用可能な更新プログラムを表示することもできます。  
  
    ![すべての更新を選択し、[状態] を [任意] に変更します。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectAllUpdates.png "SQL_Server_PDW_WSUSSelectAllUpdates")  
  
3.  [すべての更新プログラム] を選択し、右側のウィンドウで [**承認**] リンクをクリックします。  
  
    また、選択した更新プログラムを右クリックして、[**承認**] をクリックすることもできます。 "マイクロソフトソフトウェアライセンス条項" に同意するように求められる場合があります。 その場合は、ウィンドウで [**同意**する] をクリックして続行します。  
  
    ![適用するすべての更新を選択し、[承認] をクリックします。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprove.png "SQL_Server_PDW_WSUSSelectApprove")  
  
4.  [ [Configure Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)] で作成したアプライアンスサーバーグループを選択します。  
  
5.  
  **[インストールの承認]** をクリックし、**[OK]** をクリックします。  
  
    ![コンピューター グループの更新を承認します。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprovalType.png "SQL_Server_PDW_WSUSSelectApprovalType")  
  
6.  [**承認の進行状況**] ダイアログボックスで、承認プロセスが完了したら [**閉じる**] をクリックします。  
  
    ![更新が承認されたらウィンドウを閉じます。](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSCloseApprovalProgressWindow.png "SQL_Server_PDW_WSUSCloseApprovalProgressWindow")  
  
#### <a name="verify-that-the-updates-are-in-wsus"></a>更新プログラムが WSUS にあることを確認する  
  
-  すべての更新プログラムのファイルの状態を確認します。 各ファイルには、タイトルの左側に緑色の矢印アイコンが付いている必要があります。 これは、ファイルをインストールする準備ができたことを示します。  
  
    ![ファイルの状態は正常](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUS_File_Status.png "SQL_Server_PDW_WSUS_File_Status")  
  
    更新プログラムをインストールする前に、それらがすべてダウンロードされ、WSUS コンソールで使用可能であることを確認してください。  
  
#### <a name="to-verify-that-all-updates-are-downloaded"></a>すべての更新プログラムがダウンロードされていることを確認するには  
  
-  次のスクリーンショットに示すように、WSUS コンソールで更新プログラムの**ダウンロードステータス**を確認します。 すべての更新プログラムがダウンロードされたことを確認するために、**ファイルが必要な更新プログラム**が0であることを確認します。 この数が0より大きい場合は、戻って追加の更新を承認する必要があります。  
  
    ![すべての更新をダウンロードしたことを確認します。](./media/download-and-apply-microsoft-updates/SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG.png "SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG")  
  
#### <a name="apply-microsoft-updates"></a>Microsoft 更新プログラムの適用  
  
1.  開始する前に、[管理コンソール &#40;Analytics Platform System&#41;を使用してアプライアンスの監視](monitor-the-appliance-by-using-the-admin-console.md)を開き、 **[アプライアンスの状態**] タブをクリックして、**クラスター**と**ネットワーク**の列にすべてのノードが緑色 (または n) と表示されていることを確認します。 これらのいずれかの列にアラートが存在する場合、アプライアンスは更新プログラムを正しくインストールできない可能性があります。 続行する前に、**クラスター**と**ネットワーク**の列にあるすべての既存のアラートに対処してください。  
  
2.  ファブリックドメイン管理者として _<domain_name>_ **-HST01**ノードにログオンします。  
  
3.  WSUS に対して承認されたすべての更新プログラムを適用するには、更新プログラムを実行します。 手順については、以下の「[更新プログラムの実行](#RunUpdateWizard)」を参照してください。  
  
#### <a name="verify-the-updates-on-all-nodes"></a>すべてのノードで更新プログラムを確認する  
  
1.  VMM ノードから、WSUS 管理コンソールを起動します。 このアプリケーションは、[**スタート**]、[**管理ツール**]、[ **Windows Server Update Services**] の下にあります。  
  
2.  [**コンピューター**] を展開します。  
  
3.  [**すべてのコンピューター**] を展開します。  
  
4.  [ [Configure Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)] で作成したアプライアンスサーバーグループを選択します。  
  
5.  [**状態**] ドロップダウンメニューで [**任意**] を選択し、[最新の情報に**更新**] をクリックします。  
  
6.  [ **Update Services**] *<appliance name>*、[VMM]、[**更新**プログラム] *<appliance name>* 、[すべての**更新プログラム**] の順に展開します。ここで、はアプライアンス名です。  
  
7.  [**すべての更新プログラム**] ウィンドウで、[**承認**] を [**拒否] 以外**に設定します。  
  
8.  [**すべての更新プログラム**] ウィンドウで、[**状態**] を [**失敗] または [必要**] に設定します。  
  
9. [**更新**] をクリックします。  
  
10. **必要な更新プログラム**がゼロより大きい場合は、サポートにお問い合わせください。  
  
#### <a name="ensure-there-are-no-critical-alerts-in-the-sql-server-pdw-admin-console"></a>SQL Server PDW 管理コンソールで重要なアラートが発生していないことを確認する  
  
1.  管理コンソールを開き、[アプライアンスの状態] タブをクリックします。「[管理コンソール &#40;Analytics Platform System&#41;を使用したアプライアンスの監視](monitor-the-appliance-by-using-the-admin-console.md)」を参照してください。  
  
2.  **クラスター**および**ネットワーク**の列がすべてのノードに対して緑 (または n) と表示されていることを確認します。 これらのいずれかの列にアラートが存在する場合、アプライアンスは更新プログラムを正しくインストールできない可能性があります。 重大なアラートがある場合は、サポートにお問い合わせください。  
  
## <a name="RunUpdateWizard"></a>更新プログラムの実行  
Analytics Platform System Update プログラムを実行するには、次の手順に従います。  
  
> [!NOTE]  
> WSUS システムは、非同期に実行するように設計されているため、すべての更新プログラムを完全に適用するのに時間がかかることがあります。 更新プログラムを開始すると、更新プログラムがスケジュールされますが、即時更新アクティビティは保証されません。  
  
1.  HST01 ノードに、ファブリックドメイン管理者としてログインしていることを確認します。  
  
2.  コマンドプロンプトウィンドウを開き、次のコマンドを入力します。 指定*<parameter>* された情報で置き換えます。  
  
**Microsoft Update を実行するには:**  
  
```  
C:\pdwinst\media\setup.exe /action="MicrosoftUpdate" /DomainAdminPassword="<password>"  
```  
  
**Microsoft Update の状態を報告するには:**  
  
```  
C:\pdwinst\media\setup.exe /action="ReportMicrosoftUpdateClientStatus" /DomainAdminPassword="<password>"  
```  
  
## <a name="see-also"></a>参照  
[Microsoft 更新プログラムのアンインストール &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Analytics platform system の修正プログラム &#40;analytics Platform System&#41;を適用します](apply-analytics-platform-system-hotfixes.md)  
[Analytics platform system の修正プログラム &#40;Analytics Platform System&#41;をアンインストールする](uninstall-analytics-platform-system-hotfixes.md)  
[ソフトウェアサービス &#40;Analytics Platform System&#41;](software-servicing.md)  
  
