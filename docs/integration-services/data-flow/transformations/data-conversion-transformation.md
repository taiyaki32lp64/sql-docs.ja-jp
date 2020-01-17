---
title: データ変換の変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataconversiontrans.f1
- sql13.dts.designer.dataconversiontransformation.f1
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: fd515bbc-6f49-4d0c-ae7f-6ea3c3f24a1c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e1573167bfe50e5dcb63734a90c7b9b5bd00e40a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297967"
---
# <a name="data-conversion-transformation"></a>データ変換の変換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  データ変換の変換は、入力列のデータを別のデータ型に変換し、新しい出力列にコピーします。 たとえば、パッケージで複数の変換元のデータを抽出し、この変換を使用して、列を変換先のデータ ストアで要求されるデータ型に変換できます。 1 つの入力列に複数の変換を適用できます。  
  
 この変換を使用すると、パッケージで次の種類のデータ変換を実行できます。  
  
-   データ型を変更します。 詳細については、「 [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
    > [!NOTE]  
    >  date データ型または datetime データ型にデータを変換する場合、ロケール設定で別の形式が指定されている場合でも、出力列の日付は ISO 形式になります。  
  
-   文字列データの列の長さ、および数値データの有効桁数と小数点以下桁数を設定します。 詳しくは、「[有効桁数、小数点以下桁数、および長さ &#40;Transact-SQL&#41;](../../../t-sql/data-types/precision-scale-and-length-transact-sql.md)」をご覧ください。  
  
-   コード ページを指定します。 詳しくは、「 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)」をご覧ください。  
  
    > [!NOTE]  
    >  文字列データ型の 2 つの列間でコピーを行う場合、それらの列のコード ページは同じである必要があります。  
  
 文字列データの出力列の長さが、対応する入力列の長さよりも短い場合、出力データは切り捨てられます。 詳細については、「 [データのエラー処理](../../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。  
  
 この変換は、1 つの入力、1 つの出力、および 1 つのエラー出力をとります。  
  
## <a name="related-tasks"></a>Related Tasks  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。 SSIS デザイナーでのデータ変換の変換の使用については、「[データ変換の変換を使用してデータを別のデータ型に変換する](../../../integration-services/data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md)」を参照してください。 プログラムによるこの変換のプロパティの設定については、「 [共通プロパティ](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796) 」および「 [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)」をご覧ください。  
  
## <a name="related-content"></a>関連コンテンツ  
 blogs.msdn.com のブログ「 [SSIS 2008 のデータ型の変換手法間のパフォーマンス比較](https://go.microsoft.com/fwlink/?LinkId=220823)」  
  
## <a name="data-conversion-transformation-editor"></a>データ変換変換エディター
  **[データ変換変換エディター]** ダイアログ ボックスを使用すると、変換対象の列や列の変換先のデータ型を選択したり、変換属性を設定したりできます。  
  
> [!NOTE]  
>  データ変換の変換の出力列の **FastParse** プロパティは、 **[データ変換変換エディター]** ではアクセスできませんが、 **[詳細エディター]** を使用して設定できます。 このプロパティの詳細については、「 [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)」の「データ変換の変換」を参照してください。  
  
### <a name="options"></a>オプション  
 **使用できる入力列**  
 変換対象の列のチェック ボックスを使用して選択します。 選択した列が入力列として下のテーブルに追加されます。  
  
 **入力列**  
 使用できる入力列の一覧から変換対象の列を選択します。 上記のチェック ボックスに、選択内容が反映されます。  
  
 **[出力の別名]**  
 それぞれの新しい列の別名を入力します。 既定では、入力列の名前の後に " **のコピー** " が追加された別名になりますが、固有のわかりやすい名前を選択することもできます。  
  
 **[データ型]**  
 一覧から利用可能なデータ型を選択します。 詳細については、「 [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
 **[データ型]**  
 文字列データの列の長さを設定します。  
  
 **[精度]**  
 数値データの有効桁数を設定します。  
  
 **Scale**  
 数値データの小数点以下桁数を設定します。  
  
 **コード ページ**  
 DT_STR 型の列に適したコード ページを選択します。  
  
 **[エラー出力の構成]**  
 [[エラー出力の構成]](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) ダイアログ ボックスを使用して、エラーの処理方法を指定します。  
  
## <a name="see-also"></a>参照  
 [高速解析](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95)   
 [データ フロー](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
