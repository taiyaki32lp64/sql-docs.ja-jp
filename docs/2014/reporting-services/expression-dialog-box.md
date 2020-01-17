---
title: '[式] ダイアログ ボックス |Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10040"
- sql12.rtp.rptdesigner.expression.f1
helpviewer_keywords:
- Expression dialog box [Reporting Services]
ms.assetid: e6c74ccb-4594-4d4f-b958-618d710e34eb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 905aa453c8a6cac78e8423d071672d6431e3c3c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109196"
---
# <a name="expression-dialog-box"></a>[式] ダイアログ ボックス
  使用して、**式**書き込む ダイアログ ボックス[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[vbprvb](../includes/vbprvb-md.md)]の式のレポート アイテムのプロパティ。 式を使用して、色、フォント、罫線など多数のプロパティを設定できます。 実行時に、レポート プロセッサによって式が評価され、その結果がプロパティの値に置き換えられます。  
  
 式には、簡単なものも複雑なものもあります。 簡単な式は、デザイン画面またはダイアログ ボックスにあるテキスト ボックスに直接入力できます。 複雑な式を作成するには、使用、**式** ダイアログ ボックス。 作成できる式は一度に 1 つだけです。 詳細については、「[式 (レポート ビルダーおよび SSRS)](report-design/expressions-report-builder-and-ssrs.md)」を参照してください。  
  
 **[式]** ダイアログ ボックスを開くには、ダイアログ ボックスの式 ( **[fx]** ) ボタンをクリックするか、ショートカット メニューまたは [プロパティ] ペインのドロップダウン リストの **[式]** を選択します。 詳細については、次を参照してください。[レポートで式を使用して&#40;レポート ビルダーおよび SSRS&#41;](report-design/expression-uses-in-reports-report-builder-and-ssrs.md)します。  
  
 **[式]** ダイアログ ボックスには、コード ウィンドウ、カテゴリ ツリー、カテゴリ アイテム、説明ペイン、およびサンプル ペインが含まれています。  
  
 **[式]** ダイアログ ボックスは状況に依存するため、使用中の式カテゴリに応じてカテゴリ アイテムおよび説明が変わります。 このダイアログ ボックスでは、IntelliSense、入力候補、関数呼び出しの例、および構文の色分けをサポートしており、構文エラーの検出に役立ちます。  
  
## <a name="expression-constructs"></a>式の構成  
 式は等号 (=) で始まり、定数、リテラル、演算子に加え、組み込みフィールド、組み込みコレクション、組み込み関数、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ランタイム ライブラリ関数、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 共通言語ランタイム クラス、およびカスタム関数への参照を含むことができます。 式に追加できるカテゴリおよび値を次に示します。  
  
 **式を設定します。** _\<PropertyName>_  
 式を定義するプロパティの名前です。 このプロパティは、[プロパティ] ペインで名前を指定して設定することもできます。  
  
 **定数**  
 定数に基づくプロパティに有効な定義済みの値の一覧を、このプロパティに提供します。 たとえば、色に基づいたプロパティでは、有効な色の名前が表示されます。 ブール値型のプロパティの場合、値は `True` および `False` になります。  
  
 式をサポートするすべてのアイテムに定数を設定できるとは限りません。 プロパティに定数値を設定できない場合は、その情報が説明ペインに表示されます。  
  
 **組み込みフィールド**  
 式で使用できるグローバル コレクションのアイテムの一覧を表示します。 一部のコレクションは、レポートがサーバーにパブリッシュされるまでサポートされません。 詳細については、「[組み込み Globals および Users 参照 &#40;レポート ビルダーおよび SSRS&#41;](report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)」をご覧ください。  
  
 **パラメーター**  
 レポート パラメーターの一覧を表示します。  
  
 **フィールド (** _\<データセットを選択 >_ **)**  
 [データセット] カテゴリで選択したデータセットのフィールドの一覧を表示します。 **[式]** ボックスにフィールドをコピーするには、フィールドをダブルクリックします。  
  
 **データセット**  
 使用できるデータセットの一覧を提供し、データセットのメンバーのフィールドを表示します。  
  
 **変数**  
 レポート変数の一覧を表示します。 詳細については、「[レポート変数コレクションとグループ変数コレクションの参照 (レポート ビルダーおよび SSRS)](report-design/built-in-collections-report-and-group-variables-references-report-builder.md)」を参照してください。  
  
 **演算子**  
 計算または文字列操作に含めることができる演算子を表示します。 詳しくは、「[式で使用される演算子 &#40;レポート ビルダーおよび SSRS&#41;](report-design/operators-in-expressions-report-builder-and-ssrs.md)」をご覧ください。  
  
 **共通の関数**  
 共通の関数を、種類ごとにグループ化して表示します。 [アイテム] ペインで関数を選択すると、説明と例が表示されます。  
  
 共通の関数には、組み込みのレポート関数と集計関数、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ランタイム ライブラリ関数、および <xref:System.Math> 名前空間と <xref:System.Convert> 名前空間の [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 共通言語ランタイム (CLR) クラスが含まれます。 また、カテゴリの一覧には表示されない、CLR クラスおよび外部アセンブリへの参照を追加することもできます。 詳しくは、「[レポート デザイナーでカスタム コードやアセンブリを式から参照する &#40;SSRS&#41;](report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)」をご覧ください。  
  
## <a name="options"></a>および  
 [コード ウィンドウ]  
 上部ペインのコード ウィンドウを使用して式を入力します。 **[式]** ダイアログ ボックスを開くと、コード ウィンドウには式が含まれています。 式を置換または変更できます。 関数呼び出し、演算子、定数、フィールド、パラメーター、グローバル コレクションのアイテム、およびカスタム コードへの参照を追加できます。 式を変更すると、変更内容がコード ウィンドウに表示されます。  
  
 赤い波線は、構文エラーを示します。 エラー メッセージを表示するには、下線が付けられたテキストの上にカーソルを合わせます。  
  
 グローバル コレクションの用語を入力し、その後に句読点を入力すると、使用できるメンバーまたはプロパティのドロップダウン リストが表示されます。 ドロップダウン リストを使用すると、最初の何文字かを入力した後タブを入力するだけで、自動的に選択することができます。  
  
 関数名に続けて左かっこを入力すると、パラメーターと関数の戻り値に関する情報を提供するツールヒントが表示されます。  
  
 **カテゴリ**  
 式のカテゴリを表示します。 カテゴリを選択すると、式を作成するためのコンテキストが確立され、[アイテム] ペインで有効な値の一覧が変更されます。 の式のテキスト ボックスの値、共通の関数を展開し、表示する集計関数を選択します。 `Avg`、 `Count`、およびその他の関数で、**項目**ウィンドウ。  
  
 **アイテム**  
 選択したカテゴリに有効な値の一覧を表示します。 アイテムをダブルクリックすると、コード ウィンドウ内のカーソルの位置に、このアイテムの式のテキストが追加されます。  
  
 **値**  
 選択したカテゴリとアイテムに応じて、3 番目のペインには説明、サンプル式、または有効な値の一覧が表示されます。 サンプル領域を広げるには、ダイアログ ボックスの枠をドラッグします。  
  
## <a name="see-also"></a>参照  
 [式 &#40;レポート ビルダーおよび SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](report-design/expression-examples-report-builder-and-ssrs.md)   
 [レポートでの式の使用 (レポート ビルダーおよび SSRS)](report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [数値と日付の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Parameters コレクションの参照 &#40;レポート ビルダーおよび SSRS&#41;](report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [グループ式の例 &#40;レポート ビルダーおよび SSRS&#41;](report-design/group-expression-examples-report-builder-and-ssrs.md)   
 [フィルター式の例 &#40;レポート ビルダーおよび SSRS&#41;](report-design/filter-equation-examples-report-builder-and-ssrs.md)   
 [式で使用されるデータ型 &#40;レポート ビルダーおよび SSRS&#41;](report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [式で使用される組み込みコレクション (レポート ビルダーおよび SSRS)](report-design/built-in-collections-in-expressions-report-builder.md)   
 [式の追加 (レポート ビルダーおよび SSRS)](report-design/add-an-expression-report-builder-and-ssrs.md)  
  
  
