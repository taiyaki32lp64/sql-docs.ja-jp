---
title: 全体結合変換を使用してデータをマージする | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- merging datasets [Integration Services]
- merging inputs [Integration Services]
- combining datasets
- Union All transformation
- datasets [Integration Services], merging
ms.assetid: 78304403-a81c-4101-b87e-ec80ddfdac98
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7f5504c6f58d7ff5254d081ea479ca30ed6ca705
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770344"
---
# <a name="merge-data-by-using-the-union-all-transformation"></a>全体結合変換を使用してデータをマージする
  全体結合変換を追加して構成するには、パッケージに 1 つ以上のデータ フロー タスクと 2 つのデータ ソースがあらかじめ含まれている必要があります。  
  
 全体結合変換は、複数の入力を結合します。 この変換に連結される最初の入力は参照入力であり、その後に連結される入力はセカンダリ入力と呼ばれます。 出力には、参照入力内の列が含まれます。  
  
### <a name="to-combine-inputs-in-a-data-flow"></a>データ フローの入力を結合するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]で、ソリューション エクスプローラー内のパッケージをダブルクリックし、 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでそのパッケージを開きます。次に、 **[データ フロー]** タブをクリックします。  
  
2.  **[ツールボックス]** で、全体結合変換を **[データ フロー]** タブのデザイン画面にドラッグします。  
  
3.  全体結合変換をデータ フローに連結します。連結するには、データ ソースまたは前の変換から全体結合変換にコネクタをドラッグします。  
  
4.  全体結合変換をダブルクリックします。  
  
5.  **[全体結合変換エディター]** で、入力の一覧の行をクリックして次に列を選択し、入力の列を **[出力列の名前]** 一覧にある列にマップします。 列のマッピングをスキップするには、入力の一覧で **[\<無視>]** を選択します。  
  
    > [!NOTE]  
    >  2 つの列の間のマッピングでは、列のメタデータが一致する必要があります。  
  
    > [!NOTE]  
    >  参照列にマップされないセカンダリ入力の列は、出力では NULL 値に設定されます。  
  
6.  必要に応じて、 **[出力列の名前]** 列で列の名前を変更します。  
  
7.  各入力の列ごとに、手順 5. と 6. を繰り返します。  
  
8.  [**OK**] をクリックします。  
  
9. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Union All Transformation](union-all-transformation.md)   
 [Integration Services の変換](integration-services-transformations.md)   
 [Integration Services のパス](../integration-services-paths.md)   
 [[データ フロー タスク]](../../control-flow/data-flow-task.md)  
  
  
