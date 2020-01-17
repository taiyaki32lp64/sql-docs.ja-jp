---
title: アップグレード PowerPivot for SharePoint |Microsoft Docs
ms.custom: ''
ms.date: 03/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 80ba9e43-f3f0-4730-9fb1-2afd2dd3e6fc
author: Minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 78112ef90eab7b6b6dd881474d04a350f6ea6ca0
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783172"
---
# <a name="upgrade-powerpivot-for-sharepoint"></a>PowerPivot for SharePoint のアップグレード
  このトピックでは、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] の配置を [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)]にアップグレードするために必要な手順について説明します。 具体的な手順は、現在環境が実行されている SharePoint のバージョンによって異なり、PowerPivot for SharePoint アドイン (**Sppowerpivot .msi**) が含まれています。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010 | SharePoint 2013  
  
 リリースノートについては、「 [SQL Server 2014 リリースノート](https://go.microsoft.com/fwlink/?LinkID=296445)」を参照してください。  
  

  
## <a name="background"></a>背景情報  
  
-   複数の [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] インスタンスを含むマルチサーバー SharePoint 2010 ファームをアップグレードする場合は、各サーバーを完全にアップグレードした **後** で、次のサーバーのアップグレードを続行する必要があります。 完全なアップグレードでは、SQL Server セットアップを実行して [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] プログラム ファイルをアップグレードした後、アップグレードしたサービスを構成するアップグレード処理を実行します。 適切な PowerPivot 構成ツールまたは Windows PowerShell でアップグレード処理を実行するまでは、サーバーの可用性が制限されます。  
  
-   SharePoint 2010 ファーム内の PowerPivot System サービスおよび Analysis Services のインスタンスはすべて、同じバージョンである必要があります。 バージョンを確認する方法については、このトピックの「 [PowerPivot のコンポーネントとサービスのバージョンを確認](#bkmk_verify_versions)する」を参照してください。  
  
-   PowerPivot 構成ツールは SQL Server の共有機能の 1 つで、すべての共有機能は同時にアップグレードされます。 アップグレード プロセス中に、共有機能のアップグレードを必要とする他の SQL Server インスタンスまたは機能を選択すると、PowerPivot 構成ツールもアップグレードされます。 PowerPivot 構成ツールがアップグレードされても PowerPivot インスタンスがアップグレードされない場合は、問題が発生している可能性があります。 SQL Server の共有機能の詳細については、「 [Upgrade to SQL Server 2014 to &#40;the&#41;Installation Wizard Setup](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)」を参照してください。  
  
-   PowerPivot for SharePoint アドイン (**Sppowerpivot .msi**) は、以前のバージョンとサイドバイサイドでインストールされます。 たとえば [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] アドインは、 `c:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools`フォルダーにインストールされます。  
  

  
##  <a name="bkmk_prereq"></a> の前提条件  
 **Permissions**  
  
-   PowerPivot for SharePoint のインストールをアップグレードするには、ファームの管理者である必要があります。 SQL Server セットアップを実行するには、ローカル管理者である必要があります。  
  
-   ファーム構成データベースに対する **db_owner** 権限を持っている必要があります。  
  
 **SQL Server :**  
  
-   既存の PowerPivot のインストールが [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]場合、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]にアップグレードするには [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Service Pack 2 (SP2) が必要です。  
  
-   既存の PowerPivot のインストールが [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]場合、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]へのアップグレードには、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 (SP1) が必要です。  
  
 **SharePoint 2010:**  
  
-   既存のインストールで SharePoint 2010 が実行されている場合は、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]。 詳細については、「 [Microsoft SharePoint 2010 Service Pack 2](https://www.microsoft.com/download/details.aspx?id=39672)」を参照してください。 バージョンを確認するには、PowerShell コマンド `(Get-SPfarm).BuildVersion.ToString()` を使用します。 リリース日でビルド バージョンを参照するには、「 [SharePoint 2010 のビルド番号](http://www.toddklindt.com/blog/Lists/Posts/Post.aspx?ID=224)」を参照してください。  
  
 
  
##  <a name="bkmk_uprgade_sharepoint2013"></a> 既存の SharePoint 2013 ファームのアップグレード  
 SharePoint 2013 に配置された [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] をアップグレードするには、次の手順を実行します。  
  
 ![powerpivot for sharepoint 2013 のアップグレード](../../../2014/sql-server/install/media/as-powepivot-upgrade-flow-sharepoint2013.png "powerpivot for sharepoint 2013 のアップグレード")  
  
1.  SharePoint モードで [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を実行するバックエンド サーバー上で [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] セットアップを実行します。 サーバーで [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]の複数のインスタンスがホストされている場合は、少なくとも **POWERPIVOT** インスタンスをアップグレードします。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] のアップグレードに関連するセットアップ ウィザードの手順の概要を次に示します。  
  
    1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ ウィザードで、 **[インストール]** をクリックします。  
  
    2.  **[SQL Server ... からのアップグレード]** をクリックします。  
  
    3.  **[インスタンスの選択]** ページで、 **POWERPIVOT** インスタンス名を選択し、 **[次へ]** をクリックします。  
  
    4.  詳細については、「[インストール&#40;ウィザードのセットアップ&#41;を使用した SQL Server 2014 へのアップグレード](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)」を参照してください。  
  
2.  サーバーを再起動します。  
  
3.  SharePoint 2013 ファーム内の各サーバーで [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint アドイン (**spPowerPivot.msi**) を実行し、データ プロバイダーをインストールします。 データ プロバイダーもアップグレードする SQL Server セットアップ ウィザードを実行したサーバーは例外です。 詳細については、「 [PowerPivot for SharePoint アドイン&#40;SharePoint 2013&#41;をインストールまたはアンインストールする](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)」を参照してください。  
  
4.  SharePoint アプリケーションサーバーの1つで**PowerPivot for SharePoint 2013 構成**ツールを実行し、アドインによってインストールされた更新済みのソリューションファイルを使用して sharepoint ファームを構成します。 この手順に SharePoint サーバーの全体管理を使用することはできません。 詳細については、以下をご覧ください。  
  
    1.  Windows のスタートページで「 **PowerPivot** 」と入力し、検索結果で **[PowerPivot for SharePoint 2013 構成]** をクリックします。 検索結果には 2 つのバージョンの構成ツールが表示される場合があることに注意してください。  
  
         ![2つの powerpivot 構成ツール](https://docs.microsoft.com/analysis-services/analysis-services/media/as-powerpivot-configtools-bothicons.gif "2つの powerpivot 構成ツール")  
  
         または  
  
         **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、[[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントし、 **[2013 構成の PowerPivot for SharePoint]** をクリックします。 このツールは、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] がローカル サーバーにインストールされている場合にのみ表示されることに注意してください。  
  
    2.  起動時、構成ツールにより、PowerPivot ファーム ソリューションと PowerPivot Web アプリケーション ソリューションのアップグレード状態がチェックされます。 これらのソリューションの古いバージョンが検出されると、"**新しいバージョンの PowerPivot ソリューションファイルが検出されました。ファームをアップグレードするには、アップグレードオプションを選択してください**。 " **[OK]** をクリックし、システムの検証メッセージを閉じます。  
  
    3.  **[機能、サービス、アプリケーション、およびソリューションのアップグレード]** をクリックし、 **[OK]** をクリックします。  
  
    4.  左側のペインにあるタスク一覧内のアクションを確認し、ツールで実行しないアクションを除外します。 既定ではすべてのアクションが含まれています。 アクションを削除するには、左側のタスク一覧でアクションを選択し、 **[パラメーター]** ページの **[この操作をタスク一覧に含めます]** チェック ボックスをオフにします。  
  
    5.  必要に応じて、 **[スクリプト]** タブまたは **[出力]** タブの詳細情報を確認します。  
  
         [出力] タブには、ツールによって実行されるアクションの概要が示されます。 この情報は、 `C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\SPAddinConfiguration\Log`にあるログ ファイルに保存されます。  
  
         [スクリプト] タブには、PowerShell コマンドレットや、ツールが実行する PowerShell スクリプト ファイルが表示されます。  
  
    6.  **[検証]** をクリックして、それぞれのアクションが有効かどうかを確認します。 **[検証]** が使用不可能な場合、システムにおいてすべてのアクションが有効であることを意味します。 **[検証]** が使用可能な場合は、入力値 (たとえば、Excel サービス アプリケーション名) を変更している可能性があるか、または特定のアクションを実行できないことがツールによって検出された可能性があります。 アクションを実行できない場合は、そのアクションを除外するか、またはアクションが無効であることを示すフラグが設定された原因となっている根本的な条件を解決してください。  
  
        > [!IMPORTANT]  
        >  最初のアクションである **[ファーム ソリューションのアップグレード]** は、常に最初に処理する必要があります。 このアクションを実行すると、サーバーの構成に使用する PowerShell コマンドレットを登録できます。 このアクションを実行したときにエラーが発生する場合は、続行しないでください。 タスク一覧の残りのアクションを処理する前に、エラーとして返された情報に基づいて問題を診断し、解決してください。  
  
    7.  **[実行]** をクリックして、このタスクで有効なすべてのアクションを実行します。 **[実行]** は、検証チェックに合格した後でのみ使用可能になります。 **[実行]** をクリックすると、アクションがバッチモードで処理されることを示す次の警告が表示されます。 "**ツールで有効としてフラグが設定されているすべての構成設定は、SharePoint ファームに適用されます。続行しますか?** "。  
  
    8.  **[はい]** をクリックして続行します。  
  
    9. ファーム内のソリューションおよび機能のアップグレードが完了するまで、数分かかります。 この間、PowerPivot データに対する接続要求は**失敗**し、"**データを更新できません**" や "**要求された操作を実行しようとしてエラーが発生しました。もう一度お試し**ください。 " アップグレードが完了すると、サーバーは使用可能になり、これらのエラーは発生しなくなります。  
  
     詳細については、以下をご覧ください。  
  
    -   [PowerPivot 構成ツール](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools)  
  
    -   [PowerPivot for SharePoint 2013 &#40;PowerPivot 構成ツールの構成または修復&#41;](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-or-repair-power-pivot-for-sharepoint-2013)  
  
    -   [Windows PowerShell を使用した PowerPivot の構成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)  
  
    -   [PowerPivot for SharePoint の PowerShell リファレンス](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
5.  アップグレード後の手順を実行し、ファーム内の PowerPivot サーバーのバージョンを確認して、アップグレードが成功したことを確認します。 詳細については、このトピックの「 [アップグレード後の検証タスク](#verify) 」以降のセクションを参照してください。  
  
 
  
##  <a name="bkmk_uprgade_sharepoint2010"></a> 既存の SharePoint 2010 ファームのアップグレード  
 SharePoint 2010 に配置された [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] をアップグレードするには、次の手順を実行します。  
  
 ![powerpivot for sharepoint 2010 のアップグレード](../../../2014/sql-server/install/media/as-powepivot-upgrade-flow-sharepoint2010.png "powerpivot for sharepoint 2010 のアップグレード")  
  
1.  [Microsoft SharePoint 2010 Service Pack 2](https://www.microsoft.com/download/details.aspx?id=39672) をダウンロードして、ファーム内のすべてのサーバーに適用します。 SharePoint SP2 のインストールが成功したことを確認します。 [サーバーの全体管理] の [アップグレードと移行] ページで、[製品および更新プログラムのインストール状態の確認] ページを開いて SP2 に関連するステータス メッセージを参照します。  
  
2.  SharePoint 2010 Administration Windows Service が実行されていることを確認します。  
  
    ```powershell
    Get-Service | Where {$_.displayname -like "*SharePoint*"}  
    ```  
  
3.  **Sharepoint** services **SQL Server Analysis Services**を確認 SQL Server し、Sharepoint サーバーの全体管理で**PowerPivot System サービス**が開始されていることを確認するか、次の PowerShell コマンドを使用します。  
  
    ```powershell
    Get-SPServiceInstance | where {$_.typename -like "*sql*"}  
    ```  
  
4.  **Windows**サービス**SQL Server Analysis Services (PowerPivot)** が実行されていることを確認します。  
  
    ```powershell
    Get-Service | where {$_.displayname -like "*powerpivot*"}  
    ```  
  
5.  **SQL Server Analysis Services (powerpivot)** Windows サービスを実行する最初の SharePoint アプリケーションサーバーで **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] セットアップを実行**して、powerpivot インスタンスをアップグレードします。 SQL Server セットアップ ウィザードの [インストール] ページで、アップグレード オプションを選択します。 詳細については、「[インストール&#40;ウィザードのセットアップ&#41;を使用した SQL Server 2014 へのアップグレード](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)」を参照してください。  
  
6.  構成ツールを実行する前に**サーバーを再起動します** 。 これにより、SQLServer セットアップによってインストールされた更新プログラムや必須コンポーネントがシステムで完全に構成されます。  
  
7.  SQL Server Analysis Services (PowerPivot) サービスを実行する最初の SharePoint アプリケーションサーバーで**PowerPivot 構成ツールを実行**し、sharepoint のソリューションと Web サービスをアップグレードします。 この手順にサーバーの全体管理を使用することはできません。  
  
    1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** をポイントします。次に、[[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** 、 **[PowerPivot 構成ツール]** の順にクリックします。 このツールは、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] がローカル サーバーにインストールされている場合にのみ表示されることに注意してください。  
  
    2.  起動時、構成ツールにより、PowerPivot ファーム ソリューションと PowerPivot Web アプリケーション ソリューションのアップグレード状態がチェックされます。 これらのソリューションの古いバージョンが検出されると、"新しいバージョンの PowerPivot ソリューションファイルが検出されました。 ファームをアップグレードするために、アップグレード オプションを選択してください。" と表示されます。 **[OK]** をクリックして、このメッセージを閉じます。  
  
    3.  **[機能、サービス、アプリケーション、およびソリューションのアップグレード]** をクリックし、 **[OK]** をクリックして続行します。  
  
    4.  次の警告が表示されます。 "PowerPivot 管理ダッシュボードのブックを最新バージョンにアップグレードしようとしています。 既存のブックに加えたカスタマイズは失われます。 続行しますか?"  
  
         これは、データ更新操作を報告する PowerPivot 管理ダッシュボードのブックに関する警告です。 これらのブックをカスタマイズしている場合、これらのブックに加えた変更は、既存のファイルを新しいバージョンで置き換えるときに失われます。  
  
         ブックを新しいバージョンで上書きする場合は、 **[はい]** をクリックします。 それ以外の場合は、 **[いいえ]** をクリックしてホーム ページに戻ります。 ブックを別の場所に保存してコピーを作成します。続行する準備が整ったら、この手順に戻ります。  
  
         ダッシュボードで使用されるブックのカスタマイズの詳細については、「 [PowerPivot 管理ダッシュボードのカスタマイズ](https://go.microsoft.com/fwlink/?linkID=229639)」を参照してください。  
  
    5.  タスク一覧内のアクションを確認し、ツールで実行しないアクションを除外します。 既定ではすべてのアクションが含まれています。 アクションを削除するには、タスク一覧でアクションを選択し、[パラメーター] ページの **[この操作をタスク一覧に含めます]** チェック ボックスをオンにします。  
  
    6.  必要に応じて、 **[出力]** タブまたは **[スクリプト]** タブの詳細情報を確認します。  
  
         [出力] タブには、ツールによって実行されるアクションの概要が示されます。 この情報は、 `c:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\ConfigurationTool\Log`にあるログ ファイルに保存されます。  
  
         [スクリプト] タブには、PowerShell コマンドレットや、ツールが実行する PowerShell スクリプト ファイルが表示されます。  
  
    7.  **[検証]** をクリックして、それぞれのアクションが有効かどうかを確認します。 **[検証]** が使用不可能な場合、システムにおいてすべてのアクションが有効であることを意味します。 **[検証]** が使用可能な場合は、入力値 (たとえば、Excel サービス アプリケーション名) を変更している可能性があるか、または特定のアクションを実行できないことがツールによって検出された可能性があります。 アクションを実行できない場合は、そのアクションを除外するか、またはアクションが無効であることを示すフラグが設定された原因となっている根本的な条件を解決してください。  
  
        > [!IMPORTANT]  
        >  最初のアクションである **[ファーム ソリューションのアップグレード]** は、常に最初に処理する必要があります。 このアクションを実行すると、サーバーの構成に使用する PowerShell コマンドレットを登録できます。 このアクションを実行したときにエラーが発生する場合は、続行しないでください。 タスク一覧の残りのアクションを処理する前に、エラーとして返された情報に基づいて問題を診断し、解決してください。  
  
    8.  **[実行]** をクリックして、このタスクで有効なすべてのアクションを実行します。 **[実行]** は、検証チェックに合格した後でのみ使用可能になります。 **[実行]** をクリックすると、アクションがバッチ モードで処理されることを示す次の警告が表示されます: "ツールで有効としてフラグが立てられている構成設定はすべて SharePoint ファームに適用されます。 続行しますか?"  
  
    9. **[はい]** をクリックして続行します。  
  
    10. ファーム内のソリューションおよび機能のアップグレードが完了するまで、数分かかります。 この間、PowerPivot データに対する接続要求は、"データを更新できません" や "要求されたアクションを実行しようとしたときにエラーが発生しました。 再試行してください" のようなエラーが表示されます。 アップグレードが完了すると、サーバーは使用可能になり、これらのエラーは発生しなくなります。  
  
8.  ファームの各 SQL Server Analysis Services (PowerPivot) サービスに対してこの手順を**繰り返し**ます。 1) SQL Server セットアップ 2) を実行して、powerpivot 構成ツールを実行します。  
  
9. アップグレード後の手順を実行し、ファーム内の PowerPivot サーバーのバージョンを確認して、アップグレードが成功したことを確認します。 詳細については、このトピックの「 [アップグレード後の検証タスク](#verify) 」以降のセクションを参照してください。  
  
10. **エラーのトラブルシューティング**  
  
     各アクションのパラメーター ペインには、エラー情報が表示されます。  
  
     ソリューションの配置または取り消しに関連する問題に対しては、SharePoint 2010 Administrator サービスが開始されていることを確認します。 このサービスは、ファームの構成の変更をトリガーするタイマー ジョブを実行します。 サービスが実行されていない場合、ソリューションの配置または取り消しは失敗します。 永続的なエラーは、既存の配置または取り消しジョブが既にキューに格納されていて、構成ツールの他のアクションがブロックされていることを示します。  
  
    1.  SharePoint 2010 管理シェルを管理者として起動し、次のコマンドを実行してキュー内のジョブを表示します。  
  
        ```cmd
        stsadm -o enumdeployments  
        ```  
  
    2.  既存の配置について、 **[種類]** が "取り消し" または "展開" であり、 **[ファイル]** が powerpivotwebapp.wsp または powerpivotfarm.wsp であることを確認します。  
  
    3.  PowerPivot ソリューションに関連する配置または取り消しアクションの場合は、 **JobId**の GUID 値をコピーし、次のコマンドに貼り付けます (シェルの [編集] メニューの [マーク]、[コピー]、[貼り付け] コマンドを使用して guid をコピーします)。  
  
        ```cmd
        stsadm -o canceldeployment -id "<GUID>"  
        ```  
  
    4.  構成ツールで **[検証]** に続けて **[実行]** をクリックして、タスクを再試行します。  
  
     他のエラーについては、ULS ログを確認します。 詳細については、「 [SharePoint ログファイルの構成と表示&#40;」&#41;と「診断ログの PowerPivot for SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging)」を参照してください。  
  

  
##  <a name="bkmk_workbooks"></a> ブック  
 サーバーをアップグレードしても、サーバー上で実行される PowerPivot ブックがアップグレードされない場合がありますが、前のバージョンの PowerPivot for Excel で作成された古いブックは、そのリリースで利用できる機能を使用して以前と同様に機能し続けます。 ブックが機能し続けるのは、以前のインストールに含まれていた Analysis Services OLE DB プロバイダーのバージョンがアップグレードしたサーバーに残っているためです。  
  
  
  
##  <a name="bkmk_datarefresh"></a> データ更新  
 アップグレードはデータ更新操作に影響を及ぼします。 サーバーでのスケジュールされたデータ更新は、そのサーバー バージョンに対応するブックに対してのみ使用できます。 以前のバージョンのブックをホストしている場合、それらのブックに対してデータ更新が機能しなくなる可能性があります。 データ更新を再び有効にするには、ブックをアップグレードする必要があります。 PowerPivot for Excel で各ブックを手動でアップグレードするか、SharePoint 2010 でデータ更新機能の自動アップグレードを有効にすることができます。 自動アップグレードでは、データ更新を実行する前にブックが最新のバージョンにアップグレードされます。これにより、データ更新操作をスケジュールどおり行うことができます。  
  

  
##  <a name="bkmk_verify_versions"></a>PowerPivot のコンポーネントとサービスのバージョンを確認する  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System サービスと Analysis Services のインスタンスはすべて、同じバージョンである必要があります。 すべてのサーバー コンポーネントが同じバージョンであることを確認するには、次のコンポーネントのバージョン情報を確認します。  
  
### <a name="verify-the-version-of-powerpivot-solutions-and-the-powerpivot-system-service"></a>PowerPivot ソリューションおよび PowerPivot System サービスのバージョン確認  
 次の PowerShell コマンドを実行します。  
  
```powershell
Get-PowerPivotSystemService  
```  
  
 **CurrentSolutionVersion**を確認します。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のバージョンは12.0 です。メジャービルド >\<ます。\<マイナービルド >  
  
### <a name="verify-the-version-of-the-analysis-services-windows-service"></a>Analysis Services Windows サービスのバージョン確認  
 SharePoint 2010 ファーム内の [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] サーバーの一部のみをアップグレードした場合は、アップグレードされていないサーバー上の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスがファームで想定されるバージョンより古くなります。 すべてのサーバーを同じバージョンにアップグレードする必要があります。 次のいずれかの方法を使用して、各コンピューターの SQL Server Analysis Services (PowerPivot) Windows サービスのバージョンを確認します。  
  
 **エクスプローラーを使用した場合**:  
  
1.  **インスタンスの** Bin [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] フォルダーに移動します。 たとえば、 `C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT\OLAP\bin`があります。  
  
2.  `msmdsrv.exe`を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[詳細]** をクリックします。  
  
4.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ファイルのバージョンは12.00 である必要があります。メジャービルド >\<ます。マイナービルド > を\<します。  
  
5.  この数値が PowerPivot ソリューションおよびシステム サービスのバージョンと同じであることを確認します。  
  
 **サービスの開始情報を使用した場合:**  
  
 PowerPivot サービスが開始されると、Windows イベント ログにバージョン情報が書き込まれます。  
  
1.  Windows の `eventvwr`  
  
2.  ソースの `MSOLAP$POWERPIVOT`のフィルターを作成します。  
  
3.  次のような情報レベルのイベントを探します。  
  
     サービスが開始されました。 Microsoft SQL Server Analysis Services 64 ビット評価 (x64) RTM **12.0.2000.8**。  
  
 **PowerShell を使用したファイル バージョンの確認**  
  
 PowerShell を使用して製品バージョンを確認できます。 バージョンの確認をスクリプト化または自動化する場合は、PowerShell を使用すると便利です。  
  
```powershell
(Get-ChildItem "C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT2000\OLAP\bin\msmdsrv.exe").VersionInfo  
```  
  
 上記の PowerShell コマンドによって、次のような情報が返されます。  
  
 ProductVersion   FileVersion           FileName  
  
 **12.0.2000.8** 2014.0120.200 C:\Program の SQL server の msas12。POWERPIVOT2000\OLAP\bin\msmdsrv.exe  
  
### <a name="verify-the-msolap-data-provider-version-on-sharepoint"></a>SharePoint での MSOLAP データ プロバイダーのバージョン確認  
 Excel Services によって信頼されている Analysis Services OLE DB プロバイダーのバージョンを確認するには、次の手順に従います。 Excel Services の信頼できるデータ プロバイダーの設定を確認するには、ファームまたはサービス アプリケーションの管理者である必要があります。  
  
1.  サーバーの全体管理で、[アプリケーション構成の管理] の **[サービス アプリケーションの管理]** をクリックします。  
  
2.  Excel Services サービス アプリケーションの名前 (たとえば **ExcelServiceApp1**) をクリックします。  
  
3.  **[信頼できるデータ プロバイダー]** をクリックします。 MSOLAP.5 (Microsoft OLE DB プロバイダー (OLAP Services 11.0 用)) が表示されます。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] をアップグレードした場合、以前のバージョンの MSOLAP.4 も表示されます。  
  
4.  詳細については、「 [Excel Services で信頼できるデータ プロバイダーとして MSOLAP.5 を追加](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/add-msolap-5-as-a-trusted-data-provider-in-excel-services)」を参照してください。  
  
 MSOLAP.4 には、"Microsoft OLE DB プロバイダー (OLAP Services 10.0 用)" という説明が表示されます。 このバージョンは、Excel Services と共にインストールされる [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] に付属する既定のバージョンか、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] バージョンである可能性があります。 SharePoint によってインストールされる既定のバージョンでは、PowerPivot データ アクセスはサポートされません。 SharePoint で PowerPivot ブックに接続するには、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 以降のバージョンが必要です。 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] バージョンがインストールされていることを確認するには、前のセクションの手順に従って、ファイルのプロパティでバージョンを確認してください。  
  
### <a name="verify-the-adomdnet-data-provider-version"></a>ADOMD.NET データ プロバイダーのバージョン確認  
 インストールされている ADOMD.NET のバージョンを確認するには、次の手順に従います。 Excel Services の信頼できるデータ プロバイダーの設定を確認するには、ファームまたはサービス アプリケーションの管理者である必要があります。  
  
1.  SharePoint アプリケーション サーバーで、 `c:\Windows\Assembly`を参照します。  
  
2.  アセンブリ名で並べ替えて、 **Microsoft.Analysis Services.Adomd.Client**を見つけます。  
  
3.  バージョン12.0 があることを確認します。\<ビルド番号 > です。  
  

##  <a name="geminifarm"></a>SharePoint ファーム内の複数の PowerPivot for SharePoint サーバーのアップグレード  
 複数の [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] サーバーを含むマルチサーバー トポロジでは、すべてのサーバー インスタンスとコンポーネントで同じバージョンを使用する必要があります。 最新バージョンのソフトウェアを実行するサーバーによって、ファーム内のすべてのサーバーのレベルが設定されます。 一部のサーバーのみをアップグレードすると、古いバージョンのソフトウェアを実行するサーバーは、同様にアップグレードを行うまで使用できなくなります。  
  
 最初のサーバーをアップグレードした後は、まだアップグレードされていない他のサーバーが **使用できなくなります**。 すべてのサーバーが同じレベルで実行されるようになると、再び使用可能になります。  
  
 SQL Server セットアップによって PowerPivot ソリューション ファイルが物理コンピューター上の適切な位置でアップグレードされますが、ファームで使用中のソリューションをアップグレードするには、このトピックの前のセクションで説明した PowerPivot 構成ツールを使用する必要があります。  

##  <a name="qfe"></a>ファーム内の PowerPivot インスタンスに QFE を適用する  
 PowerPivot for SharePoint サーバーに修正プログラムを適用すると、既存のプログラム ファイルが、特定の問題の修正を含む新しいバージョンに更新されます。 QFE をマルチサーバー トポロジに適用するときに、最初に使用すべきプライマリ サーバーはありません。 ファーム内の他の PowerPivot サーバーに同じ QFE を適用している限り、どのサーバーからでも開始できます。  
  
 QFE を適用した場合は、ファーム構成データベース内のサーバー バージョン情報を更新する構成手順も実行する必要があります。 修正プログラムを適用したサーバーのバージョンがファームに対して新たに想定されるバージョンになります。 すべてのコンピューターに QFE が適用され、構成が完了するまで、QFE が適用されていない PowerPivot for SharePoint インスタンスを使用して PowerPivot データの要求を処理することはできません。  
  
 QFE を適切に適用および構成するには、次の手順に従います。  
  
1.  QFE で提供されている手順に従って修正プログラムをインストールします。  
  
2.  PowerPivot 構成ツールを起動します。  
  
3.  **[機能、サービス、アプリケーション、およびソリューションのアップグレード]** をクリックし、 **[OK]** をクリックします。  
  
4.  アップグレード タスクに含まれているアクションを確認し、 **[検証]** をクリックします。  
  
5.  **[実行]** をクリックしてアクションを適用します。  
  
6.  ファーム内の追加の PowerPivot for SharePoint インスタンスに対して操作を繰り返します。  
  
    > [!IMPORTANT]  
    >  マルチサーバー配置では、各インスタンスの修正を適用して構成した後で、次のコンピューターに進んでください。 PowerPivot 構成ツールでは、1 つのインスタンスのアップグレード タスクを完了してから、次のインスタンスに進む必要があります。  
  
 ファーム内のサービスのバージョン情報をチェックするには、サーバーの全体管理の [アップグレードと修正プログラムの管理] セクションにある **[製品と修正プログラムのインストール状態のチェック]** ページを使用します。  
  
##  <a name="verify"></a> アップグレード後の検証タスク  
 アップグレードが完了したら、次の手順を実行して、サーバーが動作可能であることを確認します。  
  
|タスク|リンク|  
|----------|----------|  
|PowerPivot for SharePoint を実行するすべてのコンピューターでサービスが実行されていることを確認します。|[PowerPivot for SharePoint サーバーの開始または停止](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server)|  
|サイト コレクション レベルでの機能のアクティブ化を確認します。|[サーバーの全体管理でサイトコレクションの PowerPivot 機能の統合をアクティブ化する](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca)|  
|ブックを開き、フィルターおよびスライサーをクリックしてクエリを開始することで、個々の PowerPivot ブックが適切に読み込まれることを確認します。|ハード ドライブのキャッシュ ファイルの存在をチェックします。 キャッシュ ファイルが存在する場合は、データ ファイルがその物理サーバーに読み込まれたことを示します。 c:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT\OLAP\Backup フォルダー内のキャッシュ ファイルを探します。|  
|データ更新が構成されているブックを選択して、データ更新をテストします。|データ更新をテストする最も簡単な方法は、データ更新スケジュールを変更することです。具体的には、 **[さらに、できるだけ早く更新を行います]** チェック ボックスをオンにして、データ更新がすぐに実行されるようにします。 この手順によって、データ更新が現在のブックに対して成功するかどうかが判明します。 他のよく使用されるブックにもこの手順を実行して、データ更新が機能することを確認します。 データ更新のスケジュール設定の詳細については、「 [ &#40;データ&#41;更新のスケジュール PowerPivot for SharePoint](../../../2014/analysis-services/schedule-a-data-refresh-powerpivot-for-sharepoint.md)」を参照してください。|  
|随時、PowerPivot 管理ダッシュボードのデータ更新レポートを監視して、データ更新エラーがないことを確認します。|[PowerPivot 管理ダッシュボードと使用状況データ](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data)|  
  
 PowerPivot の設定と機能を構成する方法の詳細については、「[サーバーの全体管理での Powerpivot サーバーの管理と構成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)」を参照してください。  
  
 インストール後のすべての構成タスクについて説明する詳細な手順については、「 [Initial configuration &#40;PowerPivot for SharePoint&#41;](../../../2014/sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)」を参照してください。  

## <a name="see-also"></a>参照  
 [SQL Server 2014  の各エディションがサポートする機能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
 [PowerPivot for SharePoint 2010 のインストール](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
