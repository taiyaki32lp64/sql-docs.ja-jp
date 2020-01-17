---
title: パーティション スライス プロパティ (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 08/05/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- partitions [Analysis Services], data slices
- data slices [Analysis Services]
ms.assetid: 507b91e5-7f85-4c22-be97-4d7a676e6667
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d9d7b41de3505c3b6e3ccf3886254958ee71e456
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072938"
---
# <a name="set-the-partition-slice-property-analysis-services"></a>パーティション スライス プロパティの設定 (Analysis Services)
  データ スライスとは、該当するパーティションのデータに対する直接的なクエリを円滑に行うための重要な最適化機能です。 Slice プロパティを明示的に設定すると、MOLAP パーティションと HOLAP パーティションに対して生成される既定のスライスがオーバーライドされるため、クエリのパフォーマンスが向上します。 また、Slice プロパティによって、パーティションの処理時に追加の検証チェックが提供されます。  
  
 パーティションを作成してから処理するまでに、Slice プロパティを使用してデータ スライスを指定できます。 [パーティション] タブで、メジャー グループを展開し、パーティションを右クリックして、 **[プロパティ]** をクリックします。  
  
## <a name="defining-a-slice"></a>スライスの定義  
 Slice プロパティに有効な値には、MDX メンバー、セット、または組があります。 有効なスライス構文の例を次に示します。  
  
|スライス|メンバー、セット、または組|  
|-----------|--------------------------|  
|[Date].[Calendar].[Calendar Year].&[2010]|2010 年のファクトを含むパーティションにこのスライスを指定します (モデルに Calendar Year 階層の Date ディメンションが含まれていていることを前提。2010 はメンバー)。 パーティション ソースの WHERE 句またはテーブルが既に 2010 でフィルター処理されている可能性がありますが、Slice を指定すると、処理中に追加のチェック、クエリの実行中に対象を絞ったスキャンが実行されます。|  
|{ [Sales Territory].[Sales Territory Country].&[Australia], [Sales Territory].[Sales Territory Country].&[Canada] }|販売区域情報を含むファクトが含まれるパーティションにこのスライスを指定します。 スライスには、複数のメンバーで構成される MDX セットを指定できます。|  
|[Measures].[Sales Amount Quota] > '5000'|このスライスは MDX 式を表します。|  
  
 パーティションのデータ スライスは、そのパーティションに含まれるデータを可能な限り類似した形で反映します。 たとえば、パーティションが 2012 年のデータに限定されている場合、そのパーティションのデータ スライスは時間ディメンションの 2012 メンバーを指定する必要があります。 常にパーティションの内容を正確に反映するデータ スライスを指定できるとは限りません。 たとえば、パーティションに含まれるデータが January (1 月) と February (2 月) のデータだけであっても、時間ディメンションのレベルが Year、Quarter、および Month である場合、パーティション ウィザードでは January メンバーと February メンバーを選択できません。 このような場合は、パーティションの内容を反映するメンバーの親を選択します。 この例では、Quarter&#xA0;1 を選択します。  
  
 データ スライスの利点については、「 [SSAS キューブ パーティションにスライスを設定する](https://go.microsoft.com/fwlink/?LinkId=317783)」を参照してください。  
  
> [!NOTE]  
>  動的 MDX 関数 ([Generate (MDX)](/sql/mdx/generate-mdx) または [Except (MDX)](/sql/mdx/except-mdx-function) など) はパーティションの Slice プロパティでサポートされていないことに注意してください。 明示的な組またはメンバー参照を使用して、スライスを定義する必要があります。  
>   
>  使用してなどのではなく、 [:&#40;範囲&#41; &#40;MDX&#41; ](/sql/mdx/range-mdx)範囲を定義する関数を特定の年で各メンバーを列挙する必要があります。  
>   
>  複雑なスライスを定義する必要がある場合は、XMLA Alter スクリプトを使用して、スライスで組を定義することをお勧めします。 続けて、ascmd コマンド ライン ツールまたは SSIS [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md) タスクを使用してスクリプトを実行し、指定したメンバーのセットをパーティション処理の直前に作成します。  
  
## <a name="see-also"></a>関連項目  
 [ローカル パーティションの作成と管理 (Analysis Services)](create-and-manage-a-local-partition-analysis-services.md)  
  
  
