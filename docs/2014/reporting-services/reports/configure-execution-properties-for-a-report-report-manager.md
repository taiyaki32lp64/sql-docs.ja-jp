---
title: レポートの実行プロパティを構成する (レポート マネージャー) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- reports [Reporting Services], properties
- reports [Reporting Services], execution options
ms.assetid: 73cc8dcc-ef80-40d7-9739-d33bba0eb28a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f3de8f9e708149669a65b8abf4114227392aa15a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102708"
---
# <a name="configure-execution-properties-for-a-report--report-manager"></a>レポートの実行プロパティを構成する (レポート マネージャー)
  レポートの処理オプションでは、レポート データが取得されるタイミングを指定できます。 レポート データ処理のスケジュールを設定することは、外部データ ソースが特定の時刻に更新される場合 (日次または週次で更新されるデータ ウェアハウスなど) や、レポート要求のたびに同じデータが取得されるオーバーヘッドを回避したい場合などに効果的です。 また、外部のデータベース サーバーにかかる処理負荷を制御する場合や、まったく同じ一連のデータを扱う複数のユーザーに一貫性した結果を提供する場合に役立てることもできます。 変化しやすいデータを使用した場合、レポートを要求するたびに異なる結果が生成される可能性があります。 一方、レポート スナップショットでは、同時点のデータを含む他のレポートや分析ツールとの有効な比較が可能になります。  
  
 レポート スナップショットは、特定の時点で取得されたレイアウト指定およびクエリ結果を含むレポートです。 レポートを選択したときに最新のクエリ結果を取得する要求時レポートとは異なり、レポート スナップショットはスケジュールに従って処理され、その後、レポート サーバーに保存されます。 表示するレポート スナップショットを選択すると、レポート サーバーによってレポート サーバー データベースに格納されたレポートが取得され、スナップショット作成時点のレポートで最新だったデータとレイアウトを表示します。  
  
 レポート スナップショットは、特定の表示形式では保存されません。 その代わりに、レポート スナップショットは、ユーザーまたはアプリケーションが要求したときのみ、最終的な表示形式 (HTML など) で表示されます。 遅延表示により、スナップショットの移植性が実現します。 レポートは、要求元のデバイスまたは Web ブラウザーの適切な形式で表示できます。  
  
### <a name="to-configure-report-processing-options"></a>レポート処理オプションを構成するには  
  
1.  [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../report-manager-ssrs-native-mode.md) を開始します。  
  
2.  処理オプションを設定するレポートに移動し、そのレポートを開きます。  
  
 レポートの上にマウス ポインターを移動し、下矢印をクリックします。  
  
1.  ドロップダウン メニューで、 **[管理]** をクリックし、 **[処理オプション]** タブを選択します。  
  
2.   **[このレポートを実行スナップショットから表示する]** をクリックしてから、次のオプションのいずれかを選択します。  
  
    -   スナップショットを作成する場合は、 **[次のスケジュールを使用して、レポート実行スナップショットを作成する]** を選択し、レポート固有のスケジュールを定義するか、または **[共有スケジュール]** 一覧からスケジュールを選択します。  
  
    -   スナップショットをすぐに作成する場合は、 **[このページの [適用] ボタンをクリックしたときに、レポート スナップショットを作成します]** を選択します。  
  
3.  **[適用]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [レポート処理プロパティの設定](../report-server/set-report-processing-properties.md)   
 [レポートを開閉する (レポート マネージャー)](../reports/open-and-close-a-report-report-manager.md)   
 [[コンテンツ] ページ (レポート マネージャー)](../contents-page-report-manager.md)   
 [レポート サーバー コンテンツの管理 &#40;SSRS ネイティブ モード&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [[処理オプション] プロパティ ページ (レポート マネージャー)](../processing-options-properties-page-report-manager.md)  
  
  
