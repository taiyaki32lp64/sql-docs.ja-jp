---
title: DirectQuery パーティション (SSAS テーブル) の変更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f9df1e66-dd23-41b4-95eb-af110d10eda4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1eb0b6349eac28bbd2abc22b9483ef74edf1bf33
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088189"
---
# <a name="change-the-directquery-partition-ssas-tabular"></a>DirectQuery パーティションの変更 (SSAS テーブル)
  テーブル内で DirectQuery パーティションとして指定できるパーティションは 1 つだけであるため、Analysis Services ではテーブルに作成された最初のパーティションが既定で使用されます。 モデル プロジェクトの作成時に、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]の [パーティション マネージャー] ダイアログ ボックスを使用して DirectQuery パーティションを変更できます。 配置済みのモデルでは、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]を使用して DirectQuery パーティションを変更できます  
  
### <a name="change-the-directquery-partition-for-a-tabular-model-project"></a>テーブル モデル プロジェクトの DirectQuery パーティションの変更  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]のモデル デザイナーで、パーティション テーブルが含まれているテーブル (タブ) をクリックします。  
  
2.  **[テーブル]** メニューをクリックし、 **[パーティション]** をクリックします。  
  
3.  **[パーティション マネージャー]** で、現在の直接クエリ パーティションであるパーティションはパーティション名に **(DirectQuery)** というプレフィックスで示されます。  
  
     **[パーティション]** ボックスの一覧で別のパーティションを選択し、 **[DirectQuery として設定]** をクリックします。 **[DirectQuery として設定]** ボタンは、現在の DirectQuery パーティションが選択されている場合は無効になり、モデルが直接 Direct Query モードに対して有効になっていない場合は表示されません。  
  
4.  必要に応じて、処理オプションを変更し、 **[OK]** をクリックします。  
  
### <a name="change-the-directquery-partition-for-a-deployed-tabular-model"></a>配置済みテーブル モデルの DirectQuery パーティションの変更  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]で、オブジェクト エクスプローラーにモデル データベースを開きます。  
  
2.  **[テーブル]** ノードを展開し、パーティション分割されたテーブルを右クリックして **[パーティション]** を選択します。  
  
     DirectQuery モードで使用するように指定されたパーティションには、パーティション名にプレフィックス (DirectQuery) があります。  
  
3.  別のパーティションに変更するには、 **[直接クエリ]** ツール バー アイコンをクリックして **[DirectQuery パーティションの設定]** ダイアログ ボックスを開きます。 [直接クエリ] ツール バー アイコンは、直接クエリに対して有効になっていないモデルでは使用できません。  
  
4.  **[パーティション名]** ボックスの一覧から別のパーティションを選択し、必要に応じてパーティションの処理オプションを変更します。  
  
## <a name="see-also"></a>関連項目  
 [パーティション (SSAS テーブル)](tabular-models/partitions-ssas-tabular.md)  
  
  
