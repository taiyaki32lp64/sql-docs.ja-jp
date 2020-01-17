---
title: コール センター構造 (中級者向けデータ マイニング チュートリアル) へのロジスティック回帰モデルの追加 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 97abb77a-346c-44fa-8959-688dee1af6a8
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 32e66a84dea20964c11c7de0aa568530aa8c28c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62823279"
---
# <a name="adding-a-logistic-regression-model-to-the-call-center-structure-intermediate-data-mining-tutorial"></a>コール センター構造へのロジスティック回帰モデルの追加 (中級者向けデータ マイニング チュートリアル)
  コール センターの業務に影響する可能性のある要因を分析すると共に、スタッフのサービス品質を向上させるための具体的な改善案を提出するように求められました。 ここでは、調査モデルの構築に使用したものと同じマイニング構造を使用し、予測作成用のマイニング モデルを追加します。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のロジスティック回帰モデルは、ニューラル ネットワークのアルゴリズムを基礎としているため、ニューラル ネットワーク モデルと同等の柔軟性と機能を備えながらも、 バイナリ結果を予測するという目的に特に適したモデルと言えます。  
  
 このシナリオでは、ニューラル ネットワーク モデルに使用したものと同じマイニング構造を使用します。 ただし、新しいモデルを実務上の目的に合わせてカスタマイズします。 ここでは、サービス品質を向上させることと、経験を積んだオペレーターが何人必要かを特定することが目的であるため、それらの値を予測するモデルを設定します。  
  
 コール センター データに基づくすべてのモデルの類似性をできる限り確保するために、前の作業と同じシード パラメーターを使用します。 シード パラメーターを設定すると、モデルでのデータ処理の開始位置が同じになり、データのアーティファクトによるバリエーションを最小限に抑えることができます。  
  
### <a name="to-add-a-new-mining-model-to-the-call-center-mining-structure"></a>コール センターのマイニング構造に新しいマイニング モデルを追加するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]、ソリューション エクスプ ローラーで、マイニング構造を右クリックして**Call Center Binned**、選び**デザイナーを開く**します。  
  
2.  データ マイニング デザイナーでクリックして、**マイニング モデル**タブ。  
  
3.  クリックして**関連マイニング モデル作成**です。  
  
4.  **マイニング モデルの新しい** ダイアログ ボックスの**モデル名**、型`Call Center - LR`します。  **アルゴリズム名**、 **Microsoft ロジスティック回帰**します。  
  
5.  **[OK]** をクリックします。  
  
     新しいマイニング モデルを表示、**マイニング モデル**タブ。  
  
### <a name="to-customize-the-logistic-regression-model"></a>ロジスティック回帰モデルをカスタマイズするには  
  
1.  新しいマイニング モデルの列に`Call Center - LR`、キーとしてファクト CallCenter ID のままにします。  
  
2.  ServiceGrade とレベルを 2 つの演算子の値を変更**Predict**します。  
  
     これらの列は、入力および予測の両方に使用されます。 本質的には、同じデータについて、2 つの別個のモデルを作成していることになります。ここでは、オペレーターの数を予測するモデルとサービス グレードを予測するモデルを作成しています。  
  
3.  その他のすべての列を変更**入力**します。  
  
### <a name="to-specify-the-seed-and-process-the-models"></a>シードを指定してモデルを処理するには  
  
1.  **マイニング モデルの** タブで、名前付き Call Center - LR、モデルの場合は、列を右クリックし、選択**アルゴリズム パラメーターの設定**します。  
  
2.  HOLDOUT_SEED パラメーターの行で、空のセルをクリックします。**値**、および種類`1`します。 **[OK]** をクリックします。  
  
    > [!NOTE]  
    >  関連するすべてのモデルで同じシードを使用する限り、シードとしてどのような値を選択するかは特に重要ではありません。  
  
3.  **マイニング モデル**メニューの **マイニング構造の処理とすべてのモデル**します。 クリックして**はい**サーバーに更新されたデータ マイニング プロジェクトを配置します。  
  
4.  **マイニング モデルの処理**ダイアログ ボックスで、をクリックして**実行**します。  
  
5.  をクリックして**閉じます**を閉じる、**処理の進行状況** ダイアログ ボックスをクリック**閉じます**で再度、**マイニング モデルの処理** ダイアログ ボックス。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [コール センター モデルの予測の作成&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [処理の要件および注意事項 &#40;データ マイニング&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
