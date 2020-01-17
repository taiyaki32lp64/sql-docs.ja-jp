---
title: レポート変数コレクションとグループ変数コレクションの参照 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10404"
- sql12.rtp.rptdesigner.categorygroupproperties.variables.f1
- "10083"
- sql12.rtp.rptdesigner.seriesgroupproperties.variables.f1
- sql12.rtp.rptdesigner.reportproperties.variables.f1
- sql12.rtp.rptdesigner.groupproperties.variables.f1
- "10292"
- "10412"
ms.assetid: 4be5b463-3ce2-483d-a3c6-dae752cb543e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cfedde2b9bdeff831029f2f3916f28bec480d659
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106394"
---
# <a name="report-and-group-variables-collections-references-report-builder-and-ssrs"></a>レポート変数コレクションとグループ変数コレクションの参照 (レポート ビルダーおよび SSRS)
  レポート内の式で複数回使用される複雑な計算があれば、変数を作成した方がよい場合があります。 このような場合は、レポート変数またはグループ変数を作成できます。 変数名は、レポート内で一意である必要があります。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-variables"></a>レポート変数  
 レポート変数は、為替レートやタイム スタンプなどの時間に依存する計算や、複数回参照される複雑な計算で、値を保持するために使用します。 既定では、レポート変数は 1 回計算すると、レポート全体の式で使用できます。 レポート変数は既定では読み取り専用です。 既定を変更して、レポート変数を読み書き可能にすることもできます。 レポート変数の値はセッション全体で維持され、次回レポートを処理するときまで変わりません。  
  
 レポート変数を追加するには、 **[レポートのプロパティ]** ダイアログ ボックスを開き、 **[変数]** をクリックして、名前と値を指定します。 文字で始まり、空白を含まない名前を入力します。名前の文字列は大文字と小文字が区別されます。 名前に含めることができるのは、文字、数字、またはアンダースコア (_) だけです。  
  
 式で変数を参照するには、 `=Variables!CustomTimeStamp.Value`などのグローバル コレクション構文を使用します。 デザイン画面では、この値が `<<Expr>>`としてテキスト ボックスに表示されます。  
  
 レポート変数は、次の方法で使用できます。  
  
-   **読み取り専用の使用** たとえば、タイム スタンプを作成する場合に、値を 1 回設定してレポート セッションの定数を作成します。  
  
     テキスト ボックス内の式はユーザーがレポートを読み進める間に要求に応じて評価されるため、次のページに進んでから `Now()` [戻る] **ボタンを使用して戻ると、動的な値 (時刻を返す** 関数が含まれている式など) から異なる値が返される場合があります。 レポート変数の値に式 `=Now()`を設定し、その変数を式に追加することで、レポート処理全体で同じ値が使用されるようになります。  
  
-   **読み書き可能な使用** 値を 1 回設定して、レポート セッション内でその値をシリアル化します。 変数の読み書き可能オプションは、レポート定義のコード ブロックで静的変数を使用するよりも適切な方法です。  
  
     オフにすると、**読み取り専用**変数、書き込み可能なプロパティのオプションに設定されている変数を`true`します。 式から値を更新するには、SetValue メソッド (たとえば、 `=Variables!MyVariable.SetValue("123")`) を使用します。  
  
    > [!NOTE]  
    >  レポート プロセッサによって変数が初期化される時期や、変数を更新する式が評価される時期を制御することはできません。 変数の初期化の実行順序は定義されません。  
  
 詳細については、「 [レポート ビルダーでのレポートのプレビュー](../report-builder/previewing-reports-in-report-builder.md)」を参照してください。  
  
## <a name="group-variables"></a>グループ変数  
 グループ変数は、グループのスコープ内で複合式を 1 回計算するために使用します。 グループ変数は、グループとその子グループのスコープ内でのみ有効です。  
  
 たとえば、別々の税区分にある各アイテムの在庫データをデータ領域に表示し、各カテゴリに異なる税率を適用するとします。 Category でデータをグループ化し、親グループで *Tax* 変数を定義します。 次に、税区分ごとに *ItemTax* のグループ変数を定義し、異なる Category サブグループをそれぞれ適切なグループ変数に割り当てます。 例 :  
  
-   `[Category]`に基づく親グループでは、値 *Tax* を指定して、変数 `[Tax]`を定義します。 カテゴリ値が Food と Clothing であるとします。  
  
-   `[Subcategory]`に基づく子グループでは、変数 *ItemsTax* を `=Variables!Tax.Value * Sum(Fields!Price.Value)`として定義します。 Food カテゴリのサブカテゴリ値が Beverages と Bread、 Clothing カテゴリのサブカテゴリ値が Shirts と Hats であるとします。  
  
-   子グループの行のテキスト ボックスで、式 `=Variables!ItemsTax.Value`を追加します。  
  
     このテキスト ボックスには、Food の税を使用した場合は Beverages と Bread、Clothing の税を使用した場合は Shirts と Hats の税の総額が表示されます。  
  
 グループ変数を追加するには、 **[Tablix グループのプロパティ]** ダイアログ ボックスを開き、 **[変数]** をクリックし、名前および値を指定します。 グループ変数は、一意のグループの値ごとに 1 回計算されます。  
  
 式で変数を参照するには、 `=Variables!GroupDescription.Value`などのグローバル コレクション構文を使用します。 デザイン画面では、この値が `<<Expr>>`としてテキスト ボックスに表示されます。  
  
## <a name="see-also"></a>関連項目  
 [データのフィルター、グループ化、および並べ替え &#40;レポート ビルダーおよび SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [式で使用される組み込みコレクション (レポート ビルダーおよび SSRS)](built-in-collections-in-expressions-report-builder.md)   
 [式の例 &#40;レポート ビルダーおよび SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
  
