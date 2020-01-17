---
title: 実行プランの比較 | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- comparing execution plans
- compare execution plans
- plan comparison
- execution plans [SQL Server], comparing
- Query Store, comparing plans
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: b0590a46fe9e5037f5bec1895aa6602bcd8c568a
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907664"
---
# <a name="compare-execution-plans"></a>実行プランの比較
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
このトピックでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のプラン比較機能を利用し、グラフィックによる実際の実行プラン間の類似性や相違点を比較する方法について説明します。 この機能は [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v16 以降で使用できます。
  
> [!NOTE]
> 実際の実行プランは、[!INCLUDE[tsql](../../includes/tsql-md.md)] のクエリまたはバッチが実行された後に生成されます。 そのため、実際の実行プランには、実際の行数、リソース使用状況のメトリック、ランタイムの警告 (ある場合) などのランタイム情報が含まれます。 詳細については、「[実際の実行プランの表示](../../relational-databases/performance/display-an-actual-execution-plan.md)」を参照してください。
  
プランを比較する機能は、次のようなトラブルシューティング目的でデータベースの専門家に使用されることがあります。
-   クエリまたはバッチが突然遅くなった。
-   クエリ書き直しの影響を理解する。
-   スキーマ設計に導入した特定のパフォーマンス強化が実行プランに効果を与えているかを観察する。  
 
**[プランの比較]** メニュー オプションでは、2 つの異なる実行プランを横に並べて比較できます。上述のすべての理由に対してさまざまな動作を明らかにする類似性や変化を簡単に特定できます。 このオプションでは次を比較できます。
- 以前に保存した 2 つの実行プラン ファイル ( *.sqlplan* 拡張子)。
- アクティブな実行プラン 1 つと前に保存したクエリ実行プラン 1 つ。
- [クエリ ストア](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)で選択した 2 つのクエリ プラン。

> [!TIP]
> *.sqlplan* ファイルを含むプランの比較作業。旧バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からの作業も対象。 また、このオプションではオフライン比較が可能です。そのため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続する必要がありません。 

2 つの実行プランが比較されているとき、**基本的に同じことを行う**プランのリージョンは同じ色とパターンでハイライトされます。 1 つのプランで色付きのリージョンをクリックすると、そのプランで、一致するノードの中央にもう 1 つのプランが配置されます。 引き続き実行プランの一致しない演算子やノードを比較できますが、その場合、比較する演算子を手動で選択する必要があります。

> [!IMPORTANT]
> プランの形状を変えると見なされるノードのみが類似性の確認に使用されます。 そのため、2 つのノードの真ん中で色が付いていないノードがプランの同じ下位セクションに入るということがありえます。 その場合、色が付いていないということは、セクションが等しいか確認されたとき、それらのノードが考慮されなかったことを意味します。
  
## <a name="to-compare-execution-plans"></a>実行プランを比較するには
  
1.  **[ファイル]** メニューを使用し、 **[ファイルを開く]** をクリックするか、プラン ファイルを [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] ウィンドウにドラッグすることで、前に保存したクエリ実行プラン ファイル (.sqlplan) を開きます。 あるいは、クエリを実行し、その実行プランの表示を選択したところであれば、結果ウィンドウの **[実行プラン]** タブに移動します。 

2.  実行プランの何もない領域を右クリックし、 **[プラン表示の比較]** をクリックします。 

    ![右クリックの [プラン表示の比較]](../../relational-databases/performance/media/plancomparisonmenuoption.png "右クリックの [プラン表示の比較]")   

3.  比較対象にする 2 つ目のクエリ プラン ファイルを選択します。 2 つ目のファイルが開いたら、プランを比較できます。

4.  プランが比較されると、新しいウィンドウが開きます。既定では、プランが上下に分かれて表示されます。 比較されるプランで一般的な演算子またはノードで最初に現れるものが既定で選択され、プラン間の違いが表示されます。 ハイライトされた演算子とノードはすべて両方の比較対象プランに存在します。 上または左のプランでハイライトされた演算子を選択すると、下または右のプランで該当する演算子が自動的に選択されます。 一方の比較対象プランでルート ノード演算子を選択すると (下の画像では SELECT ノード)、もう一方の比較対象プランでもルート ノード演算子が各自選択されます。

    ![保存された 2 つのプラン ファイルのプランを比較する](../../relational-databases/performance/media/plancomparison-plans.png "保存された 2 つのプラン ファイルのプランを比較する")  

     > [!TIP]
     > 実行プラン比較の表示を横並びに切り替えることができます。その場合、実行プランの何もない領域を右クリックし、 **[分割の方向の切り替え]** を選択します。

     > [!TIP]
     > 実行プランで利用できるズーム オプションとナビゲーション オプションはすべて、プラン比較モードで動作します。 詳細については、「[実際の実行プランの表示](../../relational-databases/performance/display-an-actual-execution-plan.md)」を参照してください。

5.  また、既定の選択では、右側にプロパティ ウィンドウが 2 つ開きます。 両方の比較対象演算子に存在するが違いがあるプロパティには、見分けやすいように先頭に "*不等号*" (&ne;) が付けられます。

    ![デュアル プロパティ ウィンドウ](../../relational-databases/performance/media/plancomparison-properties.png "デュアル プロパティ ウィンドウ")  

6.  下では、 **[プラン表示の分析]** 比較ナビゲーション ウィンドウも開きます。 3 つのタブを使用できます。

    1.  **[ステートメント オプション]** タブでは、既定で *[類似演算子の強調表示]* が選択されます。比較対象プランでハイライトされている同じ演算子またはノードで同じ色と線パターンが使用されます。 線パターンをクリックし、比較対象プランの類似領域間を移動します。 *[類似セグメントに一致しない演算子の強調表示]* を選択することで、類似性ではなく、プランの相違点をハイライトすることもできます。 
    
       > [!NOTE]
       > 既定では、プランを比較するとき、データベース名が無視されるため、名前が異なるがスキーマが同じデータベースに対して保存されたプランを比較できます。 たとえば、*ProdDB* データベースと *TestDB* データベースのプランを比較できます。 この動作は *[演算子を比較するときにデータベース名を無視する]* で変更できます。

       ![[プラン表示の分析] ウィンドウ](../../relational-databases/performance/media/plancomparison-analysis.png "[プラン表示の分析] ウィンドウ") 

    2.  **[複数ステートメント]** タブは、ステートメントが複数含まれるプランを比較するときに便利です。適切なステートメント ペアを比較できます。

        ![比較されるプラン内の複数のステートメント](../../relational-databases/performance/media/plancomparison-multiple.png "比較されるプラン内の複数のステートメント")  

    3.  **[シナリオ]** タブでは、比較対象プランの [[カーディナリティ推定]](../../relational-databases/performance/cardinality-estimation-sql-server.md) の相違点に関連することで最も関連性の高い側面がいくつか自動分析されています。 左側ウィンドウの一覧にある各演算子に対して、右側ウィンドウに *[このシナリオの詳細については、ここをクリックしてください]* リンクのシナリオに関する詳細と、そのシナリオが一覧に含まれる理由として考えられることが表示されます。 

        ![さまざまな推定行](../../relational-databases/performance/media/plancomparison-scenarios.png "さまざまな推定行")  

    このウィンドウが閉じられている場合、比較対象プランの何もない領域を右クリックし、 **[プラン表示の比較オプション]** を選択して再び開きます。

    ![プランの比較オプション](../../relational-databases/performance/media/plancomparison-options.png "プランの比較オプション")  

## <a name="to-compare-execution-plans-in-query-store"></a>クエリ ストアで実行プランを比較するには

1.  クエリ ストアで、実行プランが複数含まれるクエリを見つけます。 クエリ ストア シナリオの詳細については、「[クエリ ストアの使用シナリオ](../../relational-databases/performance/query-store-usage-scenarios.md#identify-and-tune-top-resource-consuming-queries)」を参照してください。

2.  SHIFT キーとマウスを組み合わせると、同じクエリに対して 2 つのプランを選択できます。 

    ![クエリ ストアでプランを 2 つ選択する](../../relational-databases/performance/media/plancomparison-querystore.png "クエリ ストアでプランを 2 つ選択する")   

3.  **[Compare the plans for the selected query in a seperate window]\(選択したクエリのプランを別のウィンドウで比較する\)** ボタンを使用し、プラン比較を開始します。 「*実行プランを比較するには*」の手順 4 から 6 が該当します。 

    ![クエリ ストアでプラン表示を比較する](../../relational-databases/performance/media/plancomparison-querystoreoption.png "クエリ ストアでプラン表示を比較する") 
