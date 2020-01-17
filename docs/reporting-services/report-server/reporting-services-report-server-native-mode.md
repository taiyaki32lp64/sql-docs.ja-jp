---
title: Reporting Services レポート サーバー (ネイティブ モード) | Microsoft Docs
ms.date: 06/06/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- administering Reporting Services
- administering [Reporting Services]
- Reporting Services, administration
ms.assetid: fa0d84e2-4c21-432c-aa7c-23517da75253
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4a0e3f521549bb309fcbd69fc7905746be09d84b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66826897"
---
# <a name="reporting-services-report-server-native-mode"></a>Reporting Services Report Server (Native Mode)
  ネイティブ モード用に構成されたレポート サーバーは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]コンポーネントのみを通じてすべての処理機能と管理機能を提供するアプリケーション サーバーとして実行されます。  
  
 いずれかを使用する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]または web ポータルを管理する[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]レポートします。 レポート サーバーをネイティブ モードで管理するには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用します。  
  
 レポート サーバーを SharePoint モード用に構成した場合、レポートや共有データ ソースなどのレポート サーバー アイテムを管理するには、SharePoint サイトのコンテンツ管理のページを使用する必要があります。  
  
 この記事には、次の情報が含まれています。  
  
-   [ネイティブ モードの概要](#bkmk_sum)  
  
-   [コンテンツの管理](#bkmk_managecontent)  
  
-   [リソースの保護と管理](#bkmk_manageresources)  
  
-   [レポートからの画像リソースの参照](#bkmk_referenceimage)  
  
##  <a name="bkmk_sum"></a> ネイティブ モードの概要  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モードは、管理とメンテナンスが必要な複数のサーバー側機能で構成されます。 次に、それらのサーバー機能の例を示します。  
  
-   レポート サーバー Web サービス。レポート サーバー サービス内で実行されます。  
  
-   バックグラウンド処理アプリケーション。スケジュールされた操作やレポート配信を処理します。  
  
-   レポート サーバー データベース。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストールを完全に管理するには、次の権限が必要です。  
  
-   レポート サーバー コンピューターのローカル Administrator グループのメンバーシップ。 リモート コンピューターで実行されるサーバー機能がインストールに含まれている場合に、リモート接続を介してサーバーを管理するには、リモート コンピューターの管理者権限が必要です。  
  
-   データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのデータベース管理者権限。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をドメイン コントローラーにインストールする場合は、ドメイン管理者のアクセス許可が必要です。  
  
##  <a name="bkmk_managecontent"></a> コンテンツの管理  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]では、コンテンツ管理はレポート、モデル、フォルダー、リソース、および共有データ ソースの管理を指します。 これらのすべてのアイテムは、プロパティおよびセキュリティの設定をとおして、個別に管理できます。 アイテムは、レポート サーバー フォルダー名前空間内のさまざまな場所に移動できます。 アイテムを効率的に管理するには、コンテンツ マネージャーで実行されるタスクを理解しておく必要があります。  
  
> [!NOTE]  
>  コンテンツ管理はレポート サーバー管理とは異なります。 レポート サーバーを実行する環境の管理方法については、「[レポート サーバーの構成と管理 &#40;Reporting Services SharePoint モード&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md)」を参照してください。  
  
 コンテンツ管理には、次のタスクが含まれます。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]で提供されるロールベースのセキュリティを適用することにより、レポート サーバー サイトおよびアイテムをセキュリティで保護します。  
  
-   フォルダーを追加、変更、および削除することにより、レポート サーバーのフォルダー階層を構造化します。  
  
-   レポート サーバーで管理されるアイテムに適用する既定値およびプロパティを設定します。 たとえば、レポート履歴の記憶域のポリシーを決定する、基準の最大値を設定できます。  
  
-   レポート固有のデータ ソース接続の代わりに使用できる共有データ ソース アイテムを作成します。 パブリッシャーまたはコンテンツ マネージャーは、たとえば、テスト データベースへの参照を運用データベースへの参照に置き換えるために、最初にレポートで定義されたものとは異なるデータ ソースを選択できます。  
  
-   レポート固有のスケジュールやサブスクリプション固有のスケジュールに置き換えて使用できる共有スケジュールを作成します。時間経過に伴うスケジュール情報の管理がより簡単になります。  
  
-   データ ストアからデータを取得することにより受信者の一覧を生成する、データ ドリブン サブスクリプションを作成します。  
  
-   レポート処理のスケジュールを設定し、要求時に実行できるレポート処理とキャッシュから読み込まれるレポート処理を指定することにより、サーバーに対するレポート処理の要求を分散させます。  
  
 管理タスクを実行するための権限は、 **システム管理者** と **コンテンツ マネージャー**という、事前定義された 2 つのロールを通じて提供されます。 レポート サーバーのコンテンツを効率よく管理するためには、両方のロールに割り当てられている必要があります。 詳細については、「[ロールとアクセス許可 &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md)」を参照してください。  
  
 レポート サーバーのコンテンツを管理するためのツールには、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] や Web ポータルなどがあります。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] では、既定値を設定したり、各機能を有効化することができます。 Web ポータルを使って、レポート サーバーのアイテムおよび操作へのユーザー アクセスを許可したり、レポートをはじめとする各種のコンテンツを表示および使用したり、すべての共有アイテムとレポート配信機能を表示および使用したりできます。  
  
##  <a name="bkmk_manageresources"></a> リソースの保護と管理  
 リソースはレポート サーバーに格納される管理対象アイテムですが、レポート サーバーで処理されるものではありません。 通常、リソースにレポート ユーザー向けの外部コンテンツが用意されています。 例としては、.jpg ファイルや、レポートで使用されるビジネス ルールを示す HTML ファイルなどがあります。 JPG ファイルや HTML ファイルはレポート サーバーに格納されますが、このファイルはレポート サーバーで処理されずに、ブラウザーに直接渡されます。  
  
 レポート サーバーにリソースを追加するには、ファイルをアップロードまたはパブリッシュします。  
  
|演算|ファイルの種類|  
|---------------|---------------|  
|アップロード|レポート定義 (.rdl) ファイルとレポート モデル (.smdl) ファイルを除くすべてのファイルがアップロードされます。<br /><br /> リソースをアップロードするには、レポート サーバーがネイティブ モードで動作している場合は Web ポータルを使用し、サーバーが SharePoint 統合モードで動作している場合は SharePoint サイト上のアプリケーション ページを使用する必要があります。 詳細については、「[レポート サーバーでファイルまたはレポートをアップロードする](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)」または「[SharePoint ライブラリへのドキュメントのアップロード &#40;Reporting Services の SharePoint モード&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)」をご覧ください。|  
|パブリッシュ|.rdl、.smdl、.rds データ ソース ファイルを除くすべてのファイルが、リソースとしてアップロードされます。 リソースをパブリッシュするには、既存のアイテムをレポート デザイナーのプロジェクトに追加した後で、そのプロジェクトをレポート サーバーにパブリッシュします。|  
  
 リソースはすべて、もともとはファイル システム上のファイルです。そのファイルがレポート サーバーにアップロードされることで、リソースになります。 制限がないファイルをアップロードできるファイルの種類、最大 1 GB のサイズします。 ただし、リソースとしてレポート サーバーにパブリッシュする場合には、適合する MIME の種類があるファイルの方が適しています。 たとえば、HTML および JPG ファイルを基にしたリソースは、ユーザーがリソースをクリックすると、HTML は Web ページとして、JPG は画像として、ユーザーが見ることができる形でブラウザー ウィンドウで開かれます。 これに対し、たとえばデスクトップ アプリケーション ファイルなど、適合する MIME の種類がないリソースは、ブラウザー ウィンドウに表示されない場合があります。  
  
 レポート ユーザーがリソースを表示できるかどうかは、ブラウザーの表示機能によって異なります。 リソースはリソース サーバーで処理されないため、特定の MIME の種類を表示するための表示機能がブラウザーに必要となります。 ブラウザーがコンテンツを表示できない場合、そのリソースを閲覧するユーザーが見ることができるのは、リソースの全般プロパティのみとなります。  
  
 リソースは、レポート サーバーのフォルダー階層に、レポート、共有データ ソース、共有スケジュール、フォルダーなどと共に名前付きアイテムとして置かれます。 レポート サーバーに保存されているアイテムと同様に、リソースは検索、表示、保護、プロパティの設定を実行できます。 リソースの表示や管理を行うには、リソース表示タスクやリソース管理タスクのロールが割り当てられている必要があります。  
  
##  <a name="bkmk_referenceimage"></a> レポートからの画像リソースの参照  
 リソースには、レポートで参照する画像を含めることができます。 レポートで外部画像を使用する必要がある場合、リソースに画像を保存しておくと次の利点が得られます。  
  
-   レポート サーバー データベースにストレージを集中する。 レポート サーバー データベースとその内容を別のコンピューターに移動しても、外部画像はレポート上にそのまま残ります。 ディスク上や他のコンピューターに保存されている画像ファイルを追跡する必要はありません。  
  
-   ファイル システムのセキュリティではなくロールの割り当てによって保護する。 レポートの表示に使用した権限をリソースにも適用できます。 一方、画像をディスク上に保存する場合は、匿名ユーザー アカウントまたは自動実行アカウントに、ファイルにアクセスするための権限を与える必要があります。  
  
 レポートに画像リソースを使用するには、画像ファイルをプロジェクトに追加し、そのプロジェクトをレポートと一緒にパブリッシュします。 画像がパブリッシュされたら、レポート内の画像参照がレポート サーバー上のリソースを指定するように更新した後で、そのレポートのみを再パブリッシュして変更を保存します。 以後、リソースを再パブリッシュすることで、レポートと関係なく画像を更新できるようになります。 レポートでは、レポート サーバー上にある最新バージョンの画像が使用されます。  
  
## <a name="see-also"></a>参照  
 [レポート サーバーを構成および管理する &#40;SSRSネイティブ モード&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [Reporting Services インストール時の問題解決](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)  
  
  
