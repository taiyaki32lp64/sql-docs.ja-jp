---
title: レポート サーバー サービスの開始と停止 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- stopping Report Server service
- Report Server Windows service, starting
- Report Server service, starting
- starting Report Server service
ms.assetid: 6ec69ac3-27b0-472d-91e1-733af9078ed2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bef23ec8291be1a1eeab8796a00e45487b82f60c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103166"
---
# <a name="start-and-stop-the-report-server-service"></a>Start and Stop the Report Server Service
  レポート サーバーは、レポート サーバー Web サービス、レポート マネージャー、およびバックグラウンド処理アプリケーションを含んだ Windows サービスとして実装されます。 レポート サーバーのなんらかの機能を使用するには、このサービスが実行されている必要があります。 このサービスを停止すると、すべてのレポート サーバー処理が停止されます。  
  
 このサービスが停止している間は、スケジュール設定されたレポートやサブスクリプション処理 (つまり、サービスが実行されていれば、本来発生するはずの処理) に対する要求はキューに追加されます。 これは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行するジョブによって、イベントが作成されるためです。 サービスの停止中に処理のバックログが蓄積されないようにする場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントも停止してください。  
  
 レポート サーバー サービスの開始および停止には、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツール、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャー、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows で提供されるサービス ツールなどさまざまなツールを使用できます。  
  
 サービス アカウントの変更など、サービスの開始および停止以外の操作を行うには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用する必要があります。 他のツールでサービス アカウントを変更すると、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストールが壊れる可能性があります。 詳細については、 [レポート サーバー サービス アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)」を参照してください。  
  
 サービスを一時停止および再開することはできません。 また、開始パラメーターはありません。 明示的な依存関係はありませんが、レポート サーバー上のサブスクリプションまたはスケジュールされた操作をサポートする場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントも実行している必要があります。  
  
### <a name="to-start-or-stop-the-service-using-the-reporting-services-configuration-tool"></a>Reporting Services 構成ツールを使用してサービスを開始または停止するには  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを起動して、レポート サーバーに接続します。  
  
2.  [レポート サーバーの状態] ページで、 **[停止]** または **[開始]** をクリックします。  
  
### <a name="to-start-or-stop-the-service-using-services-in-administrative-tools"></a>管理ツールの [サービス] を使用してサービスを開始または停止するには  
  
-   [管理ツール] の [サービス] を開きます。次に、 **[SQL Server Reporting Services (MSSQLSERVER)]** を右クリックし、 **[停止]** または **[再起動]** をクリックします。  
  
 複数のインスタンスを実行しているか、レポート サーバーが名前付きインスタンスとして実行されている場合は、かっこ内のインスタンス名が、停止または再起動するレポート サーバー インスタンスに対応していることを確認してください。  
  
### <a name="to-start-or-stop-the-service-using-sql-server-configuration-manager"></a>SQL Server 構成マネージャーを使用してサービスを開始または停止するには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを起動します。  
  
2.  [SQL Server のサービス] を選択し、 **[SQL Server Reporting Services]** を右クリックして、 **[停止]** または **[再起動]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
