---
title: セル データ (Analysis Services) へのカスタム アクセス権の付与 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.celldata.f1
helpviewer_keywords:
- user access rights [Analysis Services], cell data
- permissions [Analysis Services], cells
- read contingent permissions
- read permissions
- cells [Analysis Services]
- custom cell data access [Analysis Services]
ms.assetid: 3b13a4ae-f3df-4523-bd30-b3fdf71e95cf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5db12886384089afe87ffb5fa659c34b09a9fe23
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074977"
---
# <a name="grant-custom-access-to-cell-data-analysis-services"></a>セル データへのカスタム アクセス権の付与 (Analysis Services)
  セルのセキュリティは、キューブ内のメジャー データへのアクセスを許可または拒否するために使用します。 次の図は、ロールに特定のメジャーへのアクセスのみが許可されているユーザーとして接続されたときに、ピボットテーブルで許可されるメジャーと拒否されるメジャーの組み合わせを示しています。 この例では、このロールで利用できるメジャーは **Reseller Sales Amount** と **Reseller Total Product Cost** だけです。 他のすべてのメジャーは、暗黙的に拒否されます (この結果を取得するために使用する手順については、次のセクション「特定のメジャーへのアクセスの許可」で説明します)。  
  
 ![ピボット テーブルの表示が許可され、セルの拒否](../media/ssas-permscellsallowed.png "ピボット テーブルの表示が許可され、セルが拒否されました")  
  
 セル権限は、セル内のデータに適用され、そのメタデータには適用されません。 セルが引き続きクエリの結果に表示され、実際のセルの値ではなく `#N/A` という値が表示されている状況を確認してください。 `#N/A`クライアント アプリケーションは、値を変換または接続文字列の Secured Cell Value プロパティを設定して別の値が指定されていない限り、セルの値が表示されます。  
  
 セルを完全に非表示にするには、メンバーのディメンション、ディメンション属性、およびディメンション属性メンバーを制限する必要が、表示します。 詳細については、 [ディメンション データへのカスタム アクセス権の付与 (Analysis Services)](grant-custom-access-to-dimension-data-analysis-services.md)を参照してください。  
  
 管理者は、ロール メンバーに、キューブ内のセルに対する権限として Read、Read-Contingent、読み取り/書き込みのいずれを与えるかを指定できます。 セルに権限を設定するのは許可されるセキュリティの最小レベルであるため、このレベルで権限を適用する前に、次の事実を認識する必要があります。  
  
-   セル レベルのセキュリティでは、より上位のレベルで制限されている権限を拡張することはできません。 例: ロールによってディメンション データへのアクセスが拒否される場合、セル レベルのセキュリティでその拒否されたセットをオーバーライドすることはできません。 別の例: いるロールがある`Read`キューブに対する権限と**読み取り/書き込み**セル データ アクセスを許可することはできませんのそれぞれのアクセス許可**読み取り/書き込み**; なります`Read`。  
  
-   同じロール内のディメンション メンバーとセルとの間でカスタム権限の調整が必要になる場合がよくあります。 たとえば、再販業者のさまざまな組み合わせを対象とした複数の割引関連メジャーへのアクセスを拒否するとします。 ディメンション データとして **Resellers** があり、メジャーとして **Discount Amount** がある場合、同じロール内で (このトピックの指示を使用して) メジャーに対する権限とディメンション メンバーに対する権限の両方を組み合わせる必要があります。 ディメンション権限を設定する方法の詳細については、 [Grant custom access to dimension data &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) を参照してください。  
  
 セル レベルのセキュリティを指定するには、MDX 式を使用します。 セルは組であるため (つまり、複数のディメンションおよびメジャーの交差ポイントとなる可能性があります)、MDX を使用して特定のセルを識別する必要があります。  
  
## <a name="allow-access-to-specific-measures"></a>特定のメジャーへのアクセスの許可  
 セルのセキュリティを使用すると、使用可能なメジャーを明示的に選択できます。 許可するメンバーを明確に特定すると、他のすべてのメジャーは使用できなくなります。 これは、次の手順に示すように、MDX スクリプトで実装されるシナリオの中でも特に単純なものです。  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに接続し、データベースを選択し、 **[ロール]** フォルダーを開き、データベース ロールをクリックします (または新しいデータベース ロールを作成します)。 メンバーシップは既に指定され、ロールにはキューブへの `Read` アクセス権があるはずです。 詳細については、「 [キューブ権限またはモデル権限の付与 &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md) を参照してください。  
  
2.  **[セル データ]** で、キューブの選択を見て適切なキューブを選択していることを確認し、 **[Read 権限を有効にする]** を選択します。  
  
     このチェック ボックスをオンにしただけで MDX 式を指定しなかった場合は、キューブのすべてのセルへのアクセスを拒否するのと同じ効果が得られます。 これは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] でキューブ セルのサブセットが解決されるときに常に既定で許可されるセットが空のセットであるためです。  
  
3.  次の MDX 式を入力します。  
  
    ```  
    (Measures.CurrentMember IS [Measures].[Reseller Sales Amount]) OR (Measures.CurrentMember IS [Measures].[Reseller Total Product Cost])  
    ```  
  
     この式は、ユーザーに表示されるメジャーを明示的に特定します。 このロールで接続しているユーザーは、それ以外のメジャーを使用することはできません。 [CurrentMember (MDX)](/sql/mdx/current-mdx) でコンテキストが設定され、その後に許可されるメジャーが続くことに注意してください。 この式の効果として、現在のメンバーに **Reseller Sales Amount** と **Reseller Total Product Cost** のどちらかが含まれている場合は、値が表示されます。 それ以外の場合、アクセスが拒否されます。 式には複数の要素があり、各要素はかっこで囲まれています。 `OR` 演算子は、複数のメジャーを指定するために使用します。  
  
## <a name="deny-access-to-specific-measures"></a>特定のメジャーへのアクセスの拒否  
 次の MDX 式が **[ロールの作成]**  |  **[セル データ]**  |  **[キューブ コンテンツの読み取りを許可する]** でも指定されていると、反対の効果、つまり特定のメジャーが利用できなくなります。 この例で**Discount Amount**と**Discount Percentage**利用不可を使用して、`NOT`と`AND`演算子。 他のすべてのメジャーは、このロールで接続しているユーザーに表示されます。  
  
```  
(NOT Measures.CurrentMember IS [Measures].[Discount Amount]) AND (NOT Measures.CurrentMember IS [Measures].[Discount Percentage])  
```  
  
 Excel では、セルのセキュリティは次の図のように示されます。  
  
 ![Excel の列が使用不可としてセルを表示する](../media/ssas-permscellshidemeasure.png "Excel の列が使用不可としてセルを表示します。")  
  
## <a name="set-read-permissions-on-calculated-measures"></a>計算メジャーに対する Read 権限の設定  
 計算メジャーに対する権限は、メジャーの構成要素とは関係なく設定できます。 計算メジャーとその従属メジャーとの間で権限を調整する場合は、Read-Contingent に関する次のセクションに進んでください。  
  
 計算メジャーに対して Read 権限がどのように機能するかを理解するために、AdventureWorks での **Reseller Gross Profit** について検討します。 その派生元は、 **Reseller Sales Amount** メジャーおよび **Reseller Total Product Cost** メジャーです。 ロールに **Reseller Gross Profit** セルに対する Read 権限がある限り、他のメジャーに対して権限が明示的に拒否されている場合でも、このメジャーは表示できます。 示されているように、以下の MDX 式を **[ロールの作成]**  |  **[セル データ]**  |  **[キューブ コンテンツの読み取りを許可する]** にコピーします。  
  
```  
(NOT Measures.CurrentMember IS [Measures].[Reseller Sales Amount])  
AND (NOT Measures.CurrentMember IS [Measures].[Reseller Total Product Cost])  
```  
  
 Excel で、現在のロールを使用してキューブに接続し、3 つすべてのメジャーを選択してセルのセキュリティの効果を確認します。 拒否されたセットのメジャーは使用できませんが、計算メジャーはユーザーに表示できることに注意してください。  
  
 ![Excel の表を利用し、使用できない cellls](../media/ssas-permscalculatedcells.png "でき、使用できない cellls を Excel テーブル")  
  
## <a name="set-read-contingent-permissions-on-calculated-measures"></a>計算メジャーに対する Read-Contingent 権限の設定  
 セルのセキュリティには、計算に参加する関連セルに権限を設定するための代替手段として Read-Contingent が用意されています。 もう一度 **Reseller Gross Profit** の例を検討します。 前のセクションで示されていたのと同じ MDX 式を入力します。今回は、 **[ロールの作成]**  |  **[セル データ]** ダイアログ ボックスの 2 つ目のテキスト領域 ( **[セルのセキュリティでセル コンテンツの条件の読み取りを許可する]** の下のテキスト領域) に入力します。結果は Excel で表示したときにわかります。 **Reseller Gross Profit** は **Reseller Sales Amount** および **Reseller Total Product Cost**に基づくため、総利益の構成要素にアクセスできず、そのためこの時点では総利益にアクセスできません。  
  
> [!NOTE]  
>  同じロール内のセルに Read 権限と Read-Contingent 権限の両方を設定するとどうなりますか。 ロールによって、セルに対する Read 権限は設定されますが、Read-Contingent 権限は設定されません。  
  
 前のセクションで説明したように、 **[Read-Contingent 権限を有効にする]** チェック ボックスをオンにしても、MDX 式を指定しなければ、キューブ内のすべてのセルへのアクセスは拒否されます。 これは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] でキューブ セルのサブセットが解決されるときに常に既定で許可されるセットが空のセットであるためです。  
  
## <a name="set-readwrite-permissions-on-a-cell"></a>セルに対する読み取り/書き込み権限の設定  
 セルに対する読み取り/書き込み権限は、メンバーがキューブ自体に対する読み取り/書き込み権限を持っている場合に限り、書き戻しを有効にするために使用します。 セル レベルで付与される権限は、キューブ レベルで付与される権限以下になる必要があります。 詳細については、 [「パーティションの書き戻しの設定」](set-partition-writeback.md) を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [MDX ビルダー (Analysis Services - 多次元データ)](../mdx-builder-analysis-services-multidimensional-data.md)   
 [基本的な MDX スクリプト (MDX)](mdx/the-basic-mdx-script-mdx.md)   
 [処理権限の付与 (Analysis Services)](grant-process-permissions-analysis-services.md)   
 [ディメンションに対する権限の付与 (Analysis Services)](grant-permissions-on-a-dimension-analysis-services.md)   
 [ディメンション データへのカスタム アクセス権の付与 (Analysis Services)](grant-custom-access-to-dimension-data-analysis-services.md)   
 [キューブ権限またはモデル権限の付与 (Analysis Services)](grant-cube-or-model-permissions-analysis-services.md)  
  
  
