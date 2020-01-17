---
title: OLE DB コマンド変換の構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- parameters [Integration Services]
- OLE DB Command transformation
ms.assetid: c800f167-3d2e-4c10-8ba3-a02f1872ccea
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8c9536e14f20e62b944df44ff943b05edb92e5fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060561"
---
# <a name="configure-the-ole-db-command-transformation"></a>OLE DB コマンド変換を構成する
  OLE DB コマンド変換を追加して構成するには、パッケージに 1 つ以上のデータ フロー タスクと、フラット ファイル ソースや OLE DB ソースなどの変換元があらかじめ含まれている必要があります。 この変換は、通常、パラメーター化クエリを実行するために使用されます。  
  
### <a name="to-configure-the-ole-db-command-transformation"></a>OLE DB コマンド変換を構成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[データ フロー]** タブをクリックし、次に **[ツールボックス]** で、OLE DB コマンド変換をデザイン画面にドラッグします。  
  
4.  OLE DB コマンド変換をデータ フローに連結します。連結するには、緑または赤の矢印のコネクタを、データ ソースまたは前の変換から OLE DB コマンド変換にドラッグします。  
  
5.  コンポーネントを右クリックし、[編集] または **[詳細エディターの表示]** をクリックします。  
  
6.  **[接続マネージャー]** タブで、 **[接続マネージャー]** 一覧から OLE DB 接続マネージャーを選択します。 詳細については、「 [OLE DB 接続マネージャー](connection-manager/ole-db-connection-manager.md)」を参照してください。  
  
7.  **[コンポーネントのプロパティ]** タブをクリックし、 **[SQL コマンド]** ボックスの参照ボタン ( **[...]** ) をクリックします。  
  
8.  **[文字列値エディター]** で、各パラメーターのパラメーター マーカーとして疑問符 (?) を使用して、パラメーター化 SQL ステートメントを入力します。  
  
9. **[更新]** をクリックします。 **[更新]** をクリックすると、この変換は各パラメーターに対する列を External Columns コレクションに作成し、DBParamInfoFlags プロパティを設定します。  
  
10. **[入力プロパティと出力プロパティ]** タブをクリックします。  
  
11. **[OLE DB コマンドの入力]** を展開し、次に **[外部列]** を展開します。  
  
12. **[外部列]** 一覧に、SQL ステートメント内の各パラメーターに対する列が表示されていることを確認します。 列名は、 **Param_0**、 **Param_1**のように表示されます。  
  
     この列名は変更できません。 列名を変更すると、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] によって OLE DB コマンド変換の検証エラーが生成されます。  
  
     また、このデータ型も変更できません。 各列の DataType プロパティは、正しいデータ型に設定されます。  
  
13. **[外部列]** 一覧に列が表示されていない場合は、手動で列を追加する必要があります。  
  
    -   SQL ステートメントのパラメーターごとに、 **[列の追加]** を 1 回ずつクリックします。  
  
    -   列名を、 **Param_0**、 **Param_1**のように更新します。  
  
    -   DBParamInfoFlags プロパティの値を指定します。 この値は、OLE DB DBPARAMFLAGSENUM 列挙値と一致する必要があります。 詳細については、OLE DB のリファレンス マニュアルを参照してください。  
  
    -   データ型に応じて列のデータ型を指定し、列のコード ページ、長さ、有効桁数、および小数点以下桁数を指定します。  
  
    -   未使用のパラメーターを削除するには、 **[外部列]** でパラメーターを選択し、 **[列の削除]** をクリックします。  
  
    -   **[列マッピング]** をクリックし、 **[使用できる入力列]** 一覧の列を **[使用できる変換先列]** 一覧のパラメーターにマップします。  
  
14. **[OK]** をクリックします。  
  
15. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [OLE DB Command Transformation](data-flow/transformations/ole-db-command-transformation.md)   
 [Integration Services の変換](data-flow/transformations/integration-services-transformations.md)   
 [Integration Services のパス](data-flow/integration-services-paths.md)   
 [[データ フロー タスク]](control-flow/data-flow-task.md)  
  
  
