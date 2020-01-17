---
title: ディメンション オブジェクト (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], objects
ms.assetid: 7f3d55c7-cccb-4ad0-b6cb-3a2c9992dd68
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c0c64f95b0c366453e1099c80d8e40b217fb7801
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62702456"
---
# <a name="dimension-objects-analysis-services---multidimensional-data"></a>Dimension オブジェクト (Analysis Services - 多次元データ)
  簡単な <xref:Microsoft.AnalysisServices.Dimension> オブジェクトは、基本情報、属性、および階層で構成されます。 基本情報には、ディメンションの名前、ディメンションの種類、データ ソース、ストレージ モードなどが含まれます。 属性は、ディメンション内の実際のデータを定義します。 属性は必ずしも階層に属するわけではありませんが、階層は属性から構築されます。 階層は、順序付けされたレベルの一覧を作成し、ユーザーに可能なディメンションの探索方法を定義します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 次のトピックでは、ディメンション オブジェクトの設計方法と実装方法の詳細について説明します。  
  
|トピック|説明|  
|-----------|-----------------|  
|[ディメンション &#40;Analysis Services - 多次元データ&#41;](dimensions-analysis-services-multidimensional-data.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ディメンションはキューブの基本的なコンポーネントです。 ディメンションは、顧客、店舗、従業員など、ユーザーが関心のある分野に関するデータを編成します。|  
|[属性と属性階層](attributes-and-attribute-hierarchies.md)|ディメンションとは属性のコレクションで、これらの属性はデータ ソース ビュー内のテーブルまたはビューの 1 つ以上の列にバインドされています。|  
|[属性リレーションシップ](attribute-relationships.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ディメンション内の属性は常に関連する直接的または間接的にキー属性にします。 同一のリレーショナル テーブルからすべてのディメンション属性が派生するスター スキーマに基づいてディメンションを定義すると、ディメンションのキー属性と各非キー属性の間に自動的に属性リレーションシップが定義されます。 関連を持った複数のテーブルからディメンション属性が派生するスノーフレーク スキーマを基にディメンションを定義すると、属性リレーションシップが自動的に次のように定義されます。<br /><br /> -キー属性との間と各非キー属性は、メイン ディメンション テーブル内の列にバインドします。<br />キー属性と属性をセカンダリ テーブルの外部キーにバインドされている間は、基になるディメンション テーブルをリンクします。<br />-属性の間でセカンダリ テーブルと各非キー属性での外部にバインドされているキーは、セカンダリ テーブルの列にバインドします。|  
  
  
