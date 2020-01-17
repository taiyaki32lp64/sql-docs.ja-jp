---
title: レッスン 13:Excel で分析 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ce717071-193b-4c99-9654-c7a613e16327
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6a1564a2b190703e011624162ad4bc25fd5de794
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079189"
---
# <a name="lesson-13-analyze-in-excel"></a>レッスン 13:[Excel で分析]
  このレッスンでは、 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] で "Excel で分析" 機能を使用して Microsoft Excel を開き、モデル ワークスペースへのデータ ソース接続を自動的に作成して、ワークシートにピボットテーブルを自動的に追加します。 "Excel で分析" 機能を使用すると、モデルを配置する前に、モデル デザインの有効性をすばやく簡単にテストできます。 このレッスンでは、データの分析は行いません。 このレッスンの目的は、モデル作成者が、モデル デザインのテストに使用できるツールに慣れることです。 モデル作成者向けの "Excel で分析" 機能を使用する場合とは異なり、エンド ユーザーは Excel や [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] などのクライアント レポート アプリケーションを使用して、配置済みのモデル データへの接続と参照を行います。  
  
 このレッスンを完了するには、[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] と同じコンピューター上に Excel がインストールされている必要があります。 詳細については、「[Excel で分析 (SSAS テーブル)](tabular-models/analyze-in-excel-ssas-tabular.md)」を参照してください。  
  
 このレッスンを完了するまでに時間を推定するには。**20 分**  
  
## <a name="prerequisites"></a>前提条件  
 このトピックはテーブル モデリング チュートリアルの一部であり、チュートリアルでの順番に従って実行する必要があります。 このレッスンでは、タスクを実行する前に、前のレッスンを完了が必要があります。[レッスン 11:パーティションの作成](lesson-10-create-partitions.md)です。  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>既定のパースペクティブと Internet Sales パースペクティブを使用した参照  
 これらの最初のタスクの両方、既定のパースペクティブを含むすべてのモデル オブジェクトを使用して、モデルの参照し、もレッスン 8 で作成した Internet Sales パースペクティブを使用しています。パースペクティブを作成します。 Internet Sales パースペクティブでは、Customer テーブル オブジェクトが除外されます。  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>既定のパースペクティブを使用して参照するには  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]で、 **[モデル]** メニューの **[Excel で分析]** をクリックします。  
  
2.  **[Excel で分析]** ダイアログ ボックスで、 **[OK]** をクリックします。  
  
     Excel で新しいブックが開きます。 現在のユーザー アカウントを使用してデータ ソース接続が作成され、既定のパースペクティブを使用して表示可能なフィールドが定義されます。 ピボットテーブルがワークシートに自動的に追加されます。  
  
3.  Excel で、**ピボット テーブル フィールド リスト**に注意してください、**日付**と**Internet Sales**メジャーが表示されるだけでなく**顧客**、 **日付**、 **Geography**、**製品**、 **Product Category**、 **Product Subcategory**、および**Internet Sales**それぞれの列のすべてのテーブルが表示されます。  
  
4.  ブックを保存せずに Excel を閉じます。  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>Internet Sales パースペクティブを使用して参照するには  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]で、 **[モデル]** メニューの **[Excel で分析]** をクリックします。  
  
2.  **[Excel で分析]** ダイアログ ボックスの **[現在の Windows ユーザー]** を選択したままにして、 **[パースペクティブ]** ドロップダウン リストで **[Internet Sales]** を選択し、 **[OK]** をクリックします。 Excel が開きます。  
  
3.  Excel の **[ピボットテーブルのフィールドリスト]** で、フィールドリストから Customer テーブルが除外されます。  
  
## <a name="browse-using-roles"></a>ロールを使用した参照  
 ロールはテーブル モデルに欠かせない要素です。 ユーザーがメンバーとして追加されているロールが少なくとも 1 つなければ、ユーザーはモデルを使用してデータにアクセスし、分析することができません。 "Excel で分析" 機能を利用して、定義したロールをテストすることができます。  
  
#### <a name="to-browse-by-using-the-internet-sales-manager-user-role"></a>Internet Sales Manager ユーザー ロールを使用して参照するには  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]で、 **[モデル]** メニューの **[Excel で分析]** をクリックします。  
  
2.  **[Excel で分析]** ダイアログ ボックスの **[モデルへの接続に使用するユーザー名またはロールの指定]** で、 **[ロール]** を選択します。次にドロップダウン リストで **[Internet Sales Manager]** を選択し、 **[OK]** をクリックします。  
  
     Excel で新しいブックが開きます。 ピボット テーブルが自動的に作成されます。 [ピボット テーブル フィールド リスト] には、新しいモデルで使用できるすべてのデータ フィールドが表示されます。  
  
## <a name="next-steps"></a>次の手順  
 このチュートリアルを続行するには、次のレッスンに移動します。[レッスン 14:デプロイ](lesson-13-deploy.md)します。  
  
  
