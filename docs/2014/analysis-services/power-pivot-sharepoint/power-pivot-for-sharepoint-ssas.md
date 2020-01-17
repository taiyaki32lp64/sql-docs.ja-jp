---
title: PowerPivot for SharePoint (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c4c393d3-4856-47ac-ab5f-15da2f240d1d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ef00476e7c469a98532e58302c560c805669421d
ms.sourcegitcommit: 7183735e38dd94aa3b9bab2b73ccab54c916ff86
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2019
ms.locfileid: "74683588"
---
# <a name="powerpivot-for-sharepoint-ssas"></a>PowerPivot for SharePoint (SSAS)
  PowerPivot for SharePoint は、SharePoint モードで実行される [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーです。 PowerPivot for SharePoint は、SharePoint ファーム内の PowerPivot データのサーバー ホスティングを実現します。 PowerPivot データは、次のいずれかを使用して構築する分析データモデルです。  
  
-   PowerPivot for Excel 2010 アドイン  
  
-   Excel 2013  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]2013 |[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010  
  
 そのデータをサーバーでホストするには、SharePoint、Excel Services、および PowerPivot for SharePoint のインストールが必要です。 PowerPivot for SharePoint インスタンスにデータが読み込まれます。このデータは、PowerPivot データ更新機能を使用してスケジュール設定された間隔で更新できます。Excel 2010 ブックの場合はこの更新機能がサーバーで実行され、Excel 2013 ブックの場合は SharePoint 2013 Excel Services で実行されます。  
  
## <a name="powerpivot-for-sharepoint-2013"></a>PowerPivot for SharePoint 2013  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]で[!INCLUDE[msCoName](../../includes/msconame-md.md)]は、データモデルと Power View レポートを含む excel ブックの[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 2013 excel Services の使用がサポートされています。  
  
 SharePoint 2013 の Excel Services には、ブラウザー上で PowerPivot ブックを操作できるようにするためのデータ モデル機能が含まれます。 ファームに PowerPivot for SharePoint 2013 アドインを配置する必要はありません。 必要な操作は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーを SharePoint モードでインストールし、Excel Services の **[データ モデルの設定]** でサーバーを登録するだけです。  
  
 PowerPivot for SharePoint 2013 アドインを配置すると、SharePoint ファームで追加の機能を有効にすることができます。 追加の機能には、PowerPivot ギャラリー、データ更新のスケジュール、および PowerPivot 管理ダッシュボードがあります。  
  
 ![SSAS PowerPivot モード 2 のサーバー配置](../media/as-powerpivot-mode-2server-deployment.gif "SSAS PowerPivot モード 2 のサーバー配置")  
  
## <a name="powerpivot-for-sharepoint-2010"></a>PowerPivot for SharePoint 2010  
 PowerPivot for SharePoint 2010 は、SharePoint 2010 ファーム内の PowerPivot データのサーバー ホスティングを実現します。 PowerPivot データは、PowerPivot for Excel アドインを使用して Excel で構築する分析データ モデルです。 そのデータをサーバーでホストするには、SharePoint 2010、Excel Services、および PowerPivot for SharePoint のインストールが必要です。 ファーム内の PowerPivot for SharePoint インスタンスにデータが読み込まれます。このデータは、サーバーに用意されている PowerPivot データ更新機能を使用して、スケジュール設定された間隔で更新できます。  
  
### <a name="components-of-powerpivot-for-sharepoint-2010"></a>PowerPivot for SharePoint 2010 のコンポーネント  
 PowerPivot for SharePoint は、共有サービスとして実装されています。共有サービスとは、組み込みの機能とインフラストラクチャを使用して、PowerPivot サービス アプリケーションを管理、セキュリティ保護、および使用できることです。 サーバーとデータベースの検出、リダイレクト、および接続の管理はすべて、ファーム レベルで管理されます。 サーバーの全体管理には、サーバー ID、サーバーの状態、および構成プロパティの管理に使用するサービスへの管理インターフェイスが用意されています。  
  
 PowerPivot for SharePoint の配置全体には、SharePoint ファーム内の Excel および Excel Services と統合されるクライアント コンポーネントおよびサーバー コンポーネントが含まれます。 Excel ブック内の PowerPivot データは Analysis Services データベースであり、データの読み込みとクエリには、Analysis Services xVelocity メモリ内分析エンジン (VertiPaq) が必要です。 クライアント ワークステーションでは、xVelocity エンジンは Excel 内でインプロセスとして実行されます。 SharePoint ファームの Analysis Services は、アプリケーション サーバー上で実行され、関連サービスと組み合わされて、PowerPivot データに対する要求を処理します。 次の図は、PowerPivot クライアントとサーバー コンポーネントを示しています。  
  
 ![GMNI_GeminiArch2](../media/gmni-geminiarch2.gif "GMNI_GeminiArch2")  
  
 PowerPivot Web サービスは Web アプリケーション サーバー上で実行されます。 Web アプリケーションからの要求は、ファーム内の PowerPivot System サービス インスタンスにリダイレクトされます。  
  
 PowerPivot System サービスは、Analysis Services サーバーへの読み込み要求を発行します。キャッシュを実行したり、使用されなくなった際やシステム リソースに競合が発生した際にデータをアンロードしたりして、既にメモリに読み込まれているデータへの継続的な接続を管理します。 ユーザー利用状況の追跡も行います。 サーバーの状態データやその他の使用状況データは収集されてレポートに表示され、システム パフォーマンスを示します。  
  
 SharePoint 統合モードの Analysis Service サーバー インスタンスで、配置が完了します。 データの読み込み、クエリ、アンロードを行います。 ブックに PowerPivot データ更新が構成されている場合、データの処理も行います。  各インスタンスは、同じインストールに含まれるローカルの PowerPivot System サービスと緊密に連携します。  
  
##  <a name="bkmk_RelatedContent"></a>このセクションの説明  
 [サーバーの全体管理での PowerPivot サーバーの管理と構成](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [Windows PowerShell を使用した PowerPivot の構成](power-pivot-configuration-using-windows-powershell.md)  
  
 [PowerPivot 構成ツール](power-pivot-configuration-tools.md)  
  
 [PowerPivot の認証および承認](power-pivot-authentication-and-authorization.md)  
  
 [PowerPivot の正常性ルール - 構成](configure-power-pivot-health-rules.md)  
  
 [PowerPivot 管理ダッシュボードと使用状況データ](power-pivot-management-dashboard-and-usage-data.md)  
  
 [PowerPivot ギャラリー](../../2014-toc/index.yml)  
  
 [PowerPivot データ アクセス](power-pivot-data-access.md)  
  
 [PowerPivot データ更新](power-pivot-data-refresh.md)  
  
 [PowerPivot データフィード](power-pivot-data-feeds.md)  
  
 [PowerPivot BI セマンティックモデル接続 &#40;。 bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)  
  
 **その他のセクションの内容**  
  
## <a name="additional-topics"></a>関連トピック  
 [PowerPivot for SharePoint のアップグレード](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)  
  
 [PowerPivot for SharePoint 2013 のインストール](../instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
 [PowerShell リファレンス (PowerPivot for SharePoint)](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
 [SQL Server 2014 セルフサービスビジネスインテリジェンスのライセンストポロジとコストの例](../../sql-server/install/example-license-topologies-costs-self-service-business-intelligence.md)  
  
## <a name="see-also"></a>参照  
 [PowerPivot の計画と配置](https://go.microsoft.com/fwlink/?linkID=220972)   
 [PowerPivot for SharePoint の災害復旧](https://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
