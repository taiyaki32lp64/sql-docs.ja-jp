---
title: データ フローのデバッグ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- progress reporting [Integration Services]
- data viewers [Integration Services]
- data flow [Integration Services], debugging
- debugging [Integration Services], data flow
- counting rows
ms.assetid: 1c574f1b-54f7-4c05-8e42-8620e2c1df0f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fdfaeeb9e8dafe82a1312593df2dd128635b8365
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62766195"
---
# <a name="debugging-data-flow"></a>データ フローのデバッグ
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] と [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのデータ フローのトラブルシューティングを行うために使用できる機能とツールが含まれています。  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでは、データ ビューアーが用意されています。  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーと [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 変換では、行数が用意されています。  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでは、実行時の進行状況レポートが用意されています。  
  
## <a name="data-viewers"></a>データ ビューアー  
 データ ビューアーは、データ フローの 2 つのコンポーネント間のデータを表示します。 データ ビューアーでデータを表示できるのは、データ ソースからデータが抽出され、最初にデータ フローに入るときと、変換によりデータが更新される前後、およびデータが変換先に読み込まれる前です。  
  
 データを表示するには、2 つのデータ フロー コンポーネントを連結するパスに、データ ビューアーをアタッチします。 データ フロー コンポーネント間のデータを表示する機能を使用すると、予期しないデータ値の識別、変換による列の値の変更方法の表示、および変換が失敗した原因の検出が容易になります。 たとえば、参照テーブル内の参照が失敗する場合、それを修正するために、既定データを空白の列に提供する変換を追加できます。  
  
 データ ビューアーでは、グリッドにデータを表示できます。 グリッドを使用する場合は、表示する列を選択します。 選択した列の値は、表形式で表示されます。  
  
 1 つのパスに、複数のデータ ビューアーを含めることもできます。 このため、同じデータをさまざまな形式で表示できます。たとえば、データのグラフ表示とグリッド表示を作成したり、データの列ごとに異なるデータ ビューアーを作成したりできます。  
  
 データ ビューアーをパスに追加すると、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでは、 **[データ フロー]** タブのデザイン画面のパスの隣に、データ ビューアーのアイコンが追加されます。 条件分割変換など、複数の出力を持つ変換には、パスごとにデータ ビューアーを含めることができます。  
  
 実行時には **[データ ビューアー]** ウィンドウが開き、データ ビューアーの形式で指定された情報が表示されます。 たとえば、グリッド形式を使用するデータ ビューアーでは、選択した列のデータ、データ フロー コンポーネントに渡される出力列の数、および表示される行数が表示されます。 この情報はバッファーごとに表示されますが、データ フローの行の幅に応じて、バッファーが表示する行数は増減します。  
  
 **[データ ビューアー]** ダイアログ ボックスでは、クリップボードへのデータのコピー、テーブルのすべてのデータの消去、データ ビューアーの再構成、データのフローの再開、およびデータ ビューアーのデタッチまたはアタッチを行うことができます。  
  
#### <a name="to-add-a-data-viewer"></a>データ ビューアーを追加するには  
  
-   [データ フローにデータ ビューアーを追加する](../add-a-data-viewer-to-a-data-flow.md)  
  
## <a name="row-counts"></a>行数  
 **デザイナーでは、** [データ フロー] [!INCLUDE[ssIS](../../includes/ssis-md.md)] タブのデザイン画面のパスの隣に、パスを通過した行数が表示されます。 データがパスを移動する間、表示される行数が定期的に更新されます。  
  
 また、データ フローに行数変換を追加して、最終的な行数を変数に取り込むこともできます。 詳細については、「 [Row Count Transformation](../data-flow/transformations/row-count-transformation.md)」を参照してください。  
  
## <a name="progress-reporting"></a>進行状況レポート  
 パッケージを実行すると、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの **[データ フロー]** タブのデザイン画面に、各データ フロー コンポーネントが状態を示す色で表示され、進行状況を確認できます。 各コンポーネントが作業を開始すると、コンポーネントは無色から黄色に変わり、正常に完了すると、緑色に変わります。 赤色は、コンポーネントが失敗したことを示します。  
  
 次の表では、色分けについて説明します。  
  
|色|説明|  
|-----------|-----------------|  
|無色|データ フロー エンジンによる呼び出しの待機中です。|  
|黄|変換の実行、データの抽出、またはデータの読み込みを行っています。|  
|[緑]|正常に実行されました。|  
|赤|実行されましたがエラーが発生しました。|  
  
## <a name="see-also"></a>参照  
 [パッケージ開発のトラブルシューティング ツール](troubleshooting-tools-for-package-development.md)  
  
  
