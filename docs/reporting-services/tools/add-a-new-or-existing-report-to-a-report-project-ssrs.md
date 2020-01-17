---
title: 新規または既存のレポートをレポート プロジェクトに追加する (SSRS) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], creating
ms.assetid: 8bc0bb53-ad8a-464d-bb6a-7fea5fa62c5c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bf9345d7f707c1cebc086b9c3ff8a1d69997854c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65576801"
---
# <a name="add-a-new-or-existing-report-to-a-report-project-ssrs"></a>新規または既存のレポートをレポート プロジェクトに追加する (SSRS)
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]では、レポート ウィザードを使用するか、新しい空のレポートをプロジェクトに追加することによって、 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] のページ分割された新しいレポートを追加できます。 既存のレポートを追加することもできます。 レポートを追加すると、そのレポートの名前が、プロジェクトの **[レポート]** フォルダーに表示されます。  
  
> [!NOTE]  
>  既存のデータ ソースを使ったレポートをプレビューするには、レポート作成クライアントから、そのデータ ソースにアクセスするための権限が必要です。 詳細については、「 [データ接続、データ ソース、および接続文字列](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)」を参照してください。  
  
 レポートを追加した後、データ ソースやデータセットを定義したり、レポート レイアウトをデザインしたりできます。 開始するには、「[基本的なテーブル レポートの作成 &#40;SSRS チュートリアル&#41;](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)」または「[テーブル &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="to-add-a-new-report-using-the-report-wizard"></a>レポート ウィザードを使って新しいレポートを追加するには  
  
1.  ソリューション エクスプローラーで [レポート] フォルダーを右クリックし、 **[新しいレポートの追加]** をクリックします。 **[レポート ウィザード]** ダイアログ ボックスが表示されます。  
  
     ウィザードの手順に従うことで、データ ソースを作成したり、クエリでデータセットを作成したり、グループを定義したり、レイアウトを指定したり、レポートを作成したりできます。 次のような手順で構成されます。  
  
    -   **データ ソースの選択** レポート作成の最初の手順は、データ ソースを定義することです。 レポート ウィザードにより、レポート プロジェクト内のすべての共有データ ソースが表示されます。同時に、新しいデータ ソースを作成するオプションも表示されます。  
  
    -   **クエリのデザイン** 次の手順は、クエリを設計することです。 クエリの作成方法としては、クエリ文字列を入力する以外にも、クエリ デザイナーを使用する方法や、別のレポートからクエリをインポートする方法もあります。 クエリ デザイナーの詳細については、「 [Reporting Services クエリ デザイナー](https://msdn.microsoft.com/library/07efd3f1-804f-45f7-b62a-3e727a3d9835)」を参照してください。  
  
    -   **レポートの種類の選択** 次の手順は、作成するレポートの種類を選択することです。 表形式のレポートか、マトリックス形式のレポートを選択することができます。 表形式のレポートは、列数が固定されます。 マトリックス形式のレポート (クロス集計レポート) は、クエリの結果により列数が変化します。 マップ レポートには、地理的背景に対する分析が表示されます。  
  
    -   **レポートの名前付け**  最後の手順は、レポートに名前を付け、レポートに含まれるフィールドを確認することです。 すべての手順が完了したら、レポート デザイナーはレポートを作成し、それをレポート サーバー プロジェクトに追加します。  
  
## <a name="to-add-a-new-blank-report"></a>新しい空のレポートを追加するには  
  
1.  **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。  
  
2.  **[テンプレート]** の **[レポート]** をクリックします。  
  
3.  **[追加]** をクリックします。  
  
     新しい空のレポートがプロジェクトに追加され、デザイン画面に表示されます。  
  
## <a name="to-add-an-existing-report"></a>既存のレポートを追加するには  
  
1.  **[プロジェクト]** メニューの **[追加]** をクリックし、  **[既存の項目]** をクリックします。  
  
2.  .rdl ファイルがある場所に移動して、ファイルを選択し、 **[追加]** をクリックします。  
  
     レポートがプロジェクトの **[レポート]** フォルダーに追加されます。 プロジェクトを閉じてから開き直すと、一連のレポートがアルファベット順に並べ替えられます。  
  
## <a name="see-also"></a>参照  
 [Reporting Services チュートリアル &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
 その他の質問 [Reporting Services のフォーラムにアクセスします](https://go.microsoft.com/fwlink/?LinkId=620231)
  
  
