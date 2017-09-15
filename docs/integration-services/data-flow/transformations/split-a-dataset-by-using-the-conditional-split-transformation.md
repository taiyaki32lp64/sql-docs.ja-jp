---
title: "条件分割変換を使用してデータセットを分割 |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Conditional Split transformation
- splitting dataset
- datasets [Integration Services], splitting
ms.assetid: 23b3e84f-9296-4dc9-81c0-c7f06ae3f1ff
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 8248e068541c6bd72b21f78d121811f4851850bb
ms.contentlocale: ja-jp
ms.lasthandoff: 08/03/2017

---
# <a name="split-a-dataset-by-using-the-conditional-split-transformation"></a>条件分割変換を使用してデータセットを分割する
  条件分割変換を追加して構成するには、パッケージに 1 つ以上のデータ フロー タスクと 1 つの変換元があらかじめ含まれている必要があります。  
  
### <a name="to-conditionally-split-a-dataset"></a>データセットを条件に応じて分割するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[データ フロー]** タブをクリックし、 **[ツールボックス]**で、条件分割変換をデザイン画面にドラッグします。  
  
4.  条件分割変換をデータ フローに連結します。連結するには、データ ソースまたは前の変換から条件分割変換にコネクタをドラッグします。  
  
5.  条件分割変換をダブルクリックします。  
  
6.  **[条件分割変換エディター]**で、変数、列、関数、および演算子を、グリッドの **[条件]** 列にドラッグし、条件として使用する式を構築します。 **[条件]** 列には、式を直接入力することもできます。  
  
    > [!NOTE]  
    >  1 つの変数または列を、複数の式で使用できます。  
  
    > [!NOTE]  
    >  式が有効でない場合、式のテキストは強調表示され、列のツールヒントにエラーの説明が表示されます。  
  
7.  必要に応じ、 **[出力名]** 列の値を変更します。 既定の名前は、Case 1、Case 2 などとなります。  
  
8.  条件が評価される順序を変更するには、上矢印または下矢印をクリックします。  
  
    > [!NOTE]  
    >  該当する可能性が最も高い条件を、一覧の先頭に配置します。  
  
9. 必要に応じて、どの条件にも一致しないデータ行の、既定の出力名を変更します。  
  
10. エラー出力を構成するには、 **[エラー出力の構成]**をクリックします。 詳細については、「 [データ フローのデバッグ](../../../integration-services/troubleshooting/debugging-data-flow.md)」を参照してください。  
  
11. **[OK]**をクリックします。  
  
12. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [条件分割変換](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)   
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services のパス](../../../integration-services/data-flow/integration-services-paths.md)   
 [Integration Services のデータ型](../../../integration-services/data-flow/integration-services-data-types.md)   
 [データ フロー タスク](../../../integration-services/control-flow/data-flow-task.md)   
 [Integration Services & #40 です。SSIS &#41;式](../../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  