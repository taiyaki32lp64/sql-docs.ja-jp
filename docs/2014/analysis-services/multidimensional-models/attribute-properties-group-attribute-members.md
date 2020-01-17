---
title: グループの属性メンバー (分離) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- NameColumn property
- discretization [Analysis Services]
- member groups [Analysis Services]
- grouping members
- DiscretizationNumber property
- sort orders [Analysis Services]
- DiscretizationMethod property
- adding members to member group
- number of member groups
- members [Analysis Services], groups
- names [Analysis Services], member groups
ms.assetid: 5cf2f407-accc-4baf-b54f-7703af338325
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3cc874831f9f96c2540d58f2ffe3b89f8c4dc7aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077266"
---
# <a name="group-attribute-members-discretization"></a>属性メンバーのグループ化 (分離)
  メンバー グループは、連続したディメンション メンバーが含まれている、システムによって生成されたコレクションです。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]では、分離と呼ばれるプロセスにより、1 つの属性のメンバーを複数のメンバー グループに分割できます。 階層内のレベルには、メンバー グループまたはメンバーのどちらかが含まれています。 メンバー グループが属するレベルをビジネス ユーザーが参照すると、メンバー グループの名前とセル値が表示されます。 メンバー グループをサポートするために [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって生成されたメンバーはグループ化メンバーと呼ばれ、通常のメンバーと同じように表示されます。  
  
 属性の `DiscretizationMethod` プロパティは、メンバーがどのようにグループ化されるかを定義します。  
  
|`DiscretizationMethod` 設定|説明|  
|--------------------------------------|-----------------|  
|`None`|メンバーを表示します。|  
|`Automatic`|データを最も適切に表現するメソッドとして、`EqualAreas` メソッドまたは `Clusters` メソッドのいずれかを選択します。|  
|`EqualAreas`|属性のメンバーを、等しい数のメンバーを含んでいるグループに分割します。|  
|`Clusters`|トレーニング データをサンプリングし、多数のランダム ポイントに初期化し、Expectation-Maximization (EM) クラスター化アルゴリズムを何度か繰り返し実行して、属性のメンバーをグループに分割します。<br /><br /> このメソッドには、どのような分布曲線に対しても使用できるという利点がありますが、処理時間は長くなります。|  
  
 属性の `DiscretizationNumber` プロパティは、表示するグループの数を指定します。 このプロパティが既定値の 0 に設定されている場合、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、`DiscretizationMethod` プロパティの設定に応じてデータのサンプリングまたは読み取りを行って、グループの数を判断します。  
  
 メンバー グループ内のメンバーの並べ替え順は、属性の `OrderBy` プロパティを使用して制御します。 この並べ替え順に基づいて、メンバー グループ内のメンバーが順番に並べ替えられます。  
  
 メンバー グループの一般的な用途は、少数のメンバーを含んでいるレベルから多数のメンバーを含んでいるレベルにドリル ダウンすることです。 ユーザーがレベル間でドリル ダウンできるようにするには、多数のメンバーを含んでいるレベルの属性の `DiscretizationMethod` プロパティを、`None` から、前の表で説明したいずれかの分離メソッドに変更します。 たとえば、Client ディメンションには、500,000 のメンバーを持つ Client Name 属性階層が含まれています。 この属性名を Client Groups に変更し、`DiscretizationMethod` プロパティを `Automatic` に設定すると、属性階層メンバー レベルのメンバー グループを表示できるようになります。  
  
 各グループの個別のクライアントにドリル ダウンするには、別の Client Name 属性階層を作成し、それを同じテーブル列にバインドします。 次に、2 つの属性に基づく新しいユーザー階層を作成します。 上位レベルは Client Groups 属性に基づき、下位レベルは Client Name 属性に基づきます。 `IsAggregatable` プロパティは、両方の属性で `True` になります。 このため、ユーザーは階層の (All) レベルを展開してグループ メンバーを表示し、グループ メンバーを展開して階層のリーフ メンバーを表示できます。 グループ レベルまたはクライアント レベルを非表示にするには、対応する属性の `AttributeHierarchyVisible` プロパティを `False` に設定します。  
  
## <a name="naming-template"></a>テンプレートの名前付け  
 メンバー グループ名は、メンバー グループを作成したときに自動的に生成されます。 名前付けテンプレートを指定しない限り、既定の名前付けテンプレートが使用されます。 この名前付け方法を変更するには、属性の `Format` プロパティの `NameColumn` オプションの名前付けテンプレートを指定します。 属性の `Translations` プロパティに使用された列バインドの `NameColumn` コレクション内で指定された各言語に対し、異なる名前付けテンプレートを再定義できます。  
  
 `Format` 設定では、次の文字列式を使用して名前付けテンプレートを定義します。  
  
 `<Naming template> ::= <First definition> [;<Intermediate definition>;<Last definition>]`  
  
 `<First definition> ::= <Name expression>`  
  
 `<Intermediate definition> ::= <Name expression>`  
  
 `<Last definition> ::= <Name expression>`  
  
 `<First definition>` パラメーターは、分離メソッドによって生成される最初または唯一のメンバー グループのみに適用されます。 省略可能なパラメーターである `<Intermediate definition>` および `<Last definition>` が指定されていない場合は、その属性に対して生成されたすべてのメジャー グループに `<First definition>` パラメーターが使用されます。  
  
 `<Last definition>` パラメーターは、分離メソッドによって生成される最後のメンバー グループのみに適用されます。  
  
 `<Intermediate bucket name>` パラメーターは、分離メソッドによって生成される最初または最後のメンバー グループ以外のすべてのメンバー グループに適用されます。 生成されたメンバー グループが 2 つ以下の場合、このパラメーターは無視されます。  
  
 `<Bucket name>` パラメーターは、一連の変数を組み込むことのできる文字列式であり、メンバー グループの名前の一部としてメンバーまたはメンバー グループの情報を表します。  
  
|変数|説明|  
|--------------|-----------------|  
|%{First bucket member}|現在のメンバー グループに含まれる最初のメンバーの名前です。|  
|%{Last bucket member}|現在のメンバー グループに含まれる最後のメンバーの名前です。|  
|%{Previous bucket last member}|前のメンバー グループに割り当てられている最後のメンバーの名前です。|  
|%{Next bucket first member}|次のメンバー グループに割り当てられる最初のメンバーの名前です。|  
|%{Bucket Min}|現在のメンバー グループに割り当てられるメンバーの最小値です。|  
|%{Bucket Max}|現在のメンバー グループに割り当てられるメンバーの最大値です。|  
|%{Previous Bucket Max}|前のメンバー グループに割り当てられるメンバーの最大値です。|  
|%{Next Bucket Min}|次のメンバー グループに割り当てられるメンバーの最小値です。|  
  
 既定の名前付けテンプレートは `"%{First bucket member} - %{Last bucket member}"`であり、以前のバージョンの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]と互換性があります。  
  
> [!NOTE]  
>  名前付けテンプレートにリテラル文字としてセミコロン (;) を含めるには、その前にパーセント (%) 文字を付けます。  
  
### <a name="example"></a>例  
 次の文字列式を使用すると、 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] サンプル [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース内の Customer ディメンションの Yearly Income 属性 (メンバーのグループ化を使用する属性) を分類できます。  
  
 "Less than %{Next Bucket Min};Between %{First bucket member} and %{Last bucket member};Greater than %{Previous Bucket Max}"  
  
## <a name="adding-new-members-to-existing-member-groups"></a>既存のメンバー グループへの新しいメンバーの追加  
 新しいメンバーをディメンションに追加すると、そのメンバーの値が現在のメンバー グループ レイアウトと比較され、適切なメンバー グループに割り当てられます。  
  
 メンバーが前のメンバー グループの最後のメンバーと次のメンバー グループの最初のメンバーの間に挿入される場合、新しいメンバーは前のメンバー グループの最後のメンバーになります。  
  
## <a name="updating-a-dimension-with-discretized-attributes"></a>分離された属性があるディメンションの更新  
 ディメンションを処理するときは、完全更新 (ProcessFull) を使用した場合にのみ、分離された属性が再分離されます。 属性を再分離するには、ディメンションの完全更新を実行する必要があります。 分離された属性のディメンション テーブルが更新され、増分更新 (ProcessAdd) を使用してディメンションを処理した場合、分離された属性は再分離されません。 新しいバケットの名前および子は同じままです。 ディメンションの処理に関する詳細については、「 [Analysis Services オブジェクトの処理 (Analysis Services)](processing-analysis-services-objects.md)」を参照してください。  
  
## <a name="usage-limitations"></a>使用法の制限  
  
-   メンバー グループは、階層の最上位または最下位レベルに作成できません。 ただし、作成する必要がある場合は、1 つのレベルを追加して、メンバー グループを作成するレベルが最上位または最下位レベルにならないようにします。 追加したレベルは、`Visible` プロパティに `False` を設定して非表示にできます。  
  
-   メンバー グループは、階層の連続する 2 つのレベルには作成できません。  
  
-   メンバー グループは、ROLAP ストレージ モードを使用するディメンションに対してはサポートされません。  
  
-   メンバー グループが含まれているディメンションのディメンション テーブルが更新されると、そのディメンションが完全に処理されて、メンバー グループの新規セットが生成されます。 新規のメンバー グループと旧メンバー グループの名前と子は異なる場合があります。  
  
## <a name="see-also"></a>参照  
 [属性と属性階層](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)  
  
  
