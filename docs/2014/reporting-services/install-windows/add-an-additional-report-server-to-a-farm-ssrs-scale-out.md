---
title: ファームへのレポート サーバーの追加 (SSRS スケールアウト) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c1a6b683-15cf-44ae-ac60-ceee63a60aaf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b90bb5624e5b5cdbf3f1542ad0bef0d2765da248
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108966"
---
# <a name="add-an-additional-report-server-to-a-farm-ssrs-scale-out"></a>ファームへのレポート サーバーの追加 (SSRS スケールアウト)
  2 台目以降の SharePoint モードのレポート サーバーを SharePoint ファームに追加すると、レポート サーバーのパフォーマンスと応答時間を向上させることができます。 ユーザー、レポート、またはその他のアプリケーションをレポート サーバーに追加したときにパフォーマンスが低下する場合は、レポート サーバーを追加することでパフォーマンスを向上できます。 ハードウェアに問題がある場合、または環境内の個々のサーバーに対して全般的なメンテナンスを行う場合も、2 台目のレポート サーバーを追加してレポート サーバーの可用性を向上させることをお勧めします。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降のリリースでの SharePoint モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 環境をスケールアウトする手順では、標準の SharePoint ファーム配置に従い、SharePoint の負荷分散機能を活用します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の一部のエディションでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のスケールアウトがサポートされません。 詳細については、次を参照してください。、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]の[機能は、SQL Server 2014 の各エディションでサポートされている](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。  
  
> [!TIP]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では、サーバーの追加およびレポート サーバーのスケールアウトに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用しません。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスを使用する SharePoint サーバーがファームに追加されると、SharePoint 製品では Reporting Services のスケールアウトを管理します。  
  
 ネイティブ モードのレポート サーバーをスケールアウトする方法の詳細については、「[ネイティブ モード レポート サーバーのスケールアウト配置の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)」を参照してください。  
  
-   [負荷分散](#bkmk_loadbalancing)  
  
-   [前提条件](#bkmk_prerequisites)  
  
-   [手順](#bkmk_steps)  
  
-   [追加の構成](#bkmk_additional)  
  
##  <a name="bkmk_loadbalancing"></a> 負荷分散  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの負荷分散は、カスタムまたはサードパーティの負荷分散ソリューションが環境に含まれていない限り、SharePoint によって自動的に管理されます。 SharePoint の既定の負荷分散動作では、各 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーション サービスは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスを開始したすべてのアプリケーション サーバー間で分散されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスがインストールされていて開始されていることを確認するには、SharePoint サーバーの全体管理で **[サーバーのサービスの管理]** をクリックします。  
  
##  <a name="bkmk_prerequisites"></a> 前提条件  
  
-   SQL Server セットアップを実行するには、ローカル管理者である必要があります。  
  
-   コンピューターがドメインに参加する必要があります。  
  
-   SharePoint の構成データベースとコンテンツ データベースをホストしている既存のデータベース サーバーの名前を把握しておく必要があります。  
  
-   データベース サーバーは、リモート データベース接続を許可するように構成されている必要があります。  構成されていない場合は、新しいサーバーが SharePoint 構成データベースに接続できないため、新しいサーバーをファームに参加させることができません。  
  
-   新しいサーバーのバージョンは、現在のファーム サーバーが実行されているインストール済みの SharePoint のバージョンと同じである必要があります。 たとえば、SharePoint 2010 Service Pack 1 (SP1) が既にファームにインストールされている場合は、新しいサーバーをファームに参加させる前に、新しいサーバーにも SP1 をインストールする必要があります。  
  
-   次の追加トピックを確認し、システムとバージョンの要件を理解してください。  
  
     [SharePoint 2010 ファームで SQL Server BI 機能を使用するためのガイド](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
##  <a name="bkmk_steps"></a> 手順  
 このトピックの手順では、SharePoint ファームの管理者がサーバーをインストールして構成すると想定しています。 この図は標準的な 3 層環境を示しています。次に、図の番号付き項目の説明を示します。  
  
-   (1) 複数の Web フロントエンド (WFE) サーバー。 WFE サーバーには、SharePoint 2010 用の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインが必要です。  
  
-   (2) [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] と Web サイトを実行している単一のアプリケーション サーバー。たとえば、サーバーの全体管理などです。 次の手順では、この層に 2 つ目のアプリケーション サーバーを追加します。  
  
-   (3) 2 つの SQL Server データベース サーバー。  
  
-   (4) ソフトウェアまたはハードウェアのネットワーク負荷分散ソリューション (NLB) を表します。  
  
 ![Reporting Services アプリケーション サーバーを追加する](../../../2014/sql-server/install/media/rs-sharepointscale.gif "Reporting Services アプリケーション サーバーを追加する")  
  
 次の手順では、管理者がサーバーをインストールして構成すると想定しています。 サーバーは、新しいアプリケーション サーバーとしてファームにセットアップされ、Web フロントエンド (WFE) としては使用されません。  
  
|手順|説明とリンク|  
|----------|--------------------------|  
|SharePoint 2010 製品準備ツールを実行します。|SharePoint 2010 のインストール メディアが必要です。 準備ツールはインストール メディアの **PrerequisiteInstaller.exe** です。|  
|SharePoint 2010 製品をインストールします。|1) 選択、**サーバー ファーム**インストールの種類。<br /><br /> 2) 選択**完了**サーバーの種類。<br /><br /> 3) 既存の SharePoint ファームに SharePoint 2010 SP1 がインストールされている場合は、インストールが完了したときに SharePoint 製品構成ウィザードを実行しないでください。 SharePoint 製品構成ウィザードを実行する前に SharePoint SP1 をインストールする必要があります。|  
|SharePoint Server 2010 SP1 をインストールします。|既存の SharePoint ファームに SharePoint 2010 SP1 インストールをダウンロードしてから、SharePoint 2010 SP1 をインストールする場合:[https://support.microsoft.com/kb/2460045](https://go.microsoft.com/fwlink/p/?linkID=219697)します。<br /><br /> SharePoint 2010 SP1 の詳細については、「 [Office 2010 SP1 および SharePoint 2010 SP1 インストール時の既知の問題](https://support.microsoft.com/kb/2532126)」を参照してください。|  
|SharePoint 製品の構成ウィザードを実行して、ファームにサーバーを追加します。|1) で、 **Microsoft SharePoint 2010 製品**プログラム グループで、をクリックして**Microsoft SharePoint 2010 製品構成ウィザード**します。<br /><br /> 2)、**サーバー ファームへの接続**選択ページ**既存ファームへの接続** をクリック**次**。<br /><br /> 3)、**構成データベースの設定の指定** ページで、既存のファーム構成データベースの名前を使用するデータベース サーバーの名前を入力します。 **[次へ]** をクリックします。<br />**\*\* 重要な\* \*** で SQL Server ネットワーク構成に対してどのようなプロトコルが有効になっている確認し、次のようなエラー メッセージが表示アクセス許可があることを確認する場合は、 **Sql ServerConfiguration Manager**:"データベース サーバーへの接続に失敗しました。 確認してください、データベースが存在する、それが Sql Server、およびサーバーにアクセスする適切なアクセス許可がある。"<br />**\*\* 重要な\* \*** ページが表示された場合**サーバー ファーム製品と修正プログラムの状態**ページの情報を確認し、続行する前に、必要なファイルでサーバーを更新する必要がありますファームにサーバーを参加させる。<br /><br /> 4)、**ファームのセキュリティ設定の指定**ページは、ファームのパスフレーズを入力し、をクリックして**次**します。 確認ページで **[次へ]** をクリックして、ウィザードを実行します。<br /><br /> 5) クリック**次**を実行する、**ファーム構成ウィザード**します。|  
|サーバーが SharePoint ファームに追加されたことを確認します。|1) SharePoint サーバーの全体管理で、 **[システム設定]** の **[このファームのサーバーの管理]** をクリックします。<br /><br /> 2) 新しいサーバーが追加され、状態が正しいことを確認します。<br /><br /> サービスが表示されない 3) 注**SQL Server Reporting Services サービス**を実行します。 このサービスは次の手順でインストールされます。<br /><br /> このサーバーを WFE ロールから削除するには 4) をクリックして**サービス サーバーの管理**サービスを停止および**Microsoft SharePoint Foundation Web アプリケーション**。|  
|Reporting Services SharePoint モードをインストールして構成します。|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インストールを実行します。 インストールの詳細については[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint モードを参照してください[Install Reporting Services SharePoint Mode for SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)として、アプリケーション サーバーと、サーバーを使用するがないかどうかは、サーバーが使用されますのみWFE、する必要はありません選択**Reporting Services アドインを SharePoint 製品用**で。<br /><br /> **セットアップ ロール**] ページで、[ **SQL Server 機能のインストール**<br /><br /> **機能の選択**] ページで、[ **Reporting Services - SharePoint**<br /><br /> -または-<br /><br /> **Reporting Services 構成**ページ確認、**インストールのみ**オプションが選択されて**Reporting Services SharePoint モード**します。|  
|Reporting Services が動作することを確認します。|1) SharePoint サーバーの全体管理で、 **[システム設定]** の **[このファームのサーバーの管理]** をクリックします。<br /><br /> 2) **SQL Server Reporting Services サービス**を確認します。<br /><br /> 詳細については、「 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)」をご覧ください。|  
  
##  <a name="bkmk_additional"></a> その他の構成  
 スケールアウト配置では、個々の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サーバーを最適化して、バックグラウンド処理のみを実行できます。そのため、リソースの確保を求めて対話型のレポート実行との競合が発生することはありません。 バックグラウンド処理には、スケジュール、サブスクリプション、およびデータ警告が含まれます。  
  
 個々のレポート サーバーの動作を変更するには、**RSreportServer.config** 構成ファイルで **\<IsWebServiceEnable>** を false に設定します。  
  
 既定では、\<IsWebServiceEnable> を TRUE に設定してレポート サーバーが構成されます。 TRUE の設定を使用してすべてのサーバーが構成されている場合は、対話型処理とバックグラウンド処理がファーム内のすべてのノード間で負荷分散されます。  
  
 \<IsWebServiceEnable> を False に設定してすべてのレポート サーバーを構成した場合は、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の機能を使用しようとすると、次のようなエラー メッセージが表示されます。  
  
 Reporting Services Web サービスが無効です。 少なくとも 1 つのインスタンスが Reporting Services SharePoint サービスの構成\<IsWebServiceEnable > を true に設定します。 詳細については、「[Reporting Services の構成ファイルの変更 &#40;RSreportserver.config&#41;](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SharePoint 2013 ファームに web アプリケーションまたはアプリケーション サーバーを追加します。](https://technet.microsoft.com/library/cc261752.aspx)   
 [サービス (SharePoint Server 2010) を構成します。](https://technet.microsoft.com/library/ee794878.aspx)  
  
  
