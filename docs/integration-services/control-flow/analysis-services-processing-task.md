---
title: Analysis Services 処理タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.asprocessingtask.f1
- sql13.dts.designer.asprocessingtask.general.f1
- sql13.dts.designer.asprocessingtask.as.f1
helpviewer_keywords:
- Analysis Services Processing task
- processing objects [Integration Services]
ms.assetid: e5748836-b4ce-4e17-ab6b-617a336f02f4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 92e0656fd3625f2b93a1e097d2f81291056d01cf
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298468"
---
# <a name="analysis-services-processing-task"></a>Analysis Services 処理タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 処理タスクは、テーブル モデル、キューブ、ディメンション、マイニング モデルなどの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトを処理します。  
  
 テーブル モデルを処理する場合は、次の点に注意してください。  
  
-   テーブル モデルでは影響分析を実行できません。  
  
-   テーブル モード用のいくつかの処理オプションが表示されません ([デフラグの処理] や [再計算の処理] など)。 これらの機能は DDL 実行タスクを使用すると実行できます。  
  
-   [インデックスの処理] オプションと [更新の処理] オプションはテーブル モデルには適していないので、使用しないでください。  
  
-   テーブル モデルでは、バッチ設定が無視されます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、データ定義言語 (DDL) ステートメントやデータ マイニング予測クエリの実行など、ビジネス インテリジェンス操作を実行する多数のタスクが含まれます。 関連するビジネス インテリジェンス タスクの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Analysis Services DDL 実行タスク](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [データ マイニング クエリ タスク](../../integration-services/control-flow/data-mining-query-task.md)  
  
## <a name="object-processing"></a>オブジェクト処理  
 複数のオブジェクトを同時に処理できます。 複数のオブジェクトを処理する場合は、バッチ内のすべてのオブジェクトの処理に適用する設定を定義します。  
  
 バッチ内のオブジェクトは順に処理することも、並列処理することもできます。 順に処理することが重要なオブジェクトがバッチに含まれていない場合、並列処理を行うと処理速度が向上します。 バッチ内のオブジェクトを並列処理する場合、タスクを構成して並列処理するオブジェクト数を決定することも、同時に処理するオブジェクト数を手動で指定することもできます。 オブジェクトを順に処理する場合、1 つのトランザクションにすべてのオブジェクトを含めるか、バッチ内のオブジェクトごとに異なるトランザクションを使用して、バッチのトランザクションの属性を設定できます。  
  
 分析オブジェクトを処理する場合、その分析オブジェクトに依存するオブジェクトも処理できます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 処理タスクには、選択したオブジェクトの他に、任意の依存オブジェクトを処理するオプションが含まれています。  
  
 通常は、ファクト テーブルを処理する前にディメンション テーブルを処理します。 ディメンション テーブルを処理する前にファクト テーブルを処理しようとすると、エラーが発生する場合があります。  
  
 さらに、このタスクでは、ディメンション キーによるエラー処理を構成することもできます。 たとえば、エラーを無視したり、指定したエラー数が発生した後に停止するようにタスクを構成できます。 この場合、タスクで既定のエラー構成を使用することも、カスタム エラー構成を構築することもできます。 カスタム エラー構成では、タスクによるエラー処理方法とエラー条件を指定します。 たとえば、4 番目のエラーが発生したときにタスクが実行を停止するように指定できます。また、 **NULL** キー値をタスクが処理する方法を指定することもできます。 カスタム エラー構成には、エラー ログのパスを含めることもできます。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 処理タスクで処理できるのは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ツールを使用して作成された分析オブジェクトのみです。  
  
 このタスクは、データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに読み込む一括挿入タスク、またはデータをテーブルに読み込むデータ フローを実装するデータ フロー タスクと組み合わせて使用するのが一般的です。 たとえば、オンライン トランザクション処理 (OLTP) データベースからデータを抽出して、データ ウェアハウス内のファクト テーブルに読み込むデータ フローがデータ フロー タスク内にあり、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 処理タスクがこのタスクの処理後に呼び出され、データ ウェアハウスに構築されたキューブを処理する例などがあります。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 処理タスクは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーを使用して [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに接続します。 詳しくは、「 [Analysis Services 接続マネージャー](../../integration-services/connection-manager/analysis-services-connection-manager.md)」をご覧ください。  
  
## <a name="error-handling"></a>エラー処理  
  
## <a name="configuration-of-the-analysis-services-processing-task"></a>Analysis Services 処理タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[式] ページ](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックをクリックしてください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-analysis-services-processing-task"></a>プログラムによる Analysis Services 処理タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックを参照してください。  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.DTSProcessingTask>  
  
## <a name="analysis-services-processing-task-editor-general-page"></a>[Analysis Services 処理タスク エディター] ([全般] ページ)
  **[Analysis Services 処理タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、Analysis Services 処理タスクの名前と説明を指定できます。  
  
### <a name="options"></a>オプション  
 **[名前]**  
 Analysis Services 処理タスクに一意の名前を指定します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 Analysis Services 処理タスクの説明を入力します。  
  
## <a name="analysis-services-processing-task-editor-analysis-services-page"></a>[Analysis Services 処理タスク エディター] ([Analysis Services] ページ)
  **[Analysis Services 処理タスク エディター]** ダイアログ ボックスの **[Analysis Services]** ページを使用すると、Analysis Services 接続マネージャーの指定、処理する分析オブジェクトの選択、処理およびエラー処理オプションの設定を行うことができます。  
  
 テーブル モデルを処理する場合は、次の点に注意してください。  
  
1.  テーブル モデルでは影響分析を実行できません。  
  
2.  テーブル モード用のいくつかの処理オプションが表示されません ([デフラグの処理] や [再計算の処理] など)。 これらの機能は DDL 実行タスクを使用すると実行できます。  
  
3.  提供されているいくつかの処理オプション ([インデックスの処理] など) はテーブル モデルには適していないので、使用しないでください。  
  
4.  テーブル モデルでは、バッチ設定が無視されます。  
  
### <a name="options"></a>オプション  
 **Analysis Services 接続マネージャー**  
 既存の Analysis Services 接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続マネージャーを作成します。  
  
 **[新規作成]**  
 新しい Analysis Services 接続マネージャーを作成します。  
  
 **関連トピック:** [Analysis Services 接続マネージャー](../../integration-services/connection-manager/analysis-services-connection-manager.md)、[[Analysis Services 接続マネージャーの追加] ダイアログ ボックスの UI リファレンス](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **[オブジェクト一覧]**  
 |プロパティ|[説明]|  
|--------------|-----------------|  
|**Object Name**|指定されたオブジェクト名を表示します。|  
|**Type**|指定されたオブジェクトの種類を表示します。|  
|**[処理オプション]**|一覧から処理オプションを選択します。<br /><br /> **関連トピック:** [多次元モデルの処理 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services)|  
|**[設定]**|指定されたオブジェクトの処理設定を表示します。|  
  
 **[追加]**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトを一覧に追加します。  
  
 **[削除]**  
 オブジェクトを選択し、 **[削除]** をクリックします。  
  
 **[影響分析]**  
 選択したオブジェクトに対して影響分析を実行します。  
  
 **関連トピック:** [[影響分析] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](https://msdn.microsoft.com/library/208268eb-4e14-44db-9c64-6f74b776adb6)  
  
 **[バッチ設定の概要]**  
 |プロパティ|[説明]|  
|--------------|-----------------|  
|**[処理順序]**|オブジェクトを順番に処理するか、一括して処理するかを指定します。並行処理を行う場合は、同時に処理するオブジェクトの数を指定します。|  
|**[トランザクション モード]**|順次処理のトランザクション モードを指定します。|  
|**[ディメンション エラー]**|エラーが発生したときのタスクの動作を指定します。|  
|**[ディメンション キーのエラー ログのパス]**|エラーを記録するファイルのパスを指定します。|  
|**[影響を受けたオブジェクトの処理]**|依存オブジェクトまたは影響を受けたオブジェクトも処理するかどうかを示します。|  
  
 **[設定の変更]**  
 処理オプションおよびディメンション キー内のエラー処理を変更します。  
  
 **関連トピック:** [[設定の変更] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](https://msdn.microsoft.com/library/0041e042-d7ce-48f9-a690-a6dc65471ff3)  
  
