---
title: 実際の実行プランの分析 | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- analyzing execution plans
- analyzing actual execution plans
- execution plans [SQL Server], analyzing
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 5c94d2d60bf851742aca68d5b7bc25ea4d8afd9c
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72289322"
---
# <a name="analyze-an-actual-execution-plan"></a>実際の実行プランの分析

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このトピックでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のプラン分析機能を使用して実際のグラフィカルな実行プランを分析する方法について説明します。 この機能は [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v17.4 以降で使用できます。 一般に、[SSMS の最新バージョンをインストールする](../../ssms/download-sql-server-management-studio-ssms.md)ことをお勧めします。

> [!NOTE]
> 実際の実行プランは、[!INCLUDE[tsql](../../includes/tsql-md.md)] のクエリまたはバッチが実行された後に生成されます。 そのため、実際の実行プランには、実際の行数、リソース使用状況のメトリック、ランタイムの警告 (ある場合) などのランタイム情報が含まれます。 詳細については、「[実際の実行プランの表示](../../relational-databases/performance/display-an-actual-execution-plan.md)」を参照してください。
  
クエリ パフォーマンスのトラブルシューティングには、根本原因を実際に見つけて修正するために、クエリ処理と実行プランを理解する上で重要な専門知識が必要です。

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] には、特に大規模で複雑なプラン向けに、実際の実行プラン分析のタスクにある程度の自動化を実装する機能が含まれています。 目標は、簡単に不正確な[基数推定](../../relational-databases/performance/cardinality-estimation-sql-server.md)のシナリオを見つけ、利用できる可能性がある緩和策に関する推奨事項を得ることです。

> [!IMPORTANT]
> 提案された緩和策は、運用環境に適用する前に必ず適切にテストしてください。
  
## <a name="to-analyze-an-execution-plan-for-a-query"></a>クエリの実行プランを分析するには  
  
1.  **[ファイル]** メニューを使用し、 **[ファイルを開く]** をクリックするか、プラン ファイルを [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] ウィンドウにドラッグすることで、前に保存したクエリ実行プラン ファイル (.sqlplan) を開きます。 あるいは、クエリを実行し、その実行プランの表示を選択したところであれば、結果ウィンドウの **[実行プラン]** タブに移動します。 

2.  実行プランの何もない領域を右クリックし、 **[実際の実行プランの分析]** をクリックします。 

    ![[実際の実行プランの分析] の右クリック](../../relational-databases/performance/media/plananalysismenuoption.png "[実際の実行プランの分析] の右クリック")   

3.  下部に **[プラン表示の分析]** が表示されます。 **[複数ステートメント]** タブは、ステートメントが複数含まれるプランを分析するときに便利です。適切なステートメントを分析できます。

4.  [シナリオ] タブを選択すると、実際の実行プランで見つかった問題の詳細が表示されます。 左側ウィンドウの一覧にある各演算子に対して、右側ウィンドウに *[このシナリオの詳細については、ここをクリックしてください]* リンクのシナリオに関する詳細と、そのシナリオが一覧に含まれる理由として考えられることが表示されます。

    ![実行プランの分析結果](../../relational-databases/performance/media/plananalysis-scenarios.png "実行プランの分析結果") 
