---
title: 予測クエリを手動で編集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying prediction queries
- Mining Model Prediction [Analysis Services], modifying prediction queries
- manual prediction query modification [Analysis Services]
ms.assetid: 9f6a9298-49d5-4675-ad49-977a47dff5a6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ce2086e998704e893beaa92aabd2e51129a0450f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084207"
---
# <a name="manually-edit-a-prediction-query"></a>手動での予測クエリの編集
  予測クエリ ビルダーでクエリのデザインを終えたら、データ マイニング デザイナーの **[マイニング モデル予測]** タブにあるクエリ テキスト ビューに切り替えて、クエリを変更できます。 画面の下部に、クエリ ビルダーによって作成されたクエリを含んでいるテキスト エディターが表示されます。  
  
 クエリ テキスト ビューに切り替えると、クエリへの追加を行う場合に便利です。 たとえば、WHERE 句や ORDER BY 句を追加できます。  
  
 予測クエリ ビルダーのグリッドを使用してオブジェクトおよび列の名前を挿入し、個々の予測関数の構文を設定してから、手動編集モードに切り替えて、パラメーター値を変更します。  
  
> [!NOTE]  
>  **クエリ テキスト** ビューから **デザイン** ビューに戻ると、 **クエリ テキスト** ビューで行った変更は失われます。  
  
### <a name="modify-a-query"></a>クエリの変更  
  
1.  **のデータ マイニング デザイナーにある** [マイニング モデル予測] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]タブで、 **[SQL]** をクリックします。  
  
     画面の下部にあるグリッドが、クエリを含んでいるテキスト エディターに置き換わります。 このエディターでクエリの変更を入力できます。  
  
2.  クエリを実行するには、 **[マイニング モデル]** メニューの **[結果]** をクリックするか、クエリ結果に切り替えるボタンをクリックします。  
  
    > [!NOTE]  
    >  作成したクエリが無効であれば、[結果] ウィンドウにはエラーも結果も表示されません。 **[デザイン]** ボタンをクリックするか、 **[マイニング モデル]** メニューの **[デザイン]** または **[クエリ]** をクリックして問題を修正し、再度クエリを実行してください。  
  
## <a name="see-also"></a>参照  
 [データ マイニング クエリ](data-mining-queries.md)   
 [予測クエリ ビルダー &#40;データ マイニング&#41;](../prediction-query-builder-data-mining.md)   
 [レッスン 6:予測の作成と操作&#40;基本的なデータ マイニング チュートリアル&#41;](../../tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
  
  
