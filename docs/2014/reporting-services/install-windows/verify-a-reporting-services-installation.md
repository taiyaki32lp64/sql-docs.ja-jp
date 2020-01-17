---
title: Reporting Services のインストール状態の検証 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- checking report server installations
- verifying report server installations
- Report Designer [Reporting Services], verifying installations
- installing Reporting Services, verifying installations
- Report Manager [Reporting Services], verifying installations
- report servers [Reporting Services], verifying installations
- Setup [Reporting Services], verifying installations
ms.assetid: 82a51a99-66f0-4b0c-b05b-07d22387adb0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9106ff624c9a8e50bd292166690fc220eaea527e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108567"
---
# <a name="verify-a-reporting-services-installation"></a>Verify a Reporting Services Installation
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーは、ネイティブまたは SharePoint の 2 つのモードのうちのいずれかのモードでインストールできます。 インストールの確認に必要な手順は、レポート サーバーのモードによって変わります。  
  
 このトピックの内容は次のとおりです。  
  
-   [SharePoint モード インストールを確認します。](#bkmk_sharepointmode)  
  
-   [ネイティブ モードのインストールを確認します。](#bkmk_nativemode)  
  
##  <a name="bkmk_sharepointmode"></a> SharePoint モードのインストールの確認  
  
#### <a name="to-verify-the-reporting-services-service"></a>Reporting Services サービスを確認するには  
  
1.  SharePoint サーバーの全体管理で、 **[システム設定]** の **[サーバーのサービスの管理]** をクリックします。  
  
2.  **SQL Server Reporting Services サービス** がインストールされ、 **実行中** の状態であることを確認します。  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスが一覧に表示されない場合は、サービスがインストールされていることを確認します。 詳細については、の「インストールと Reporting Services SharePoint サービスの開始」セクションを参照してください。 [Install Reporting Services SharePoint Mode for SharePoint 2010](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)します。  
  
#### <a name="to-verify-the-service-application"></a>サービス アプリケーションを確認するには  
  
1.  サーバーの全体管理から確認するには、少なくとも 1 つの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションを使用します。 **[アプリケーション構成の管理]** で **[サービス アプリケーションの管理]** をクリックします。  
  
2.  種類が **[SQL Server Reporting Services サービス アプリケーション]** のサービス アプリケーションと、対応するアプリケーション プロキシがあることを確認します。  
  
3.  サービス アプリケーションの名前の **近く** をクリックし、SharePoint ツール バーの **[プロパティ]** をクリックします。  サービス アプリケーションの名前をクリックすると、プロパティ ページではなく、サービス アプリケーションの管理ページが開きます。  
  
4.  必要な Web アプリケーションを指すように **[Web アプリケーションの関連付け]** が構成されていることを確認します。  
  
#### <a name="to-verify-the-site-collection-feature"></a>サイト コレクション機能を確認するには  
  
1.  サイトの設定の **[サイト コレクションの管理]** で **[サイト コレクションの機能]** をクリックします。  
  
2.  **[レポート サーバーの統合機能]** がアクティブであることを確認します。  
  
#### <a name="to-verify-reporting-server-content-types"></a>レポート サーバー コンテンツの種類を確認するには  
  
1.  確認または追加[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]レポート サーバー コンテンツの種類を参照してください[ライブラリにレポート サーバー コンテンツ タイプの追加&#40;Reporting Services SharePoint 統合モードで&#41;](../add-reporting-services-content-types-to-a-sharepoint-library.md)します。  
  
#### <a name="to-verify-you-can-launch-report-builder"></a>レポート ビルダーが起動できることを確認するには  
  
1.  ドキュメント ライブラリから、SharePoint リボンの **[ドキュメント]** をクリックします。  
  
2.  **[新しいドキュメント]** をクリックし、 **[レポート ビルダー レポート]** をクリックします。 このオプションが表示されない場合は、レポート サーバー コンテンツの種類をライブラリに追加するための前の手順を確認してください。  
  
#### <a name="create-a-basic-report"></a>基本的なレポートの作成  
  
1.  SharePoint ドキュメント ライブラリ内で、タイトルなどに使用するテキスト ボックスのみを含む基本的な [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポートを作成します。 このレポートには、データ ソースやデータセットは何も含めません。 目標は、レポート ビルダーを開いて基本的なレポートをプレビューできることの確認です。  
  
2.  レポートをドキュメント ライブラリに保存し、ライブラリからレポートを実行します。 レポート ビルダーでレポートを作成する方法の詳細については、「[レポート ビルダーの起動 (レポート ビルダー)](https://technet.microsoft.com/library/ms159221.aspx)」を参照してください。  
  
#### <a name="reporting-services-samples"></a>Reporting Services のサンプル  
  
1.  Reporting Services のチュートリアルのいずれかを完了します。 詳細については、「[Reporting Services のチュートリアル (SSRS)](../reporting-services-tutorials-ssrs.md)」を参照してください。  
  
2.  CodePlex から AdventureWorks の作業のサンプル データベースと [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サンプル レポートをダウンロードします。 詳細については、「 [AdventureWorks レポート サンプル](https://msftrsprodsamples.codeplex.com/wikipage?title=SS2012!AdventureWorks2012%20Report%20Samples&referringTitle=Home)」を参照してください。  
  
##  <a name="bkmk_nativemode"></a> ネイティブ モードのインストールの確認  
 既定の構成を使用してネイティブ モードでレポート サーバーをインストールする場合、セットアップでサーバーをインストールし、配置します。 いくつかの簡単なテストを行うことで、レポート サーバーが正常に配置されたかどうかを確認できます。 これらの手順を実行するには、ローカル管理者である必要があります。 他のユーザーがテストを実行する場合は、そのユーザーがレポート サーバーにアクセスできるように構成する必要があります。  
  
#### <a name="to-verify-that-the-report-server-is-installed-and-running"></a>レポート サーバーが正常にインストールされ、実行されていることを確認するには  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを実行し、インストールしたレポート サーバー インスタンスに接続します。 [Web サービス URL] ページには、レポート サーバー Web サービスへのリンクが含まれています。 このリンクをクリックして、サーバーにアクセスできることを確認します。 レポート サーバー データベースが構成されていない場合は、リンクをクリックする前にレポート サーバー データベースを構成してください。  
  
2.  Services コンソール アプリケーションを開き、レポート サーバー サービスが実行されていることを確認します。 レポート サーバー サービスの状態を表示するには、 **[スタート]** ボタンをクリックし、 **[コントロール パネル]** をポイントして、 **[管理ツール]** をダブルクリックします。次に、 **[サービス]** をダブルクリックします。 サービスの一覧が表示されたら、 **[Report Server (MSSQLSERVER)]** までスクロールします。 状態が **[開始]** になっていることを確認してください。  
  
3.  ブラウザーを開き、アドレス バーにレポート サーバーの URL を入力します。 アドレスは、セットアップ時にレポート サーバーに指定したサーバー名と仮想ディレクトリ名で構成されます。 既定では、レポート サーバーの仮想ディレクトリ名は **ReportServer**です。 http:// *\<コンピューター名>* /ReportServer *\<_インスタンス名>* という URL を使用して、レポート サーバーのインストール状態を確認できます。 レポート サーバーを名前付きインスタンスとしてインストールした場合、URL は異なります。 URL 形式の詳細については、「[レポート サーバー URL の構成 (SSRS 構成マネージャー)](configure-report-server-urls-ssrs-configuration-manager.md)」を参照してください。 Windows Vista または Windows Server 2008 上のローカル管理者である場合は、「[ローカル管理用のネイティブ モードのレポート サーバー (SSRS) の構成](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)」を参照してください。  
  
4.  レポートを実行して、レポート サーバーの動作をテストします。 この手順では、チュートリアルからサンプル レポートを作成できます。 詳細については、「[基本的なテーブル レポートの作成 (SSRS チュートリアル)](../create-a-basic-table-report-ssrs-tutorial.md)」を参照してください。  
  
#### <a name="to-verify-that-report-manager-is-installed-and-running"></a>レポート マネージャーが正常にインストールされ、実行されていることを確認するには  
  
1.  ブラウザーを開き、アドレス バーにレポート マネージャーの URL を入力します。 このアドレスは、セットアップ時または Reporting Services 構成ツールの [レポート マネージャー URL] ページでレポート マネージャーに対して指定したサーバー名と仮想ディレクトリ名で構成されます。 既定では、レポート マネージャーの仮想ディレクトリは **Reports**です。 次の URL を使用して、レポート マネージャーのインストール状態を確認できます。  
  
     http:// *\<コンピューター名>* /Reports *\<_インスタンス名>*  
  
2.  レポート サーバー データベースに定義が戻されるかどうかをテストするため、レポート マネージャーを使用して新しいフォルダーを作成するか、ファイルをアップロードします。 操作が成功した場合、接続は正しく機能しています。  
  
     詳細については、「[レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../report-manager-ssrs-native-mode.md)」を参照してください。  
  
#### <a name="to-verify-that-report-designer-is-installed-and-running"></a>レポート デザイナーが正常にインストールされ、実行されていることを確認するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]を開き、レポート サーバーのプロジェクトの種類に基づいて新しいプロジェクトを作成します。 レポート サーバー プロジェクト ウィザードの使用方法の詳細については、SQL Server オンライン ブックの「[SQL Server データ ツールの Reporting Services (SSDT)](../tools/reporting-services-in-sql-server-data-tools-ssdt.md)」を参照してください。  
  
2.  サンプル レポートをインストールした場合は、サンプル レポート プロジェクト ファイルを開き、レポート サーバーにレポートをパブリッシュします。  
  
## <a name="see-also"></a>参照  
 [Reporting Services インストール時の問題解決](troubleshoot-a-reporting-services-installation.md)   
 [Reporting Services エラーの原因と解決方法](../troubleshooting/cause-and-resolution-of-reporting-services-errors.md)  
  
  
