---
title: 'レッスン 10: 階層を作成する |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eb70d7d495d88ee62e98bf27f2b92bf569c98387
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078190"
---
# <a name="lesson-10-create-hierarchies"></a>レッスン 10: 階層を作成する
  このレッスンでは、階層を作成します。 階層は、複数のレベルに分類された列のグループです。たとえば、Geography という階層に、Country、State、County、および City というサブレベルを含めることができます。 階層は、あるレポート クライアント アプリケーション フィールドの一覧の他の列とは分けて表示できるため、クライアントのユーザーは簡単に移動し、レポートに含めることができます。 詳細については、[「階層 (SSAS テーブル)」](tabular-models/hierarchies-ssas-tabular.md) を参照してください。  
  
 階層を作成するには、*ダイアグラム ビュー*のモデル デザイナーを使用します。 階層の作成と管理は、データ ビューのモデル デザイナーではサポートされていません。  
  
 このレッスンを完了するまでに時間を推定するには。**20 分**  
  
## <a name="prerequisites"></a>前提条件  
 このトピックはテーブル モデリング チュートリアルの一部であり、チュートリアルでの順番に従って実行する必要があります。 このレッスンでは、タスクを実行する前に、前のレッスンを完了が必要があります。[レッスン 9:パースペクティブを作成する](lesson-8-create-perspectives.md)します。  
  
## <a name="create-hierarchies"></a>階層を作成する  
  
#### <a name="to-create-a-category-hierarchy-in-the-product-table"></a>Product テーブル内に Category 階層を作成するには  
  
1.  モデル デザイナーで をクリックして、`Model`メニューから、をポイント**モデル ビュー**、 をクリックし、**ダイアグラム ビュー**します。  
  
    > [!TIP]  
    >  モデル デザイナーの右上にあるミニマップ コントロールを使用すると、ダイアグラム ビューでのオブジェクトの表示方法を変更できます。 ダイアグラム ビューでモデルを移動した場合、プロジェクトを保存する際にそのビューが保持されます。  
  
2.  モデル デザイナーで右クリックし、`Product`テーブル、およびクリックして**階層の作成**です。 テーブル ウィンドウの下部に新しい階層が表示されます。  
  
3.  」と入力して、階層の名前を変更、階層名で`Category`、し、ENTER キーを押します。  
  
4.  `Product`テーブルで、をクリックして、 **Product Category Name**列で、ドラッグ、`Category`階層、およびの上に、リリース、`Category`名。  
  
5.  `Category`階層を右クリックし、 **Product Category Name**列順にクリックします**の名前を変更**、し、入力`Category`します。  
  
    > [!NOTE]  
    >  階層内の列の名前を変更しても、テーブル内のその列の名前は変更されません。 階層内の列は、テーブル内の列の 1 つの表現形態に過ぎません。  
  
6.  `Product`テーブルを右クリックして、 **Product Subcategory Name**列で、コンテキスト メニューのをポイント**階層を追加する**、順にクリックします`Category`。  
  
7.  名前を変更**Product Subcategory Name**に`Subcategory`します。  
  
8.  クリックしてドラッグを使用するかを使用して、**階層を追加する**コンテキスト メニューでコマンドを追加、**モデル名**と**製品名**列 (この順序) で下に配置し、**Product Subcategory Name**列。 これらの列の名前を変更`Model`と`Product`、それぞれします。  
  
#### <a name="to-create-hierarchies-in-the-date-table"></a>Date テーブル内に階層を作成するには  
  
1.  モデル デザイナーで、 **Date** テーブルをクリックし、 **[階層の作成]** をクリックします。  
  
2.  階層の名前を **Calendar**に変更します。  
  
3.  次の列を (順序どおりに) 追加し、名前を次のように変更します。  
  
    |[列]|変更後の名前|  
    |------------|----------------|  
    |Calendar Year|年|  
    |Calendar Semester|Semester|  
    |Calendar Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|日|  
  
4.  **Date** テーブルで上記の手順を繰り返し、次の列を含んだ **Fiscal** 階層を作成します。  
  
    |[列]|変更後の名前|  
    |------------|----------------|  
    |Fiscal Year|年|  
    |Fiscal Semester|Semester|  
    |Fiscal Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|日|  
  
5.  最後に、 **Date** テーブルで上記の手順を繰り返し、次の列を含んだ **Production Calendar** 階層を作成します。  
  
    |[列]|変更後の名前|  
    |------------|----------------|  
    |Calendar Year|年|  
    |Week Number Of Year|Week|  
    |Day Of Week|日|  
  
## <a name="next-steps"></a>次の手順  
 このチュートリアルを続行するには、次のレッスンに移動します。[レッスン 11:パーティションの作成](lesson-10-create-partitions.md)です。  
  
  
