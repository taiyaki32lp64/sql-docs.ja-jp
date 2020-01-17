---
title: Reporting Services のサイト設定とサイト機能 (SharePoint モード) | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 73d357b6a601265df5e579f1b6acaff6ce8d648d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580455"
---
# <a name="reporting-services-site-settings-and-site-features-sharepoint-mode"></a>Reporting Services のサイト設定とサイト機能 (SharePoint モード)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Reporting Services の SharePoint モードには、SharePoint の [サイトの設定] ページから管理できるいくつかのサイト レベルのカスタム機能とサイト機能があります。 これらはサイト全体に対する設定で、すべての Reporting Services サービス アプリケーションに影響を与えます。 このページを表示するには、コンテンツ マネージャーとシステム管理者の権限が必要です。  

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。

|サイトの設定|[説明]|  
|------------------|-----------------|  
|Reporting Services のサイト設定|このトピックで説明するサイト全体の設定。|  
|データ警告の管理|データ警告機能の管理。|  
|レポート サーバー ファイル同期|既定では非アクティブ化されているサイト レベルの機能。<br /><br /> ドキュメント ライブラリ内でファイルが直接追加または更新された場合に、SharePoint ドキュメント ライブラリのレポート サーバー ファイル (.rdl、.rsds、.smdl、.rsd、.rsc、および .rdlx) をレポート サーバーと同期します。<br /><br /> 詳しくは、「 [SharePoint サーバーの全体管理でレポート サーバーのファイル同期機能をアクティブにする](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)」をご覧ください。|  
  
## <a name="open-the-reporting-services-site-settings-page"></a>[Reporting Services のサイト設定] ページを開く
  
1.  SharePoint サイトの **[サイトの操作]** メニューの **[サイトの設定]** を選びます。  
  
2.  **[Reporting Services]** セクションで、 **[Reporting Services のサイト設定]** を選びます。  
  
## <a name="options-for-reporting-services-site-settings"></a>[Reporting Services のサイト設定] のオプション
  
|オプション|[説明]|  
|------------|-----------------|  
|**RSClientPrint ActiveX コントロールのダウンロードの有効化**|このコントロールによって表示されるカスタム印刷ダイアログ ボックスでは、印刷プレビュー、特定のページや範囲を指定するためのページ選択、ページ余白、ページの向きなど、一般的な印刷ダイアログ ボックスの機能がサポートされています。 コントロールの詳細については、「 [カスタム アプリケーション内での RSClientPrint コントロールの使用](../../reporting-services/report-server-web-service/net-framework/using-the-rsclientprint-control-in-custom-applications.md)」をご覧ください。|  
|**ローカル モードでのリモート エラーを有効にします**|ローカル モードでの実行時にリモート コンピューターの詳細なエラー メッセージの表示と非表示を切り替えます。 次のようなエラー メッセージが表示される場合は、リモート エラーを有効にすると役立つことがあります。<br /><br /> `For more information about this error navigate to the report server on the local server machine or enable remote errors`|  
|**レポートのアクセシビリティ メタデータを有効にします**|レポートの HTML 出力でアクセシビリティ メタデータを有効にします。|  
|**データの視覚エフェクトをレポートのサイズに正確に合わせます**|Tablix 内でデータの視覚エフェクトが正確に調整されるように調整動作を構成します。 これには、グラフ、ゲージ、およびマップが含まれます。 この動作を無効にすると、データの視覚エフェクトをおおよそのサイズに合わせることになり、空白が残る場合があります。 この設定は、レポート ビューアー Web パーツの表示にのみ適用されます。 サーバー側の表示に対するこの動作を管理する場合は、**rsreportserver.config** ファイルを変更する必要があります。 詳細については、以下を参照してください。<br /><br /> [RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)<br /><br /> [RSReportServer.Config で表示拡張機能パラメーターをカスタマイズする](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)<br /><br /> [HTML デバイス情報設定](../../reporting-services/html-device-information-settings.md)<br /><br /> このオプションを有効にした場合は、正確なサイズを特定するために、おおよそのサイズに合わせる場合よりも処理に時間がかかることがあるため、パフォーマンスに影響する可能性があります。|  
  
## <a name="see-also"></a>参照

 [Reporting Services SharePoint サービス アプリケーションの管理](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
  
