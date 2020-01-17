---
title: ファームへの Reporting Services Web フロントエンドの追加 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: d7a11bda-ae26-49ac-b071-37d83cae5afe
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a7996ea2541963d0c7a2060d819667e25d102305
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108959"
---
# <a name="add-an-additional-reporting-services-web-front-end-to-a-farm"></a>ファームへの Reporting Services Web フロントエンドの追加
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードには、アプリケーション サーバーと Web フロントエンド (WFE) サーバーに必要なコンポーネントが含まれています。 このトピックでは、WFE サーバーに必要な [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントのインストールに焦点を当てます。これらのコンポーネントには、サブスクリプション、データ警告、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] など、 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]機能で使用されるアプリケーション ページが含まれます。 WFE に必要な主要な [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インストールは、SharePoint 2010 製品用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインをインストールすることです。  
  
## <a name="prerequisites"></a>前提条件  
  
-   SQL Server セットアップを実行するには、ローカル管理者である必要があります。  
  
-   コンピューターがドメインに参加する必要があります。  
  
-   SharePoint の構成データベースとコンテンツ データベースをホストしている既存のデータベース サーバーの名前を把握しておく必要があります。  
  
-   データベース サーバーは、リモート データベース接続を許可するように構成されている必要があります。  構成されていない場合は、新しいサーバーが SharePoint 構成データベースに接続できないため、新しいサーバーをファームに参加させることができません。  
  
-   新しいサーバーのバージョンは、現在のファーム サーバーが実行されているインストール済みの SharePoint のバージョンと同じである必要があります。 たとえば、SharePoint 2010 Service Pack 1 (SP1) が既にファームにインストールされている場合は、新しいサーバーをファームに参加させる前に、新しいサーバーにも SP1 をインストールする必要があります。  
  
-   次の追加トピックを確認し、システムとバージョンの要件を理解してください。  
  
     [SharePoint 2010 ファームで SQL Server BI 機能を使用するためのガイド](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
## <a name="steps"></a>手順  
 このトピックの手順では、SharePoint ファームの管理者がサーバーをインストールして構成すると想定しています。 この図は標準的な 3 層環境を示しています。次に、図の番号付き項目の説明を示します。  
  
-   (1) 複数の Web フロントエンド (WFE) サーバー。 WFE サーバーには、SharePoint 2010 用の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインが必要です。 次の手順では、この層に 2 つ目のアプリケーション サーバーを追加します。  
  
-   (2) [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] と Web サイトを実行している 2 つのアプリケーション サーバー。たとえば、サーバーの全体管理などです。  
  
-   (3) 2 つの SQL Server データベース サーバー。  
  
-   (4) ソフトウェアまたはハードウェアのネットワーク負荷分散ソリューション (NLB) を表します。  
  
 ![SSRS を新しい SharePoint WFE に追加する](../../../2014/sql-server/install/media/rs-sharepointscale-wfe.gif "SSRS を新しい SharePoint WFE に追加する")  
  
 次の手順では、管理者がサーバーをインストールして構成すると想定しています。  
  
|手順|説明とリンク|  
|----------|--------------------------|  
|SharePoint 2010 製品準備ツールを実行します。|SharePoint 2010 のインストール メディアが必要です。 準備ツールはインストール メディアの **PrerequisiteInstaller.exe** です。|  
|SharePoint 2010 製品をインストールします。|1) 選択、**サーバー ファーム**インストールの種類。<br /><br /> 2) 選択**完了**サーバーの種類。<br /><br /> 3) 既存の SharePoint ファームに SharePoint 2010 SP1 がインストールされている場合は、インストールが完了したときに SharePoint 製品構成ウィザードを実行しないでください。 SharePoint 製品構成ウィザードを実行する前に SharePoint SP1 をインストールする必要があります。|  
|SharePoint Server 2010 SP1 をインストールします。|既存の SharePoint ファームに SharePoint 2010 SP1 インストールをダウンロードしてから、SharePoint 2010 SP1 をインストールする場合:[https://support.microsoft.com/kb/2460045](https://go.microsoft.com/fwlink/p/?linkID=219697)します。<br /><br /> SharePoint 2010 SP1 の詳細については、「 [Office 2010 SP1 および SharePoint 2010 SP1 インストール時の既知の問題](https://support.microsoft.com/kb/2532126)」を参照してください。|  
|SharePoint 製品の構成ウィザードを実行して、ファームにサーバーを追加します。|1) で、 **Microsoft SharePoint 2010 製品**プログラム グループで、をクリックして**Microsoft SharePoint 2010 製品構成ウィザード**します。<br /><br /> 2)、**サーバー ファームへの接続**選択ページ**既存ファームへの接続** をクリック**次**。<br /><br /> 3)、**構成データベースの設定の指定** ページで、既存のファーム構成データベースの名前を使用するデータベース サーバーの名前を入力します。 **[次へ]** をクリックします。<br />**&#42;&#42;重要な&#42; &#42;** で SQL Server ネットワーク構成に対してどのようなプロトコルが有効になっている確認し、次のようなエラー メッセージが表示アクセス許可があることを確認する場合は、 **Sql ServerConfiguration Manager**します。 "データベース サーバーへの接続に失敗しました。 確認してください、データベースが存在する、それが Sql Server、およびサーバーにアクセスする適切なアクセス許可がある。"<br />**&#42;&#42;重要な&#42; &#42;** ページが表示された場合**サーバー ファーム製品と修正プログラムの状態**、ページの情報を確認しへの参加を続行する前に、必要なファイルでサーバーを更新する必要がありますファームにサーバー。<br /><br /> 4)、**ファームのセキュリティ設定の指定**ページは、ファームのパスフレーズを入力し、をクリックして**次**します。 確認ページで **[次へ]** をクリックして、ウィザードを実行します。<br /><br /> 5) クリック**次**を実行する、**ファーム構成ウィザード**します。|  
|サーバーが SharePoint ファームに追加されたことを確認します。|1) SharePoint サーバーの全体管理で、 **[システム設定]** の **[このファームのサーバーの管理]** をクリックします。<br /><br /> 2) 新しいサーバーが追加され、状態が正しいことを確認します。<br /><br /> このサーバーを WFE ロールから削除するには 3) をクリックして**サービス サーバーの管理**サービスを停止および**Microsoft SharePoint Foundation Web アプリケーション**。|  
|インストール、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 2010 製品用アドイン。|アドインをインストールするには、いくつかの方法があります。 次の手順では、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] セットアップ ウィザードを使用します。 アドインをインストールする方法の詳細については、次を参照してください。[インストールまたは SharePoint 用 Reporting Services アドインのアンインストール&#40;SharePoint 2010 および SharePoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)します。 実行[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]インストール。<br /><br /> 1) **[セットアップ ロール]** ページで、 **[SQL Server 機能のインストール]** を選択します。<br /><br /> 2)、**機能の選択**] ページで、[ **Reporting Services アドインを SharePoint 製品用**<br /><br /> 3) をクリックして**次**セットアップ オプションを完了する次のいくつかのページにします。<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]の詳細については、「 [SharePoint 2010 用 Reporting Services の SharePoint モードのインストール](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)」を参照してください。|  
|新しいサーバーが稼働することを確認します。|1) SharePoint サーバーの全体管理で、 **[システム設定]** の **[このファームのサーバーの管理]** をクリックします。<br /><br /> 2) 新しいサーバーが一覧に含まれていることを確認します。|  
|NLB ソリューションを更新します。|該当する場合は、ハードウェアまたはソフトウェア NLB 環境を更新し、新しいサーバーを環境に含めます。|  
  
## <a name="see-also"></a>参照  
 [追加の Web またはアプリケーション サーバーをファーム (SharePoint Server 2010)](https://technet.microsoft.com/library/bb218968.aspx?missingurl=%2fen-us%2flibrary%2fe1aeaddf-6ee4-43a9-82b7-db20b68c71db\(Office.14\))   
 [サービス (SharePoint Server 2010) を構成します。](https://technet.microsoft.com/library/ee794878.aspx)  
  
  
