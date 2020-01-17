---
title: 並べ替え変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sorttrans.f1
- sql13.dts.designer.sorttransformation.f1
helpviewer_keywords:
- Sort transformation
- descending sorts
- ascending sorts
- sorting data [Integration Services]
- multiple sorts
- duplicate data [Integration Services]
ms.assetid: 728c9351-84a8-4a89-be4d-d50d4adc04e0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1b8c49f0f462bf62bde8e92a1e51f981d18d7ef7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297746"
---
# <a name="sort-transformation"></a>並べ替え変換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  並べ替え変換は、入力データを昇順または降順で並べ替え、並べ替えたデータを変換出力にコピーします。 入力には複数の並べ替えを適用できます。各並べ替えは、並べ替えの順序を決定する数値によって識別されます。 順序の数値が最も小さい列が最初に並べ替えられ、順序の数値の大きさの順に列が並べ替えられます。 たとえば、 **CountryRegion** という名前の列の並べ替え順序が 1 で、 **City** という名前の列の並べ替え順序が 2 の場合、出力は、国または地域、次に都市の順に並べ替えられます。 正の値は昇順の並べ替えを表し、負の値は降順の並べ替えを表します。 並べ替えを行わない列の並べ替え順序は 0 です。 並べ替えを選択されていない列は、並べ替えられた列と共に、自動的に変換出力にコピーされます。  
  
 並べ替え変換には、比較オプションのセットが含まれており、変換による列の文字列データの処理方法を決定します。 詳しくは、「 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)」をご覧ください。  
  
> [!NOTE]  
>  並べ替え変換では、GUID は Transact-SQL で ORDER BY 句を使用したときと同じ順序では並べ替えられません。 並べ替え変換では、0 ～ 9 で始まる GUID は A ～ F で始まる GUID の前に並べ替えられますが、ORDER BY 句では [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]での実装と同じく、並べ替え変換とは異なる順番で並べ替えられます。 詳細については、「[ORDER BY 句 (Transact-SQL)](../../../t-sql/queries/select-order-by-clause-transact-sql.md)」を参照してください。  
  
 また、並べ替え変換では、並べ替えの実行時に重複する行を削除できます。 重複する行とは、並べ替えキーの値が同じ行のことです。 並べ替えキーの値は、使用する文字列比較オプションに基づいて生成されます。したがって、リテラル文字列が異なっていても、並べ替えキーの値は同じとなる場合があります。 並べ替え変換は、値は異なるが並べ替えキーが同じ入力列の行を、重複していると識別します。  
  
 並べ替え変換には、パッケージの読み込み時にプロパティ式で更新できる、**MaximumThreads** カスタム プロパティがあります。 詳細については、「[Integration Services (SSIS) の式](../../../integration-services/expressions/integration-services-ssis-expressions.md)」、「[パッケージでプロパティ式を使用する](../../../integration-services/expressions/use-property-expressions-in-packages.md)」、および「[変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)」を参照してください。  
  
 この変換は 1 つの入力と 1 つの出力をとります。 エラー出力はサポートされていません。  
  
## <a name="configuration-of-the-sort-transformation"></a>並べ替え変換の構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 コンポーネントのプロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="related-content"></a>関連コンテンツ  
 codeplex.com のサンプル「 [SortDeDuplicateDelimitedString カスタム SSIS コンポーネント](https://go.microsoft.com/fwlink/?LinkId=220821)」  
  
## <a name="sort-transformation-editor"></a>並べ替え変換エディター
  **[並べ替え変換エディター]** ダイアログ ボックスを使用すると、並べ替える列を選択し、並べ替え順を設定して、重複する部分を削除するかどうかを指定できます。  
  
### <a name="options"></a>オプション  
 **使用できる入力列**  
 このチェック ボックスを使用して、並べ替える列を指定します。  
  
 **[名前]**  
 使用できる各入力列の名前を表示します。  
  
 **パススルー**  
 並べ替えられる出力に列が含まれるかどうかを指定します。  
  
 **入力列**  
 各行に対して使用できる入力列の一覧から選択します。 選択内容が **[使用できる入力列]** テーブルのチェック ボックスに反映されます。  
  
 **[出力の別名]**  
 各出力列の別名を入力します。 既定は入力列の名前です。一意のわかりやすい名前を付けることもできます。  
  
 **[並べ替えの種類]**  
 昇順で並べ替えるか、降順で並べ替えるかを示します。  
  
 **並べ替え順序**  
 列を並べ替える順序を示します。 各列に対して手動で設定する必要があります。  
  
 **[比較フラグ]**  
 文字列比較オプションについては、「 [文字列データの比較](../../../integration-services/data-flow/comparing-string-data.md)」を参照してください。  
  
 **[重複した並べ替え値を含む行を削除する]**  
 指定された文字列比較オプションに基づいて、重複した列を変換出力にコピーするか、すべての重複部分に対して 1 つのエントリを作成するかを示します。  
  
## <a name="see-also"></a>参照  
 [データ フロー](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
