---
title: Integration Services (SSIS) プロジェクトとソリューション | Microsoft Docs
ms.custom: ''
ms.date: 09/20/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: vanto
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.importprojectwizard.f1
helpviewer_keywords:
- projects [Integration Services], creating
- folders [Integration Services], projects
- files [Integration Services], projects
- folders [Integration Services]
- projects [Integration Services], about projects
ms.assetid: 28ea8120-0a79-4029-93f0-07d521b32bee
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 50938fe4f3be40f280340fff5bfbca23ac8b1b44
ms.sourcegitcommit: 445842da7c7d216b94a9576e382164c67f54e19a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71680982"
---
# <a name="integration-services-ssis-projects-and-solutions"></a>Integration Services (SSIS) プロジェクトとソリューション

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] には [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] パッケージを開発するための [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] が用意されています。  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージはプロジェクト内に存在します。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを作成して作業するには、[SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md) をインストールする必要があります。 詳細については、「 [Integration Services のインストール](../integration-services/install-windows/install-integration-services.md)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で新しい [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]プロジェクトを作成する場合は、 **[新しいプロジェクト]** ダイアログ ボックスに **[Integration Services プロジェクト]** テンプレートが表示されます。 このプロジェクト テンプレートでは、パッケージを 1 つ含む新しいプロジェクトが作成されます。
  
## <a name="projects-and-solutions"></a>[プロジェクトおよびソリューション]  
 プロジェクトはソリューション内に保存されます。 最初にソリューションを作成し、次に [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトをそのソリューションに追加できます。 既存のソリューションがない場合、最初にプロジェクトを作成したときに [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] は自動的にソリューションを作成します。 1 つのソリューションにさまざまな種類の複数のプロジェクトを含めることができます。  
  
> [!TIP]  
>  既定では、[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] で新しいプロジェクトを作成すると、そのソリューションは**ソリューション エクスプローラー** ペインに表示されません。 既定の動作を変更するには、 **[ツール]** メニューの **[オプション]** をクリックします。 **[オプション]** ダイアログ ボックスで、 **[プロジェクトおよびソリューション]** を展開し、 **[全般]** をクリックします。 **[全般]** ページで、 **[常にソリューションを表示]** を選択します。  

## <a name="solutions-contain-projects"></a>プロジェクトを格納するソリューション  
 ソリューションとは、エンド ツー エンドのビジネス ソリューションを開発するときに使用するプロジェクトを、グループ化して管理するコンテナーのことです。 ソリューションを使用すると、複数のプロジェクトを 1 単位として処理し、ビジネス ソリューションに役立つ 1 つ以上の関連プロジェクトをまとめることができます。  
  
 ソリューションには、さまざまな種類のプロジェクトを含めることができます。 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーを使用して [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを作成する場合は、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で用意されているソリューション内の [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]プロジェクトで作業します。  
  
 新しいソリューションを作成すると、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] のソリューション エクスプローラーにソリューション フォルダーが自動的に追加され、拡張子 .sln および .suo のファイルが作成されます。  
  
-   *.sln ファイルには、ソリューションの構成情報、およびソリューション内のプロジェクトの一覧が格納されます。  
  
-   *.suo ファイルには、ソリューションを操作するうえでのユーザー設定情報が格納されます。  
  
 新しいプロジェクトを作成すると [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] でソリューションが自動的に作成されますが、空白のソリューションを作成して、プロジェクトを後で追加することもできます。  
   
## <a name="integration-services-projects-contain-packages"></a>パッケージを格納する Integration Services プロジェクト  
 プロジェクトとは [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを開発するコンテナーのことです。  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトにはパッケージに関連するファイルが格納され、グループ化されます。 たとえば、プロジェクトには、特定の抽出、変換、および読み込み (ETL) ソリューションの作成に必要なファイルが含まれます。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを作成する前に、この種のプロジェクトの基本的な内容を理解しておく必要があります。 プロジェクトの内容を理解すれば、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトの作成および作業を開始することができます。  
  
## <a name="folders-in-integration-services-projects"></a>Integration Services プロジェクトのフォルダー  
 次の図は、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] での [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]プロジェクト内のフォルダーを示しています。  
  
![ssis-solution-explorer.png](media/ssis-solution-explorer.png)
  
 次の表では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトに表示されるフォルダーについて説明します。  
  
|フォルダー|[説明]|  
|------------|-----------------|
|接続マネージャー|プロジェクト接続マネージャーが含まれています。 詳細については、「[Integration Services (SSIS) の接続](../integration-services/connection-manager/integration-services-ssis-connections.md)」を参照してください。|
|[!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ|パッケージが含まれます。 詳細については、「[Integration Services &#40;SSIS&#41; Packages](../integration-services/integration-services-ssis-packages.md)」を参照してください。|  
|パッケージ パーツ|再利用またはインポートできるパッケージ パーツが含まれています。 詳細については、「[制御フロー パッケージ パーツを使用することによりパッケージ間で制御フローを再利用する](reuse-control-flow-across-packages-by-using-control-flow-package-parts.md)」を参照してください。
|その他|パッケージ ファイル以外のファイルが含まれます。|  
  
## <a name="files-in-integration-services-projects"></a>Integration Services プロジェクトのファイル  
 新しい [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトまたは既存のプロジェクトをソリューションに追加すると、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] により、.dtproj、.dtproj.user、.database、Project.params 拡張子を持つプロジェクト ファイルが作成されます。 
  
-   *.dtproj ファイルには、プロジェクトの構成と、パッケージなどのアイテムに関する情報が含まれます。  
  
-   *.dtproj.user ファイルには、プロジェクト処理の設定に関する情報が含まれます。  
  
-   *.database ファイルには、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開くために必要な情報が含まれます。

-   Project.params ファイルには、[プロジェクト パラメーター](integration-services-ssis-package-and-project-parameters.md)に関する情報が含まれています。
  
## <a name="version-targeting-in-integration-services-projects"></a>Integration Services プロジェクトの対象バージョン  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] では、SQL Server 2017、SQL Server 2016、SQL Server 2014 または SQL Server 2012 を対象とするパッケージを実行、作成、および管理できます。  
  
 ソリューション エクスプローラーで Integration Services プロジェクトを右クリックし、 **[プロパティ]** を選択すると、そのプロジェクトのプロパティ ページが開きます。 **[構成プロパティ]** の **[全般]** タブで、 **[TargetServerVersion]** プロパティを選択した後、[SQL Server 2017]、[SQL Server 2016]、[SQL Server 2014]、または [SQL Server 2012] を選択します。  
  
 ![[プロジェクトのプロパティ] ダイアログ ボックスの TargetServerVersion プロパティ](../integration-services/media/targetserverversion2.png "[プロジェクトのプロパティ] ダイアログ ボックスの TargetServerVersion プロパティ")  

## <a name="create-a-new-integration-services-project"></a>新しい Integration Services プロジェクトを作成する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]を開きます。  
  
2.  **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。  
  
3.  **[新しいプロジェクト]** ダイアログ ボックスで **[ビジネス インテリジェンス]** を選択してから、 **[Integration Services プロジェクト]** テンプレートを選択します。  
  
     **[Integration Services プロジェクト]** テンプレートでは、空のパッケージを 1 つ含む [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトが作成されます。

  ![ssis-ssdt-new-project.png](media/ssis-ssdt-new-project.png)
  
4.  (省略可) プロジェクトの名前と場所を変更します。  
  
     ソリューション名は、プロジェクト名と一致するように自動的に更新されます。  
  
5.  ソリューション ファイル用に別のフォルダーを作成するには、 **[ソリューションのディレクトリを作成]** を選択します。 既定のオプションです。  
  
6.  ソース管理ソフトウェアがコンピューターにインストールされている場合、プロジェクトをソース管理に関連付けるには、 **[ソース管理に追加]** を選択します。  
  
7.  ソース管理ソフトウェアが [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe の場合、 **[Visual SourceSafe ログイン]** ダイアログ ボックスが開きます。 **[Visual SourceSafe ログイン]** ダイアログ ボックスで、ユーザー名、パスワード、および [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe データベースの名前を指定します。 データベースを探すには、 **[参照]** をクリックします。  
  
    > **注:** 選択したソース管理プラグインを表示、変更したり、ソース管理の環境を構成するには、 **[ツール]** メニューの **[オプション]** をクリックし、 **[ソース管理]** ノードを展開します。  
  
8.  **[OK]** をクリックしてソリューションを**ソリューション エクスプローラー**に追加し、プロジェクトをソリューションに追加します。  

## <a name="import-an-existing-project-with-the-import-project-wizard"></a>プロジェクトのインポート ウィザードで既存のプロジェクトをインポートする
  
1.  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]で、 **[ファイル]**  > **メニューの** [新規作成] **[プロジェクト]** をクリックします。  
  
2.  **[新しいプロジェクト]** ウィンドウの **[インストールされているテンプレート]** 領域で **[ビジネス インテリジェンス]** を展開し、 **[Integration Services]** をクリックします。  
  
3.  プロジェクトの種類の一覧から **Integration Services プロジェクトのインポート ウィザード** をクリックします。  
  
4.  作成する新しいプロジェクトの名前を、 **[名前]** ボックスに入力します。  
  
5.  プロジェクトのパスまたは場所を **[場所]** ボックスに入力するか、または **[参照]** をクリックして選択します。  
  
6.  **[ソリューション名]** ボックスにソリューションの名前を入力します。  
  
7.  **[OK]** をクリックして **[Integration Services プロジェクトのインポート ウィザード]** ダイアログ ボックスを起動します。  
  
8.  **[次へ]** をクリックして、 **[ソースの選択]** ページに移動します。  
  
9. **.ispac** ファイルからインポートする場合は、ファイル名を含むパスを **[パス]** テキスト ボックスに入力します。 **[参照]** をクリックして、ソリューションを格納するフォルダーに移動し、 **[ファイル名]** ボックスにファイル名を入力して、 **[開く]** をクリックします。  
  
     **Integration Services カタログ**からインポートする場合は、データベース インスタンス名を **[サーバー名]** ボックスに入力するか、または **[参照]** をクリックしてカタログを含むデータベース インスタンスを選択します。  
  
     **[パス]** ボックスの横にある **[参照]** をクリックし、カタログのフォルダーを展開して、インポートするプロジェクトを選択し、 **[OK]** をクリックします。  
  
     **[次へ]** をクリックして **[確認]** ページに移動します。  
  
10. 情報を確認し、 **[インポート]** をクリックして、選択した既存のプロジェクトに基づくプロジェクトを作成します。  
  
11. 省略可能: **[レポートの保存]** をクリックして、結果をファイルに保存します  
  
12. **[閉じる]** をクリックして **[Integration Services プロジェクトのインポート ウィザード]** ダイアログ ボックスを閉じます。  

## <a name="add-a-project-to-a-solution"></a>ソリューションにプロジェクトを追加する 
 プロジェクトを追加する場合は、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で新しい空のプロジェクトを作成することも、別のソリューション用に既に作成したプロジェクトを追加することもできます。 プロジェクトを既存のソリューションに追加できるのは、そのソリューションが [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で表示されている場合のみです。  
  
### <a name="add-a-new-project-to-a-solution"></a>ソリューションへの新しいプロジェクトの追加  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で、新しい [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトの追加先となるソリューションを開き、次のいずれかの操作を行います。  
  
    -   ソリューションを右クリックして **[追加]** をクリックし、 **[新しいプロジェクト]** をクリックします。  
  
    -   **[ファイル]** メニューの **[追加]** をポイントし、 **[新しいプロジェクト]** をクリックします。  
  
2.  **[新しいプロジェクトの追加]** ダイアログ ボックスの **[テンプレート]** ペインで、 **[Integration Services プロジェクト]** をクリックします。  
  
3.  必要に応じて、プロジェクトの名前と場所を変更します。  
  
4.  **[OK]** をクリックします。  
  
### <a name="add-an-existing-project-to-a-solution"></a>ソリューションへの既存のプロジェクトの追加  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で、既存の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを追加するソリューションを開き、次のいずれかの操作を行います。  
  
    -   ソリューションを右クリックして **[追加]** をポイントし、 **[既存のプロジェクト]** をクリックします。  
  
    -   **[ファイル]** メニューの **[追加]** をクリックし、 **[既存のプロジェクト]** をクリックします。  
  
2.  **[既存プロジェクトの追加]** ダイアログ ボックスで、追加するプロジェクトを選択して、 **[開く]** をクリックします。  
  
3.  選択したプロジェクトが、**ソリューション エクスプローラー**のソリューション フォルダーに追加されます。  
  
## <a name="remove-a-project-from-a-solution"></a>ソリューションからプロジェクトを削除する
 プロジェクトをソリューションから削除できるのは、そのソリューションが [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で表示されている場合のみです。 ソリューションが表示されていれば、1 つのプロジェクト以外はすべて削除できます。 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] では、残りのプロジェクトが 1 つのみになった時点でソリューション フォルダーが表示されなくなるので、最後の 1 つのプロジェクトは削除できません。  
   
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを削除する対象となるソリューションを開きます。  
  
2.  ソリューション エクスプローラーでプロジェクトを右クリックし、 **[プロジェクトのアンロード]** をクリックします。  
  
3.  **[OK]** をクリックして変更を確認します。  

## <a name="add-an-item-to-a-project"></a>プロジェクトにアイテムを追加する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、アイテムを追加する [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトが含まれているソリューションを開きます。  
  
2.  ソリューション エクスプローラーで、プロジェクトを右クリックして **[追加]** をポイントし、次のいずれかの操作を行います。  
  
    -   **[新しい項目]** をクリックし、 **[新しい項目の追加]** ダイアログ ボックスの **[テンプレート]** ペインで、テンプレートを選択します。  
  
    -   **[既存の項目]** をクリックし、 **[既存項目の追加]** ダイアログ ボックス内を参照して、プロジェクトに追加するアイテムを探します。次に、 **[追加]** をクリックします。  
  
3.  ソリューション エクスプローラーの該当フォルダーに、新しいアイテムが表示されます。  

## <a name="copy-project-items"></a>プロジェクト アイテムをコピーする  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクト内または [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクト間でオブジェクトをコピーすることができます。 他の種類の [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] プロジェクト、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]、および [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] の間でオブジェクトをコピーすることもできます。 プロジェクト間でコピーするには、プロジェクトが同じ [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ソリューションに含まれている必要があります。

1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で、作業対象とする [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトまたはソリューションを開きます。  
  
2.  コピー元のプロジェクトとアイテム フォルダーを展開します。  
  
3.  アイテムを右クリックし、 **[コピー]** をクリックします。  
  
4.  コピー先の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを右クリックし、 **[貼り付け]** をクリックします。  
  
     アイテムが適切なフォルダーに自動的にコピーされます。 パッケージではない [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトにアイテムをコピーする場合は、アイテムが **[その他]** フォルダーにコピーされます。  

## <a name="next-steps"></a>次の手順

- [SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md) のダウンロードとインストール。
- [SSIS ETL パッケージを作成する方法](ssis-how-to-create-an-etl-package.md)