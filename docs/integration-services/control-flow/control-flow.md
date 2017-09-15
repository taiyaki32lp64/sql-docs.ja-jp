---
title: "制御フロー |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- control flow [Integration Services], elements
- SSIS control flow elements
- SQL Server Integration Services control flow elements
ms.assetid: 0cc042a9-1a7f-49ed-9f47-091653d5ef6e
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: de01c45d538cd7117b81ea55613aa66be643a2c2
ms.contentlocale: ja-jp
ms.lasthandoff: 08/03/2017

---
# <a name="control-flow"></a>制御フロー
  パッケージは、制御フローと、オプションで含まれる 1 つ以上のデータ フローから構成されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 3 つのさまざまな種類の制御フロー要素を提供します。 パッケージ、タスクの機能を提供すると、順序付けされた制御フローを実行可能ファイル、コンテナー、およびタスクを連結する優先順位制約で構造体を提供するコンテナーです。  
  
 詳細については、「 [優先順位制約](../../integration-services/control-flow/precedence-constraints.md)」、「 [Integration Services コンテナー](../../integration-services/control-flow/integration-services-containers.md)」、および「 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)」を参照してください。  
  
 次の図は、1 つのコンテナーと 6 つのタスクで構成される制御フローを示しています。 タスクのうち 5 つはパッケージ レベルで定義され、残りの 1 つのタスクはコンテナー レベルで定義されています。 タスクは、コンテナーの内部にあります。  
  
 ![6 つのタスクとコンテナーのフロー制御](../../integration-services/control-flow/media/ssis-controlflowelmt.gif "6 つのタスクとコンテナーのフロー制御")  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のアーキテクチャでは入れ子のコンテナーがサポートされており、制御フローには複数のレベルで入れ子になったコンテナーを含めることができます。 たとえば、パッケージには Foreach ループ コンテナーなどのコンテナーを含めることができ、Foreach ループ コンテナーには、さらに別の Foreach ループ コンテナーなどを含めることができます。  
  
 また、イベント ハンドラーにも、同じ種類の制御フローの要素を使用して作成される制御フローが含まれます。  
  
## <a name="control-flow-implementation"></a>制御フローの実装  
 パッケージの制御フローを作成するには、 **デザイナーの** [制御フロー] [!INCLUDE[ssIS](../../includes/ssis-md.md)] タブを使用します。 **[制御フロー]** タブがアクティブになっている場合、ツールボックスには、制御フローに追加できるタスクとコンテナーが表示されます。  
  
 次の図は、制御フロー デザイナーに表示された、簡単なパッケージの制御フローを示しています。 この図で表示されている制御フローは、パッケージレベルの 3 つのタスク、および 3 つのタスクが含まれるパッケージレベルの 1 つのコンテナーで構成されています。 タスクとコンテナーは、優先順位制約を使用して連結されます。  
  
 ![パッケージの制御フロー デザイナーのスクリーン ショット](../../integration-services/connection-manager/media/samplecontrolflow.gif "パッケージの制御フロー デザイナーのスクリーン ショット")  
  
 制御フローを作成するには、次の作業を行います。  
  
-   パッケージ内で繰り返すワークフローを実装するコンテナー、または制御フローをサブセットに分割するコンテナーを追加します。  
  
-   データ フローのサポート、データの準備、ワークフローとビジネス インテリジェンス機能の実行、およびスクリプトの実装を行うタスクを追加します。  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、パッケージのビジネス要件を満たす制御フローを作成するための、さまざまなタスクが含まれています。 パッケージでデータを処理する必要がある場合、制御フローには少なくとも 1 つのデータ フロー タスクを含める必要があります。 たとえば、データの抽出、データ値の集計、およびデータ ソースへの結果の書き込みをパッケージで行う必要がある場合などです。  詳細については、「 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md) 」と「 [制御フローのタスクまたはコンテナーを追加または削除する](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)」を参照してください。  
  
-   優先順位制約を使用してコンテナーとタスクを連結し、順序付けされた制御フローを作成します。  
  
     **[制御フロー]** タブのデザイン画面にタスクまたはコンテナーを追加すると、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーは、アイテムにコネクタを自動的に追加します。 パッケージに 2 つ以上のアイテム、つまりタスクまたはコンテナーが含まれている場合、コネクタを 1 つのアイテムから別のアイテムにドラッグすると、それらを制御フローに結合できます。  
  
     2 つのアイテム間のコネクタは、優先順位制約を表します。 優先順位制約では、連結された 2 つのアイテムの関連性を定義します。 ここでは、実行時にタスクとコンテナーが実行される順序、およびタスクとコンテナーが実行される条件を指定します。 たとえば、優先順位制約は、あるタスクが成功した場合にのみ、制御フロー内の次のタスクが実行されるように指定できます。 優先順位制約の詳細については、「 [優先順位制約](../../integration-services/control-flow/precedence-constraints.md)」を参照してください。  
  
-   接続マネージャーを追加します。  
  
     多くのタスクではデータ ソースに接続する必要があるため、タスクに必要な接続マネージャーをパッケージに追加する必要があります。 使用する列挙子の型に応じて、Foreach ループ コンテナーにも接続マネージャーが必要となる場合があります。 接続マネージャーは、制御フローをアイテム別に作成するときに追加できます。または、制御フローの作成を開始する前に追加することもできます。 詳細については、「[Integration Services (SSIS) の接続](../../integration-services/connection-manager/integration-services-ssis-connections.md)」および「[接続マネージャーを作成する](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)」を参照してください。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)]デザイナーには、デザイン画面を管理し、制御フローを自己文書化に使用できる多くのデザイン時機能も含まれています。  
  
## <a name="related-tasks"></a>関連タスク  
  
-   [タスクまたはコンテナーを制御フローに追加または削除](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
-   [タスクまたはコンテナーのプロパティを設定する](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
-   [グループまたはグループ解除コンポーネント](../../integration-services/group-or-ungroup-components.md)  
  
  