---
title: レポートのパブリッシュ |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], publishing
- publishing reports [Reporting Services]
ms.assetid: ef5a514e-e818-4041-a8b0-15835f9a046b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 86ab056f18e69b0b264525377efb0d257ebc2b95
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108029"
---
# <a name="publish-reports"></a>レポートのパブリッシュ
  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]から、プロジェクトを配置してレポート サーバーにレポート サーバー プロジェクト内のすべてのレポートおよび共有データ ソースをパブリッシュしたり、単一のレポートをパブリッシュしたりできます。 レポートをパブリッシュする前に、ターゲット レポート サーバーの URL を指定する必要があります。 詳細については、「[配置プロパティを設定する (Reporting Services)](tools/set-deployment-properties-reporting-services.md)」を参照してください。  
  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] の [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] バージョンを使用すると、 [!INCLUDE[ssRSversion2005](../includes/ssrsversion2005-md.md)] と [!INCLUDE[ssRSversion10](../includes/ssrsversion10-md.md)] の両方のレポートを開くことや、変更、プレビュー、保存、およびパブリッシュを行うことができます。 詳細については、「 [SQL Server データ ツールの配置およびバージョン サポート (SSRS)](tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)には含まれていません。  
  
### <a name="to-publish-all-reports-in-a-project"></a>プロジェクトのすべてのレポートをパブリッシュするには  
  
-   **[ビルド]** メニューで **[\<レポート プロジェクト名> の配置]** をクリックします。 または、ソリューション エクスプローラーでレポート プロジェクトを右クリックして、 **[配置]** をクリックします。 パブリッシュ処理の状態が、[出力] ウィンドウに表示されます。  
  
    > [!NOTE]  
    >  レポート サーバー プロジェクトを配置すると、レポート プロジェクトの共有データ ソースも配置されます。  
  
### <a name="to-publish-a-single-report"></a>1 つのレポートをパブリッシュするには  
  
-   ソリューション エクスプローラーで、レポートを右クリックし、 **[配置]** をクリックします。 パブリッシュ処理の状態が、[出力] ウィンドウに表示されます。  
  
    > [!NOTE]  
    >  レポートをパブリッシュするときは、レポートが使用する共有データ ソースを配置する必要もあります。  
  
## <a name="see-also"></a>参照  
 [データ ソースとレポートのパブリッシュ](reports/publishing-data-sources-and-reports.md)   
 [レポートのプレビュー](reports/previewing-reports.md)   
 [レポート サーバーへのレポートのパブリッシュ](reports/publishing-reports-to-a-report-server.md)   
 [レポートの検索、表示、管理 (レポート ビルダーおよび SSRS)](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [レポートのエクスポート&#40;レポート ビルダーおよび SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
