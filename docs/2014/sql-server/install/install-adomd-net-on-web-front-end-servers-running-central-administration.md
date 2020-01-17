---
title: サーバーの全体管理を実行している Web フロントエンドサーバーに ADOMD.NET をインストールする |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c2372180-e847-4cdb-b267-4befac3faf7e
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: f36e00a9393dcbdf1f8cbfe878b8382e6a8dac9d
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952151"
---
# <a name="install-adomdnet-on-web-front-end-servers-running-central-administration"></a>サーバーの全体管理を実行している Web フロントエンド サーバーに ADOMD.NET をインストールする
  Excel Services または PowerPivot for SharePoint がインストールされていない、サーバーの全体管理のトポロジを持つファームに PowerPivot for SharePoint をインストールするときに、PowerPivot 管理ダッシュボードの組み込みレポートへのフル アクセスが必要な場合は、Microsoft ADOMD.NET クライアント ライブラリをダウンロードしてインストールしてください。 ダッシュボードの一部のレポートでは、ADOMD.NET を使用して、ファームの PowerPivot クエリ処理およびサーバーの状態に関するレポート データを提供する内部データにアクセスします。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010  
  
 SharePoint 2013 では、プロバイダーは SQL Server 機能パックに含まれています。 SpPowerPivot .msi をダウンロードする方法の詳細については、「 [Microsoft SQL Server 2014 Feature Pack](https://www.microsoft.com/download/details.aspx?id=35577) 」を参照してください。  
  
### <a name="download-and-install-the-client-library"></a>クライアント ライブラリのダウンロードとインストール  
  
1.  [ [SQL Server 2014 Feature Pack] ページ](https://go.microsoft.com/fwlink/?LinkID=296473)で、Microsoft ADOMD.NET を見つけます。  
  
2.  `SQL_AS_ADOMD.msi` インストール プログラムの x64 パッケージをダウンロードします。  
  
3.  .Msi を実行して、ライブラリをインストールします。  
  
4.  インストールの完了後、IIS をリセットします。 管理コマンドプロンプトを開き、「 **IISRESET**」と入力します。  
  
### <a name="verify-installation"></a>インストールの確認  
  
1.  Windows\Assembly に移動します。  
  
2.  Microsoft.analysisservices.sharepoint.integration.dll を右クリックし、 **[プロパティ]** を選択します。  
  
3.  **[バージョン]** をクリックします。  
  
4.  バージョンに12.00 が含まれていることを確認します。ビルド番号 >\<、説明が Microsoft.analysisservice.adomdclient になります。  
  
## <a name="see-also"></a>参照  
 [PowerPivot 管理ダッシュボードと使用状況データ](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data)  
  
  
