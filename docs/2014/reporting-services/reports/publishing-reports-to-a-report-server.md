---
title: レポート サーバーへのレポートのパブリッシュ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- production environments [Reporting Services]
- report projects [Reporting Services]
- Debug configuration [Reporting Services]
- report publishing [Reporting Services]
- publishing reports [Reporting Services]
- report properties [Reporting Services]
- Report Designer [Reporting Services], deploying reports
- Production configuration [Reporting Services]
- publishing reports [Reporting Services], production environments
- DebugLocal configuration [Reporting Services]
- deploying [Reporting Services], reports
- Report Designer [Reporting Services], publishing reports
ms.assetid: bd7aa5e0-61ce-43fd-8f74-5d1aeed078bb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5c73e75bbdf458b27d0f879a91e72ececc832b88
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102492"
---
# <a name="publishing-reports-to-a-report-server"></a>レポート サーバーへのレポートのパブリッシュ
  1 つまたは複数のレポートのデザインおよびテストが完了したら、[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] の組み込みの配置機能を使用してレポート サーバーにレポートをパブリッシュします。 個々のレポートまたはレポート サーバー プロジェクトをパブリッシュできます。 複数のレポートをパブリッシュする最も簡単な方法は、レポート サーバー プロジェクトをパブリッシュする方法です。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 用語を使用して*デプロイ*、用語ではなく*発行*。 この 2 つの用語は同義です。  
  
 レポートをパブリッシュするには、そのための権限が必要です。 この権限は、レポート サーバー管理者が定義するロールベースのセキュリティによって決まります。 パブリッシュ操作は、通常、パブリッシャー ロールを介して許可されます。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] では、レポートのパブリッシュを管理するためのプロジェクト構成が提供されます。 構成では、レポート サーバーの場所、レポート サーバーにインストールされている SQL Server Reporting Services のバージョンのほか、レポートにパブリッシュされたデータ ソースは上書きされるかどうかなどが指定されます。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] が提供する構成を使用する他に、構成を追加作成することもできます。  
  
## <a name="project-configurations"></a>プロジェクトの構成  
 有効なレポート定義のみがレポート サーバーにパブリッシュされるように、レポートはパブリッシュされる前にビルドされます。 プロジェクト構成には、ビルド レポートを一時的に保存するフォルダー、ビルドの問題の対処方法など、レポートをビルドするためのプロパティが含まれます。 構成には、レポート サーバーの場所やバージョン、レポート サーバー上のフォルダーの指定に使用されるプロパティも含まれます。  
  
 既定では、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 3 つのプロジェクト構成を提供します。DebugLocal、Debug、およびリリースします。 既定の構成は DebugLocal です。 通常、DebugLocal 構成はローカル プレビュー ウィンドウでのレポートの表示に、Debug 構成はテスト サーバーへのレポートのパブリッシュに、Release 構成は実稼働サーバーへのレポートのパブリッシュに使用できます。 標準ツール バーの [ソリューション構成] ドロップダウン リストには、アクティブな構成が表示されます。 別の構成を使用するには、一覧からその構成を選択します。  
  
 ご使用のレポート環境に、複数のレポート サーバーが含まれる場合や異なるバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] がインストールされている場合は、 複数の構成を作成し、配置シナリオに応じて異なる構成を使用できます。 詳細については、次を参照してください。[配置およびバージョン サポートでは、SQL Server Data Tools &#40;SSRS&#41; ](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)と[配置プロパティを設定&#40;Reporting Services&#41;](../tools/set-deployment-properties-reporting-services.md)します。  
  
## <a name="publishing-reports"></a>レポートのパブリッシュ  
 単一のレポートだけでなく、複数のレポートが含まれるレポート サーバー プロジェクトをパブリッシュできます。 レポートのパブリッシュ方法については、次を参照してください。[レポートのパブリッシュ](../publish-reports.md)します。  
  
### <a name="publishing-a-single-report"></a>単一のレポートのパブリッシュ  
 プロジェクト内のすべてのレポートをパブリッシュしない場合、単一のレポートのみのパブリッシュを選択できます。 この操作を行うには、レポートを配置する構成 (たとえば、Release 構成など) を選択し、レポートを右クリックして、 **[配置]** をクリックします。  
  
 レポートが共有データ ソースを使用する場合は、共有データ ソースを配置する必要もあります。共有データ ソースを配置しないと、配置されたレポートが実行されません。 共有データ ソースを右クリックし、 **[配置]** をクリックします。  
  
 レポート サーバーのターゲット サーバー URL を指定する必要があります。レポートおよび共有データ ソースが配置される既定のフォルダーは変更できます。  
  
### <a name="publishing-multiple-reports"></a>複数のレポートのパブリッシュ  
 レポート サーバー プロジェクトをパブリッシュすると、そのプロジェクト内にあるすべてのレポートをパブリッシュできます。 すべてのレポートは、同じプロジェクト構成を使用して同じレポート サーバー、サーバー上の同じフォルダーというように配置されます。 異なるサーバーにレポートを配置するには、これらのレポートを 1 つずつパブリッシュするか、レポート サーバー プロジェクトに必要なレポートのみを含めます。 ソリューションには、複数のレポート サーバー プロジェクトを含めることができます。複数のプロジェクトを使用すると、異なる構成を使用してさまざまなプロジェクトを配置できるため、レポートの配置を簡単に管理できます。  
  
## <a name="see-also"></a>参照  
 [[プロパティ ページ] ダイアログ ボックス](../tools/project-property-pages-dialog-box.md)   
 [レポート サーバー コンテンツの管理 &#40;SSRS ネイティブ モード&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [レポートのアップグレード](../install-windows/upgrade-reports.md)  
  
  
