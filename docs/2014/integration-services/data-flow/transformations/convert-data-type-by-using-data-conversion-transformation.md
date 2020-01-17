---
title: データ変換の変換を使用してデータを別のデータ型に変換 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: 4aabbe4f-7666-4672-865a-9627bd25fbfd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 13faac66894298c4d08cd40a1eab9d3d823fd0ee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900872"
---
# <a name="convert-data-to-a-different-data-type-by-using-the-data-conversion-transformation"></a>データ変換の変換を使用してデータを別のデータ型に変換する
  データ変換の変換を追加して構成するには、パッケージに 1 つ以上のデータ フロー タスクと 1 つの変換元があらかじめ含まれている必要があります。  
  
### <a name="to-convert-data-to-a-different-data-type"></a>データを別のデータ型に変換するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[データ フロー]** タブをクリックし、次に **[ツールボックス]** で、データ変換の変換をデザイン画面にドラッグします。  
  
4.  データ変換の変換をデータ フローに連結します。連結するには、変換元または前の変換からデータ変換の変換にコネクタをドラッグします。  
  
5.  データ変換の変換をダブルクリックします。  
  
6.  **[データ変換変換エディター]** ダイアログ ボックスの **[使用できる入力列]** テーブルで、データ型を変換する列の隣にあるチェック ボックスをオンにします。  
  
    > [!NOTE]  
    >  1 つの入力列に複数のデータ変換を適用できます。  
  
7.  必要に応じ、 **[出力の別名]** 列の既定値を変更します。  
  
8.  **[データ型]** 一覧で、列の新しいデータ型を選択します。 既定のデータ型は、入力列のデータ型です。  
  
9. 選択したデータ型によっては、必要に応じて **[長さ]** 、 **[有効桁数]** 、 **[小数点以下桁数]** 、および **[コード ページ]** 列の値を更新します。  
  
10. エラー出力を構成するには、 **[エラー出力の構成]** をクリックします。 詳細については、「 [データ フロー コンポーネントでエラー出力を構成する](../../configure-an-error-output-in-a-data-flow-component.md)」を参照してください。  
  
11. **[OK]** をクリックします。  
  
12. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [Data Conversion Transformation](data-conversion-transformation.md)   
 [Integration Services の変換](integration-services-transformations.md)   
 [Integration Services のパス](../integration-services-paths.md)   
 [Integration Services のデータ型](../integration-services-data-types.md)   
 [[データ フロー タスク]](../../control-flow/data-flow-task.md)  
  
  
