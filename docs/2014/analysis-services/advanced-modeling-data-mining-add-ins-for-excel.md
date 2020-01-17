---
title: 高度なモデリング (データ マイニング Excel 用アドイン) |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures, creating
ms.assetid: 042270a3-6ec7-4b52-b2ba-2adb6c4740d5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 669fa1fcd9e4802a4d4102120a373dd615741017
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062736"
---
# <a name="advanced-modeling-data-mining-add-ins-for-excel"></a>高度なモデリング (Excel 用データ マイニング アドイン)
  使用することができます、**詳細**データ モデリング オプションをカスタム データ マイニング構造とモデル パラメーターを作成するウィザードで作成したものと異なる。 このセクションで説明する 2 つのウィザードでは、まったく新しいデータ マイニング構造を作成したり、既存のデータ マイニング構造に適用する新しいマイニング モデルを作成したりできます。  
  
## <a name="create-mining-structure"></a>マイニング構造の作成  
 ![マイニング構造の作成 ボタン、データ マイニング リボン](media/dmc-createstruct.gif "Create Mining Structure ボタン、データ マイニング リボン")  
  
 **マイニング構造の作成ウィザード**新しいデータ マイニング構造を構築するのに役立ちます。 構造とは、指定したデータ ソースから抽出したデータのコレクションです。  マイニング構造は、基になる新しいデータで更新できますが、マイニング構造を作成するときは、分析時のデータの使用方法を定義するデータ型と名前を定義します。  
  
 Excel テーブル、Excel 範囲、または [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データ ソース ビューとして定義済みである外部データ ソースの任意のデータをデータ ソースとして、構造を構築することができます。  
  
 テスト用および検証用のデータを構造ごとに確保することができます。 これを作成して*予約データ セット*データ ソースを設定するとき、構造に基づくすべてのモデルが一貫性のあるデータ セットを使用してテストするためにできることを確認できます。  
  
 マイニング構造を作成した後、複数のモデルを追加して、異なる分析方法を適用することができます。  
  
 使用する方法についての詳細、**マイニング構造の作成ウィザード**を参照してください[Create Mining Structure &#40;SQL Server データ マイニング アドイン&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)します。  
  
## <a name="add-model-to-structure"></a>構造へのモデルの追加  
 ![モデル構造 ボタンを追加](media/dmc-addmodel.gif "モデル構造 ボタンの追加")  
  
 新しいモデルを構造に追加する場合は、別のアルゴリズムまたは別のパラメーターを使用してデータを分析します。 このオプションは、データ マイニング クライアント ツールで公開されていないアルゴリズムの 1 つを使用してモデルを作成する場合に特に役立ちます。  
  
 たとえば、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] でサポートされている次のようなアルゴリズムを使用することができます。  
  
-   線形回帰  
  
-   シーケンス クラスター  
  
-   入れ子になったデータ セットのアソシエーション分析  
  
 マイニング構造の種類を確認してくださいを参照できます、モデルとに格納されている構造体[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]いずれかをクリックして**モデルの管理**または**参照**します。  
  
 使用できるのは、現在のセッション中に作成されたデータ マイニング構造、または、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のインスタンスに保存されたマイニング構造に限定されています。  
  
 詳細については、次を参照してください。[構造への追加モデル&#40;Excel 用データ マイニング アドインで&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)します。  
  
## <a name="see-also"></a>参照  
 [モデルの管理&#40;SQL Server データ マイニング アドイン&#41;](manage-models-sql-server-data-mining-add-ins.md)   
 [Excel におけるモデルの参照&#40;SQL Server データ マイニング アドイン&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
