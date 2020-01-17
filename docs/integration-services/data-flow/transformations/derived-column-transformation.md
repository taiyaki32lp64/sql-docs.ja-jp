---
title: 派生列変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.derivedcolumntrans.f1
- sql13.dts.designer.derivedcolumntransformation.f1
helpviewer_keywords:
- multiple derived columns
- expressions [Integration Services], derived columns
- derived columns
- columns [Integration Services], derivations
- Derived Column transformation
ms.assetid: 8eba755e-8e48-4233-bd1e-09a46bf2692f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e605c4fb62e56113a5cc36e418d5648ed6ba3031
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297953"
---
# <a name="derived-column-transformation"></a>派生列変換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  派生列変換では、式を変換入力列に適用することにより新しい列の値を作成します。 式には、変換入力からの列、変数、関数、および演算子の任意の組み合わせを含めることができます。 結果は、新しい列として追加するか、または既存の列の値を置き換える値として挿入できます。 派生列変換では複数の派生列を定義でき、任意の変数または入力列を複数の式に含めることができます。  
  
 この変換を使用すると、次のタスクを実行できます。  
  
-   複数の異なる列のデータを 1 つの派生列に連結します。 たとえば、 **という式を使用すると、** FirstName **列と** LastName **列の値を、1 つの**FullName `FirstName + " " + LastName`という名前の派生列に結合できます。  
  
-   SUBSTRING などの関数を使用して文字列データから文字を抽出し、その結果を派生列に格納します。 たとえば、 **という式を使用すると、** FirstName `SUBSTRING(FirstName,1,1)`列から名前の頭文字を抽出できます。  
  
-   数学関数を数値データに適用し、その結果を派生列に格納します。 たとえば、 **という式を使用すると、数値列**SalesTax `ROUND(SalesTax, 2)`の長さと有効桁数を、小数点以下 2 桁に変更できます。  
  
-   入力列と変数を比較する式を作成します。 たとえば、 **という式を使用すると、変数** Version **と列**ProductVersion **のデータを比較し、その比較結果に応じて、** Version **と**ProductVersion `ProductVersion == @Version? ProductVersion : @Version`のどちらかの値を使用できます。  
  
-   datetime 値の一部を抽出します。 たとえば、 `DATEPART("year",GETDATE())`という式を使用すると、GETDATE 関数と DATEPART 関数を使用して現在の年を抽出できます。  
  
-   式を使用して、日付文字列を特定の形式に変換します。  
  
## <a name="configuration-of-the-derived-column-transformation"></a>派生列変換の構成  
 派生列変換は、次の方法で構成できます。  
  
-   各入力列または変更する新しい列に対し、式を設定します。 詳細については、「[Integration Services &#40;SSIS&#41; の式](../../../integration-services/expressions/integration-services-ssis-expressions.md)」を参照してください。  
  
    > [!NOTE]  
    >  派生列変換によって上書きされる入力列を式が参照する場合、その式は派生した値ではなく、列の元の値を使用します。  
  
-   データ型が **文字列**の場合に結果を新しい列に追加するには、コード ページを指定します。 詳しくは、「 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)」をご覧ください。  
  
 派生列変換には、FriendlyExpression カスタム プロパティがあります。 このプロパティは、パッケージの読み込み時にプロパティ式で更新できます。 詳細については、「 [パッケージでプロパティ式を使用する](../../../integration-services/expressions/use-property-expressions-in-packages.md)」および「 [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)」を参照してください。  
  
 この変換は、1 つの入力、1 つの標準出力、および 1 つのエラー出力をとります。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 プロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [派生列変換を使用して列の値を取得する](../../../integration-services/data-flow/transformations/derive-column-values-by-using-the-derived-column-transformation.md)  
  
## <a name="derived-column-transformation-editor"></a>派生列変換エディター
  **[派生列変換エディター]** ダイアログ ボックスを使用すると、新しい列または置換列を作成する式を作成できます。  
  
### <a name="options"></a>オプション  
 **[変数] と [列]**  
 使用可能な変数と列の一覧から、下のペインにある既存のテーブル行または一覧の下の新しい行へドラッグすることによって、変数または入力列を使用する式を作成します。  
  
 **[関数] と [演算子]**  
 関数と演算子を一覧から下のペインにドラッグすることによって、入力データおよび直接出力データを評価する関数または演算子を使用する式を作成します。  
  
 **[派生列名]**  
 派生列名を指定します。 既定は派生列の番号付けされた一覧ですが、一意のわかりやすい名前を付けることもできます。  
  
 **[派生列]**  
 一覧から派生列を選択します。 派生列を新しい出力列として追加するか、既存の列のデータを置き換えるかを選択します。  
  
 **[式]**  
 式を入力するか、前述の使用可能な列、変数、関数、および演算子の一覧からドラッグすることによって式を作成します。  
  
 このプロパティの値は、プロパティ式を使用して指定することができます。  
  
 **関連トピック**: [Integration Services &#40;SSIS&#41; 式](../../../integration-services/expressions/integration-services-ssis-expressions.md)、[演算子 &#40;SSIS 式&#41;](../../../integration-services/expressions/operators-ssis-expression.md)、[関数 &#40;SSIS 式&#41;](../../../integration-services/expressions/functions-ssis-expression.md)  
  
 **[データ型]**  
 新しい列にデータを追加すると、 **[派生列変換エディター]** ダイアログ ボックスによって自動的に式が評価され、データ型が適切に設定されます。 この列の値は読み取り専用です。 詳細については、「 [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
 **[データ型]**  
 新しい列にデータを追加すると、 **[派生列変換エディター]** ダイアログ ボックスによって自動的に式が評価され、文字列データに対する列の長さが設定されます。 この列の値は読み取り専用です。  
  
 **[精度]**  
 新しい列にデータを追加すると、 **[派生列変換エディター]** ダイアログ ボックスによって、データ型に基づく数値データの有効桁数が自動的に設定されます。 この列の値は読み取り専用です。  
  
 **[スケール]**  
 新しい列にデータを追加すると、 **[派生列変換エディター]** ダイアログ ボックスによって、データ型に基づく数値データの小数点以下桁数が自動的に設定されます。 この列の値は読み取り専用です。  
  
 **コード ページ**  
 新しい列にデータを追加すると、 **[派生列変換エディター]** ダイアログ ボックスによって、DT_STR データ型のコード ページが自動的に設定されます。 **[コード ページ]** は必要に応じて更新できます。  
  
 **[エラー出力の構成]**  
 [[エラー出力の構成]](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) ダイアログ ボックスを使用して、エラーの処理方法を指定します。  
  
## <a name="related-content"></a>関連コンテンツ  
 social.technet.microsoft.com の技術記事「 [SSIS 式の例](https://go.microsoft.com/fwlink/?LinkId=220761)」  
