---
title: 推定実行プランの表示 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- zoom [SQL Server]
- estimated execution plan [SQL Server]
- displaying execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
- customizing execution plan display [SQL Server]
- modifying execution plan display
- custom zoom [SQL Server]
ms.assetid: e94aa576-4c0c-4c54-ad05-6c3432cc615b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 555ded0e34c0dc13ce794cc6f3119af7b2688910
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150881"
---
# <a name="display-the-estimated-execution-plan"></a>推定実行プランの表示
  このトピックでは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して、グラフィカルな推定実行プランを生成する方法について説明します。 推定実行プランを生成するときには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] のクエリやバッチは実行されません。 代わりに、クエリが実際に実行された場合に [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] によって使用される可能性が最も高いクエリ実行プランが、生成された実行プランに表示されます。  
  
 この機能を使用するには、グラフィカルな実行プランの生成に使用する [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリを実行できる適切な権限を持ち、このクエリが参照するすべてのデータベースに SHOWPLAN 権限が与えられている必要があります。  
  
### <a name="to-display-the-estimated-execution-plan-for-a-query"></a>クエリの推定実行プランを表示するには  
  
1.  ツール バーの **[データベース エンジン クエリ]** をクリックします。 また、ツール バーの **[ファイルを開く]** をクリックして既存のクエリを参照することにより、既存のクエリを開き、推定実行プランを表示することもできます。  
  
2.  表示する推定実行プランに対するクエリを入力します。  
  
3.  **[クエリ]** メニューの **[推定実行プランの表示]** をクリックするか、ツール バーの **[推定実行プランの表示]** をクリックします。 推定実行プランが、結果ペインの **[実行プラン]** タブに表示されます。 追加情報を表示するには、マウス ポインターを論理操作や物理操作のアイコン上にしばらく置き、各操作について、表示されるツールヒント内の説明とプロパティを参照します。 また、プロパティ ウィンドウでも操作のプロパティを参照できます。 プロパティが表示されていない場合は、任意の操作を右クリックし、 **[プロパティ]** をクリックします。 特定の操作のプロパティを表示するには、その操作をクリックします。  
  
4.  実行プランの表示を変更するには、実行プランを右クリックし、 **[拡大]** 、 **[縮小]** 、 **[ズームの指定]** 、 **[ウィンドウのサイズに合わせて大きさを変更]** のいずれかをクリックします。 **[拡大]** と **[縮小]** では、実行プランを固定比率ずつ拡大または縮小できます。 **[ズームの指定]** を使用すると、表示倍率 (80% など) を定義できます。 **[ウィンドウのサイズに合わせて大きさを変更]** では、結果ペインの大きさに合わせて実行プランを拡大できます。  
  
  
