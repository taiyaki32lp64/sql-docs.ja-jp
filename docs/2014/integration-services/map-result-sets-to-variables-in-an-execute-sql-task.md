---
title: マップの結果セット内の変数を SQL 実行タスク |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- result sets [Integration Services]
- mapping result sets to variables [Integration Services]
- variables [Integration Services], mapping result sets to
ms.assetid: f76738b6-dc75-4ff9-a3dd-8b083d8e410e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 995afe55c1cd1b7d925c9267ba5dfa3aed038358
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057757"
---
# <a name="map-result-sets-to-variables-in-an-execute-sql-task"></a>結果セットを SQL 実行タスクの変数にマップする
  このトピックでは、結果セットと SQL 実行タスクの変数との間のマッピングを作成する方法について説明します。 結果セットを変数にマップすることで、結果セットをパッケージ内の他の要素で使用できるようになります。 たとえば、スクリプト タスクのスクリプトでは、変数を読み取ってから、結果セットからの値を使用できます。XML ソースでは、変数に格納された結果セットを利用できます。 親パッケージで結果セットが生成される場合、パッケージ実行タスクから呼び出された子パッケージでその結果セットを使用できるようにするには、結果セットを親パッケージ内の変数にマップしてから、子パッケージ内で親パッケージの変数構成を作成して、親変数の値を格納します。  
  
 結果セットの種類と、結果セットにマップできる変数のデータ型の説明については、「 [SQL 実行タスクにおける結果セット](control-flow/execute-sql-task.md)」を参照してください。  
  
### <a name="to-map-a-result-set-to-a-variable"></a>結果セットを変数にマップするには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  **ソリューション エクスプローラー**で、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックします。  
  
4.  SQL 実行タスクがまだパッケージに含まれていない場合、SQL 実行タスクをパッケージの制御フローに追加します。 詳細については、次を参照してください[タスクまたはコンテナーの制御フローに追加または削除。](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
5.  SQL 実行タスクをダブルクリックします。  
  
6.  **[SQL 実行タスク エディター]** ダイアログ ボックスの **[全般]** ページで、 **[単一行]** 、 **[完全な結果セット]** 、 **[XML]** のいずれかの種類の結果セットを選択します。  
  
     結果セットの種類の説明については、「 [SQL 実行タスクにおける結果セット](result-sets-in-the-execute-sql-task.md)」を参照してください。  
  
7.  **[結果セット]** をクリックします。  
  
8.  結果セット マッピングを追加するには、 **[追加]** をクリックします。  
  
9. **[変数名]** の一覧で、変数を選択するか、新しい変数を作成します。 詳細については、「 [パッケージ内のユーザー定義変数のスコープの追加、削除、変更](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)」を参照してください。  
  
     各種の結果セットにマップできる変数のデータ型の説明については、「 [SQL 実行タスクにおける結果セット](result-sets-in-the-execute-sql-task.md)」を参照してください。  
  
     変数を単一の列にマップする方法と、複数の変数を複数の列にマップする方法については、「 **SQL 実行タスクにおける結果セット** 」の「 [結果セットによる変数の設定](control-flow/execute-sql-task.md)」のセクションを参照してください。  
  
10. **[結果名]** の一覧で、必要に応じて結果セットの名前を変更します。  
  
     一般に、列名を結果セット名として使用することも、列リストでの列の序数位置を結果セットとして使用することもできます。 列名を結果セットの名前として使用できるかどうかは、タスクの構成で指定されているプロバイダーによって異なります。 すべてのプロバイダーで列名が使用できるわけではありません。  
  
11. **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [SQL 実行タスク](control-flow/execute-sql-task.md)   
 [結果セットで、SQL 実行タスク](result-sets-in-the-execute-sql-task.md)   
 [パッケージ実行タスク](control-flow/execute-package-task.md)   
 [[パッケージ構成]](../../2014/integration-services/package-configurations.md)   
 [パッケージ構成を作成する](../../2014/integration-services/create-package-configurations.md)   
 [子パッケージで変数とパラメーターの値を使用します。](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)   
 [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)  
  
  
