---
title: SSRS サービス アプリケーションを使用するためのサブスクリプションと警告の準備 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Shared Service
- SharePoint Mode [Reporting Services]
- SharePoint Mode
- Reporting Services Service Application
- SSRS service application
ms.assetid: d0de3f1f-4887-47fb-bacf-46aaad74c4be
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 69724baa3790f2b7475369c8f947a4201bcd57f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108720"
---
# <a name="provision-subscriptions-and-alerts-for-ssrs-service-applications"></a>SSRS サービス アプリケーションを使用するためのサブスクリプションと警告の準備
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のサブスクリプションとデータ警告を利用するには、SQL Server エージェントが必要です。また、SQL Server エージェントに対する権限を構成する必要もあります。 SQL Server エージェントが実行中であるにもかかわらず、SQL Server エージェントが必要であることを示すエラー メッセージが表示された場合は、権限を更新または確認してください。 このトピックでは、SharePoint モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を対象とし、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サブスクリプションを使用して SQL Server エージェントの権限を更新する 3 つの方法について説明します。 このトピックの手順で使用する資格情報には、サービス アプリケーション データベース、msdb データベース、および master データベースのオブジェクトに対する実行権限を RSExecRole に許可するための十分な権限が必要です。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010|  
  
 ![サービス アプリケーション データベースへの SQL エージェント アクセス許可](../../../2014/sql-server/install/media/rs-provisionsqlagent.gif "サービス アプリケーション データベースへの SQL エージェント アクセス許可")  
  
||説明|  
|------|-----------------|  
|**1**|Reporting Services サービス アプリケーション データベースをホストしている SQL Server データベース エンジンのインスタンス。|  
|**2**|SQL データベース エンジンのインスタンスに対応する SQL Server エージェントのインスタンス。|  
|**3**|Reporting Services サービス アプリケーション データベース。 名前は、サービス アプリケーションの作成時に使用された情報に基づいて付けられます。 データベース名の例を次に示します。<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0_Alerting<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0TempDB|  
|**4**|SQL Server データベース エンジンのインスタンスの master および MSDB データベース。|  
  
 権限を更新するには、次の 3 つの方法のいずれかを使用してください。  
  
1.  **[サブスクリプションと警告の準備]** ページで資格情報を入力し、 **[OK]** をクリックします。  
  
2.  [サブスクリプションと警告の準備] ページの **[スクリプトのダウンロード]** をクリックして、権限の構成に使用できる Transact-SQL スクリプトをダウンロードします。  
  
3.  PowerShell コマンドレットを実行して、権限の構成に使用できる Transact-SQL スクリプトを作成します。  
  
### <a name="to-update-permissions-using-the-provision-page"></a>準備ページを使用して権限を更新するには  
  
1.  SharePoint サーバーの全体管理で、 **[アプリケーション構成の管理]** の **[サービス アプリケーションの管理]** をクリックします。  
  
2.  リストからサービス アプリケーションを探し、アプリケーションの名前をクリックするか、または **[種類]** 列をクリックしてサービス アプリケーションを選択し、SharePoint リボンで **[管理]** ボタンをクリックします。  
  
3.  **[Reporting Services アプリケーションの管理]** ページで、 **[サブスクリプションと警告の準備]** をクリックします。  
  
4.  SharePoint 管理者がマスター データベースとサービス アプリケーション データベースに対する十分な権限を持っている場合は、それらの資格情報を入力します。  
  
5.  **[OK]** をクリックします。  
  
##  <a name="bkmk_download"></a> Transact-SQL スクリプトをダウンロードするには  
  
1.  SharePoint サーバーの全体管理で、 **[アプリケーション構成の管理]** の **[サービス アプリケーションの管理]** をクリックします。  
  
2.  リストからサービス アプリケーションを探し、アプリケーションの名前をクリックするか、または **[種類]** 列をクリックしてサービス アプリケーションを選択し、SharePoint リボンで **[管理]** ボタンをクリックします。  
  
3.  **[Reporting Services アプリケーションの管理]** ページで、 **[サブスクリプションと警告の準備]** をクリックします。  
  
4.  **[状態の表示]** 領域で、SQL Server エージェントが実行中であることを確認します。  
  
5.  **[スクリプトのダウンロード]** をクリックして、SQL Server Management Studio 内で実行することにより権限を構成できる Transact-SQL スクリプトをダウンロードします。 作成されるスクリプト ファイル名には、Reporting Services サービス アプリケーションの名前が使用されます (例: **[サービス アプリケーションの名前]** -GrantRights.sql)。  
  
### <a name="to-generate-the-transact-sql-statement-with-powershell"></a>PowerShell を使用して Transact-SQL ステートメントを生成するには  
  
1.  SharePoint 2010 管理シェルで Windows PowerShell コマンドレットを使用して、Transact-SQL スクリプトを作成することもできます。  
  
2.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** をクリックします。  
  
3.  展開**Microsoft SharePoint 2010 製品**クリック**SharePoint 2010 管理シェル**します。  
  
4.  次の PowerShell コマンドレットの、レポート サーバー データベース名、アプリケーション プール アカウント、およびステートメント パスを置き換えます。  
  
     **コマンドレットの構文:** `Get-SPRSDatabaseRightsScript -DatabaseName <ReportingServices database name> -UserName <app pool account> -IsWindowsUser | Out-File <path of statement>`  
  
     **サンプル コマンドレット:** `Get-SPRSDatabaseRightsScript -DatabaseName ReportingService_46fd00359f894b828907b254e3f6257c -UserName "NT AUTHORITY\NETWORK SERVICE" -IsWindowsUser | Out-File c:\SQLServerAgentrights.sql`  
  
## <a name="using-the-transact-sql-script"></a>Transact-SQL スクリプトの使用  
 次の手順は、準備ページからダウンロードしたスクリプトか、または PowerShell を使用して作成したスクリプトに対して使用できます。  
  
#### <a name="to-load-the-transact-sql-script-in-sql-server-management-studio"></a>SQL Server Management Studio に Transact-SQL スクリプトを読み込むには  
  
1.  SQL Server Management Studio を開くには、**開始** メニューのをクリックして**Microsoft SQL Server 2012**クリック**SQL Server Management Studio**。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスで、次のオプションを設定します。  
  
    -   **[サーバーの種類]** ボックスの一覧で、 **[データベース エンジン]** をクリックします。  
  
    -   **[サーバー名]** で、SQL Server エージェントの構成対象となる SQL Server インスタンスの名前を入力します。  
  
    -   認証モードを選択します。  
  
    -   SQL Server 認証を使用して接続する場合は、ログイン名とパスワードを入力します。  
  
3.  **[接続]** をクリックします。  
  
#### <a name="to-run-the-transact-sql-statement"></a>Transact-SQL ステートメントを実行するには  
  
1.  SQL Server Management Studio のツール バーで、 **[新しいクエリ]** をクリックします。  
  
2.  **[ファイル]** メニューの **[開く]** をポイントし、 **[ファイル]** をクリックします。  
  
3.  SharePoint 2010 管理シェルで生成した Transact-SQL ステートメントの保存先フォルダーに移動します。  
  
4.  ファイルをクリックし、 **[開く]** をクリックします。  
  
     ステートメントがクエリ ウィンドウに追加されます。  
  
5.  **[実行]** をクリックします。  
  
  
