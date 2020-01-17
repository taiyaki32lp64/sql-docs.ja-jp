---
title: ビジネス インテリジェンス ウィザードを使用してタイム インテリジェンス計算の定義 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- period over period growth [Analysis Services]
- parallel period comparisons [Analysis Services]
- Business Intelligence enhancements [Analysis Services], time intelligence
- time views [Analysis Services]
- hierarchies [Analysis Services], time
- time periods [Analysis Services]
- moving averages
- time [Analysis Services]
- period to date [Analysis Services]
- calculations [Analysis Services], time
- time hierarchies [Analysis Services]
- time intelligence [Analysis Services]
ms.assetid: be36e8fc-f46e-4553-8623-b27d695c330b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c665c894a4e0bb3691c483a8d8bab084ac2fa276
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075430"
---
# <a name="define-time-intelligence-calculations-using-the-business-intelligence-wizard"></a>ビジネス インテリジェンス ウィザードを使用したタイム インテリジェンス計算の定義
  タイム インテリジェンス拡張機能は、選択した階層に時間計算 (または時間ビュー) を追加するキューブ拡張機能です。 この拡張機能では、次の計算のカテゴリがサポートされています。  
  
-   期間累計  
  
-   前期比成長率  
  
-   移動平均  
  
-   並列期間比較  
  
 時間ディメンションを持つキューブにタイム インテリジェンスを適用します (時間ディメンションは、`Type` プロパティが `Time` に設定されているディメンションです)。 また、そのディメンションの時間属性には、`Type` プロパティの適切な設定 (Years や Months など) も指定する必要があります。 ディメンション ウィザードを使用して時間ディメンションを作成すると、ディメンションとその属性の両方の `Type` プロパティが正しく設定されます。  
  
 タイム インテリジェンスをキューブに追加するには、ビジネス インテリジェンス ウィザードを使用して、 **[拡張機能の選択]** ページの **[タイム インテリジェンスの定義]** オプションを選択します。 このウィザードでは、タイム インテリジェンスの追加先となる階層を選択し、その階層内でタイム インテリジェンスを適用するメンバーを指定する手順が示されます。 ウィザードの最後のページでは、選択したタイム インテリジェンスを追加するために [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースに対して行われる変更内容を表示できます。  
  
## <a name="selecting-a-time-hierarchy"></a>時間階層の選択  
 **[対象となる階層と計算の選択]** ページで、タイム インテリジェンス拡張機能の適用先となる時間階層を選択します。 タイム インテリジェンス拡張機能は、ビジネス インテリジェンス ウィザードを実行するたびに 1 つの時間階層にのみ適用できます。 複数の時間階層に拡張機能を適用する場合は、ウィザードをもう一度実行します。  
  
 時間階層を選択したら、 **[使用できる時間の計算]** の一覧で、階層に適用する計算を選択します。 一覧表示される計算は、階層内のレベルと、各レベルの属性の `Type` プロパティ設定によって異なります。 たとえば、Years 階層では年度累計と前年比成長率がサポートされますが、Quarters 階層ではサポートされません。  
  
> [!NOTE]  
>  Timeintelligence.xml テンプレート ファイルでは、 **[使用できる時間の計算]** に一覧表示される時間計算を定義します。 一覧表示された計算がニーズに合わない場合は、既存の計算を変更するか、Timeintelligence.xml ファイルに新しい計算を追加できます。  
  
> [!TIP]  
>  計算の説明を表示するには、上矢印と下矢印を使用して、その計算を強調表示します。  
  
## <a name="apply-time-views-to-members"></a>メンバーへの時間ビューの適用  
 **[計算範囲の定義]** ページで、新しい時間ビューを適用するメンバーを指定します。 新しい時間ビューは、次のいずれかのオブジェクトに適用できます。  
  
-   **勘定科目ディメンションのメンバー** 。 **[計算範囲の定義]** ページの **[使用できるメジャー]** 一覧には、勘定科目ディメンションが含まれます。 勘定科目ディメンションの `Type` プロパティは `Accounts` に設定されています。 勘定科目ディメンションがあるのに、そのディメンションが **[使用できるメジャー]** 一覧に表示されない場合は、ビジネス インテリジェンス ウィザードを使用して、そのディメンションに勘定科目インテリジェンスを適用できます。 詳細については、「 [ディメンションへの勘定科目インテリジェンスの追加](bi-wizard-add-account-intelligence-to-a-dimension.md)」を参照してください。  
  
-   **メジャー** 。勘定科目ディメンションを指定する代わりに、時間ビューの適用先となるメジャーを指定できます。 この場合、選択した時間計算の適用先となるビューを選択します。 たとえば、資産および負債は年度累計のデータであるため、年度累計の計算は資産または負債のメジャーに適用しません。  
  
## <a name="viewing-the-time-intelligence-enhancement"></a>タイム インテリジェンス拡張機能の表示  
 ビジネス インテリジェンス ウィザードの最後のページで、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースに対して行われる変更内容を表示できます。 タイム インテリジェンス拡張機能では、次の表で説明されているように、選択した時間ディメンション、関連付けられているデータ ソース ビュー、および関連付けられているキューブがウィザードによって変更されます。  
  
|オブジェクト|[変更]|  
|------------|------------|  
|時間ディメンション|計算 (またはビュー) ごとに属性を追加します。|  
|データ ソース ビュー|時間ディメンションの新しい属性ごとに、計算される列を時間テーブルに追加します。|  
|Cube|計算を実行する多次元式 (MDX) コードを定義する、計算されるメンバーを追加します。|  
  
## <a name="see-also"></a>参照  
 [計算されるメンバーの作成](create-calculated-members.md)  
  
  
