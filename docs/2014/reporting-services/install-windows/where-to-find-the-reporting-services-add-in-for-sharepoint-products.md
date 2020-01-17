---
title: SharePoint 製品用 Reporting Services アドインの検索場所 | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- rsSharePoint
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 11/16/2015
ms.openlocfilehash: adee6ee7d0d769d8e87e228c475b224a3e78675b
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637873"
---
# <a name="where-to-find-the-reporting-services-add-in-for-sharepoint-products"></a>SharePoint 製品用 Reporting Services アドインの検索場所

SharePoint 製品およびテクノロジ (rsSharePoint.msi) 用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) アドインは Web からダウンロードでき、SharePoint で構築した配置にレポート サーバーを統合する機能を提供します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドイン、レポートサーバー、および SharePoint のサポートされている組み合わせの一覧については、「 [sharepoint のサポートされる組み合わせ」と「Reporting Services サーバーとアドイン&#40;SQL Server 2014&#41;](supported-combinations-of-sharepoint-and-reporting-services-server.md)」を参照してください。  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SharePoint 製品用 Reporting Services アドイン  
 アドインをダウンロードしてインストールするには、以下の [!INCLUDE[msCoName](../../includes/msconame-md.md)] ダウンロード センターを参照してください。  
  
-   [Microsoft SharePoint 用 Microsoft® SQL Server® 2014 Reporting Services アドイン](https://www.microsoft.com/download/details.aspx?id=53162)  
  
 このアドインの [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] バージョンは、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] インストール ウィザードでも提供されます。  
  
-   セットアップ ウィザードの **[機能の選択]** ページで、 **[SharePoint 製品用 Reporting Services アドイン]** を選択します。  
  
-   コマンド プロンプトでのインストールから、 **RS_SHPWFE** オプションを使用してアドインをインストールします。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コマンドプロンプトのインストールの詳細については、「 [Reporting Services SharePoint モードとネイティブモードのコマンドプロンプトインストール](install-reporting-services-at-the-command-prompt.md)」を参照してください。  
  
##  <a name="bkmk_sql11sp1"></a> [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] SharePoint 製品用 Reporting Services アドイン  
 アドインとレポート サーバーの [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] バージョンには、SharePoint Server 2013 のサポートが追加されます。  
  
 アドインをダウンロードしてインストールするには、以下の [!INCLUDE[msCoName](../../includes/msconame-md.md)] ダウンロード センターを参照してください。  
  
-   **SP1 アドイン:**  [Microsoft® SQL Server® 2012 SP1 Reporting Services Add-in for Microsoft® SharePoint®](https://www.microsoft.com/download/details.aspx?id=35583)(https://www.microsoft.com/download/details.aspx?id=35583)。  
  
-   **SP1:**  [Microsoft® SQL Server® 2012 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=35575) (https://www.microsoft.com/download/details.aspx?id=35575)。  
  
##  <a name="bkmk_sql11"></a> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SharePoint 2010 製品用 Reporting Services アドイン  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] リリースから、アドインは [機能の選択] ページで SQL Server インストール ウィザードの一部としてインストールできるようになりました。 アドインを別途ダウンロードしてインストールする場合、このファイルの最新バージョンは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ダウンロード センターの「 [Microsoft® SharePoint® テクノロジ 2010 用 Microsoft® SQL Server® 2012 Reporting Services アドイン](https://go.microsoft.com/fwlink/?LinkID=207242) 」ページからオンラインで入手できます。  
  
##  <a name="bkmk_sql2008r2"></a>SharePoint 2010 製品用 SQL Server 2008 R2 Reporting Services アドイン  
 Microsoft SharePoint 2010 製品用 Microsoft SQL Server 2008 R2 Reporting Services アドインは、SharePoint 2010 製品準備ツール (**PreRequisiteInstaller.exe**) によってインストールされます。 アドインを別途ダウンロードしてインストールする場合、このファイルの最新バージョンは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ダウンロード センターの「 [Microsoft SharePoint テクノロジ 2010 用 SQL Server 2008 R2 Reporting Services アドイン](https://www.microsoft.com/download/details.aspx?id=622)」ページからオンラインで入手できます。  
  
> [!TIP]  
>  これを、Cumulative Update #8 以降を含む SQL Server 2008 Service Pack 1 (SP1) と使用する場合は、「 [SQL Server 2008 SP2 Report Servers と SharePoint 2010 の統合](https://technet.microsoft.com/library/ff946055%28SQL.100%29.aspx)」の「SharePoint 2010 統合での既知の問題」を確認してください。  
  
##  <a name="bkmk_sql2008sp2"></a>SQL Server 2008 SP2 Reporting Services SharePoint 2007 の製品およびテクノロジ用アドイン  
 Microsoft SQL Server 2008 SP2 Reporting Services アドインは、SharePoint 2007 製品と 2008 R2 レポート サーバーの統合のサポートを追加する 2008 アドインの更新バージョンです。  
  
 このファイルの最新バージョンは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ダウンロード センターの「 [Microsoft SharePoint テクノロジ用 Microsoft SQL Server 2008 SP2 Reporting Services アドイン](https://www.microsoft.com/download/details.aspx?id=793)」ページからオンラインで入手できます。  
  
##  <a name="bkmk_sql2008"></a>SharePoint 2007 製品およびテクノロジ用 SQL Server 2008 Reporting Services アドイン  
 Microsoft SharePoint テクノロジ用 Microsoft SQL Server 2008 Reporting Services アドインは、Windows SharePoint Services 3.0 または Microsoft Office SharePoint Server 2007 で構築した配置内でレポート サーバーを実行するための機能を提供します。  
  
 このファイルの最新バージョンは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ダウンロード センターの「 [Microsoft SharePoint テクノロジ用 Microsoft SQL Server 2008 Reporting Services アドイン](https://www.microsoft.com/download/details.aspx?id=622)」ページからオンラインで入手できます。  
  
## <a name="see-also"></a>参照  
 [Sharepoint &#40;2010 および sharepoint 2013&#41;用の Reporting Services アドインのインストールまたはアンインストール](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [SharePoint 統合モード&#40;&#41;のライブラリ Reporting Services にレポートサーバーのコンテンツの種類を追加](../add-reporting-services-content-types-to-a-sharepoint-library.md)   
 [Reporting Services アドインをアンインストールした後は、既定以外のゾーンで SharePoint ページを参照することはできません。](https://support.microsoft.com/kb/2009212)  
  
  
