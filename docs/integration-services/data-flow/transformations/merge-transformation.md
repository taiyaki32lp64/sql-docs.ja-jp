---
title: マージ変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.mergetrans.f1
- sql13.dts.designer.mergetransformation.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- merging data [Integration Services]
- Merge transformation
- combining datasets
- datasets [Integration Services], merging
ms.assetid: cff8690c-07ac-46a0-aab5-20bd4848c677
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5badfcd6c8b9603e30e2a413bb6486fcf9d2c6b8
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291231"
---
# <a name="merge-transformation"></a>マージ変換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  マージ変換は、並べ替えられた 2 つのデータセットを 1 つのデータセットに結合します。 各データセットの行は、各キー列の値に基づいて出力に挿入されます。  
  
 データ フローにマージ変換を含めると、次のタスクを実行できます。  
  
-   テーブルやファイルなど、2 つのデータ ソースのデータをマージします。  
  
-   マージ変換を入れ子にして、複合データセットを作成します。  
  
-   データのエラーを修正後、行を再マージします。  
  
 マージ変換は、全体結合変換と似ています。 次の場合には、マージ変換ではなく全体結合変換を使用します。  
  
-   変換入力の並べ替えを行わない場合。  
  
-   結合された出力を並べ替える必要がない場合。  
  
-   マージ変換は 3 つ以上の入力をとります。  
  
## <a name="input-requirements"></a>入力要件  
 マージ変換では、入力データが並べ替えられている必要があります。 この重要な要件の詳細については、「 [マージ変換およびマージ結合変換用にデータを並べ替える](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)」を参照してください。  
  
 マージ変換では、入力されたマージ列のメタデータが一致している必要もあります。 たとえば、数値データ型の列と文字データ型の列はマージできません。 データが文字列データ型の場合、2 番目の入力の列の長さは、マージ先の最初の入力の列の長さ以下である必要があります。  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーのマージ変換のユーザー インターフェイスでは、同じメタデータを持つ列は自動的にマップされます。 互換性のあるデータ型を持つ他の列は、手動でマップできます。  
  
 この変換は、2 つの入力と 1 つの出力をとります。 エラー出力はサポートされていません。  
  
## <a name="configuration-of-the-merge-transformation"></a>マージ変換の構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 プログラムによって設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 プロパティの設定方法の詳細については、次の各トピックを参照してください。  
  
-   [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [マージ変換およびマージ結合変換用にデータを並べ替える](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="merge-transformation-editor"></a>マージ変換エディター
  **[マージ変換エディター]** を使用すると、マージする 2 つの並べ替え済みデータのセットの列を指定できます。  
  
> [!IMPORTANT]  
>  マージ変換では、入力データが並べ替えられている必要があります。 この重要な要件の詳細については、「 [マージ変換およびマージ結合変換用にデータを並べ替える](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **[出力列の名前]**  
 出力列の名前を指定します。  
  
 **[マージの入力 1]**  
 マージの入力の 1 つ目の列を選択します。  
  
 **[マージの入力 2]**  
 マージの入力の 2 つ目の列を選択します。  
  
## <a name="see-also"></a>参照  
 [マージ結合変換](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [全体結合変換](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [データ フロー](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
