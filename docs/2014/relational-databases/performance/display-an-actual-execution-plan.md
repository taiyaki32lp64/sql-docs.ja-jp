---
title: 実際の実行プランの表示 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- displaying execution plans
- actual execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9403e6e2cf1c341780a06bbdff1c5f38685dd34a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150967"
---
# <a name="display-an-actual-execution-plan"></a>実際の実行プランの表示
  このトピックでは、実際のグラフィカルな実行プランを [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して生成する方法について説明します。 実際の実行プランの生成時には、 [!INCLUDE[tsql](../../includes/tsql-md.md)] のクエリまたはバッチが実行されます。 生成される実行プランには、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] によりクエリの実行に使用される実際のクエリ実行プランが表示されます。  
  
 この機能を使用するユーザーには、グラフィカルな実行プランの生成に対応した [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリの実行に必要な権限があり、このクエリが参照するすべてのデータベースに対する SHOWPLAN 権限が付与されている必要があります。  
  
### <a name="to-include-an-execution-plan-for-a-query-during-execution"></a>クエリの実行に実行プランを含めるには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のツール バーの **[データベース エンジン クエリ]** をクリックします。 また、ツール バーの **[ファイルを開く]** をクリックして既存のクエリを参照することにより、既存のクエリを開き、推定実行プランを表示することもできます。  
  
2.  表示する実際の実行プランに対するクエリを入力します。  
  
3.  **[クエリ]** メニューの **[実際の実行プランを含める]** をクリックするか、ツール バーの **[実際の実行プランを含める]** をクリックします。  
  
4.  ツール バーの **[実行]** をクリックしてクエリを実行します。 クエリ オプティマイザーで使用されるプランが、結果ペインの **[実行プラン]** タブに表示されます。 マウス ポインターを論理操作や物理操作の上に置くと、各操作について、表示されるツールヒント内の説明とプロパティを確認できます。  
  
     また、プロパティ ウィンドウでも操作のプロパティを参照できます。 プロパティが表示されていない場合は、任意の操作を右クリックし、 **[プロパティ]** をクリックします。 特定の操作のプロパティを表示するには、その操作をクリックします。  
  
5.  実行プランを右クリックし、 **[拡大]** 、 **[縮小]** 、 **[ズームの指定]** 、 **[ウィンドウのサイズに合わせて大きさを変更]** のいずれかをクリックして、実行プランの表示を変更できます。 **[拡大]** と **[縮小]** では、実行プランを拡大したり縮小したりできます。 **[ズームの指定]** では、80% で表示するなど、独自の縮尺を指定できます。 **[ウィンドウのサイズに合わせて大きさを変更]** では、結果ペインの大きさに合わせて実行プランを拡大できます。  
  
  
