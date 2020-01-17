---
title: SharePoint サイトのレポート ビューアー Web パーツ |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- Web Parts [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
ms.assetid: b6341a73-172f-4632-a9e9-cc79fed3f36b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ba8b23c800718d289b2a7a633d5244261b5ab8a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103049"
---
# <a name="report-viewer-web-part-on-a-sharepoint-site"></a>SharePoint サイトのレポート ビューアー Web パーツ
  レポート ビューアー Web パーツは、SharePoint 製品用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインによってインストールされるカスタム Web パーツです。 Web パーツを使用すると、統合モードで動作するように構成されたレポート サーバー上でレポートの表示、ナビゲーション、印刷、およびエクスポートを行うことができるようになります。 レポート ビューアー Web パーツは、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーによって処理されるレポート定義 (.rdl) ファイルに関連付けられます。 他のソフトウェア製品を使用して作成した他のレポート ドキュメントで、レポート ビューアー Web パーツを使用することはできません。  
  
 この Web パーツをインストールするには、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドイン用のセットアップを実行する必要があります。 Web パーツは個別にインストール/アンインストールしないでください。 Web パーツはアドインの一部であり、アドイン セットアップ パッケージを使用してのみインストールできます。 レポート ビューアー Web パーツのファイル名は、ReportViewer.dwp です。 このファイルは、Program Files\Common Files\Microsoft Shared\web server extensions\12\template\features\reportserver フォルダーに格納されています。このファイルを別のフォルダーに移動してはいけません。  
  
 Web パーツを使用するには、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインのインストールと構成が完了していて、SharePoint との統合用にレポート サーバーが構成されている必要があります。 ビューアーに表示するためのレポートも必要です。 開くことができるレポートは、ライブラリ、ライブラリ フォルダー、レポート履歴、またはライブラリ Web パーツからレポート ビューアー Web パーツへのリンクに含まれているレポートのみです。 カスタム リスト内のアイテムの添付ファイルとして保存されているレポートは開くことができません。  
  
 レポート ビューアー Web パーツのプロパティを設定すると、ツール バーや表示領域の外観を制御したり、Web パーツを特定のレポートにリンクしたりできます。 レポート ビューアーには、明示的にリンクが設定されたレポートか、開かれた任意の .rdl ファイルが表示されます。  
  
 複数のレポートを単独のレポート ビューアー インスタンスにリンクすることはできませんが、複数のレポートをグループ化したい場合は、複数のレポート ビューアー Web パーツ インスタンスが単独のページに埋め込まれたダッシュボードまたは Web パーツ ページを作成できます。  
  
 Web パーツには、表示領域、ツール バー、資格情報とパラメーターを設定するための折りたたみ可能な領域、およびプロパティが含まれます。 次の図に、サンプル Company Sales レポートを表示する Web パーツと、ツール バーから選択できるエクスポート オプションを示します。  
  
 ![レポート ビューアー Web パーツ](media/rs-sharepointrvwebpart.gif "レポート ビューアー Web パーツ")  
  
## <a name="web-part-components"></a>Web パーツのコンポーネント  
 表示領域には、HTML 形式でレポートが表示されます。 Web パーツの構成方法に応じて、表示領域を最大化してレポートをページ全体モードで表示することも、利用できる領域を隣接するペインおよびツール バーと共有することもできます。  
  
 ツール バーは、ページ ナビゲーション、検索、拡大/縮小機能に加え、他のアプリケーション形式でレポートを表示できるようにするエクスポート機能を提供します。 さらに、オプションで印刷機能も用意されているので、HTML レポートの印刷出力のページ割り当てや、ページ レイアウトおよび余白設定の変更が可能です。 **[レポート ビルダーで開く]、[サブスクライブ]**、 **[エクスポート]**、および **[印刷]** は、ツール バーの **[アクション]** メニューにあります。 ページ ナビゲーションと拡大/縮小のコントロールは、ツール バー上に直接配置されています。  
  
> [!NOTE]  
>  コードを記述しない限りツール バーをカスタマイズすることはできませんが、プロパティを設定することで、コントロールのすべてまたは一部を非表示にすることができます。  
  
### <a name="export-action-on-the-report-toolbar"></a>レポート ツール バーにおけるエクスポート アクション  
 **[アクション]** メニューの **[エクスポート]** では、レポート サーバー上に配置されている表示拡張機能に関連付けられたアプリケーション形式が表示されます。 特定の形式の可用性を決定するには、レポート サーバーの表示拡張機能を追加または削除するか、あるいは構成設定を変更して特定のエクスポート形式を一覧から削除できます。 レポート サーバーの構成設定を指定して、どの形式を使用可能にするかを制御することもできます。 表示拡張機能の構成設定を追加および変更することで、特定の形式の既定の動作を変更できます。  
  
### <a name="print-action-on-the-report-toolbar"></a>レポート ツール バーにおける印刷アクション  
 **[アクション]** メニューの **[印刷]** は、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]全体で提供されるカスタム印刷機能です。 **[印刷]** をクリックすると、ActiveX クライアント側印刷コントロールがクライアント コンピューターにダウンロードされます。 ほとんどの場合、 **[印刷]** をクリックするユーザーには、ローカル コンピューターに対する管理者権限が必要になります。 通常、ActiveX コントロールをダウンロードできるユーザーは、管理者権限を持つユーザーのみに制限するのが一般的です。 SharePoint サーバーの全体管理を使用して、有効または、クライアント側印刷コントロールのダウンロードを無効にすることができます。  
  
### <a name="find-action-on-the-report-toolbar"></a>レポート ツール バーにおける検索アクション  
 **[アクション]** メニューの **[検索]** は、レポート内の目的の場所に移動する手段を提供します。 検索する単語または語句を入力することで、レポート内を検索できます。 最大で 256 文字の文字列を検索できます。 レポート内で一致が見つかると、その値を含む部分にフォーカスが移動します。  
  
 検索する値を入力する際には、レポートで実際に使用されていることが予想される値を入力します。 「今月の平均利益は」のような質問は、この文字列がレポートに含まれていると予想できる場合を除いて不適切です。  
  
 一度に検索できる用語または値は 1 つだけです。 検索演算子 (`AND` や `OR` など)、記号、およびワイルドカードは使用できません。 複数のセクションにわたったデータは検索できません (たとえば、特定の製品のある月の純売上高を検索することはできません)。 このような分析を行うには、レポート ビルダーを使用してクリックスルー レポートを作成します。  
  
 レポート データへのアクセスを制限するデータベースとモデルのセキュリティ設定は、検索操作にも適用されます。 データ ソースにモデルを使用しているクリックスルー レポートで値を検索する場合に、そのモデルの一部にアクセス権限がないと、その部分に含まれるデータは検索対象外になります。  
  
### <a name="panes-for-specifying-credentials-and-parameters"></a>資格情報およびパラメーターを指定するためのペイン  
 **[資格情報]** と **[パラメーター]** は、表示領域の横に表示されるペインです。 **[資格情報]** は、データ ソースにアクセスする権限を持つアカウントとパスワードの入力をユーザーに求めるようにレポートのデータ ソース接続が構成されている場合に表示されます。 **[パラメーター]** は、レポートに定義されているパラメーターのユーザー入力をレポートが受け付ける場合に表示されます。  
  
### <a name="setting-properties-on-the-report-viewer-web-part"></a>レポート ビューアー Web パーツのプロパティの設定  
 Web パーツのプロパティには、レポート ビューアーに固有のカスタム プロパティと、任意の Web パーツに対して設定できる全般プロパティがあります。 詳細については、「 [レポート ビューアー Web パーツのカスタマイズ](../../2014/reporting-services/customize-the-report-viewer-web-part.md)」を参照してください。  
  
 既定では、レポートはページ全体モードで表示されます。 ページ全体モードでは、ページ ナビゲーション、検索、およびその他の機能を提供するツール バーが表示されます。 Web パーツをカスタマイズすることで、外観や既定の動作を変更できます。  
  
## <a name="see-also"></a>参照  
 [インストールまたはアンインストール、Reporting Services アドイン、SharePoint の&#40;SharePoint 2010 および SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [レポート ビューアー Web パーツを Web ページに追加する &#40;Reporting Services の SharePoint 統合モード&#41;](report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
  
