---
title: 表示し、予測クエリの結果の保存 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- prediction queries [Analysis Services]
- viewing prediction query results
- displaying prediction query results
- Mining Model Prediction [Analysis Services], viewing results
ms.assetid: abba4d24-3619-44c1-8279-88f27ad627d3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9abaf092d00a8acaf6c0b3ef963c940199068ce9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082708"
---
# <a name="view-and-save-the-results-of-a-prediction-query"></a>予測クエリの結果の表示および保存
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の予測クエリ ビルダーを使用してクエリを定義した後は、クエリ結果ビューに切り替えてクエリを実行し、結果を表示できます。  
  
 予測クエリの結果は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトで定義される任意のデータ ソースのテーブルに保存できます。 新しいテーブルを作成するか、または既存のテーブルにクエリ結果を保存できます。 既存のテーブルに結果を保存する場合は、テーブルに現在保存されているデータを上書きするように選択できます。上書きしない場合、クエリ結果は、テーブルの既存のデータに追加されます。  
  
### <a name="run-a-query-and-view-the-results"></a>クエリを実行し、結果を表示する  
  
1.  **のデータ マイニング デザイナーの** [マイニング モデル予測] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]タブにあるツール バーで、 **[結果]** をクリックします。  
  
     クエリ結果ビューが表示され、クエリが実行されます。 結果がビューアーのグリッドに表示されます。  
  
### <a name="save-the-results-of-a-prediction-query-to-a-table"></a>予測クエリの結果をテーブルに保存する  
  
1.  データ マイニング デザイナーの **[マイニング モデル予測]** タブのツール バーで、 **[クエリ結果の保存]** をクリックします。  
  
     **[データ マイニングのクエリ結果を保存]** ダイアログ ボックスが開きます。  
  
2.  **[データ ソース]** 一覧からデータ ソースを選択するか、 **[新規作成]** をクリックして新しいデータ ソースを作成します。  
  
3.  **[テーブル名]** ボックスにテーブルの名前を入力します。 同じテーブル名が既に存在する場合、テーブルの内容をクエリ結果に置き換えるには、 **[存在する場合は上書きする]** チェック ボックスをオンにします。 テーブルの内容を上書きしない場合は、このチェック ボックスをオフにします。 新しいクエリ結果が、テーブルの既存のデータに追加されます。  
  
4.  データ ソース ビューにテーブルを追加する場合は、 **[DSV に追加]** からデータ ソース ビューを選択します。  
  
5.  **[保存]** をクリックします。  
  
    > [!WARNING]  
    >  保存先で階層的な行セットがサポートされていない場合は、結果に FALTTENED キーワードを追加して、フラット テーブルとして保存できます。  
  
  
