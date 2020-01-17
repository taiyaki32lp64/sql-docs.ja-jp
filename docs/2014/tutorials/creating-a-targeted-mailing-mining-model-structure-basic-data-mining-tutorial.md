---
title: ターゲット メーリングのマイニング モデル構造 (基本的なデータ マイニング チュートリアル) の作成 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a9c67f29-0c47-4a5a-862b-db0f5213c2c9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2bd2e9d0decc730a59b63ee600bec2d080cc85fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62856163"
---
# <a name="creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial"></a>絞り込みメール配信マイニング モデル構造の作成 (基本的なデータ マイニング チュートリアル)
  絞り込みメール配信シナリオを作成するには、まず、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] のデータ マイニング ウィザードを使用して、新しいマイニング構造とデシジョン ツリー マイニング モデルを作成します。  
  
 このタスクでは、新しいマイニング構造をセットアップしに基づく初期マイニング モデルを追加、[!INCLUDE[msCoName](../includes/msconame-md.md)]デシジョン ツリー アルゴリズムです。 マイニング構造を作成するには、まずテーブルとビューを選択し、トレーニングに使用する列とテストに使用する列を特定します。  
  
### <a name="to-create-a-mining-structure-for-the-targeted-mailing-scenario"></a>絞り込みメール配信シナリオ用のマイニング構造を作成するには  
  
1.  ソリューション エクスプ ローラーで右クリック**マイニング構造**選択と**新しいマイニング構造**データ マイニング ウィザードを起動します。  
  
2.  **[データ マイニング ウィザードへようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **定義方法の選択**ことを確認します ページで、**既存のリレーショナル データベースまたはデータ ウェアハウスから**が選択されているし、をクリックし、 **次へ**します。  
  
4.  **データ マイニング構造の作成**] ページ [**を使用するデータ マイニング技法を指定しますか?** を選択します**Microsoft デシジョン ツリー**します。  
  
    > [!NOTE]  
    >  データ マイニング アルゴリズムが見つからないという警告が発生する場合は、プロジェクトのプロパティが適切に構成されていない可能性があります。 この警告は、プロジェクトが [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] サーバーからデータ マイニング アルゴリズムの一覧を取得しようとして、サーバーが見つからない場合に発生します。 既定では、[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]使用**localhost**サーバーとします。 別のインスタンスまたは名前付きインスタンスを使用している場合は、プロジェクトのプロパティを変更する必要があります。 詳細については、次を参照してください。 [Analysis Services プロジェクトを作成する&#40;Basic Data Mining Tutorial&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)します。  
  
5.  **[次へ]** をクリックします。  
  
6.  **データ ソース ビューの選択**ページで、**使用可能なデータ ソース ビュー**ウィンドウで選択します**Targeted Mailing**します。 クリックすることができます**参照**クリックして、テーブル、データ ソース ビューで表示**閉じる**ウィザードに戻ります。  
  
7.  **[次へ]** をクリックします。  
  
8.  **テーブルの種類の指定** ページで、チェック ボックスをオン、**ケース**列をケース テーブルとして使用し、をクリックし、vTargetMail **次へ**します。 ProspectiveBuyer テーブルは後でテストに使用するので、ここでは無視します。  
  
9. **トレーニング データの指定** ページで、少なくとも 1 つの予測可能列、1 つのキー列を識別して、1 つの入力、モデルの列。 チェック ボックスをオン、**予測可能**内の列、 **BikeBuyer**行。  
  
    > [!NOTE]  
    >  ウィンドウの下部に表示される警告に注意してください。 少なくとも 1 つを選択するまでに、次のページに移動することはできません**入力**と 1 つ**予測可能**列。  
  
10. クリックして**提案**を開く、**関連列の提示** ダイアログ ボックス。  
  
     **提案**に少なくとも 1 つの予測可能な属性が選択されているときにボタンが有効にします。 **関連列の提示** ダイアログ ボックスは、予測可能列に最も密接に関連する列の一覧し、属性、予測可能属性との関係を順序付けます。 します。 相関性の高い列 (信頼スコアが 95% を超えている場合) は、モデルに追加する対象として自動的に選択されます。  
  
     推奨事項を確認し、クリックして**キャンセル**toignore 提案します。  
  
    > [!NOTE]  
    >  をクリックすると**OK**、一覧内のすべての提案は、ウィザードで入力列としてマークされます。 提示内容の一部のみを使用する場合、値を手動で変更する必要があります。  
  
11. いることを確認のチェック ボックス、**キー**で列が選択されて、 **CustomerKey**行。  
  
    > [!NOTE]  
    >  データ ソース ビューのソース テーブルにキーが表示されていれば、その列がモデルのキーとして自動的に選択されます。  
  
12. チェック ボックスをオン、**入力**次の行に列。 複数の列をオンにするには、セルの範囲を強調表示し、&lt;localizedText&gt;Ctrl&lt;/localizedText&gt; キーを押しながらチェック ボックスをオンにします。  
  
    -   **経過時間**  
  
    -   **CommuteDistance**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **Gender**  
  
    -   **GeographyKey**  
  
    -   **HouseOwnerFlag**  
  
    -   **MaritalStatus**  
  
    -   **NumberCarsOwned**  
  
    -   **NumberChildrenAtHome**  
  
    -   **Region**  
  
    -   **TotalChildren**  
  
    -   **YearlyIncome**  
  
13. ページの左端の列で、次の行のチェック ボックスをオンにします。  
  
    -   **AddressLine1**  
  
    -   **AddressLine2**  
  
    -   **DateFirstPurchase**  
  
    -   **EmailAddress**  
  
    -   **FirstName**  
  
    -   **LastName**  
  
     上記の行の左の列のみがオンになっていることを確認します。 これらの列は構造に追加されますが、モデルには追加されません。 ただし、モデル作成後は、ドリルスルーやテストに使用できるようになります。 ドリルスルーの詳細については、次を参照してください[ドリルスルー クエリ&#40;データ マイニング。&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
14. **[次へ]** をクリックします。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [データ型とコンテンツの種類を指定する&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [テーブル型を指定&#40;データ マイニング ウィザード&#41;](../../2014/analysis-services/specify-table-types-data-mining-wizard.md)   
 [Data Mining Designer](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft デシジョン ツリー アルゴリズム](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md)  
  
  
