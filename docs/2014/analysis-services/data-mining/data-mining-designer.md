---
title: データ マイニング デザイナー |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], structure
- mining structures [Analysis Services], modifying
- data mining editor [Analysis Services]
- Data Mining Designer
- data mining [Analysis Services], modifying
ms.assetid: 2540db5b-2bf3-4b6c-87c8-79c48d71acce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b0a54a0ae2bab2c8019b706a51b94f0338dcb3cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085110"
---
# <a name="data-mining-designer"></a>Data Mining Designer
  データ マイニング デザイナーは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のマイニング モデルを操作するための主要な環境です。 データ マイニング デザイナーにアクセスするには、既存のマイニング構造を選択するか、またはデータ マイニング ウィザードを使用して新しいマイニング構造とマイニング モデルを作成します。 データ マイニング デザイナーを使用すると、次の作業を実行できます。  
  
-   最初にデータ マイニング ウィザードで作成したマイニング構造とマイニング モデルを変更する。  
  
-   既存のマイニング構造に基づいて新しいモデルを作成する。  
  
-   マイニング モデルをトレーニングして参照する。  
  
-   精度チャートを使用してモデルを比較する。  
  
-   マイニング モデルに基づいて予測クエリを作成する。  
  
## <a name="mining-structure-tab"></a>[マイニング構造] タブ  
 **[マイニング構造]** タブを使用すると、列を追加したり、既存のマイニング構造のプロパティを変更したりできます。 次のタスクおよびトピックでは、マイニング構造の操作の詳細について説明します。  
  
 [マイニング構造 (Analysis Services - データ マイニング)](mining-structures-analysis-services-data-mining.md)  
  
 [マイニング構造のタスクと操作方法](mining-structure-tasks-and-how-tos.md)  
  
## <a name="mining-models-tab"></a>[マイニング モデル] タブ  
 **[マイニング モデル]** タブを使用すると、既存のマイニング モデルを管理したり、新しいモデルを作成したりできます。 マイニング モデルは、常に既存のマイニング構造に基づきます。  
  
 **[マイニング モデル]** タブでは、アルゴリズムの種類の変更、モデル構造に関連付けられている列の追加または削除、アルゴリズム固有の列プロパティの調整、マイニング モデル列の使用法の指定、およびマイニング モデルに関連付けられているアルゴリズム パラメーターの調整を行うことができます。 また、マイニング構造は、選択したモデルまたは関連付けられているすべてのモデルと共に処理することもできます。  
  
 マイニング モデルの操作の詳細については、次のトピックを参照してください。  
  
 [マイニング モデル (Analysis Services - データ マイニング)](mining-models-analysis-services-data-mining.md)  
  
 [マイニング モデル タスクと操作方法](mining-model-tasks-and-how-tos.md)  
  
## <a name="mining-model-viewer-tab"></a>[マイニング モデル ビューアー] タブ  
 **[マイニング モデル ビューアー]** タブは、マイニング モデルを視覚的に調べるときに使用します。 各マイニング モデルは、そのモデルに固有のコンテンツを表示するカスタム ビューアーに関連付けられています。 また、コンテンツ ビューアーを使用して、マイニング モデル コンテンツを表示することもできます。  
  
 データ マイニング ビューアーを使用したマイニング モデルの調査の詳細については、次のトピックを参照してください。  
  
 [データ マイニング モデル ビューアー](data-mining-model-viewers.md)  
  
 [マイニング モデル ビューアーのタスクと操作方法](mining-model-viewer-tasks-and-how-tos.md)  
  
## <a name="mining-accuracy-chart-tab"></a>[マイニング精度チャート] タブ  
 **[マイニング精度チャート]** タブは、1 つのマイニング モデルの予測精度をテストしたり、マイニング構造内に含まれている複数のマイニング モデルの効果を比較したりするときに使用します。 このタブには、データのフィルター選択、マイニング モデルの選択、およびリフト チャート、利益チャート、または分類マトリックスへの結果の表示を行うためのツールがあります。  
  
 マイニング モデルのテストおよび検証の詳細については、次のトピックを参照してください。  
  
 [テストおよび検証 (データ マイニング)](testing-and-validation-data-mining.md)  
  
 [テストおよび検証タスク、および操作方法 (データ マイニング)](testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
## <a name="mining-model-prediction-tab"></a>[マイニング モデル予測] タブ  
 **[マイニング モデル予測]** タブには予測クエリ ビルダーがあり、これを使用してデータ マイニング拡張機能 (DMX) の予測クエリを作成できます。 このタブには、マイニング モデルと入力テーブルの指定、入力テーブル内の列へのマイニング モデル内の列のマッピング、クエリへの機能の追加、および各列の条件の指定を行うためのツールがあります。  
  
 クエリをデザインした後、タブのさまざまなビューを使用して、クエリの結果を表示したり、クエリを手動で変更したりできます。 また、クエリの結果をデータベースのテーブルに保存することもできます。  
  
 データ マイニング クエリの作成の詳細については、次のトピックを参照してください。  
  
 [データ マイニング クエリ](data-mining-queries.md)  
  
 [データ マイニングのクエリ タスクと操作方法](data-mining-query-tasks-and-how-tos.md)  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング ソリューション](data-mining-solutions.md)  
  
  
