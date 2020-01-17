---
title: レポートへのドリルスルー アクションの追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 153729c4-d01e-4629-b78f-0cfd5a7f83da
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cfae70562bf244ba9294f31f1dcba9d85f5699f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574868"
---
# <a name="add-a-drillthrough-action-on-a-report-report-builder-and-ssrs"></a>レポートへのドリルスルー アクションの追加 (レポート ビルダーおよび SSRS)
  メイン レポートのリンクをクリックすると開くレポートが *詳細レポート*です。 このドリルスルー リンクを使用すると、ドリルスルー アクションを実行できます。  
  
 詳細レポートはメイン レポートと同じレポート サーバーにパブリッシュする必要がありますが、別のフォルダーでもかまいません。 テキスト ボックス、画像、グラフ上のデータ ポイントなど、 **Action** プロパティがあるアイテムにドリルスルー リンクを追加できます。  
  
 レポートにドリルスルー リンクを追加するには、まず、メイン レポートからリンクする詳細レポートを作成する必要があります。 詳細レポートには、通常、元の要約レポートに含まれるアイテムについての詳細が含まれています。また、多くの場合、メイン レポートから渡されるパラメーターに基づいて詳細レポートをフィルターするパラメーターも含まれます。 詳細レポートの作成方法については、「[詳細レポート (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/drillthrough-reports-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-drillthrough-action"></a>ドリルスルー アクションを追加するには  
  
1.  デザイン ビューで、リンクを追加するテキスト ボックス、画像、またはグラフを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  アイテムの **[プロパティ]** ダイアログ ボックスで **[アクション]** をクリックします。  
  
3.  **[レポートに移動する]** を選択します。 このオプションのダイアログ ボックスに追加のセクションが表示されます。  
  
4.  **[レポートの指定]** で、 **[参照]** をクリックして移動先レポートを指定するか、移動先レポートの名前を入力します。 または、式 ( **[fx]** ) ボタンをクリックしてレポート名の式を作成します。  
  
     詳細レポートのパスの形式は、ネイティブ モードと SharePoint 統合モードとで異なります。 参照によってレポートを指定した場合は、パスが正しい形式で指定されます。 詳細については、「[外部アイテムへのパスの指定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)」を参照してください。  
  
     詳細レポートのパラメーターを指定する必要がある場合は、次の手順に従ってください。  
  
5.  **[レポートの実行に以下のパラメーターを使用]** で、 **[追加]** をクリックします。 パラメーター グリッドに、新しい行が追加されます。  
  
    -   **[名前]** ボックスで、詳細レポートのレポート パラメーターの名前を一覧から選択するか入力します。  
  
        > [!NOTE]  
        >  パラメーターの一覧にある名前は、対象となるレポートで予測されるパラメーターと完全に一致する必要があります。 たとえば、パラメーター名の大文字と小文字の違いも一致する必要があります。 これらの名前が一致しない場合、または予測されるパラメーターが一覧にない場合は、詳細レポートは失敗します。  
  
    -   **[値]** に、詳細レポートのパラメーターに渡す値を入力するか、選択します。  
  
        > [!NOTE]  
        >  レポート パラメーターに渡す値には、結果が値になる式を指定できます。 値の一覧にある式には、現在のレポートのフィールドの一覧が含まれています。  
  
     レポートのパラメーターを非表示にする方法については、「[レポート パラメーターの追加、変更、または削除 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)」を参照してください。  
  
6.  (省略可) テキスト ボックスの場合、リボンの **[ホーム]** タブでテキストの色と効果を変更してそのテキストがリンクであることをユーザーに示すと便利です。  
  
7.  リンクをテストするには、レポートを実行し、このリンクを設定したレポート アイテムをクリックします。  
  
## <a name="see-also"></a>参照  
 [アクション プロパティ ダイアログ ボックス (レポート ビルダーおよび SSRS)](https://msdn.microsoft.com/library/2c5d915b-4f97-42cf-b8f1-49ca3ff3d0f9)   
 [グラフでのデータ ポイントの書式設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [系列へのツールヒントの表示 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
  
