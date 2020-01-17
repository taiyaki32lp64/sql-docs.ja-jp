---
title: ドリルスルー アクション フォーム エディター ([アクション] タブ、キューブ デザイナー) (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.drillthroughaction.f1
ms.assetid: 225fd818-b5ea-494f-b67b-66e09798274a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 33d20da736308b4436c40a50b8b01da7445663c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081454"
---
# <a name="drillthrough-action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>ドリルスルー アクション フォーム エディター (キューブ デザイナーの [アクション] タブ) (Analysis Services - 多次元データ)
  キューブ デザイナーの **[アクション]** タブの **[ドリルスルー アクション フォーム エディター]** ペインを使用すると、 **[アクション オーガナイザー]** ペインで選択したドリルスルー アクションを変更できます。 アクションの種類の詳細については、「[アクション (Analysis Services - 多次元データ)](multidimensional-models/actions-analysis-services-multidimensional-data.md)」を参照してください。  
  
> [!NOTE]  
>  ドリルスルー アクションでは、基になるデータ ストアへのドリル ダウンは行われなくなりました。 ドリルスルー アクションでアクセスする情報は、ディメンションまたは階層メンバーを使用してキューブ内でモデル化する必要があります。  
  
## <a name="options"></a>および  
 **name**  
 アクションの名前を入力します。  
  
 **[アクションの対象]**  
 展開すると、 **[メジャー グループのメンバー]** オプションが表示されます。  
  
 **メジャー グループのメンバー**  
 ドリルスルー アクションを関連付けるメジャー グループを選択します。  
  
 **[条件 (省略可能)]**  
 オプションの条件を記述する多次元式 (MDX) を入力します。この式は、アクションが使用可能な場合にさらに制限を設定する **[メジャー グループのメンバー]** のメンバーと一緒に使用されます。 この式は、ブール値を返す必要があります (true は、アクションが使用可能なことを示します)。  
  
 選択した要素を **[計算ツール]** ペインからこのオプションへドラッグして、選択した要素に対して MDX 構文を含めます。  
  
 **[ドリルスルー列]**  
 展開すると、ユーザーがこのアクションを実行したときに返される属性を示すグリッドが表示されます。  
  
> [!NOTE]  
>  複数のディメンションを選択できますが、1 回のドリルスルー アクションで複数回使用できるディメンションはありません。  
  
 このグリッドには次の列が含まれています。  
  
|[列]|説明|  
|------------|-----------------|  
|**Dimensions**|返される属性の派生元のディメンションを選択します。 メジャーをドリルスルーするには、[メジャー] を選択します。|  
|**列を返す**|アクションが実行されたときに、選択されたディメンションから返される属性またはメジャーを選択します。|  
  
 **[追加のプロパティ]**  
 展開すると、 **[既定]** 、 **[最大行数]** 、 **[呼び出し]** 、 **[アプリケーション]** 、 **[説明]** 、 **[キャプション]** 、および **[キャプションに MDX を使用]** の各オプションが表示されます。  
  
 **[Default]**  
 このドリルスルー アクションを既定のドリルスルー アクションとして含める場合は **[True]** を選択します。それ以外の場合は、 **[False]** を選択します。  
  
 場合、 `RETURN` MDX 句が省略されて`DRILLTHROUGH`、クライアント アプリケーションによって実行されたステートメント、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]インスタンスは、すべての既定のドリルスルー アクションを評価し、最初の既定のドリルスルーの実行空セットを返すアクションです。 MDX の詳細については`DRILLTHROUGH`ステートメントを参照してください[DRILLTHROUGH ステートメント&#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-drillthrough)します。  
  
> [!NOTE]  
>  このオプションは、下位互換性を保つために使用します。  
  
 **行の最大数**  
 ドリルスルー アクションによって返される最大行数を入力します。 このオプションを 0 または空の値に設定すると、ドリルスルー アクションによって取得されたすべての行がクライアント アプリケーションに返されます。  
  
 **[呼び出し]**  
 いつアクションを実行する必要があるかを設定します。  
  
> [!NOTE]  
>  このオプションは、クライアント アプリケーションがアクションをいつ実行するかについて推奨するだけで、アクションの呼び出しを直接制御することはありません。  
  
 次の表では、使用可能な設定について説明しています。  
  
|値|説明|  
|-----------|-----------------|  
|Batch|アクションは、バッチ操作または [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] タスクの一部として実行されます。|  
|Interactive|アクションは、ユーザーがアクションを呼び出したときに実行されます。|  
|[オープン時]|アクションは、キューブが最初に開いたときに実行されます。|  
  
 **アプリケーション**  
 ドリルスルー アクションを実行できるアプリケーションの名前を入力します。  
  
 このオプションを使用して、どのクライアント アプリケーションが最もよくこのアクションを使用するか識別したり、ポップアップ メニューのアクションの横に適切なアイコンを表示したりできます。  
  
> [!NOTE]  
>  このオプションは、どのクライアント アプリケーションがアクションを実行するかについて推奨するだけで、アクションへのアクセスを直接制御することはありません。 クライアント アプリケーションでは、他のクライアント アプリケーションに関連付けられているすべてのアクションを非表示にする必要があります。  
  
 **[説明]**  
 アクションの説明をオプションで入力します。  
  
 **Caption**  
 **[キャプションに MDX を使用]** を **[False]** に設定する場合は、クライアント アプリケーションでアクションに対して表示されるキャプションを入力します。  
  
 **[キャプションに MDX を使用]** を **[True]** に設定する場合は、キャプションの文字列を返す多次元式 (MDX) を入力します。  
  
 **キャプションに MDX**  
 クライアント アプリケーションのアクションに表示されるキャプションを表すリテラル文字列が **[キャプション]** に入力されている場合は、 **[False]** を選択します。  
  
 クライアント アプリケーションのアクションに表示されるキャプションを表す文字列を返す MDX 式が **[キャプション]** に入力されている場合は、 **[True]** を選択します。 MDX 式は、アクションがクライアント アプリケーションに返される前に解析される必要があります。  
  
## <a name="see-also"></a>参照  
 [多次元式 (MDX) リファレンス](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [アクション&#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [ツールバー&#40;アクションタブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [アクション オーガナイザー&#40;アクション タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [計算ツール&#40;アクション タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [アクション フォーム エディター&#40;アクション タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [レポート アクション フォーム エディター&#40;アクション タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
