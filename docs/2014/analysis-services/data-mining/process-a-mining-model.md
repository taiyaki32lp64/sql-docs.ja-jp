---
title: マイニング モデルの処理 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], processing
ms.assetid: c2204472-c500-47a5-9afa-7ce2ca78b233
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fd2506e835f634937d5bf135ed7eec7cfa259b5f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083097"
---
# <a name="process-a-mining-model"></a>マイニング モデルの処理
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]のデータ マイニング デザイナーにある [マイニング モデル] タブを使用すると、特定のマイニング モデル構造に関連するマイニング モデルを処理したり、その構造に関連するすべてのモデルを処理したりできます。  
  
 マイニング モデルは、次のツールを使用して処理できます。  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
 XMLA 処理コマンドを使用することもできます。 詳細については、「[処理するためのツールと方法 (Analysis Services)](../multidimensional-models/tools-and-approaches-for-processing-analysis-services.md)」を参照してください。  
  
### <a name="process-a-single-mining-model-using-sql-server-data-tools"></a>SQL Server データ ツールを使用した単一のマイニング モデルの処理  
  
1.  データ マイニング デザイナーの **[マイニング モデル]** タブで、グリッドにある 1 つまたは複数のモデル列からマイニング モデルを 1 つ選択します。  
  
2.  **[マイニング モデル]** メニューの **[モデルの処理]** をクリックします。  
  
     マイニング構造に変更を加えた場合は、モデルを処理する前に構造を再配置するように求められます。 **[はい]** をクリックします。  
  
3.  **マイニング モデルの処理 -\<モデル >** ダイアログ ボックスで、をクリックして**実行**します。  
  
     **[処理の進行状況]** ダイアログ ボックスが開き、モデル処理の詳細が表示されます。  
  
4.  モデルの処理が問題なく終了したら、 **[処理の進行状況]** ダイアログ ボックスで **[閉じる]** をクリックします。  
  
5.  クリックして**閉じる**で、**マイニング モデルの処理 -\<モデル >**  ダイアログ ボックス。  
  
 そのマイニング構造と選択したマイニング モデルのみが処理されます。  
  
### <a name="process-all-mining-models-that-are-associated-with-a-mining-structure"></a>マイニング構造に関連するすべてのマイニング モデルの処理  
  
1.  データ マイニング デザイナーの **[マイニング モデル]** タブにある **[マイニング モデル]** メニューで **[マイニング構造および全モデルの処理]** をクリックします。  
  
2.  マイニング構造に変更を加えた場合は、モデルを処理する前に構造を再配置するように求められます。 **[はい]** をクリックします。  
  
3.  **マイニング構造の処理 -\<構造 >** ダイアログ ボックスで、をクリックして**実行**します。  
  
4.  **[処理の進行状況]** ダイアログ ボックスが開き、モデル処理の詳細が表示されます。  
  
5.  モデルの処理が問題なく終了したら、 **[処理の進行状況]** ダイアログ ボックスで **[閉じる]** をクリックします。  
  
6.  クリックして**閉じる**で、**処理\<モデル >**  ダイアログ ボックス。  
  
 マイニング構造および関連するすべてのマイニング モデルが処理されます。  
  
## <a name="see-also"></a>参照  
 [マイニング モデル タスクと操作方法](mining-model-tasks-and-how-tos.md)  
  
  
