---
title: OLE DB 接続マネージャーを使用してフル キャッシュ モードで参照変換を実装する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation [Integration Services]
ms.assetid: c4150e1b-bdff-4f7a-af4c-3401c34def83
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a11eb545aa4d9beefc0852bb68ed18a84ffe3256
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833708"
---
# <a name="implement-a-lookup-transformation-in-full-cache-mode-using-the-ole-db-connection-manager"></a>OLE DB 接続マネージャーを使用してフル キャッシュ モードの参照変換を実装する
  フル キャッシュ モードおよび OLE DB 接続マネージャーを使用するように参照変換を構成できます。 フル キャッシュ モードでは、参照変換の実行前に参照データセットがキャッシュに読み込まれます。  
  
 参照変換は、接続されているデータ ソースの入力列のデータを参照データセットの列と結合することにより参照を実行します。 詳細については、「 [Lookup Transformation](../data-flow/transformations/lookup-transformation.md)」を参照してください。  
  
 OLE DB 接続マネージャーを使用するように参照変換を構成する場合は、テーブル、ビュー、または SQL クエリを選択して参照データセットを生成します。  
  
### <a name="to-implement-a-lookup-transformation-in-full-cache-mode-by-using-ole-db-connection-manager"></a>OLE DB 接続マネージャーを使用してフル キャッシュ モードの参照変換を実装するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開き、ソリューション エクスプローラーでそのパッケージをダブルクリックします。  
  
2.  **[データ フロー]** タブで、 **[ツールボックス]** から参照変換をデザイン画面にドラッグします。  
  
3.  参照変換をデータ フローに連結します。連結するには、変換元または前の変換から参照変換にコネクタをドラッグします。  
  
    > [!NOTE]  
    >  参照変換が空の日付フィールドを含むフラット ファイルに接続される場合、その変換は検証されないことがあります。 変換が検証されるかどうかは、フラット ファイルの接続マネージャーが NULL 値を保持するように構成されているかどうかによって決まります。 参照変換が検証されるようにするには、 **フラット ファイル ソース エディター**の **[接続マネージャー]** ページで、 **[データ ソースの NULL 値をデータ フローで NULL 値として保持する]** オプションを選択します。  
  
4.  変換元または前の変換をダブルクリックして、コンポーネントを構成します。  
  
5.  参照変換をダブルクリックし、 **参照変換エディター**の **[全般]** ページで **[フル キャッシュ]** を選択します。  
  
6.  **[接続の種類]** 領域で、 **[OLE DB 接続マネージャー]** を選択します。  
  
7.  **[エントリが一致しない行の処理方法を指定する]** ボックスの一覧で、一致するエントリがない行のエラー処理オプションを選択します。  
  
8.  [接続] ページで、 **[OLE DB 接続マネージャー]** ボックスの一覧から接続マネージャーを選択するか、 **[新規作成]** をクリックして新しい接続マネージャーを作成します。 詳細については、「 [OLE DB 接続マネージャー](ole-db-connection-manager.md)」を参照してください。  
  
9. 次のいずれかの手順を実行します。  
  
    -   **[テーブルまたはビューを使用する]** をクリックし、テーブルまたはビューを選択するか、 **[新規作成]** をクリックしてテーブルまたはビューを作成します。  
  
         \- または -  
  
    -   **[SQL クエリの結果を使用する]** をクリックし、 **[SQL コマンド]** ウィンドウでクエリを作成するか、 **[クエリの作成]** をクリックし、 **[クエリ ビルダー]** に用意されているグラフィック ツールを使用してクエリを作成します。  
  
         \- または -  
  
    -   **[参照]** をクリックして、ファイルから SQL ステートメントをインポートします。  
  
     SQL クエリを検証するには、 **[クエリの解析]** をクリックします。  
  
     データのサンプルを表示するには、 **[プレビュー**] をクリックします。  
  
10. **[列]** ページをクリックし、 **[使用できる入力列]** ボックスの一覧から 1 列以上を **[使用できる参照列]** ボックスの一覧の列にドラッグします。  
  
    > [!NOTE]  
    >  参照変換は、同じ名前で同じデータ型を持つ列を自動的にマップします。  
  
    > [!NOTE]  
    >  列をマップするには、データ型が一致している必要があります。 詳細については、「 [Integration Services Data Types](../data-flow/integration-services-data-types.md)」を参照してください。  
  
11. 次のタスクを実行して、参照列を出力に追加します。  
  
    1.  **[使用できる参照列]** ボックスの一覧で、 列を選択します。  
  
    2.  **[参照操作]** ボックスの一覧で、参照列の値を入力列の値と置き換えるか、新しい列に書き出すかを指定します。  
  
12. エラー出力を構成するには、 **[エラー出力]** ページをクリックし、エラー処理オプションを設定します。 詳細については、「[[参照変換エディター] ([エラー出力] ページ)](../lookup-transformation-editor-error-output-page.md)」をご覧ください。  
  
13. **[OK]** をクリックして参照変換への変更を保存し、パッケージを実行します。  
  
## <a name="see-also"></a>関連項目  
 [キャッシュ接続マネージャーを使用してフル キャッシュ モードの参照変換を実装する](lookup-transformation-full-cache-mode-ole-db-connection-manager.md)   
 [キャッシュなしモードまたは部分キャッシュ モードの参照を実装する](../data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)   
 [Integration Services の変換](../data-flow/transformations/integration-services-transformations.md)  
  
  
