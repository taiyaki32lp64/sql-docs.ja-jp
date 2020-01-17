---
title: Analysis Services プロジェクト (SSDT) の作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- templates [Analysis Services]
- templates [Analysis Services], projects
- projects [Analysis Services], creating
- projects [Analysis Services], Business Intelligence Development Studio
- Business Intelligence Development Studio, defining projects [Analysis Services]
- items [Analysis Services]
ms.assetid: d00913b0-cd6d-4de0-a1e7-4ce86fcc078d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 313fdd08234e9dd784d45c65d7ee23cd0a0a308c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076237"
---
# <a name="create-an-analysis-services-project-ssdt"></a>Analysis Services プロジェクトの作成 (SSDT)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] を使用して定義できます。具体的には、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクト テンプレートを使用するか、または [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースのインポート ウィザードを使用して、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースのコンテンツを読み取ります。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]に読み込まれているソリューションがない場合は、新しい [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトを作成すると自動的に新しいソリューションが作成されます。 それ以外の場合は、新しい [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトが既存のソリューションに追加されます。 ソリューション開発のベスト プラクティスでは、アプリケーション データの種類ごとにプロジェクトを個別に作成することが必要です。複数のプロジェクトが関係していても、使用するソリューションは 1 つです。 たとえば、Integration Services パッケージ、Analysis Services データベース、および Reporting Services レポートすべてを同じビジネス アプリケーションが使用し、これらのための独立した複数プロジェクトを含むソリューションが 1 つ存在する場合があります。  
  
 Analysis Services プロジェクトには、1 つの Analysis Services データベースで使用されるオブジェクトが複数存在します。 プロジェクトの配置プロパティは、プロジェクト メタデータがインスタンス化されたオブジェクトとして配置されるデータベース名とサーバーを指定します。  
  
 このトピックには、次のセクションが含まれます。  
  
 [Analysis Services プロジェクト テンプレートを使用して、新しいプロジェクトを作成します。](#bkmk_NewUsingTemplate)  
  
 [既存の Analysis Services データベースを使用した新しいプロジェクトの作成](#bkmk_NewUsingWizard)  
  
 [既存ソリューションへの Analysis Services プロジェクトの追加](#bkmk_AddtoExistingSolution)  
  
 [ソリューションの作成と配置](#bkmk_buildDeploy)  
  
 [Analysis Services のプロジェクト フォルダー](#bkmk_ProjectFolders)  
  
 [Analysis Services のファイルの種類](#bkmk_FileTypes)  
  
 [Analysis Services 項目テンプレート](#bkmk_ItemTemplates)  
  
##  <a name="bkmk_NewUsingTemplate"></a> Analysis Services プロジェクト テンプレートを使用して、新しいプロジェクトを作成します。  
 次に示す手順を使用して、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトを定義する空のプロジェクトを作成します。このオブジェクトは、その後に新しい [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースとして配置できます。  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。 **[新しいプロジェクト]** ダイアログ ボックスの **[プロジェクトの種類]** ペインで、 **[ビジネス インテリジェンス プロジェクト]** を選択します。  
  
2.  **[新しいプロジェクト]** ダイアログ ボックスの **[Visual Studio にインストールされたテンプレート]** カテゴリで、 **[Analysis Services プロジェクト]** を選択します。  
  
3.  **[プロジェクト名]** ボックスに、プロジェクトの名前を入力します。 ここで入力する名前が、既定のデータベース名として使用されます。  
  
4.  プロジェクトのファイルを保存するフォルダーを **[場所]** ボックスに入力するか、このボックスの一覧から選択します。または、 **[参照]** をクリックしてフォルダーを選択します。  
  
5.  新しいプロジェクトを既存のソリューションに追加するには、 **[ソリューション]** の一覧から **[ソリューションに追加する]** をクリックします。  
  
     \- または -  
  
     新規のソリューションを作成するには、 **[ソリューション]** の一覧で **[新しいソリューションを作成する]** をクリックします。 新しいソリューション用に新規のフォルダーを作成するには、 **[ソリューションのディレクトリを作成]** をクリックします。 **[ソリューション名]** に、新しいソリューションの名前を入力します。  
  
6.  **[OK]** をクリックします。  
  
##  <a name="bkmk_NewUsingWizard"></a> 既存の Analysis Services データベースを使用した新しいプロジェクトの作成  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースのインポート ウィザードを使用して、既存の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースのオブジェクトに基づいて新しいプロジェクトを作成できます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトを既存の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースに基づいて定義した場合、そのデータベースのメタデータは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]プロジェクトで開きます。 これらのオブジェクトは元のオブジェクトに影響を及ぼすことなくプロジェクト内で変更できます。そして、配置プロパティがそのデータベースを指定する場合は同じ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースに配置できます。または、新たに作成した [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースに配置して、比較テストを行うこともできます。 変更内容が配置されるまでは、既存の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースに対する変更は有効になりません。  
  
 また、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースをインポート テンプレートを使用して、元の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトが配置された後に変更が直接行われた実稼働データベースから新しいプロジェクトを作成することもできます。  
  
 プロジェクトを処理または配置する前に、データ ソースで指定されたデータ プロバイダーを変更する必要がある場合があります。 使用している SQL Server ソフトウェアが、データベース作成に使用されたソフトウェアより新しい場合、プロジェクトで指定されたデータ プロバイダーがコンピューターにインストールされていない可能性があります。 処理中には、Analysis Services データベース内のデータの取得にサービス アカウントが使用されます。 このデータベースがリモート サーバー上にある場合、ローカル サービスにそのサーバーでの処理と読み取りのアクセス許可があるかどうかを確認してください。  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。 **[新しいプロジェクト]** ダイアログ ボックスの **[プロジェクトの種類]** ペインで、 **[ビジネス インテリジェンス プロジェクト]** を選択します。  
  
2.  **[新しいプロジェクト]** ダイアログ ボックスの **[Visual Studio にインストールされたテンプレート]** の一覧から、 **[Analysis Services データベースのインポート]** をクリックします。  
  
3.  ファイルの名前や場所など、プロジェクトとソリューションのプロパティ情報を入力します。 **[OK]** をクリックします。  
  
4.  **[Analysis Services データベースのインポート ウィザードへようこそ]** ページで、 **[次へ]** をクリックします。  
  
5.  **[転送元データベース]** ページで、コンテンツの抽出元のサーバーとデータベースを指定し、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトを作成し、 **[次へ]** をクリックします。  
  
     サポート対象データベースとしては、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、および [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]のバージョンの Analysis Services で作成されたデータベースがあります。  
  
     データベース名は直接入力することも、サーバーをクエリして、サーバー上の既存のデータベースを表示してから選択することもできます。 データベースがリモート サーバーまたは実稼働サーバー上にある場合、データベース読み取りアクセス許可を申請する必要がある場合があります。 ファイアウォール構成設定を使用すると、データベースへのアクセスをさらに制限できます。 データベースへの接続を試みてエラーが発生する場合、最初にアクセス許可とファイアウォール設定を確認してください。  
  
6.  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースのコンテンツの抽出が完了したら、 **[ウィザードの完了]** ページの **[完了]** をクリックします。  
  
7.  [ソリューション エクスプローラー] ウィンドウを開き、プロジェクトのコンテンツを表示します。  
  
##  <a name="bkmk_AddtoExistingSolution"></a> 既存ソリューションへの Analysis Services プロジェクトの追加  
 あるビジネス アプリケーションのソース ファイルをすべて含んだソリューションが既にある場合、そのソリューションに新しい Analysis Services プロジェクトを追加できます。  
  
 ソリューションに既存プロジェクトを追加すると、プロジェクトがそのソリューションに関連付けられますが、コピーはされません。 その Analysis Services プロジェクトが別のソリューションで作成された場合、プロジェクト ファイルは元の作成対象ソリューションにとどまります。 つまり、いずれのソリューションを通じてプロジェクトに加えられた変更も、同じソース ファイル セットに反映されます。 この動作が望ましくない場合は、プロジェクト ファイルを最初に新しいソリューション フォルダーにコピーまたは移動してから、プロジェクトをソリューションに追加します。  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、ソリューションを開きます。 ソリューション エクスプローラーで、ソリューションを右クリックして **[追加]** をポイントし、 **[既存のプロジェクト]** をクリックし、追加するプロジェクトを選択します。  
  
2.  ソリューションに追加する .dwproj ファイルを選択します。  
  
##  <a name="bkmk_buildDeploy"></a> ソリューションの作成と配置  
 既定では、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] は、ローカル コンピューター上の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の既定のインスタンスにプロジェクトを配置します。 この配置先を変更するには、 **プロジェクトの** [プロパティ ページ] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ダイアログ ボックスで **[サーバー]** 構成プロパティを変更します。  
  
> [!NOTE]  
>  既定では、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] は、ソリューションの配置の際に配置スクリプトと依存オブジェクトにより変更されたオブジェクトのみを処理します。 この機能を変更するには、 **プロジェクトの** [プロパティ ページ] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ダイアログ ボックスで [処理オプション] 構成プロパティを変更します。  
  
 ソリューションを作成し、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスにテスト用に配置します。 ソリューションを作成すると、プロジェクト内のオブジェクト定義および依存関係が検証され、配置スクリプトが生成されます。 ソリューションの配置では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Deployment Engine を使用して、指定のインスタンスに配置スクリプトが送信されます。  
  
 プロジェクトを配置した後、配置済みデータベースを確認し、テストします。 その後は、プロジェクトが完成するまで、オブジェクト定義を変更したり、作成と配置を再度行ったりすることができます。  
  
 プロジェクトが完成したら、配置ウィザードを使用して、ソリューションの作成時に生成された配置スクリプトを宛先インスタンスに配置し、最終的なテスト、ステージング、および配置を行うことができます。  
  
##  <a name="bkmk_ProjectFolders"></a> Analysis Services のプロジェクト フォルダー  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトには、プロジェクトに含まれているアイテムを整理するための次のフォルダーがあります。  
  
|フォルダー|説明|  
|------------|-----------------|  
|ソリューション エクスプローラー|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトのデータ ソースが含まれています。 これらのオブジェクトは、データ ソース ウィザードで作成し、データ ソース デザイナーで編集します。|  
|データ ソース ビュー|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトのデータ ソース ビューが含まれています。 これらのオブジェクトは、データ ソース ビュー ウィザードで作成し、データ ソース ビュー デザイナーで編集します。|  
|キューブ|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトのキューブが含まれています。 これらのオブジェクトは、キューブ ウィザードで作成し、キューブ デザイナーで編集します。|  
|ディメンション|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトのディメンションが含まれています。 これらのオブジェクトは、ディメンション ウィザードまたはキューブ ウィザードで作成し、ディメンション デザイナーで編集します。|  
|マイニング構造|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトのマイニング構造が含まれています。 これらのオブジェクトは、マイニング モデル ウィザードで作成し、マイニング モデル デザイナーで編集します。|  
|ロール|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトのデータベース ロールが含まれています。 ロール デザイナーでロールを作成および管理します。|  
|アセンブリ|[!INCLUDE[msCoName](../../includes/msconame-md.md)] プロジェクトの COM ライブラリおよび [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .NET Framework アセンブリへの参照が含まれています。 **[参照の追加]** ダイアログ ボックスで参照を作成します。|  
|その他|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の種類のファイルを除くすべての種類のファイルが含まれています。 このフォルダーを使用して、プロジェクトの注釈が書かれているテキスト ファイルなど、その他のファイルを追加します。|  
  
##  <a name="bkmk_FileTypes"></a> Analysis Services のファイルの種類  
 1 つの [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ソリューションで、複数のファイルの種類を使用できます。ファイルの種類は、ソリューションに含まれるプロジェクトおよびそのソリューションの各プロジェクトに含まれるアイテムによって異なります。 通常、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ソリューションの各プロジェクトのファイルは、ソリューションのフォルダー内でプロジェクト別に異なるフォルダーに保存されます。  
  
> [!NOTE]  
>  オブジェクトのファイルをプロジェクト フォルダーにコピーしても、オブジェクトはプロジェクトに追加されません。 **でプロジェクトのショートカット メニューから** [追加] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] コマンドを使用して、既存のオブジェクト定義をプロジェクトに追加する必要があります。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトのプロジェクト フォルダーには、次の表に示す種類のファイルを格納できます。  
  
|ファイルの種類|説明|  
|---------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクト定義ファイル (.dwproj)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトで定義されて含まれているアイテム、構成、およびアセンブリ参照のメタデータが保存されています。|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトのユーザー設定 (.dwproj.user)|特定のユーザーに対する [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトの構成情報が含まれています。|  
|データ ソース ファイル (.ds)|データ ソースのメタデータを定義している [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] スクリプト言語 (ASSL) の要素が含まれています。|  
|データ ソース ビュー ファイル (.dsv)|データ ソース ビューのメタデータを定義する ASSL の要素が含まれています。|  
|キューブ ファイル (.cube)|メジャー グループ、メジャー、キューブ ディメンションなど、キューブのメタデータを定義する ASSL の要素が含まれています。|  
|パーティション ファイル (.partitions)|指定したキューブのパーティションのメタデータを定義する ASSL の要素が含まれています。|  
|ディメンション ファイル (.dim)|データベース ディメンションのメタデータを定義する ASSL の要素が含まれています。|  
|マイニング構造ファイル (.dmm)|マイニング構造および関連マイニング モデルのメタデータを定義する ASSL の要素が含まれています。|  
|データベース ファイル (.database)|勘定科目の種類、翻訳、データベース権限など、データベースのメタデータを定義する ASSL の要素が含まれています。|  
|データベース ロール ファイル (.role)|ロール メンバーなど、データベース ロールのメタデータを定義する ASSL の要素が含まれています。|  
  
##  <a name="bkmk_ItemTemplates"></a> Analysis Services 項目テンプレート  
 **[新しい項目の追加]** ダイアログ ボックスを使用して新しいアイテムを [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトに追加する場合は、指定された動作を実行する方法を示した事前定義済みのスクリプトまたはステートメントである、項目テンプレートを必要に応じて使用します。  
  
 次の表に示す項目テンプレートは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] [新しい項目の追加] **ダイアログ ボックスの [** プロジェクト アイテム] カテゴリにあります。  
  
|カテゴリ|項目テンプレート|説明|  
|--------------|-------------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクト アイテム|Cube|キューブ ウィザードを起動して、新しいキューブを [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトに追加します。|  
||[データ ソース]|データ ソース ウィザードを起動して、新しいデータ ソースを [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトに追加します。|  
||[データ ソース ビュー]|データ ソース ビュー ウィザードを起動して、新しいデータ ソース ビューを [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトに追加します。|  
||データベース ロール|新しいデータベース ロールを [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトに追加して、新しいデータベース ロールのロール デザイナーを表示します。|  
||[ディメンション]|ディメンション ウィザードを起動して、新しいデータベース ディメンションを [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトに追加します。|  
||[マイニング構造]|データ マイニング ウィザードを起動して、新しいマイニング構造と関連マイニング モデルを [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトに追加します。|  
  
## <a name="see-also"></a>関連項目  
 [Analysis Services プロジェクトのプロパティの構成 &#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md)   
 [Analysis Services プロジェクトのビルド &#40;SSDT&#41;](build-analysis-services-projects-ssdt.md)   
 [Analysis Services プロジェクトの配置 &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
  
