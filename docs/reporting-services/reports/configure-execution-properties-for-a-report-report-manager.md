---
title: レポートの実行プロパティを構成する - Reporting Services | Microsoft Docs
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- reports [Reporting Services], properties
- reports [Reporting Services], execution options
ms.assetid: 73cc8dcc-ef80-40d7-9739-d33bba0eb28a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6dfb24b6314529b19fb7bb5edb81534f30dc018a
ms.sourcegitcommit: c0e48b643385ce19c65ca6e348ce83b2d22b6514
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492750"
---
# <a name="configure-execution-properties-for-a-report"></a>レポートの実行プロパティを構成する
  レポートの処理オプションでは、レポート データが取得されるタイミングを指定できます。 レポート データ処理のスケジュールを設定することは、外部データ ソースが特定の時刻に更新される場合 (日次または週次で更新されるデータ ウェアハウスなど) や、レポート要求のたびに同じデータが取得されるオーバーヘッドを回避したい場合などに効果的です。 また、外部のデータベース サーバーにかかる処理負荷を制御する場合や、まったく同じ一連のデータを扱う複数のユーザーに一貫性した結果を提供する場合に役立てることもできます。 変化しやすいデータを使用した場合、レポートを要求するたびに異なる結果が生成される可能性があります。 一方、レポート スナップショットでは、同時点のデータを含む他のレポートや分析ツールとの有効な比較が可能になります。  
  
 レポート スナップショットは、特定の時点で取得されたレイアウト指定およびクエリ結果を含むレポートです。 レポートを選択したときに最新のクエリ結果を取得する要求時レポートとは異なり、レポート スナップショットはスケジュールに従って処理され、その後、レポート サーバーに保存されます。 表示するレポート スナップショットを選択すると、レポート サーバーによってレポート サーバー データベースに格納されたレポートが取得され、スナップショット作成時点のレポートで最新だったデータとレイアウトを表示します。  
  
 レポート スナップショットは、特定の表示形式では保存されません。 その代わりに、レポート スナップショットは、ユーザーまたはアプリケーションが要求したときのみ、最終的な表示形式 (HTML など) で表示されます。 遅延表示により、スナップショットの移植性が実現します。 レポートは、要求元のデバイスまたは Web ブラウザーの適切な形式で表示できます。  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
## <a name="to-configure-report-processing-options"></a>レポート処理オプションを構成するには  
  
1.  [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896) を開始します。  
  
2.  処理オプションを設定するレポートに移動し、そのレポートを開きます。  
  
 レポートの上にマウス ポインターを移動し、下矢印をクリックします。  
  
1.  ドロップダウン メニューで、 **[管理]** をクリックし、 **[処理オプション]** タブを選択します。  
  
2.  **[このレポートを実行スナップショットから表示する]** をクリックしてから、次のオプションのいずれかを選択します。  
  
    -   スナップショットを作成する場合は、 **[次のスケジュールを使用して、レポート実行スナップショットを作成する]** を選択し、レポート固有のスケジュールを定義するか、または **[共有スケジュール]** 一覧からスケジュールを選択します。  
  
    -   スナップショットをすぐに作成する場合は、 **[このページの [適用] ボタンをクリックしたときに、レポート スナップショットを作成します]** を選択します。  
  
3.  **[適用]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [レポート処理プロパティの設定](../../reporting-services/report-server/set-report-processing-properties.md)   
 [[コンテンツ] ページ (レポート マネージャー)](https://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378)   
 [レポート サーバー コンテンツの管理 &#40;SSRS ネイティブ モード&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [[処理オプション] プロパティ ページ &#40;レポート マネージャー&#41;](https://msdn.microsoft.com/library/28f07c70-7132-4d15-9505-4fdf31dc9cc0)  
  
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
  
## <a name="to-configure-report-execution-properties"></a>レポート実行プロパティを構成するには  
  
「[レポート サーバーの Web ポータル (SSRS ネイティブ モード)](../../reporting-services/web-portal-ssrs-native-mode.md)」から:  
  
1. 実行プロパティを構成するレポートに移動します。  
  
2. 右クリックし、レポート**管理**ドロップダウン メニューから。

3. 選択、**履歴スナップショット**タブを表示する、**履歴スナップショット**ページ。  
  
4. 選択**スケジュールと設定**ボタンをクリックし、確認**スケジュールに従って履歴スナップショットを作成する**がチェックされていない場合。
  
5. いずれかを選択、**共有スケジュール**または**レポート固有スケジュール**に応じて。  
  
6. **[詳細設定]** セクションで、目的の**保有**履歴スナップショットのポリシー。  
  
7. **[適用]** を選択します。  
  
   >[!NOTE]
   >スナップショットをすぐに作成する場合は、選択、**新しい履歴スナップショット**ボタンの代わりに、**スケジュールと設定**ボタン、およびレポートのスナップショットがすぐに作成されます。  
  
## <a name="see-also"></a>参照  
 [レポート処理プロパティの設定](../../reporting-services/report-server/set-report-processing-properties.md)   
 [レポート サーバー コンテンツの管理 (SSRS ネイティブ モード)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [レポート処理プロパティの設定](../../reporting-services/report-server/set-report-processing-properties.md)   

::: moniker-end