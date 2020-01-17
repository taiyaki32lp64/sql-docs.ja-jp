---
title: 制御フローに列挙を追加する |Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- adding enumerations
- Foreach Loop containers
- control flow [Integration Services], enumerations
- repeating workflows
- enumerations [Integration Services]
ms.assetid: f212b5fb-3cc4-422e-9b7c-89eb769a812a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cad9c6a3537fb523a13f0206eed6c8eee837ed06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061909"
---
# <a name="add-enumeration-to-a-control-flow"></a>制御フローに列挙を追加する
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、Foreach ループ コンテナーが含まれています。Foreach ループ コンテナーとは制御フローの要素で、これを使用すると、パッケージの制御フロー内のファイルおよびオブジェクトを列挙するループ構造を簡単に含めることができます。 詳細については、「 [Foreach ループ コンテナー](control-flow/foreach-loop-container.md)」を参照してください。  
  
 Foreach ループ コンテナーに機能は用意されていません。繰り返し可能な制御フローの構築、列挙子の型の指定、および列挙子の構成を行う構造を提供するだけです。 コンテナーに機能を設定するには、Foreach ループ コンテナーに少なくとも 1 つのタスクを含める必要があります。 詳細については、「 [Integration Services のタスク](control-flow/integration-services-tasks.md)」を参照してください。  
  
 Foreach ループ コンテナーには、複数のタスクを持つ制御フローおよび他のコンテナーを含めることができます。 Foreach ループ コンテナーにタスクとコンテナーを追加する手順は、タスクとコンテナーをドラッグする先がパッケージではなく Foreach ループ コンテナーであること以外は、パッケージに追加する手順と同様です。 Foreach ループ コンテナーに複数のタスクまたはコンテナーが含まれる場合、パッケージで行う場合と同様に、優先順位制約を使用してそれらを連結できます。 優先順位制約の詳細については、「 [優先順位制約](control-flow/precedence-constraints.md)」を参照してください。  
  
### <a name="to-implement-a-foreach-loop-container-in-a-control-flow"></a>Foreach ループ コンテナーを制御フローに実装するには  
  
1.  Foreach ループ コンテナーをパッケージに追加します。 詳細については、次を参照してください[タスクまたはコンテナーの制御フローに追加または削除。](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
2.  タスクとコンテナーを Foreach ループ コンテナーに追加します。 詳細については、次を参照してください[タスクまたはコンテナーの制御フローに追加または削除。](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
3.  優先順位制約を使用して、Foreach ループ コンテナー内のタスクとコンテナーを連結します。 詳細については、「 [既定の優先順位制約を使用してタスクとコンテナーを連結する](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)」を参照してください。  
  
4.  Foreach ループ コンテナーを構成します。 詳細については、「 [Foreach ループ コンテナーを構成する](../../2014/integration-services/configure-a-foreach-loop-container.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [制御フローのタスクまたはコンテナーを追加または削除する](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [グループまたはグループ化解除のコンポーネント](group-or-ungroup-components.md)   
 [優先順位制約](control-flow/precedence-constraints.md)   
 [繰り返し制御フローを追加します。](add-iteration-to-a-control-flow.md)   
 [制御フロー](control-flow/control-flow.md)  
  
  
