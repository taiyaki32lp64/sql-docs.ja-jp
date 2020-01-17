---
title: 'レッスン 9: パースペクティブを作成する |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 55b0f0d0-1cdf-4876-9c3d-d0c848be3f5d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd395e605bfde9d34ed0dc4f16060812464efb56
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078250"
---
# <a name="lesson-9-create-perspectives"></a>レッスン 9: パースペクティブを作成する
  このレッスンでは、Internet Sales パースペクティブを作成します。 パースペクティブとは、モデルの一部を表示可能なサブセットとして定義するものです。これにより、ビジネス固有またはアプリケーション固有のビューポイントを的を絞って作成できます。 パースペクティブを使用してモデルに接続すると、そのパースペクティブ内に定義されたモデル オブジェクト (テーブル、列、メジャー、階層、および KPI) のみがフィールドとして表示されます。  
  
 このレッスンで作成する Internet Sales パースペクティブでは、Customer テーブル オブジェクトが除外されます。 特定のオブジェクトをビューから除外するパースペクティブを作成した場合、そのオブジェクトはモデル内に依然として存在しますが、レポート クライアントのフィールドの一覧には表示されなくなります。 計算列とメジャーは、パースペクティブに含まれているかどうかに関係なく、除外されたデータ オブジェクトに基づく計算を引き続き実行できます。  
  
 このレッスンの目的は、パースペクティブの作成方法を知ることと、テーブル モデル作成ツールに慣れることです。 後でこのモデルにテーブルを追加する場合は、追加のパースペクティブを作成して、モデルに対する異なるビューポイント (Inventory や Sales Force など) を定義できます。  
  
 詳細については、「[パースペクティブ (SSAS テーブル)](tabular-models/perspectives-ssas-tabular.md)」を参照してください。  
  
 このレッスンを完了するまでに時間を推定するには。**5 分**  
  
## <a name="prerequisites"></a>前提条件  
 このトピックはテーブル モデリング チュートリアルの一部であり、チュートリアルでの順番に従って実行する必要があります。 このレッスンでは、タスクを実行する前に、前のレッスンを完了が必要があります。[レッスン 8: 主要業績評価指標の作成](lesson-7-create-key-performance-indicators.md)です。  
  
## <a name="create-perspectives"></a>パースペクティブを作成する  
  
#### <a name="to-create-an-internet-sales-perspective"></a>Internet Sales パースペクティブを作成するには  
  
1.  モデル デザイナーで、クリックして、**モデル** メニューをクリック**パースペクティブ**します。  
  
2.  **[パースペクティブ]** ダイアログ ボックスで、 **[新しいパースペクティブ]** をクリックします。  
  
3.  パースペクティブの名前を変更するには、ダブルクリック、**新しいパースペクティブ 1**列見出しをして入力`Internet Sales`します。  
  
4.  **フィールド**、次のテーブルを選択する**日付**、 **Geography**、**製品**、 **Product Category**、 **Product Subcategory**、および`Internet Sales`します。  
  
     Customer テーブルおよびそのすべての列をこのパースペクティブから除外したことに注意してください。 後ほど、レッスン 12 で、"Excel で分析" 機能を使用してこのパースペクティブをテストします。 Excel ピボットテーブルのフィールドの一覧には、Customer テーブルを除く各テーブルが含まれます。  
  
5.  選択内容を確認し、 **Customer** テーブルがオフになっていることを確認して、 **[OK]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
 このチュートリアルを続行するには、次のレッスンに移動します。[レッスン 10:階層を作成する](lesson-9-create-hierarchies.md)します。  
  
  
