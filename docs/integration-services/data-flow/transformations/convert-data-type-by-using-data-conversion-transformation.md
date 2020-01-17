---
title: データ変換の変換を使用してデータ型を変換する | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: 4aabbe4f-7666-4672-865a-9627bd25fbfd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2587c08c3ebf919a1665989863dc46e23a0ae690
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297989"
---
# <a name="convert-data-type-by-using-data-conversion-transformation"></a>データ変換の変換を使用してデータ型を変換する

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
10. エラー出力を構成するには、 **[エラー出力の構成]** をクリックします。 詳細については、「 [データ フローのデバッグ](../../../integration-services/troubleshooting/debugging-data-flow.md)」を参照してください。  
  
11. **[OK]** をクリックします。  
  
12. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)   
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services のパス](../../../integration-services/data-flow/integration-services-paths.md)   
 [Integration Services のデータ型](../../../integration-services/data-flow/integration-services-data-types.md)   
 [[データ フロー タスク]](../../../integration-services/control-flow/data-flow-task.md)  
  
  
