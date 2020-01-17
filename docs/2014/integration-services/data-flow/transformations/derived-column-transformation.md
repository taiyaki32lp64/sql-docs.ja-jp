---
title: 派生列変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.derivedcolumntrans.f1
helpviewer_keywords:
- multiple derived columns
- expressions [Integration Services], derived columns
- derived columns
- columns [Integration Services], derivations
- Derived Column transformation
ms.assetid: 8eba755e-8e48-4233-bd1e-09a46bf2692f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2a2767de67eac1a0346f059e1a2c81a5698607dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900515"
---
# <a name="derived-column-transformation"></a>派生列変換
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
  
-   各入力列または変更する新しい列に対し、式を設定します。 詳細については、「[Integration Services &#40;SSIS&#41; の式](../../expressions/integration-services-ssis-expressions.md)」を参照してください。  
  
    > [!NOTE]  
    >  派生列変換によって上書きされる入力列を式が参照する場合、その式は派生した値ではなく、列の元の値を使用します。  
  
-   データ型が `string` の結果を新しい列に追加する場合は、コード ページを指定します。 詳しくは、「 [Comparing String Data](../comparing-string-data.md)」をご覧ください。  
  
 派生列変換には、FriendlyExpression カスタム プロパティがあります。 このプロパティは、パッケージの読み込み時にプロパティ式で更新できます。 詳細については、「 [パッケージでプロパティ式を使用する](../../expressions/use-property-expressions-in-packages.md)」および「 [変換のカスタム プロパティ](transformation-custom-properties.md)」を参照してください。  
  
 この変換は、1 つの入力、1 つの標準出力、および 1 つのエラー出力をとります。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[派生列変換エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、「 [派生列変換エディター](../../derived-column-transformation-editor.md)」を参照してください。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../../common-properties.md)  
  
-   [変換のカスタム プロパティ](transformation-custom-properties.md)  
  
 プロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [データ フロー コンポーネントのプロパティを設定する](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [派生列変換を使用して列の値を取得する](derived-column-transformation.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 social.technet.microsoft.com の技術記事「 [SSIS 式の例](https://go.microsoft.com/fwlink/?LinkId=220761)」  
  
 ブログ、 [SSIS を使用して列データの分割方法](https://microsoft-ssis.blogspot.com/2012/10/split-multi-value-column-into-multiple.html)します。  
  
  
