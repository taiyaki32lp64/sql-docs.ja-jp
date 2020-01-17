---
title: Analysis Services 処理タスク | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asprocessingtask.f1
helpviewer_keywords:
- Analysis Services Processing task
- processing objects [Integration Services]
ms.assetid: e5748836-b4ce-4e17-ab6b-617a336f02f4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 02023482a2f3537872b50ac70f8bfd68d2128e1b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62832967"
---
# <a name="analysis-services-processing-task"></a>Analysis Services 処理タスク
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 処理タスクは、テーブル モデル、キューブ、ディメンション、マイニング モデルなどの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトを処理します。  
  
 テーブル モデルを処理する場合は、次の点に注意してください。  
  
-   テーブル モデルでは影響分析を実行できません。  
  
-   テーブル モード用のいくつかの処理オプションが表示されません ([デフラグの処理] や [再計算の処理] など)。 これらの機能は DDL 実行タスクを使用すると実行できます。  
  
-   [インデックスの処理] オプションと [更新の処理] オプションはテーブル モデルには適していないので、使用しないでください。  
  
-   テーブル モデルでは、バッチ設定が無視されます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、データ定義言語 (DDL) ステートメントやデータ マイニング予測クエリの実行など、ビジネス インテリジェンス操作を実行する多数のタスクが含まれます。 関連するビジネス インテリジェンス タスクの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Analysis Services DDL 実行タスク](analysis-services-execute-ddl-task.md)  
  
-   [Data Mining Query Task](data-mining-query-task.md)  
  
## <a name="object-processing"></a>オブジェクト処理  
 複数のオブジェクトを同時に処理できます。 複数のオブジェクトを処理する場合は、バッチ内のすべてのオブジェクトの処理に適用する設定を定義します。  
  
 バッチ内のオブジェクトは順に処理することも、並列処理することもできます。 順に処理することが重要なオブジェクトがバッチに含まれていない場合、並列処理を行うと処理速度が向上します。 バッチ内のオブジェクトを並列処理する場合、タスクを構成して並列処理するオブジェクト数を決定することも、同時に処理するオブジェクト数を手動で指定することもできます。 オブジェクトを順に処理する場合、1 つのトランザクションにすべてのオブジェクトを含めるか、バッチ内のオブジェクトごとに異なるトランザクションを使用して、バッチのトランザクションの属性を設定できます。  
  
 分析オブジェクトを処理する場合、その分析オブジェクトに依存するオブジェクトも処理できます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 処理タスクには、選択したオブジェクトの他に、任意の依存オブジェクトを処理するオプションが含まれています。  
  
 通常は、ファクト テーブルを処理する前にディメンション テーブルを処理します。 ディメンション テーブルを処理する前にファクト テーブルを処理しようとすると、エラーが発生する場合があります。  
  
 さらに、このタスクでは、ディメンション キーによるエラー処理を構成することもできます。 たとえば、エラーを無視したり、指定したエラー数が発生した後に停止するようにタスクを構成できます。 この場合、タスクで既定のエラー構成を使用することも、カスタム エラー構成を構築することもできます。 カスタム エラー構成では、タスクによるエラー処理方法とエラー条件を指定します。 たとえば、4 番目のエラーが発生したときにタスクが実行を停止するように指定できます。また、 **NULL** キー値をタスクが処理する方法を指定することもできます。 カスタム エラー構成には、エラー ログのパスを含めることもできます。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 処理タスクで処理できるのは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ツールを使用して作成された分析オブジェクトのみです。  
  
 このタスクは、データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに読み込む一括挿入タスク、またはデータをテーブルに読み込むデータ フローを実装するデータ フロー タスクと組み合わせて使用するのが一般的です。 たとえば、オンライン トランザクション処理 (OLTP) データベースからデータを抽出して、データ ウェアハウス内のファクト テーブルに読み込むデータ フローがデータ フロー タスク内にあり、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 処理タスクがこのタスクの処理後に呼び出され、データ ウェアハウスに構築されたキューブを処理する例などがあります。  
  
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 処理タスクは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続マネージャーを使用して [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに接続します。 詳しくは、「 [Analysis Services 接続マネージャー](../connection-manager/analysis-services-connection-manager.md)」をご覧ください。  
  
## <a name="error-handling"></a>エラー処理  
  
## <a name="configuration-of-the-analysis-services-processing-task"></a>Analysis Services 処理タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[Analysis Services 処理タスク エディター] &#40;[全般] ページ&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [[Analysis Services 処理タスク エディター] &#40;[Analysis Services] ページ&#41;](../analysis-services-processing-task-editor-analysis-services-page.md)  
  
-   [[式] ページ](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックをクリックしてください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-analysis-services-processing-task"></a>プログラムによる Analysis Services 処理タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.DTSProcessingTask>  
  
  
