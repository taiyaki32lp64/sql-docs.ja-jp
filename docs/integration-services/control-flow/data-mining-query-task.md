---
title: データ マイニング クエリ タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingquerytask.f1
- sql13.dts.designer.dmquerytask.miningmodel.f1
- sql13.dts.designer.dmquerytask.query.f1
- sql13.dts.designer.dmquerytask.output.f1
helpviewer_keywords:
- prediction queries [Integration Services]
- Data Mining Query task [Integration Services]
ms.assetid: f489348c-2008-4f66-8c2c-c07c3029439a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3cba502e5f89c39df67b74909f3185ad45c659e2
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298354"
---
# <a name="data-mining-query-task"></a>データ マイニング クエリ タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  データ マイニング クエリ タスクは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]に構築されたデータ マイニング モデルに基づいて、予測クエリを実行します。 予測クエリは、マイニング モデルを使用して新しいデータの予測を作成します。 たとえば、予測クエリにより、夏季のヨット販売数を予測したり、ヨットを購入する可能性の高い顧客の一覧を生成できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、データ定義言語 (DDL) ステートメントの実行や分析オブジェクトの処理など、ビジネス インテリジェンス操作を実行するその他のタスクが用意されています。  
  
 その他のビジネス インテリジェンス タスクの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Analysis Services DDL 実行タスク](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Analysis Services 処理タスク](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
## <a name="prediction-queries"></a>予測クエリ  
 予測クエリは、データ マイニング拡張機能 (DMX) ステートメントです。 DMX 言語は、マイニング モデルでの作業をサポートするための SQL 言語の拡張機能です。 DMX 言語の使用方法の詳細については、「[データ マイニング拡張機能 &#40;DMX&#41; リファレンス](../../dmx/data-mining-extensions-dmx-reference.md)」を参照してください。  
  
 このタスクは、同じマイニング構造で構築された複数のマイニング モデルに対してクエリを実行できます。 マイニング モデルは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] が提供するデータ マイニング アルゴリズムのいずれかを使用して構築されます。 データ マイニング クエリ タスクが参照するマイニング構造には、異なるアルゴリズムを使用して構築された複数のマイニング モデルを含めることができます。 詳細については、「[マイニング構造 &#40;Analysis Services - データ マイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-structures-analysis-services-data-mining)」および「[データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)」を参照してください。  
  
 データ マイニング クエリ タスクが実行する予測クエリは、単一行または 1 つのデータセットを結果として返します。 単一行を返すクエリは、単一クエリと呼ばれます。たとえば、夏季のヨット販売数を予想するクエリは、1 つの数値を返します。 単一行を返す予測クエリの詳細については、「 [データ マイニング クエリ ツール](https://docs.microsoft.com/analysis-services/data-mining/data-mining-query-tools)」を参照してください。  
  
 クエリ結果は、テーブルに保存されます。 データ マイニング クエリ タスクで指定された名前のテーブルが既に存在している場合、タスクで同じ名前の末尾に番号を追加して新しいテーブルを作成することも、テーブルの内容を上書きすることもできます。  
  
 結果に入れ子が含まれる場合は、フラット化された後に保存されます。 結果をフラット化すると、入れ子の結果セットはテーブルに変更されます。 たとえば、 **Customer** 列に **Product** 列が入れ子になっている、入れ子の結果をフラット化すると、 **Customer** 列に行が追加され、顧客ごとの製品が含まれるテーブルが作成されます。 たとえば、3 つの異なる製品を購入した顧客は、3 行のテーブルになります。つまり、顧客は各行で繰り返され、行ごとに異なる製品が含まれます。 FLATTENED キーワードを省略すると、テーブルには、**Customer** 列と各顧客につき 1 行のみが含まれます。 詳細については、「[SELECT &#40;DMX&#41;](../../dmx/select-dmx.md)」を参照してください。  
  
## <a name="configuration-of-the-data-mining-query-task"></a>データ マイニング クエリ タスクの構成  
 データ マイニング クエリ タスクには 2 つの接続が必要です。 1 つ目の接続は [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーで、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンス、またはマイニング構造とマイニング モデルを含む [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトのいずれかに接続します。 2 つ目の接続は OLE DB 接続マネージャーで、タスクが書き込むテーブルを含む [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに接続します。 詳細については、「 [Analysis Services 接続マネージャー](../../integration-services/connection-manager/analysis-services-connection-manager.md) 」および「 [OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)」を参照してください。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
> [!NOTE]  
>  [データ マイニング クエリ変換エディター] には、[式] ページがありません。 代わりに **[プロパティ]** ウィンドウを使用して、データ マイニング クエリ タスクのプロパティのプロパティ式を作成、管理するツールにアクセスできます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-data-mining-query-task"></a>プログラムによるデータ マイニング クエリ タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.DMQueryTask.DMQueryTask>  
  
## <a name="data-mining-query-task-editor-mining-model-tab"></a>[データ マイニング クエリ タスク エディター] ([マイニング モデル] タブ)
  **[データ マイニング クエリ タスク]** ダイアログ ボックスの **[マイニング モデル]** タブを使用すると、使用するマイニング構造とマイニング モデルを指定できます。  
  
 パッケージでのデータ マイニングの実装の詳細については、「 [データ マイニング クエリ タスク](../../integration-services/control-flow/data-mining-query-task.md) 」および「 [データ マイニング ソリューション](https://docs.microsoft.com/analysis-services/data-mining/data-mining-solutions)」を参照してください。  
  
### <a name="general-options"></a>[全般] のオプション  
 **[名前]**  
 データ マイニング クエリ タスクに固有の名前を指定します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 データ マイニング クエリ タスクの説明を入力します。  
  
### <a name="mining-model-tab-options"></a>[マイニング モデル] タブのオプション  
 **[接続]**  
 既存の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [Analysis Services 接続マネージャー](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **[新規作成]**  
 新しい [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーを作成します。  
  
 **関連トピック:** [[Analysis Services 接続マネージャーの追加] ダイアログ ボックスの UI リファレンス](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **マイニング構造**  
 一覧からマイニング構造を選択します。  
  
 **[マイニング モデル]**  
 選択したマイニング構造に基づいて構築されるマイニング モデルを選択します。  

## <a name="data-mining-query-task-editor-query-tab"></a>[データ マイニング クエリ タスク エディター] ([クエリ] タブ)
  **[データ マイニング クエリ タスク]** ダイアログ ボックスの **[クエリ]** タブを使用すると、マイニング モデルに基づいて予測クエリを作成できます。 このダイアログ ボックスでは、パラメーターおよび結果セットを変数にバインドすることもできます。  
  
 パッケージでのデータ マイニングの実装の詳細については、「 [データ マイニング クエリ タスク](../../integration-services/control-flow/data-mining-query-task.md) 」および「 [データ マイニング ソリューション](https://docs.microsoft.com/analysis-services/data-mining/data-mining-solutions)」を参照してください。  
  
### <a name="general-options"></a>[全般] のオプション  
 **[名前]**  
 データ マイニング クエリ タスクに固有の名前を指定します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 データ マイニング クエリ タスクの説明を入力します。  
  
### <a name="build-query-tab-options"></a>[クエリの作成] タブのオプション  
 **[データ マイニング クエリ]**  
 データ マイニング クエリを入力します。  
  
 **関連トピック:** [データ マイニング拡張機能 &#40;DMX&#41; リファレンス](../../dmx/data-mining-extensions-dmx-reference.md)  
  
 **[新しいクエリの作成]**  
 グラフィカル ツールを使用してデータ マイニング クエリを作成します。  
  
 **関連トピック:** [データ マイニング クエリ](../../integration-services/control-flow/data-mining-query.md)  
  
### <a name="parameter-mapping-tab-options"></a>[パラメーター マッピング] タブのオプション  
 **[パラメーター名]**  
 オプションで、パラメーター名を更新します。 **[変数名]** 一覧から変数を選択して、パラメーターを変数にマップします。  
  
 **[変数名]**  
 パラメーターにマップする変数を一覧から選択します。  
  
 **[追加]**  
 一覧にパラメーターを追加します。  
  
 **[削除]**  
 パラメーターを選択してから、 **[削除]** をクリックします。  
  
### <a name="result-set-tab-options"></a>[結果セット] タブのオプション  
 **[結果名]**  
 オプションで、結果セット名を更新します。 **[変数名]** 一覧から変数を選択して、結果を変数にマップします。  
  
 **[追加]** をクリックして結果を追加したら、結果の一意な名前を指定します。  
  
 **[変数名]**  
 結果セットにマップする変数を一覧から選択します。  
  
 **結果の種類**  
 1 行だけを返すか、完全な結果セットを返すかを示します。  
  
 **[追加]**  
 一覧に結果セットを追加します。  
  
 **[削除]**  
 結果を選択してから、 **[削除]** をクリックします。  
## <a name="data-mining-query-task-editor-output-tab"></a>[データ マイニング クエリ タスク エディター] ([出力] タブ)
  **[データ マイニング クエリ タスク エディター]** ダイアログ ボックスの **[出力]** タブを使用すると、予測クエリの出力先を指定できます。  
  
 パッケージでのデータ マイニングの実装の詳細については、「 [データ マイニング クエリ タスク](../../integration-services/control-flow/data-mining-query-task.md) 」および「 [データ マイニング ソリューション](https://docs.microsoft.com/analysis-services/data-mining/data-mining-solutions)」を参照してください。  
  
### <a name="general-options"></a>[全般] のオプション  
 **[名前]**  
 データ マイニング クエリ タスクに固有の名前を指定します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 データ マイニング クエリ タスクの説明を入力します。  
  
### <a name="output-tab-options"></a>[出力] タブのオプション  
 **[接続]**  
 接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続マネージャーを作成します。  
  
 **[新規作成]**  
 新しい接続マネージャーを作成します。 使用できる接続マネージャーの種類は、ADO.NET および OLE DB のみです。  
  
 **[出力テーブル]**  
 予測クエリの結果が書き込まれるテーブルを指定します。  
  
 **[出力テーブルを削除して、再作成する]**  
 予測クエリで、出力先のテーブルを削除して再作成することにより、テーブルの内容を上書きするかどうかを指定します。  
  
