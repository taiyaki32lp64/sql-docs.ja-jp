---
title: レポート ビルダー (レポート ビルダー) の起動 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Builder, launching
- launching Report Builder
- SharePoint integration [Reporting Services], starting Report Builder
- starting Report Builder
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6fc123be862320cd35ccf4aec76d8bc9cf7877af
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107598"
---
# <a name="start-report-builder-report-builder"></a>レポート ビルダーの起動 (レポート ビルダー)
  [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] スタンドアロンが含まれていますと[!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)]レポート ビルダーのバージョン。 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] バージョンは、ネイティブ モードまたは SharePoint 統合モードでインストールされた [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] と共に使用できます。  
  
> [!NOTE]  
>  レポート ビルダーは、Itanium 64 ベースのコンピューターにはインストールできません。 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] バージョンおよびスタンドアロン バージョンのレポート ビルダーの場合も同様です。  
  
 場合、[!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)]表示されるレポート ビルダーのバージョンが以前のバージョンのレポート ビルダーを使用するには、レポート マネージャーおよび SharePoint サイトに更新できるユーザー、管理者に問い合わせて、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]レポート ビルダーのバージョン  
  
 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] バージョンのレポート ビルダーを使用して、SharePoint にパブリッシュされている [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] ブックについてのレポートを作成することもできます。 レポート ビルダーの使用の詳細については[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]を参照してください[PowerPivot データを Reporting Services レポートの作成](https://go.microsoft.com/fwlink/?LinkId=185238)technet.microsoft.com します。  
  
 レポート ビルダー スタンドアロンを起動する、**開始**メニューで、ローカル コンピューター、ユーザーまたは管理者は、ツールを使用するには前に、コンピューターに直接のレポート ビルダーをインストールする必要があります。 スタンドアロン バージョンは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインストール時にインストールされません。別途ダウンロードして、インストールする必要があります。 レポート ビルダーをダウンロードするには、次を参照してください。 [Microsoft® SQL Server® 2012 レポート ビルダー](https://go.microsoft.com/fwlink/?LinkId=401502)します。  
  
### <a name="to-start-report-builder-clickonce-from-report-manager"></a>レポート マネージャーからレポート ビルダー ClickOnce を起動するには  
  
1.  Web ブラウザーで、アドレス バーにレポート サーバーの URL を入力します。 既定の URL は http://\<*servername*>/reports です。 レポート マネージャーが開きます。  
  
2.  **[レポート ビルダー]** をクリックします。  
  
     レポート ビルダーが開き、レポート サーバー上でレポートを作成したり、レポートを開いたりできます。  
  
### <a name="to-start-report-builder-clickonce-using-a-url"></a>URL を使用してレポート ビルダー ClickOnce を起動するには  
  
1.  Web ブラウザーでアドレス バーに次の URL を入力します。  
  
     http://\<servername>/reportserver/reportbuilder/ReportBuilder_3_0_0_0.application  
  
2.  Enter キーを押します。  
  
     レポート ビルダーが開き、レポート サーバー上でレポートを作成したり、レポートを開いたりできます。  
  
### <a name="to-start-report-builder-clickonce-in-sharepoint-integrated-mode"></a>レポート ビルダー ClickOnce を SharePoint 統合モードで起動するには  
  
1.  目的のライブラリがある SharePoint サイトに移動します。  
  
2.  ライブラリを開きます。  
  
3.  **[ドキュメント]** をクリックします。  
  
4.  **[新しいドキュメント]** メニューの **[レポート ビルダー レポート]** をクリックします。  
  
     レポート ビルダーが開き、レポート サーバー上でレポートを作成したり、レポートを開いたりできます。  
  
     **注**場合、**新しいドキュメント**メニューに表示されない、**レポート ビルダー レポート**、**レポート ビルダーのモデル**、および**レポートのデータソース**オプション、そのコンテンツの種類を SharePoint ライブラリに追加する必要があります。 詳細については、次を参照してください[追加レポート サーバー コンテンツ タイプをライブラリに&#40;Reporting Services SharePoint 統合モードで&#41;](../add-reporting-services-content-types-to-a-sharepoint-library.md)で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][オンライン ブックの「](https://go.microsoft.com/fwlink/?LinkId=154888)で。msdn.microsoft.com します。  
  
### <a name="to-start-report-builder-stand-alone-from-the-start-menu"></a>[スタート] メニューからレポート ビルダー スタンドアロンを起動するには  
  
1.  [スタート] メニューで、次のようにクリックします。**すべてのプログラム**、 をクリックし、 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] **レポート ビルダー**します。  
  
2.  **[レポート ビルダー]** をクリックします。  
  
     レポート ビルダーが開き、レポートを作成したり、レポートを開いたりできます。  
  
3.  新しいレポートを作成するには、レポート ビルダーの左上隅の SQL Server アイコンをクリックし、[新規作成] をクリックします。  
  
4.  ローカル コンピューターまたはレポート サーバーに保管された既存のレポートを開くには、左上隅の SQL Server アイコンをクリックし、[開く] をクリックします。  
  
     既存のサーバーの一覧で、レポート サーバーが表示されない場合は閉じます、**レポートを開く** ダイアログ ボックスをクリック**Connect**サーバーに接続するレポート ビルダーの下部にあります。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2014 のレポート ビルダー](report-builder-in-sql-server-2016.md)  
  
  
