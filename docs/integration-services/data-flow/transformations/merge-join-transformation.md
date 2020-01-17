---
title: マージ結合変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.mergejointrans.f1
- sql13.dts.designer.mergejointransformation.f1
helpviewer_keywords:
- datasets [Integration Services]
- Merge Join transformation
- datasets [Integration Services], joining
- joining datasets [Integration Services]
- joins [SQL Server], SSIS
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f963a3f8bf82ed3de76e31b6872ac6475d6dfd83
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297847"
---
# <a name="merge-join-transformation"></a>Merge Join Transformation

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  マージ結合変換では、FULL、LEFT、または INNER 結合を使用して並べ替えた 2 つのデータセットを結合した出力が生成されます。 たとえば、LEFT 結合を使用して、製品情報を含むテーブルを、製品が製造された国または地域を一覧表示するテーブルと結合します。 その結果、すべての製品とその製造元である国または地域を一覧表示するテーブルが生成されます。  
  
 マージ結合変換は、次の方法で構成できます。  
  
-   FULL、LEFT、または INNER 結合のうち、どの結合を使用するかを指定します。  
  
-   結合で使用する列を指定します。  
  
-   NULL 値を、他の NULL と等しい値として処理するかどうかを指定します。  
  
    > [!NOTE]  
    >  NULL 値どうしを等しい値として扱わない場合、マージ結合変換では、SQL Server データベース エンジンによる処理方法と同様に NULL 値が処理されます。  
  
 この変換は、2 つの入力と 1 つの出力をとります。 エラー出力はサポートされていません。  
  
## <a name="input-requirements"></a>入力要件  
 マージ結合変換では、入力データが並べ替えられている必要があります。 この重要な要件の詳細については、「 [マージ変換およびマージ結合変換用にデータを並べ替える](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)」を参照してください。  
  
## <a name="join-requirements"></a>結合要件  
 マージ結合変換では、結合列のメタデータが一致している必要があります。 たとえば、数値データ型の列と文字データ型の列は結合できません。 データが文字列データ型の場合、2 番目の入力の列の長さは、マージ先の最初の入力の列の長さ以下である必要があります。  
  
## <a name="buffer-throttling"></a>バッファー スロットル  
 マイクロソフトが行った変更により、マージ結合変換によってメモリが過度に消費されるリスクが軽減したため、 **MaxBuffersPerInput** プロパティの値を構成する必要はなくなりました。 この問題は、マージ結合の複数の入力からデータが不均一なレートで生成される場合に発生することがありました。  
  
## <a name="related-tasks"></a>Related Tasks  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 この変換のプロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [マージ結合変換を使用してデータセットを拡張する](../../../integration-services/data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)  
  
-   [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [マージ変換およびマージ結合変換用にデータを並べ替える](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="merge-join-transformation-editor"></a>マージ結合変換エディター
  **[マージ結合変換エディター]** ダイアログ ボックスを使用すると、結合の種類、結合列、および結合によって組み合わされた 2 つの入力をマージするための出力列を指定できます。  
  
> [!IMPORTANT]  
>  マージ結合変換では、入力データが並べ替えられている必要があります。 この重要な要件の詳細については、「 [マージ変換およびマージ結合変換用にデータを並べ替える](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **[結合の種類]**  
 内部結合、左外部結合、または完全結合を使用するかどうかを指定します。  
  
 **[入力の入れ替え]**  
 **[入力の入れ替え]** ボタンを使用して、入力間の順序を切り替えます。 この選択は、左外部結合オプションで使用すると便利です。  
  
 **入力**  
 出力をマージする各列は、使用できる入力の一覧から最初に選択します。  
  
 入力は 2 つの個別のテーブルに表示されます。 出力に含める列を選択します。 テーブル間の結合を作成する列をドラッグします。 結合を削除するには、選択してから Del キーを押します。  
  
 **入力列**  
 選択した入力の使用できる列の一覧からマージする出力に含める列を選択します。  
  
 **[出力の別名]**  
 各出力列の別名を入力します。 既定は入力列の名前です。一意のわかりやすい名前を付けることもできます。  
  
## <a name="see-also"></a>参照  
 [マージ変換](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [全体結合変換](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
