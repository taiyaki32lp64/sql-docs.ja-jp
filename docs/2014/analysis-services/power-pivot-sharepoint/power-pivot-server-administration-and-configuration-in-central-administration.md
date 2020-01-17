---
title: サーバーの全体管理で PowerPivot サーバーの管理と構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2cdbfdc5-45a9-4000-a03d-318cc7ac8fe9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: de72001ced1b7e2690f90b2de4c59bb35aca6ce4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071111"
---
# <a name="powerpivot-server-administration-and-configuration-in-central-administration"></a>サーバーの全体管理での PowerPivot サーバーの管理と構成
  PowerPivot サーバーの管理および構成は、SharePoint サービス アプリケーションの管理者が SharePoint サーバーの全体管理を使用して実行します。  
  
 PowerPivot for SharePoint を使用するには、このコンポーネントがあらかじめ構成されている必要があります。 PowerPivot for SharePoint は、SQL Server セットアップを使用してインストールした後、次のいずれかの方法を使用して構成できます。  
  
-   PowerPivot 構成ツールまたは PowerPivot for SharePoint 2013 構成ツール  
  
-   SharePoint サーバーの全体管理  
  
-   PowerShell コマンドレット  
  
 3 つの方法はすべて、完全に構成されたサーバーを提供します。  
  
 ここでは、サーバーの全体管理を使用してソフトウェアを構成するタスクについて説明します。 少なくとも、以下に示す 3 つの必須の構成タスクをすべて実行する必要があります。  
  
> [!IMPORTANT]  
>  SharePoint 2010 の場合は、PowerPivot for SharePoint、または [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] データベース サーバーを使用する SharePoint ファームを構成する前に、SharePoint 2010 Service Pack 1 (SP1) をインストールする必要があります。 サービス パックをインストールしていない場合は、サーバーの構成を始める前にここでインストールしてください。  
  
## <a name="benefits-of-configuring-powerpivot-for-sharepoint-using-central-administration"></a>For SharePoint サーバーの全体管理を使用して PowerPivot を構成する利点  
 SharePoint サーバーの全体管理は、SharePoint ファームの管理アプリケーションです。 ファームの管理者は、PowerPivot for SharePoint インスタンスをファームに追加するときに、使い慣れたツールの使用を好む場合があります。  
  
 PowerPivot 構成ツールや PowerShell コマンドレットとは対照的に、サーバーの全体管理には、アプリケーションまたはサーバーの構成時に設定できるすべてのオプションを完全に指定するページがあります。 他の方法では、構成ワークフローがより少数の手順に圧縮されるか、PowerShell を使用して SharePoint サーバーを構成する方法に関する知識が事前に必要です。  
  
## <a name="related-content"></a>関連コンテンツ  
 [Windows PowerShell を使用した PowerPivot の構成](power-pivot-configuration-using-windows-powershell.md)  
  
 [PowerPivot 構成ツール](power-pivot-configuration-tools.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
|リンク|型|タスクの説明|  
|----------|----------|----------------------|  
|[SharePoint に PowerPivot ソリューションを配置します。](deploy-power-pivot-solutions-to-sharepoint.md)|必須|この手順では、プログラム ファイルとアプリケーション ページをファームとサイト コレクションに追加するソリューション ファイルをインストールします。|  
|[作成し、サーバーの全体管理で PowerPivot サービス アプリケーションを構成します。](create-and-configure-power-pivot-service-application-in-ca.md)|必須|この手順では、PowerPivot System サービスを準備します。|  
|[サーバーの全体管理のサイト コレクションの PowerPivot 機能の統合をアクティブ化します。](activate-power-pivot-integration-for-site-collections-in-ca.md)|必須|この手順では、サイト コレクション レベルで PowerPivot 機能を有効にします。|  
|[Excel Services で信頼できるデータ プロバイダーとして MSOLAP.5 を追加](add-msolap-5-as-a-trusted-data-provider-in-excel-services.md)|必須|この手順では、Analysis Services OLE DB プロバイダーを Excel Services の信頼できるプロバイダーとして追加します。|  
|[SharePoint 2010 での PowerPivot データ更新](../powerpivot-data-refresh-with-sharepoint-2010.md)|推奨|データの更新は省略可能ですが推奨されます。 発行された Excel ブックで PowerPivot データに自動更新をスケジュールできます。|  
|[構成、PowerPivot 自動データ更新アカウント&#40;PowerPivot for SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)|推奨|この手順では、サーバー上でデータの更新ジョブを実行するために使用できる特別な目的のアカウントを準備します。|  
|[使用状況データ収集の構成&#40;PowerPivot for SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)|省略可|使用状況データ コレクションは既定で構成されています。 これらの手順を使用して、既定の設定を変更できます。|  
|[データ更新専用またはクエリ専用処理構成&#40;PowerPivot for SharePoint&#41;](../configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)|省略可|PowerPivot インスタンスは、データ更新ジョブまたはクエリ専用にすることができます。 さらに、並列データ更新ジョブの既定の設定を変更できます。|  
|[PowerPivot サービス アカウントの構成](configure-power-pivot-service-accounts.md)|省略可|パスワードの更新とサービス アカウントの変更方法について説明します。|  
|[サーバーの全体管理での SharePoint Web アプリケーションへの PowerPivot サービス アプリケーションを接続します。](connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)|省略可|サービスの関連付けを変更する方法について説明します。|  
|[サーバーの全体管理で PowerPivot サイト用の信頼できる場所を作成します。](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)|省略可|PowerPivot ギャラリーを信頼できる場所として追加する方法について説明します。|  
|[SharePoint ログ ファイルと診断のログ記録構成し、表示&#40;PowerPivot for SharePoint&#41;](configure-and-view-sharepoint-and-diagnostic-logging.md)|省略可|イベントのログ記録は既定で構成されています。 これらの手順を使用して、既定の設定を変更できます。|  
|[PowerPivot の正常性ルール - 構成します。](configure-power-pivot-health-rules.md)|省略可|サーバーの正常性ルールは既定で構成されています。 これらの手順を使用して、既定の設定の一部を変更できます。|  
|[PowerPivot ギャラリーの作成およびカスタマイズ](create-and-customize-power-pivot-gallery.md)|省略可|インストールを手動で構成している場合は、この手順で、格納している PowerPivot ブックのサムネイル画像を示す PowerPivot ギャラリー ライブラリの作成方法を説明します。|  
|[BI セマンティック モデル接続のコンテンツ タイプをライブラリに追加&#40;PowerPivot for SharePoint&#41;](add-bi-semantic-model-connection-content-type-to-library.md)|省略可|BI セマンティック モデル接続ファイルの作成をサポートするようにドキュメント ライブラリを拡張する方法について説明します。|  
  
## <a name="see-also"></a>参照  
 [PowerPivot for SharePoint 2010 のインストール](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [構成設定のリファレンス&#40;PowerPivot for SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Powerpivot for SharePoint の災害復旧](https://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
