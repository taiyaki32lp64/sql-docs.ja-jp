---
title: OLE DB 変換先を使用してデータを読み込む | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- loading data
- OLE DB destination [Integration Services]
- destinations [Integration Services], OLE DB
ms.assetid: 78899498-725e-4300-a7af-f983f4ea384b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 114460af84d4e820ccd263fc4bf5188b65775c85
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62902479"
---
# <a name="load-data-by-using-the-ole-db-destination"></a>OLE DB 変換先を使用してデータを読み込む
  OLE DB 変換先を追加して構成するには、パッケージに 1 つ以上のデータ フロー タスクと 1 つの変換元があらかじめ含まれている必要があります。  
  
### <a name="to-load-data-using-an-ole-db-destination"></a>OLE DB 変換先を使用してデータを読み込むには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[データ フロー]** タブをクリックし、次に **[ツールボックス]** で、OLE DB 変換先をデザイン画面にドラッグします。  
  
4.  OLE DB 変換先をデータ フローに連結します。連結するには、データ ソースまたは前の変換から変換先にコネクタをドラッグします。  
  
5.  OLE DB 変換先をダブルクリックします。  
  
6.  **[OLE DB 変換先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページで、既存の OLE DB 接続マネージャーを選択するか、 **[新規作成]** をクリックして新しい接続マネージャーを作成します。 詳細については、「 [OLE DB 接続マネージャー](../connection-manager/ole-db-connection-manager.md)」を参照してください。  
  
7.  データのアクセス方法を、次の中から選択します。  
  
    -   **[テーブルまたはビュー]** データが含まれるデータベース内のテーブルまたはビューを選択します。  
  
    -   **[テーブルまたはビュー - 高速読み込み]** データが含まれるデータベース内のテーブルまたはビューを選択し、高速読み込みのオプションを設定します。高速読み込みのオプションには、 **[ID を保持する]** 、 **[NULL を保持する]** 、 **[テーブル ロック]** 、 **[CHECK 制約]** 、 **[バッチごとの行数]** 、または **[挿入コミット サイズの最大値]** があります。  
  
    -   **[テーブル名またはビュー名の変数]** データベースのテーブルまたはビューの名前が含まれている、ユーザー定義変数を選択します。  
  
    -   **[テーブル名またはビュー名の変数 - 高速読み込み]** データが含まれるデータベースのテーブルまたはビューの名前が含まれているユーザー定義変数を選択し、次に高速読み込みのオプションを設定します。  
  
    -   **[SQL コマンド]** SQL コマンドを入力するか、 **[クエリ ビルダー]** で **[クエリの作成]** をクリックして、SQL コマンドを記述します。  
  
8.  **[マッピング]** をクリックし、 **[使用できる入力列]** 一覧にある列を、 **[使用できる変換先列]** 一覧の列にドラッグして、列をマップします。  
  
    > [!NOTE]  
    >  OLE DB 変換先では、同じ名前の列は自動的にマップされます。  
  
9. エラー出力を構成するには、 **[エラー出力]** をクリックします。 詳細については、「 [データ フロー コンポーネントでエラー出力を構成する](../configure-an-error-output-in-a-data-flow-component.md)」を参照してください。  
  
10. **[OK]** をクリックします。  
  
11. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [OLE DB 変換先](ole-db-destination.md)   
 [Integration Services の変換](transformations/integration-services-transformations.md)   
 [Integration Services のパス](integration-services-paths.md)   
 [[データ フロー タスク]](../control-flow/data-flow-task.md)  
  
  
