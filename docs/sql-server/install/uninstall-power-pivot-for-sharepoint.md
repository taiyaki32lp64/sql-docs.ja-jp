---
title: Power Pivot for SharePoint のアンインストール | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 3941a2f0-0d0c-4d1a-8618-7a6a7751beac
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b39d5f4e33b9ecae8617cb414854d423945637d6
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952736"
---
# <a name="uninstall-power-pivot-for-sharepoint"></a>Power Pivot for SharePoint のアンインストール
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] のアンインストールは、複数の手順で構成されるプロセスです。これには、アンインストールの準備、ファームからの機能およびソリューションの削除、プログラム ファイルおよびレジストリ設定の削除が含まれます。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **この記事の内容:**  
  
-   [前提条件](#prereq)  
  
-   [ステップ 1:アンインストール前のチェックリスト](#bkmk_before)  
  
-   [手順 2:SharePoint から機能とソリューションを削除する](#bkmk_remove)  
  
-   [ステップ 3:SQL Server セットアップを実行してローカル コンピューターからプログラムを削除する](#bkmk_uninstall)  
  
-   [手順 4:Power Pivot for SharePoint アドインをアンインストールする](#bkmk_addin)  
  
-   [手順 5:アンインストールの確認](#verify)  
  
-   [手順 6:アンインストール後のチェックリスト](#bkmk_post)  
  
##  <a name="prereq"></a> 前提条件  
  
-   ファームの機能とソリューションをアンインストールするには、SharePoint ファームの管理者またはサービス アプリケーションの管理者である必要があります。  
  
-   データベース エンジンもアンインストールする場合は、SQL Server のシステム管理者であり、ローカル Administrators グループのメンバーであることが必要です。  
  
-   Analysis Services と [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]をアンインストールするには、Analysis Services のシステム管理者であり、ローカル Administrators グループのメンバーであることが必要です。  
  
##  <a name="bkmk_before"></a> ステップ 1:アンインストール前のチェックリスト  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データ アクセスは、クエリとデータ処理をサポートするソフトウェアがファームから削除されると無効になります。 最初の手順として、機能しなくなるファイルとライブラリを事前に削除する必要があります。 これにより、ソフトウェアのアンインストール前の "欠落データ" に関する問題と懸念に対処できます。  
  
1.  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint のインストールに関連付けられているすべての [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブック、ドキュメント、およびライブラリを削除します。 ソフトウェアをアンインストールすると、ライブラリとドキュメントはどちらも機能しなくなります。  
  
    -   [Power Pivot ギャラリーの削除](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/delete-power-pivot-gallery)  
  
    -   [Power Pivot データ フィード ライブラリの削除](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library)  
  
2.  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データを含むまたは参照する他のライブラリ内の Excel ブックまたは Reporting Services レポートを削除します。  
  
3.  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データを参照する PerformancePoint ダッシュボードの Web パーツを削除します。  
  
4.  既存のサイトとライブラリに対する SharePoint 権限を確認して、それらを変更する必要があるかどうかを判断します。 一部の [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データ アクセス シナリオ (特に、URL 接続文字列を介した別のブック内の [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データへのセカンダリ データ アクセス) では、サイトへのアクセスのみを行う SharePoint ユーザーに通常割り当てられる表示権限よりも高い読み取り権限が必要です。 読み取り権限が不要になった場合は、それに応じて権限を縮小できます。  
  
5.  オプションとして、サービスを停止した後、数日待ってからソフトウェアをアンインストールします。 この手順はアンインストールには必要ありませんが、実行し忘れていたデータ移行またはテクノロジの置き換えの問題を解決するときに、サービスを一時的に再開できます。  
  
##  <a name="bkmk_remove"></a> ステップ 2:SharePoint から機能とソリューションを削除する  
 SharePoint から [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] のサービスやアプリケーションを削除するには、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 構成ツールを使用します。  
  
-   ツールを使用するには、ファーム管理者、Analysis Services インスタンスでのサーバー管理者、およびファームの構成データベースの **db_owner** である必要があります。  
  
-   SharePoint のバージョンに応じた、適切なバージョンの構成ツールを使用します。 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] インストールでは、どちらのツールも使用しないでください。  
  
-   SharePoint Administration Service が実行されていることを確認します。  
  
1.  **構成ツールを実行する:** [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] がローカル サーバーにインストールされている場合にのみ、構成ツールが表示されることに注意してください。 **[スタート]** メニューの **[すべてのプログラム]** をポイントし、[[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にクリックして、次のいずれかをクリックします。  
  
    -   **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 の構成**  
  
    -   **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 構成ツール**  
  
2.  **[機能、サービス、アプリケーション、およびソリューションの削除]** を選択し、 **[OK]** をクリックします。  
  
3.  必要に応じて、ウィンドウを最大化します。 ウィンドウの下部に **[検証]** 、 **[実行]** 、および **[終了]** の各コマンドを含むボタン バーが表示されます。  
  
4.  タスク一覧内の各アクションの機能を確認します。  
  
     **[削除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Service アプリケーションの削除]** では、サービス アプリケーションに関連付けられたアプリケーション データを削除することを選択できます。 アプリケーション データは、データ更新スケジュール、データベース インスタンス情報、使用状況データ、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint によって使用されるその他のデータを格納するためにサービス アプリケーションを使って作成された SQL Server データベースです。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブックなどのユーザー ファイルは格納されません。 (たとえば、データ更新またはデータ アクセスに関連するデータ保持ポリシーに従うなど) アプリケーション データを保持する特定の理由がある場合を除き、SharePoint ユーザーによって作成または保存されたファイルを削除することなく、アプリケーション データベースを削除できます。  
  
     データベースを削除するには、 **[削除] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Service アプリケーションの削除** を選択し、 **[このサービス アプリケーションに関連付けられているアプリケーション データを削除します]** をアンインストールするには、Analysis Services のシステム管理者であり、ローカル Administrators グループのメンバーであることが必要です。  
  
5.  必要に応じて、 **[出力]** タブまたは **[スクリプト]** タブの詳細情報を確認します。  
  
     [出力] タブには、ツールによって実行されるアクションの概要が示されます。 この情報は、次の場所にあるログ ファイルに保存されます。  
  
     `C:\Program Files\Microsoft SQL Server\130\Tools\PowerPivotTools\SPAddinConfiguration\Log`  
  
     [スクリプト] タブには、PowerShell コマンドレットや、ツールが実行する PowerShell スクリプト ファイルが表示されます。  
  
6.  **[検証]** をクリックして、それぞれのアクションが有効かどうかを確認します。 **[検証]** が使用不可能な場合、システムにおいてすべてのアクションが有効であることを意味します。  
  
7.  **[実行]** をクリックして、このタスクで有効なすべてのアクションを実行します。 **[実行]** は、検証チェックに合格した後でのみ使用可能になります。 **[実行]** をクリックすると、アクションがバッチ モードで処理されることを示す次の警告が表示されます: "ツールで有効としてフラグが立てられている構成設定はすべて SharePoint ファームに適用されます。 続行しますか?"  
  
8.  **[はい]** をクリックして続行します。  
  
 **エラーのトラブルシューティング**  
  
 構成ツールでは、各アクションのパラメーター ペインにエラー情報が表示されます。 ソリューションの配置または取り消しに関連する問題に対しては、SharePoint Administration Service が開始されていることを確認します。 このサービスは、ファームの構成の変更をトリガーするタイマー ジョブを実行します。 サービスが実行されていない場合、ソリューションの配置または取り消しは失敗します。 永続的なエラーは、既存の配置または取り消しジョブが既にキューに格納されていて、構成ツールの他のアクションがブロックされていることを示します。 次の PowerShell コマンドを使用すると、サービスが実行されていることを確認できます。  
  
```  
Get-Service | where {$_.displayname -like "*sharepoint* administration*"}  
```  
  
 既にキューに入っている配置または取り消しジョブを見つけて削除するには、次の操作を行います。  
  
1.  他のエラーについては、ULS ログを確認します。 詳細については、「[SharePoint ログ ファイルと診断ログの構成と表示 &#40;Power Pivot for SharePoint&#41;](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging)」を参照してください。  
  
2.  SharePoint 管理シェルを管理者として起動し、次のコマンドを実行してキュー内のジョブを表示します。  
  
    ```  
    Stsadm -o enumdeployments  
    ```  
  
3.  既存の配置について、 **[種類]** が "取り消し" または "展開" であり、 **[ファイル]** が powerpivotwebapp.wsp または powerpivotfarm.wsp であることを確認します。  
  
4.  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ソリューションに関連するデプロイまたは取り消しの場合、 **[JobId]** の GUID 値をコピーし、次のコマンドに貼り付けます (シェルの [編集] メニューの [マーク]、[コピー]、および [貼り付け] を使用して GUID をコピーします)。  
  
    ```  
    Stsadm -o canceldeployment -id "<GUID>"  
    ```  
  
5.  構成ツールで **[検証]** に続けて **[実行]** をクリックして、タスクを再試行します。  
  
 また、PowerShell を使用して、機能とソリューションをファームから削除することもできます。 詳細については、「 [Power Pivot for SharePoint 用 PowerShell リファレンス](https://docs.microsoft.com/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)」を参照してください。  
  
##  <a name="bkmk_uninstall"></a> ステップ 3:SQL Server セットアップを実行してローカル コンピューターからプログラムを削除する  
 プログラム ファイルを削除するには、SQL Server セットアップを実行してソフトウェアをアンインストールする必要があります。 アンインストールを実行すると、ファイルだけでなく、セットアップによって作成されたレジストリ エントリも削除されます。 [プログラムと機能] ページを使用して、ソフトウェアをアンインストールできます。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] インストールは、SQL Server インストールの一部です。  
  
 インストールの一部を、既にインストールされている他の SQL Server インスタンス (または同じインスタンスの機能) に影響を与えずにアンインストールすることができます。 たとえば、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 、データベース エンジンなどの他のコンポーネントを残したまま、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] for SharePoint をアンインストールすることができます。  
  
1.  プログラム リストから **[Microsoft SQL Server 2014 (64 ビット)]** を選択します。  
  
2.  **[アンインストール] または [変更]** をクリックします。  
  
3.  **[削除]** をクリックします。 SQL Server セットアップが起動します。  
  
     セットアップで **[[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]]** インスタンスを選択してから、 **[Analysis Services]** および **[Analysis Services SharePoint 統合]** を選択して、他はすべてそのままの状態で、その機能だけを削除できます。  
  
##  <a name="bkmk_addin"></a> 手順 4:Power Pivot for SharePoint アドインをアンインストールする  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 配置に 2 台以上のサーバーがあり、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] アドインをインストールした場合は、インストール先の各サーバーから [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] アドインをアンインストールして、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] のすべてのファイルを完全にアンインストールします。 詳細については、「 [Power Pivot for SharePoint アドインのインストールまたはアンインストール &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)」を参照してください。  
  
##  <a name="verify"></a> 手順 5:アンインストールの確認  
  
1.  [サーバーの全体管理] の **[サーバーのサービスの管理]** で、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint をアンインストールしたサーバーに接続します。  
  
2.  -   [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 をアンインストールした場合は、 **[SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System サービス]** が一覧に表示されないことを確認します。  
  
    -   [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 をアンインストールした場合は、 **[SQL Server Analysis Services]** と **[SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System サービス]** が一覧に表示されないことを確認します。  
  
3.  ファーム内の最後の [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint サーバーをアンインストールしたら、次の手順を実行します。  
  
    1.  [アプリケーション構成の管理] の **[サービス アプリケーションの管理]** で、[ [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] サービス アプリケーション] が一覧に表示されないことを確認します。  
  
    2.  [システム設定] の **[ファーム機能の管理]** で、[ [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 統合機能] がページに表示されないことを確認します。 **[ファーム ソリューションの管理]** で、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ソリューションがページに表示されないことを確認します。  
  
    3.  [監視] の **[診断ログの構成]** と **[使用状況と正常性のデータ収集の構成]** で、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] イベントとイベント カテゴリが表示されないことを確認します。  
  
    4.  [アプリケーションの全般設定] で、 **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理ダッシュボード** がページに表示されないことを確認します。  
  
##  <a name="bkmk_post"></a> 手順 6:アンインストール後のチェックリスト  
 次の一覧を使用して、アンインストール時に削除されなかったソフトウェアとファイルを削除します。  
  
1.  `C:\Program Files\Microsoft SQL Server\MSAS13.PowerPivot`のすべてのデータ ファイルおよびサブフォルダーを削除し、次にこのフォルダーを削除します。 この手順では、DATA ディレクトリ内のキャッシュされたファイルも削除されます。  
  
2.  すべての [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ブック、ドキュメント、およびライブラリをまだ削除していない場合は、削除します。  
  
    -   [Power Pivot ギャラリーの削除](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/delete-power-pivot-gallery)  
  
    -   [Power Pivot データ フィード ライブラリの削除](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library)  
  
3.  Secure Store Service で、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint で使用されている保存された資格情報を含む対象アプリケーションを削除します。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint をアンインストールすると、Secure Store Service のエントリの一部は削除されますが、削除されないエントリもあります。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 自動データ更新アカウント用に作成された対象アプリケーションと、データ更新用に作成した対象アプリケーションはまだ存在しているため、手動で削除する必要があります。  
  
     一方で、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System サービスで自動生成された個々の対象アプリケーションは、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] のアンインストール時に自動的に削除されます。  
  
4.  コントロール パネルで、 **[プログラム]** 、 **[プログラムのアンインストール]** の順にクリックします。使用しなくなった Analysis Services クライアント ライブラリをアンインストールします。 Analysis Services ADOMD.NET と Microsoft SQL Server Analysis 管理オブジェクトは、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint をアンインストールしても削除されません。 ライブラリは、Analysis Services データを使用する他のプログラムで使用されることがあるので、SQL Server セットアップではこれらは自動的にはアンインストールされません。 クライアント ライブラリが不要になった場合には、これらを個別にアンインストールする必要があります。  
  
     SQL Server Reporting Services SharePoint 2010 アドインは、そのアンインストールを具体的に指示するトラブルシューティングまたはインストール手順に従う場合以外はアンインストールしないでください。 Reporting Services アドインは Access Services で使用されます。 これは SharePoint 製品準備ツールでインストールされ、SharePoint に必要な機能をサポートするためにシステムに残しておく必要があります。  
  
     Analysis Services OLE DB プロバイダーはアンインストールしないでください。 SharePoint では、Analysis Services データベースに接続する Excel ブックの前提条件として OLE DB プロバイダーがインストールされます。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] では、より新しいバージョンがインストールされますが、このバージョンは下位互換性があるため、後でデータ接続の問題が発生するのを避けるためにシステムに残しておく必要があります。  
  
## <a name="see-also"></a>参照  
 [Power Pivot for SharePoint アドインのインストールまたはアンインストール &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)   
 [Power Pivot の構成ツール](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools)  
  
  
