---
title: 複数の優先順位制約 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- multiple precedence constraints
- precedence executables [Integration Services]
- precedence constraints [Integration Services], multiple
- constrained executables [Integration Services]
ms.assetid: 71c53ead-3d19-4bc1-aafd-e5b32595b420
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c0b75b96f30d2fe7f104e8f59aa03d7de6202e6a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057410"
---
# <a name="multiple-precedence-constraints"></a>複数の優先順位制約
  優先順位制約は、2 つのタスク、2 つのコンテナー、1 つのタスクと 1 つのコンテナーなど、2 つの実行可能ファイルを連結します。 これらは優先順位付き実行可能ファイル、および制約付き実行可能ファイルと呼ばれています。 制約付き実行可能ファイルには、複数の優先順位制約を含めることができます。 優先順位制約の詳細については、「[優先順位制約](control-flow/precedence-constraints.md)」を参照してください。  
  
 制約をグループ化して複雑な制約シナリオを組み立てると、複雑な制御フローをパッケージに実装できます。 たとえば、次の図で、タスク D は、`Success` 制約によってタスク A にリンクされ、`Failure` 制約によってタスク B にリンクされ、さらに `Success` 制約によってタスク C にリンクされています。 タスク D とタスク A の間、タスク D とタスク B の間、およびタスク D とタスク C の間の優先順位制約は、論理 *AND* リレーションシップになります。 したがって、タスク D を実行するには、タスク A の実行が成功し、タスク B が失敗し、タスク C の実行が成功する必要があります。  
  
 ![優先順位制約によってリンクされているタスク](media/precedenceconstraints.gif "優先順位制約によってリンクされているタスク")  
  
## <a name="logicaland-property"></a>LogicalAnd プロパティ  
 タスクまたはコンテナーに複数の制約がある場合、`LogicalAnd` プロパティにより、優先順位制約を単独で評価するか、別の制約と組み合わせて評価するかを指定します。  
  
 設定することができます、`LogicalAnd`プロパティを使用して、**優先順位制約エディター**で[!INCLUDE[ssIS](../includes/ssis-md.md)]デザイナー、または [プロパティ] ウィンドウを[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]を提供します。  
  
## <a name="related-tasks"></a>Related Tasks  
 [優先順位制約のプロパティを設定する](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
  
