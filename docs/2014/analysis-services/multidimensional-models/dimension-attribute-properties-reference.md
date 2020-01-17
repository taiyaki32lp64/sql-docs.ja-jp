---
title: ディメンションの属性のプロパティの参照 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- properties [Analysis Services], attributes
- attributes [Analysis Services], properties
ms.assetid: 7f83d1cb-4732-424f-adc5-2449c1dd1008
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: db132a4a4cf6e8c2b73067220a5ed91a5316afef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075192"
---
# <a name="dimension-attribute-properties-reference"></a>ディメンションの属性のプロパティの参照
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]には、ディメンションやディメンション属性の機能を決定する多くのプロパティがあります。 次の表に、このような属性のプロパティの一覧とその説明を示します。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|`AttributeHierarchyDisplayFolder`|フォルダーを指定します。このフォルダー内で、関連付けられた属性階層をエンド ユーザーに対して表示します。|  
|`AttributeHierarchyEnabled`|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] で属性に対して属性階層を生成するかどうかを指定します。 属性階層が有効ではない場合、その属性をユーザー定義の階層で使用することも、属性階層を多次元式 (MDX) ステートメントで参照することもできません。|  
|`AttributeHierarchyOptimizedState`|属性階層に適用される最適化のレベルを指定します。 既定では、属性階層が完全に最適化されます (`FullyOptimized`)。つまり、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] により、クエリ パフォーマンスを向上させるために、属性階層にインデックスが構築されます。 他方のオプション `NotOptimized` を指定すると、属性階層にインデックスが構築されません。 属性階層をクエリ以外の目的で使用する場合は、`NotOptimized` を使用することをお勧めします。その場合、属性に対して追加のインデックスは構築されません。 属性階層の用途としては、他にも、別の属性の順序付けを行うことなどが考えられます。|  
|`AttributeHierarchyOrdered`|関連付けられた属性階層に順序付けを行うかどうかを指定します。 既定値は `True` です。 ただし、属性階層をクエリに使用しない場合は、このプロパティの値を `False` に変更する方が処理時間を節約できます。|  
|`AttributeHierarchyVisible`|属性階層をクライアント アプリケーションに対して公開するかどうかを指定します。 既定値は `True` です。 ただし、属性階層をクエリに使用しない場合は、このプロパティの値を `False` に変更する方が処理時間を節約できます。|  
|`CustomRollupColumn`|カスタム ロールアップ式を定義する列を指定します。|  
|`CustomRollupPropertiesColumn`|カスタム ロールアップ式のプロパティを含む列を指定します。|  
|`DefaultMember`|属性の既定のメジャーを定義する多次元式 (MDX) 式を指定します。|  
|`Description`|属性の説明を示します。|  
|`DiscretizationBucketCount`|分離対象のバケット数を示します。|  
|`DiscretizationMethod`|分離方法を定義します。|  
|`EstimatedCount`|属性内の推定メンバー数を指定します。 集計のデザイン ウィザードを実行するまで、既定値はゼロになります。 このウィザードでは、レコード数をカウントすることも、推定値を入力することもできます。 メンバー数がわかっており、そのカウントについてデータベースをクエリする時間を節約する必要がある場合は、手動で値を入力します。 実稼働データのテスト用サブセットを使用して作業している場合、実稼働データのカウントを使用することにより、テスト データではなく実稼働データに対して集計デザインを最適化できます。|  
|`GroupingBehavior`|クライアント アプリケーションに、属性のグループ化方法についてのヒントを提供するユーザー定義の値です。|  
|`ID`|ディメンションの一意識別子 (ID) を示します。|  
|`InstanceSelection`|一覧の推定項目数に基づいて、項目の一覧を表示する方法のヒントをクライアント アプリケーションに提供します。 次のオプションを使用できます。<br /><br /> **None** : クライアント アプリケーションにヒントは提供されません。 これが既定値です。<br /><br /> **DropDown** : 項目数が多すぎず、ドロップダウン リストに収まる場合に使用します。<br /><br /> **List** : 項目の数が多すぎてドロップダウン **リスト**に表示できないが、フィルター選択を必要としない場合に使用します。<br /><br /> **FilteredList** : 項目数が多いために、表示する項目をユーザーにフィルター選択させる必要がある場合に使用します。<br /><br /> **MandatoryFilter** : 常にフィルター選択する必要があるほど項目数が多い場合に使用します。|  
|`IsAggregatable`|属性メンバーの値を集計できるかどうかを指定します。 既定値は `True` (属性階層に (All) レベルがある) です。 このプロパティの値が `False` の場合、属性階層には (All) レベルがありません。|  
|`KeyColumns`|属性のキーを表す 1 つ以上の列を示します。この列は、属性がバインドされるデータ ソース ビュー内の基になるリレーショナル テーブルにある列です。 この列の各メンバーに対応する値は、`NameColumn` プロパティに値が指定されている場合を除き、ユーザーに対して表示されます。|  
|`MemberNamesUnique`|属性階層内のメンバー名を一意にする必要があるかどうかを指定します。|  
|`MembersWithData`|親属性で使用されます。親属性内の非リーフ メンバーのデータ メンバーを表示するかどうかを指定します。 このプロパティ値は、`Usage` プロパティの値が Parent に設定されている場合にのみ使用されます。 これは、親子階層が定義されていることを意味します。 次のオプションを使用できます。<br /><br /> **NonLeafDataHidden** : 非リーフ データは表示されません。<br /><br /> **NonLeafDataVisible** : 非リーフ データは表示されます。|  
|`MembersWithDataCaption`|親属性内でシステム生成データ メンバーのキャプションを作成する場合に、親属性で使用されるテンプレート文字列を指定します。 このプロパティ値は、`Usage` プロパティの値が Parent に設定されている場合にのみ使用されます。 これは、親子階層が定義されていることを意味します。|  
|`Name`|属性のわかりやすい名前を格納します。|  
|`NameColumn`|属性のキー列の値ではなく、ユーザーに対して表示される属性の名前を示す列を指定します。 この列は、属性メンバーのキー列値がわかりにくいかユーザーにとって有用ではない場合や、キー列が複合キーに基づいている場合に使用されます。 この `NameColumn` プロパティが親子階層内で使用されるのではなく、子メンバーの `NameColumn` プロパティが親子階層内でメンバー名として使用されます。|  
|`NamingTemplate`|親属性で構成された親子階層内のレベルに名前を付ける方法を定義します。 このプロパティ値は、`Usage` プロパティの値が Parent に設定されている場合にのみ使用されます。 これは、親子階層が定義されていることを意味します。|  
|`OrderBy`|属性階層内のメンバーに順序を付ける方法を説明します。 既定値は Name であり、`NameColumn` プロパティの値が存在する場合はその値に基づいて属性のメンバーに順序を付け、 それ以外の場合はキー列の値で順序を付けることを指定します。 次のオプションを使用できます。<br /><br /> `NameColumn` 値の並べ替え順、`NameColumn`プロパティ。<br /><br /> **Key** : 属性メンバーのキー列の値に基づいて順序が付けられます。<br /><br /> **AttributeKey** : 指定された属性のメンバー キーの値に基づいて順序が付けられます。この場合、この属性に対する属性リレーションシップが必要です。<br /><br /> **AttributeName** : 指定された属性のメンバー名の値に基づいて順序が付けられます。この場合、この属性に対する属性リレーションシップが必要です。|  
|`OrderByAttribute`|属性階層のメンバーに順序を付ける際に使用する属性を指定します。|  
|`RootMemberIf`|親子階層のルート メンバー (最上位メンバー) を識別する方法を指定します。 このプロパティ値は、`Usage` プロパティの値が Parent に設定されている場合にのみ使用されます。 これは、親子階層が定義されていることを意味します。 既定値は `ParentIsBlankSelfOrMissing` です。これは、`ParentIsBlank`、`ParentIsSelf`、または `ParentIsMissing` に記述されている条件を 1 つ以上満たすメンバーだけがルート メンバーとして扱われることを意味します。 また、次の値も指定できます。<br /><br /> `ParentIsBlank` Null、0、または空の文字列のキー列または列があるメンバーのみがルート メンバーとして扱われます。<br /><br /> `ParentIsSelf` 親として自体が唯一のメンバーは、ルート メンバーとして扱われます。<br /><br /> `ParentIsMissing` 親が見つからないメンバーだけがルート メンバーとして扱われます。|  
|`Type`|属性の型を示します。 詳細については、「 [属性の種類の構成](attribute-properties-configure-attribute-types.md)」を参照してください。|  
|`UnaryOperatorColumn`|単項演算子を含む列を指定します。 単項演算子を含む列の詳細を定義する DataItem 型のバインドです。|  
|`Usage`|属性の使用方法を説明します。<br /><br /> 次のオプションを使用できます。<br /><br /> `Regular` 属性は、標準の属性です。 これが既定値です。<br /><br /> **Key** : この属性はキー属性です。<br /><br /> **Parent** : この属性は親属性です。|  
|`ValueColumn`|属性の値を示す列を指定します。 属性の `NameColumn` 要素が指定されている場合は、`DataItem` 要素の既定値と同じ `ValueColumn` 値が使用されます。 属性の `NameColumn` 要素が指定されていないときに、属性の `KeyColumns` コレクションに、文字列データ型のキー列を表す 1 つの `KeyColumn` 要素が含まれている場合は、`DataItem` 要素の既定値と同じ `ValueColumn` 値が使用されます。|  
  
> [!NOTE]  
>  値を設定する方法については、 `KeyColumn` null 値とその他のデータ整合性の問題を操作するときに、プロパティを参照してください[Analysis Services 2005 でのデータの整合性問題の処理](https://go.microsoft.com/fwlink/?LinkId=81891)します。  
  
> [!NOTE]  
>  クエリで階層のメンバーが明示的に指定されていない場合は、属性の既定のメンバーが式の評価に使用されます。 属性の既定のメンバーは、属性の `DefaultMember` プロパティによって指定されます。 ディメンションからの階層がクエリに含まれている場合は、階層内のレベルに対応する属性からのすべての既定のメンバーは無視されます。 ディメンションの階層がクエリに含まれていない場合は、既定のメンバーがディメンションのすべての属性に対して使用されます。 既定のメンバーの詳細については、「 [既定メンバーの定義](attribute-properties-define-a-default-member.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [属性と属性階層](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)  
  
  
