---
title: パッケージ構成を作成する |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, configurations
- Package Configurations Organizer dialog box
- SSIS packages, configurations
- Integration Services packages, configurations
- configurations [Integration Services]
- packages [Integration Services], configurations
- deploying packages [Integration Services], configurations
ms.assetid: 91ac0347-f908-44f5-bd3d-115790223af4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 287ac1a5631cf2e3925e5895db7f04bb7b89bf5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060165"
---
# <a name="create-package-configurations"></a>パッケージ構成を作成する
  パッケージの構成は、 **[パッケージ構成オーガナイザー]** ダイアログ ボックスまたはパッケージ構成ウィザードを使用して作成します。 これらのツールにアクセスするには、 **で** [SSIS] **メニューの** [パッケージ構成] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]をクリックします。  
  
> [!NOTE]  
>  **パッケージ構成オーガナイザー**にアクセスするには、 **[構成]** プロパティの横にある参照ボタンをクリックする方法もあります。 構成プロパティは、パッケージのプロパティ ウィンドウに表示されます。  
  
> [!NOTE]  
>  パッケージ配置モデルの構成を使用できます。 パラメーターは、プロジェクト配置モデルの構成の代わりに使用します。 プロジェクト配置モデルを使用すると、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーに [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを配置できます。 配置モデルの詳細については、「 [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。  
  
 **[パッケージ構成オーガナイザー]** ダイアログ ボックスでは、パッケージに対する構成の有効化、構成の追加および削除、構成の優先読み込み順序の設定を行えます。  
  
> [!NOTE]  
>  パッケージ構成を優先順序で読み込むと、 **[パッケージ構成オーガナイザー]** ダイアログ ボックスに表示された一覧の上から下へと構成が読み込まれます。 ただし、実行時にパッケージ構成が優先順序で読み込まれるとは限りません。 具体的には、親のパッケージ構成は他の種類の構成の後に読み込まれます。  
  
> [!NOTE]  
>  複数の構成で同じオブジェクト プロパティが設定された場合、最後に読み込まれた値が実行時に使用されます。  
  
 **[パッケージ構成オーガナイザー]** ダイアログ ボックスから、手順に従って構成を作成できるパッケージ構成ウィザードを実行できます。 パッケージ構成ウィザードを実行するには、 **[パッケージ構成オーガナイザー]** ダイアログ ボックスで新しい構成を追加するか、既存の構成を編集します。 ウィザードの各ページで、構成の種類を選択し、構成に直接アクセスするか環境変数を使用するかを選択し、構成に保存するプロパティを選択します。  
  
 次の例は、パッケージ構成ウィザードの [ウィザードの完了] ページに表示される、変数およびパッケージの対象になるプロパティを示しています。  
  
 \Package.Variables[User::TodaysDate].Properties[RaiseChangedEvent]  
  
 \Package.Properties[MaximumErrorCount]  
  
 \Package.Properties[LoggingMode]  
  
 \Package.Properties[LocaleID]  
  
 \Package\My SQL Task.Variables[User::varTableName].Properties[Value]  
  
 この例では、構成によって次のプロパティが更新されます。  
  
-   ユーザー定義変数 `TodaysDate`の RaiseChangedEvent プロパティ。  
  
-   パッケージの MaximumErrorCount プロパティ、LoggingMode プロパティ、および LocaleID プロパティ。  
  
-   ユーザー定義変数 `varTableName`の Value プロパティ (タスク My SQL Task のスコープ内)。  
  
 "\Package" はルートを表し、ピリオド (.) は構成で更新されるプロパティへのパスを定義するオブジェクトを区切ります。 変数とプロパティの名前は角かっこで囲みます。 パッケージ名に関係なく、構成では常に Package という用語を使用します。ただし、その他のオブジェクトのパスにはすべてユーザーが定義した名前を使用します。  
  
 ウィザードの終了後、新しい構成が **[パッケージ構成オーガナイザー]** ダイアログ ボックスの構成の一覧に追加されます。  
  
> [!NOTE]  
>  パッケージ構成ウィザードの最後に表示される [ウィザードの完了] ページには、構成内の対象プロパティが一覧表示されます。 **dtexec** コマンド プロンプト ユーティリティを使用してパッケージの実行時にプロパティを更新するには、パッケージ構成ウィザードを実行してプロパティのパスを表す文字列を生成し、それらの文字列をコピーしてコマンド プロンプト ウィンドウに貼り付け、**dtexec** の set オプションと一緒に使用します。  
  
 次の表に、 **[パッケージ構成オーガナイザー]** ダイアログ ボックスの構成の一覧の列を示します。  
  
|[列]|説明|  
|------------|-----------------|  
|**[構成名]**|構成の名前です。|  
|**[構成の種類]**|構成の種類です。|  
|**[構成文字列]**|構成の場所です。 場所は、パス、環境変数、レジストリ キー、親パッケージの変数名、または [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースのテーブルの場合があります。|  
|**[対象になるオブジェクト]**|構成を持つプロパティを設定するオブジェクトの名前です。 構成が XML 構成ファイルの場合、構成で複数のオブジェクトを更新できるため、この列は空白になります。|  
|**[対象になるプロパティ]**|プロパティの名前。 構成が XML 構成ファイルまたは SQL Server テーブルに書き込まれる場合は、構成で複数のオブジェクトを更新できるため、この列は空白になります。|  
  
### <a name="to-create-a-package-configuration"></a>パッケージの構成を作成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーの **[制御フロー]** タブ、 **[データ フロー]** タブ、 **[イベント ハンドラー]** タブ、または **[パッケージ エクスプローラー]** タブをクリックします。  
  
4.  **[SSIS]** メニューの **[パッケージ構成]** をクリックします。  
  
5.  **[パッケージ構成オーガナイザー]** ダイアログ ボックスで、 **[パッケージの構成を有効にする]** を選択し、 **[追加]** をクリックします。  
  
6.  パッケージ構成ウィザードの最初のページが表示されたら、 **[次へ]** をクリックします。  
  
7.  [構成の種類の選択] ページで構成の種類を指定してから、選択した構成の種類に対応するプロパティを設定します。 詳細については、「 [Package Configuration Wizard UI Reference](../../2014/integration-services/package-configuration-wizard-ui-reference.md)」を参照してください。  
  
8.  [エクスポートするプロパティの選択] ページで、構成に含めるパッケージ オブジェクトのプロパティを選択します。 この構成の種類でサポートされているプロパティが 1 つのみである場合、ウィザード ページのタイトルは [対象になるプロパティの選択] になります。 詳細については、「 [Package Configuration Wizard UI Reference](../../2014/integration-services/package-configuration-wizard-ui-reference.md)」を参照してください。  
  
    > [!NOTE]  
    >  構成の種類が **[XML 構成ファイル]** および **[SQL Server]** の場合のみ、構成に複数のプロパティを含めることができます。  
  
9. [ウィザードの完了] というページが表示されたら、構成の名前を入力して **[完了]** をクリックします。  
  
10. **[パッケージ構成オーガナイザー]** ダイアログ ボックスで構成を確認します。  
  
11. **[閉じる]** をクリックします。  
  
## <a name="external-resources"></a>外部リソース  
  
-   msdn.microsoft.com の技術記事「 [Integration Services パッケージ構成について](https://go.microsoft.com/fwlink/?LinkId=165643)」  
  
-   ブログ エントリ「[コード - パッケージ構成でパッケージを作成する](https://go.microsoft.com/fwlink/?LinkId=217663)、 www.sqlis.com にします。  
  
-   ブログ エントリ「 [API のサンプル - がプログラムによって構成ファイル パッケージに追加](https://go.microsoft.com/fwlink/?LinkId=217664)、blogs.msdn.com します。  
  
## <a name="see-also"></a>関連項目  
 [[パッケージ構成]](../../2014/integration-services/package-configurations.md)   
 [パッケージの配置&#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)   
 [プログラムによる変数の使用](building-packages-programmatically/working-with-variables-programmatically.md)  
  
  
