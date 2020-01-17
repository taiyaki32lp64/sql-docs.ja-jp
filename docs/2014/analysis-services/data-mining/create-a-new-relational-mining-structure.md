---
title: 新しいリレーショナル マイニング構造の作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], relational
- mining structures [Analysis Services], creating
- relational mining models [Analysis Services]
ms.assetid: 55bac3bd-700e-4f91-bcc6-f3cd8c026da1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b4ec4bc871723b829d9ce9ec805d4b52b1c649e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085389"
---
# <a name="create-a-new-relational-mining-structure"></a>新しいリレーショナル マイニング構造の作成
  データ マイニング ウィザードを使用すると、リレーショナル データベースなどのソースのデータを使用して新しいマイニング構造を作成し、その構造とすべての関連モデルを [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースに保存できます。  
  
### <a name="to-create-a-relational-mining-structure"></a>リレーショナル マイニング構造を作成するには  
  
1.  ソリューション エクスプローラーで、 **プロジェクトの** [マイニング構造] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] フォルダーを右クリックし、 **[新しいマイニング構造]** をクリックします。  
  
     データ マイニング ウィザードが開きます。  
  
2.  **[データ マイニング ウィザードへようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **[定義方法の選択]** ページで、 **[既存のリレーショナル データベースまたはデータ ウェアハウスを使用する]** を選択して **[次へ]** をクリックします。  
  
4.  **[データ マイニング技法の選択]** ページで、使用するデータ マイニング アルゴリズムを選択して、**[次へ]** をクリックします。  
  
     データ マイニング アルゴリズムの詳細については、「[データ マイニング アルゴリズム (Analysis Services - データ マイニング)](data-mining-algorithms-analysis-services-data-mining.md)」をご覧ください。  
  
5.  **[データ ソース ビューの選択]** ページの **[使用できるデータ ソース ビュー]** で、使用するデータ ソース ビューをクリックしてから **[次へ]** をクリックします。  
  
     データ ソース ビューの作成方法の詳細については、「 [多次元モデルのデータ ソース ビュー](../multidimensional-models/data-source-views-in-multidimensional-models.md)」をご覧ください。  
  
6.  **[テーブルの種類の指定]** ページの **[入力テーブル]** で、ケース テーブルと入れ子になったテーブルを選択します。  
  
7.  **[トレーニング データの指定]** ページの **[マイニング モデル構造]** で、キー列、入力列、予測可能列を選択します。  
  
     予測可能列を選択した後、 **[候補検索]** ボタンをクリックすると **[関連列の提示]** ダイアログ ボックスが開きます。 このダイアログ ボックスで **[OK]** をクリックして、提示された列を受け入れると、選択された列をマイニング構造に含めることができます。また、 **[入力]** 列で選択内容を変更してから、 **[OK]** をクリックしてもかまいません。 提示された内容を無視するには、 **[キャンセル]** をクリックします。  
  
8.  [**次へ**] をクリックします。  
  
9. **[列のコンテンツおよびデータ型の指定]** ページの **[マイニング モデル構造]** では、各列のコンテンツの種類とデータ型を調整できます。  
  
    > [!NOTE]  
    >  **[検出]** をクリックすると、連続データまたは不連続なデータを含む列を自動的に検出できます。 このボタンをクリックすると、**[コンテンツの種類]** と **[データ型]** 列で、列の内容とデータ型が更新されます。 コンテンツの種類とデータ型の詳細については、「[コンテンツの種類 (データ マイニング)](content-types-data-mining.md)」および「[データ型 (データ マイニング)](data-types-data-mining.md)」をご覧ください。  
  
10. [**次へ**] をクリックします。  
  
11. **[ウィザードの完了]** ページで、作成するマイニング構造とそれに関連した初期マイニング モデルの名前を指定し、 **[完了]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [マイニング構造のタスクと操作方法](mining-structure-tasks-and-how-tos.md)  
  
  
