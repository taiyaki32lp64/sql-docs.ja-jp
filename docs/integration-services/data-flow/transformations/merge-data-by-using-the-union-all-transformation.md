---
title: "和集合のすべての変換を使用してデータをマージ |Microsoft ドキュメント"
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
- merging datasets [Integration Services]
- merging inputs [Integration Services]
- combining datasets
- Union All transformation
- datasets [Integration Services], merging
ms.assetid: 78304403-a81c-4101-b87e-ec80ddfdac98
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b2f9933f48083b0849ba01312979911bacb4fd86
ms.contentlocale: ja-jp
ms.lasthandoff: 08/03/2017

---
# <a name="merge-data-by-using-the-union-all-transformation"></a>全体結合変換を使用してデータをマージする
  全体結合変換を追加して構成するには、パッケージに 1 つ以上のデータ フロー タスクと 2 つのデータ ソースがあらかじめ含まれている必要があります。  
  
 全体結合変換は、複数の入力を結合します。 この変換に連結される最初の入力は参照入力であり、その後に連結される入力はセカンダリ入力と呼ばれます。 出力には、参照入力内の列が含まれます。  
  
### <a name="to-combine-inputs-in-a-data-flow"></a>データ フローの入力を結合するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]で、ソリューション エクスプローラー内のパッケージをダブルクリックし、 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでそのパッケージを開きます。次に、 **[データ フロー]** タブをクリックします。  
  
2.  **[ツールボックス]**で、全体結合変換を **[データ フロー]** タブのデザイン画面にドラッグします。  
  
3.  全体結合変換をデータ フローに連結します。連結するには、データ ソースまたは前の変換から全体結合変換にコネクタをドラッグします。  
  
4.  全体結合変換をダブルクリックします。  
  
5.  **[全体結合変換エディター]** で、入力の一覧の行をクリックして次に列を選択し、入力の列を **[出力列の名前]** 一覧にある列にマップします。 選択**\<無視 >**列のマッピングをスキップする入力の一覧にします。  
  
    > [!NOTE]  
    >  2 つの列の間のマッピングでは、列のメタデータが一致する必要があります。  
  
    > [!NOTE]  
    >  参照列にマップされないセカンダリ入力の列は、出力では NULL 値に設定されます。  
  
6.  必要に応じて、 **[出力列の名前]** 列で列の名前を変更します。  
  
7.  各入力の列ごとに、手順 5. と 6. を繰り返します。  
  
8.  **[OK]**をクリックします。  
  
9. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Union All Transformation](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services のパス](../../../integration-services/data-flow/integration-services-paths.md)   
 [データ フロー タスク](../../../integration-services/control-flow/data-flow-task.md)  
  
  