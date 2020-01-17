---
title: SharePoint サーバーの全体管理でレポート サーバー ファイル同期機能をアクティブ化 |Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 03/06/2017
ms.openlocfilehash: 762cf7e67a9983c345b58d2afd1c47da93306bd0
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67413142"
---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint-central-administration"></a>SharePoint サーバーの全体管理でレポート サーバーのファイル同期機能をアクティブにする

[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバー ファイル同期機能では、SharePoint イベント ハンドラーを利用して、レポート サーバー カタログをドキュメント ライブラリのアイテムと同期します。 この機能は、ユーザーがパブリッシュされたレポート アイテムを SharePoint ドキュメント ライブラリに頻繁に直接アップロードする場合に役立ちます。 ファイル同期機能がアクティブになって、コンテンツは引き続き頻繁ではなく同期します。  
  
ファイル同期機能は、SharePoint 製品用 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] アドインをインストールしてから SharePoint サイトの管理でアクティブ化できます。  
  
この機能は、サイトごとに手動でアクティブ化および非アクティブ化できますが、サイト コレクション レベルではアクティブ化および非アクティブ化することはできません。  
  
## <a name="prerequisites"></a>前提条件  
 SharePoint 用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインをインストールする必要があります。 アドインがインストールされていない場合は、ファイル同期機能がサイト機能の一覧に表示されません。  
  
 インストールを確認するには、 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows の **コントロール パネル**でインストール済みアプリケーションの一覧を表示します。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインがインストールされている場合は、このトピックの手順に従ってレポート サーバー ファイル同期機能をアクティブ化できます。  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>サイトの Reporting Services ファイル同期機能をアクティブ化または非アクティブ化するには  
  
1.  サイトのメイン ページでをクリックして、**サイトの操作**メニューをクリックします**サイト設定**します。  
  
2.  **サイトの操作**、 をクリックして**サイト機能の管理**します。  
  
3.  一覧で **[レポート サーバー ファイル同期]** を見つけます。  
  
4.  **[アクティブ化]** をクリックします。  
  
> [!NOTE]  
>  レポート サーバー ファイル同期機能を非アクティブ化するには、 **[非アクティブ化]** をクリックする点を除き、同じ手順を実行します。  
  
## <a name="see-also"></a>参照  
 [レポート パーツのトラブルシューティング&#40;レポート ビルダーおよび SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [SharePoint でのレポート サーバーと Power View の統合機能のアクティブ化](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [インストールまたはアンインストール、Reporting Services アドイン、SharePoint の&#40;SharePoint 2010 および SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [インストールまたはアンインストール、Reporting Services アドイン、SharePoint の&#40;SharePoint 2010 および SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
