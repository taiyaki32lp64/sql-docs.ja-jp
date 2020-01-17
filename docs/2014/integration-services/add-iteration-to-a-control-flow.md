---
title: 繰り返し制御フローを追加する |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- repeating workflows
- adding iterations
- control flow [Integration Services], iterations
- expressions [Integration Services], control flow
- iterations [Integration Services]
- For Loop containers
ms.assetid: eb3a7494-88ae-4165-9d0f-58715eb1734a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b96f5f900e8c1a3adf136c7bdaf1b89f297e4921
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061979"
---
# <a name="add-iteration-to-a-control-flow"></a>制御フローに繰り返しを追加する
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には For ループ コンテナーが含まれています。For ループ コンテナーとは制御フローの要素で、これを使用すると、条件に応じてパッケージ内の制御フローを繰り返すループを、簡単に含めることができます。 詳細については、「 [For ループ コンテナー](control-flow/for-loop-container.md)に評価されるまでそのワークフローを繰り返します。  
  
 For ループ コンテナーは、ループの各繰り返しにおいて条件を評価し、条件が FALSE に評価されると停止します。 For ループ コンテナーに含まれる式によって、ループの初期化、繰り返される制御フローの実行を停止する評価条件の指定、評価条件の比較対象となる値を更新する式への値の代入を行います。 評価条件は必ず指定する必要がありますが、初期化式および代入式の指定は任意です。  
  
 For ループ コンテナーに機能は用意されていません。繰り返し可能な制御フローを構築する構造を提供するだけです。 コンテナーに機能を設定するには、For ループ コンテナーに少なくとも 1 つのタスクを含める必要があります。 詳細については、「[Integration Services のタスク](control-flow/integration-services-tasks.md)」を参照してください。  
  
 For ループ コンテナーには、複数のタスクを持つ制御フローを含めたり、他のコンテナーを含めることができます。 For ループ コンテナーにタスクとコンテナーを追加する手順は、タスクとコンテナーをドラッグする先がパッケージではなく For ループ コンテナーであること以外は、パッケージに追加する手順と同様です。 For ループ コンテナーに複数のタスクまたはコンテナーが含まれる場合、パッケージの場合と同様に、優先順位制約を使用してそれらを連結できます。 優先順位制約の詳細については、「 [優先順位制約](control-flow/precedence-constraints.md)」を参照してください。  
  
## <a name="using-expressions-in-for-loop-configuration"></a>For ループ構成での式の使用  
 評価条件、初期化の値、または代入値を指定することによって For ループ コンテナーを構成する場合、リテラルまたは式のどちらかを使用できます。  
  
 式には変数を含めることができます。 変数を使用する利点は実行時に更新できるので、パッケージの管理がより柔軟かつ容易になることです。 式の最大長は 4,000 文字です。  
  
 式の内部で変数を指定する場合、変数名をアット マーク (@) で始める必要があります。 たとえば、という名前の変数`Counter`、入力@CounterFor ループ コンテナーを使用する式。 変数の名前空間のプロパティを含める場合は、変数と名前空間を角かっこで囲む必要があります。 たとえば、`Counter`変数、`MyNamespace`名前空間、型 [@MyNamespace::Counter]。  
  
 For ループ コンテナーが使用する変数は、For ループ コンテナーのスコープ、またはパッケージ コンテナー階層において上位層にある任意のコンテナーのスコープ内で定義する必要があります。 たとえば、For ループ コンテナーは、それ自体のスコープ内で定義された変数と、パッケージ スコープ内で定義された変数を使用できます。 詳しくは、「[Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)」と「[パッケージで変数を使用する](../../2014/integration-services/use-variables-in-packages.md)」をご覧ください。  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] の式文法には、評価、初期化、または代入に使用する複雑な式を実装するための、演算子と関数の完全なセットが用意されています。 詳細については、「 [Integration Services (SSIS) 式](expressions/integration-services-ssis-expressions.md)に評価されるまでそのワークフローを繰り返します。  
  
### <a name="to-implement-a-for-loop-container-in-a-control-flow"></a>For ループ コンテナーを制御フローに実装するには  
  
1.  For ループ コンテナーをパッケージに追加します。 詳細については、次を参照してください[タスクまたはコンテナーの制御フローに追加または削除。](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
2.  タスクとコンテナーを For ループ コンテナーに追加します。 詳細については、次を参照してください[タスクまたはコンテナーの制御フローに追加または削除。](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
3.  優先順位制約を使用して、For ループ コンテナー内のタスクとコンテナーを連結します。 詳細については、「[既定の優先順位制約を使用してタスクとコンテナーを連結する](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)」を参照してください。  
  
4.  For ループ コンテナーを構成します。 詳細については、「[For ループ コンテナーを構成する](../../2014/integration-services/configure-a-for-loop-container.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [制御フローのタスクまたはコンテナーを追加または削除する](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [グループまたはグループ化解除のコンポーネント](group-or-ungroup-components.md)   
 [既定の優先順位制約を使用してタスクとコンテナーを連結する](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [制御フローに列挙を追加します。](../../2014/integration-services/add-enumeration-to-a-control-flow.md)   
 [制御フロー](control-flow/control-flow.md)  
  
  
