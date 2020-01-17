---
title: 推定実行プランの表示 | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4d0d5930734bb48c0914300a735f81e3ca2ced38
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946868"
---
# <a name="display-the-estimated-execution-plan"></a>推定実行プランの表示
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して、グラフィカルな推定実行プランを生成する方法について説明します。 推定実行プランを生成するときには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] のクエリやバッチは実行されません。 そのため、推定実行プランには、実際のリソース使用状況のメトリックやランタイムの警告などのランタイム情報が含まれていません。 代わりに、クエリが実際に実行された場合に [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] によって使用される可能性が最も高いクエリ実行プランが、生成された実行プランに表示されます。また、プラン内の複数の操作で使用される推定行数も表示されます。  
  
 この機能を使用するには、グラフィカルな実行プランの生成に使用する [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリを実行できる適切な権限を持ち、このクエリが参照するすべてのデータベースに SHOWPLAN 権限が与えられている必要があります。  
  
## <a name="to-display-the-estimated-execution-plan-for-a-query"></a>クエリの推定実行プランを表示するには  
  
1.  ツール バーの **[データベース エンジン クエリ]** をクリックします。 また、ツール バーの **[ファイルを開く]** をクリックして既存のクエリを参照することにより、既存のクエリを開き、推定実行プランを表示することもできます。  
  
2.  表示する推定実行プランに対するクエリを入力します。  
  
3.  **[クエリ]** メニューの **[推定実行プランの表示]** をクリックするか、ツール バーの **[推定実行プランの表示]** をクリックします。 推定実行プランが、結果ペインの **[実行プラン]** タブに表示されます。 

    ![ツール バーの推定実行プラン ボタン](../../relational-databases/performance/media/estimatedexecplantoolbar.png "ツール バーの推定実行プラン ボタン")    

    追加情報を表示するには、マウス ポインターを論理操作や物理操作のアイコン上にしばらく置き、各操作について、表示されるツールヒント内の説明とプロパティを参照します。 また、プロパティ ウィンドウでも操作のプロパティを参照できます。 プロパティが表示されていない場合は、任意の操作を右クリックし、 **[プロパティ]** をクリックします。 特定の操作のプロパティを表示するには、その操作をクリックします。  

    ![プラン オペレーターの [プロパティ] を右クリック](../../relational-databases/performance/media/planproperties.png "プラン オペレーターの [プロパティ] を右クリック")    
  
4.  実行プランの表示を変更するには、実行プランを右クリックし、 **[拡大]** 、 **[縮小]** 、 **[ズームの指定]** 、 **[ウィンドウのサイズに合わせて大きさを変更]** のいずれかをクリックします。 **[拡大]** と **[縮小]** では、実行プランを固定比率ずつ拡大または縮小できます。 **[ズームの指定]** を使用すると、表示倍率 (80% など) を定義できます。 **[ウィンドウのサイズに合わせて大きさを変更]** では、結果ペインの大きさに合わせて実行プランを拡大できます。 または、Ctrl キーとマウス ホイールを組み合わせて、**動的ズーム**を有効にすることもできます。  

5.  実行プランの表示画面を移動するには、垂直または水平のスクロール バーを使用するか、実行プランの **何もない領域をクリックしたまま** **マウス カーソルをドラッグします** 。 あるいは、実行プラン ウィンドウの右下隅にあるプラス (+) 記号をクリック アンド ホールドすると、実行プラン全体の縮小マップが表示されます。
 
> [!NOTE] 
> または、[SET SHOWPLAN_XML](../../t-sql/statements/set-showplan-xml-transact-sql.md) を使用して、実行せずに各ステートメントの実行プラン情報を返します。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で使用すると、 *[結果]* タブにはリンクが表示され、リンクをクリックするとグラフィック形式で実行プランが表示されます。   
