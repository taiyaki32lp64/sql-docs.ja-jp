---
title: 集計変換を使用してデータセットの値を集計する | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- aggregate values [Integration Services]
- datasets [Integration Services], aggregate values
ms.assetid: 01b81c0f-d5e0-483b-81b2-73800a6945ac
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 805ca71b22a0c5f280c6e3475ba21133bef6dd6e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298030"
---
# <a name="aggregate-values-in-a-dataset-by-using-the-aggregate-transformation"></a>集計変換を使用してデータセットの値を集計する

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  集計変換を追加して構成するには、パッケージに 1 つ以上のデータ フロー タスクと 1 つの変換元があらかじめ含まれている必要があります。  
  
### <a name="to-aggregate-values-in-a-dataset"></a>データセットの値を集計するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[データ フロー]** タブをクリックし、次に **[ツールボックス]** で、集計変換をデザイン画面にドラッグします。  
  
4.  集計変換をデータ フローに連結します。連結するには、変換元または前の変換から集計変換にコネクタをドラッグします。  
  
5.  集計変換をダブルクリックします。  
  
6.  **[集計変換エディター]** ダイアログ ボックスで、 **[集計]** タブをクリックします。  
  
7.  **[使用できる入力列]** 一覧で、値を集計する列のチェック ボックスをオンにします。 選択した列が、テーブルに表示されます。  
  
    > [!NOTE]  
    >  1 つの列を複数回選択して、複数の変換をその列に適用できます。 集計を一意に識別するために、既定の名前に番号が追加され、列の出力が別名で保存されます。  
  
8.  必要に応じ、 **[出力の別名]** 列の値を変更します。  
  
9. 既定の集計操作である **[グループ化]** を変更するには、 **[操作]** 一覧で別の操作を選択します。  
  
10. 既定の比較を変更するには、 **[比較フラグ]** 列に示された各比較フラグを選択します。 既定の比較では、大文字と小文字、ひらがなとカタカナ、非空白文字、および文字幅は無視されます。  
  
11. **[個別のカウント]** 集計では、必要に応じて、個別の値の正確な数を **[個別カウント キー数]** 列で指定するか、カウントの概数を **[個別カウント スケール]** 列で選択します。  
  
    > [!NOTE]  
    >  個別の値を正確な数または概数で指定することにより、変換作業に適したメモリ量が事前に割り当てられるので、パフォーマンスを最適化できます。  
  
12. 必要に応じ、 **[詳細設定]** をクリックして集計変換出力の名前を更新します。 集計に **グループ化** 操作が含まれる場合、グループ化のキー値のカウントの概数を **[キー スケール]** 列で選択することも、グループ化のキー値の正確な数を **[キー]** 列で指定することもできます。  
  
    > [!NOTE]  
    >  個別の値を正確な数または概数で指定することにより、変換作業に適したメモリ量が事前に割り当てられるので、パフォーマンスを最適化できます。  
  
    > [!NOTE]  
    >  **[キー スケール]** と **[キー]** オプションは、相互に排他的です。 両方の列に値を入力した場合、 **[キー スケール]** と **[キー]** のうち、いずれか大きい方の値が使用されます。  
  
13. 必要に応じ、 **[詳細設定]** タブをクリックして、集計変換が実行するすべての操作を最適化する属性を設定します。  
  
14. **[OK]** をクリックします。  
  
15. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [集計変換](../../../integration-services/data-flow/transformations/aggregate-transformation.md)   
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services のパス](../../../integration-services/data-flow/integration-services-paths.md)   
 [[データ フロー タスク]](../../../integration-services/control-flow/data-flow-task.md)  
  
  
