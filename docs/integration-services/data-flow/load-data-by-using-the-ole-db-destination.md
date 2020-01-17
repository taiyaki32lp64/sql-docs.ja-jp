---
title: OLE DB 変換先を使用してデータを読み込む | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- loading data
- OLE DB destination [Integration Services]
- destinations [Integration Services], OLE DB
ms.assetid: 78899498-725e-4300-a7af-f983f4ea384b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 235491b5a3595098b42689f77fdc9077efd9b758
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292340"
---
# <a name="load-data-by-using-the-ole-db-destination"></a>OLE DB 変換先を使用してデータを読み込む

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  OLE DB 変換先を追加して構成するには、パッケージに 1 つ以上のデータ フロー タスクと 1 つの変換元があらかじめ含まれている必要があります。  
  
### <a name="to-load-data-using-an-ole-db-destination"></a>OLE DB 変換先を使用してデータを読み込むには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[データ フロー]** タブをクリックし、次に **[ツールボックス]** で、OLE DB 変換先をデザイン画面にドラッグします。  
  
4.  OLE DB 変換先をデータ フローに連結します。連結するには、データ ソースまたは前の変換から変換先にコネクタをドラッグします。  
  
5.  OLE DB 変換先をダブルクリックします。  
  
6.  **[OLE DB 変換先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページで、既存の OLE DB 接続マネージャーを選択するか、 **[新規作成]** をクリックして新しい接続マネージャーを作成します。 詳細については、「 [OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)」を参照してください。  
  
7.  データのアクセス方法を、次の中から選択します。  
  
    -   **[テーブルまたはビュー]** データが含まれるデータベース内のテーブルまたはビューを選択します。  
  
    -   **[テーブルまたはビュー - 高速読み込み]** データが含まれるデータベース内のテーブルまたはビューを選択し、高速読み込みのオプションを設定します。高速読み込みのオプションには、 **[ID を保持する]** 、 **[NULL を保持する]** 、 **[テーブル ロック]** 、 **[CHECK 制約]** 、 **[バッチごとの行数]** 、または **[挿入コミット サイズの最大値]** があります。  
  
    -   **[テーブル名またはビュー名の変数]** データベースのテーブルまたはビューの名前が含まれている、ユーザー定義変数を選択します。  
  
    -   **[テーブル名またはビュー名の変数 - 高速読み込み]** データが含まれるデータベースのテーブルまたはビューの名前が含まれているユーザー定義変数を選択し、次に高速読み込みのオプションを設定します。  
  
    -   **[SQL コマンド]** SQL コマンドを入力するか、 **[クエリ ビルダー]** で **[クエリの作成]** をクリックして、SQL コマンドを記述します。  
  
8.  **[マッピング]** をクリックし、 **[使用できる入力列]** 一覧にある列を、 **[使用できる変換先列]** 一覧の列にドラッグして、列をマップします。  
  
    > [!NOTE]  
    >  OLE DB 変換先では、同じ名前の列は自動的にマップされます。  
  
9. エラー出力を構成するには、 **[エラー出力]** をクリックします。 詳細については、「 [データ フローのデバッグ](../../integration-services/troubleshooting/debugging-data-flow.md)」を参照してください。  
  
10. **[OK]** をクリックします。  
  
11. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [OLE DB 変換先](../../integration-services/data-flow/ole-db-destination.md)   
 [Integration Services の変換](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services のパス](../../integration-services/data-flow/integration-services-paths.md)   
 [[データ フロー タスク]](../../integration-services/control-flow/data-flow-task.md)  
  
  
