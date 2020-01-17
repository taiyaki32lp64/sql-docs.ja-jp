---
title: ディメンションの属性 (ディメンション ウィザード) を選択します |。Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensionattributes.f1
ms.assetid: f58a3e14-ab27-44d3-8c26-f5c9ee7583b0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 482e4ebbd467f3bc8946d90b9ad77bb892e85504
ms.sourcegitcommit: 9af07bd57b76a34d3447e9e15f8bd3b17709140a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2019
ms.locfileid: "67624349"
---
# <a name="select-dimension-attributes-dimension-wizard"></a>[ディメンション属性の選択] (ディメンション ウィザード)
  **[ディメンション属性の選択]** ページを使用すると、作成するディメンションの属性を選択したり変更したりできます。  
  
> [!NOTE]  
>  列の値を読み取れない場合は、ウィザード ウィンドウを最大化して、値を確認できるように各列の見出しの幅を変更します。  
  
 **ディメンション ウィザードを開く**  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]の **ソリューション エクスプローラー**で、 **プロジェクトの** [ディメンション] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] フォルダーを右クリックし、 **[新しいディメンション]** をクリックします。  
  
## <a name="options"></a>および  
 (チェック ボックスのある列)  
 ディメンションに属性を含めます。  
  
 特定の属性を含めるには、その属性のチェック ボックスをオンにします。  
  
 すべての属性を含めるには、列ヘッダーのチェック ボックスをオンにします。  
  
> [!NOTE]  
>  キー属性のチェック ボックスをオフにすることはできません。  
  
 **属性名**  
 利用可能な属性を一覧表示します。  
  
 属性の名前を変更するには、属性名をクリックして、属性の新しい名前を入力します。  
  
 **参照を有効にします。**  
 エンド ユーザーが参照やフィルター選択にその属性を使用できるようにします。 キー属性では、 **[参照を有効にする]** を選択する必要があります。 非キー属性では、既定で **[参照を有効にする]** は選択されていないので、非キー属性はメンバー プロパティとしてのみ表示されます。  
  
 ほとんどの場合、属性を参照できるようにするには `AttributeHierarchyEnabled` プロパティを `True`、参照できないようにするには `False` に設定します。 ただし、次の 3 つの例では、ウィザードで使用される設定が異なります。  
  
|例|設定|  
|----------|--------------|  
|ディメンションに親子階層が含まれており、 **[参照を有効にする]** が選択されていない場合|ウィザードでは、キー属性の `AttributeHierarchyEnabled` プロパティは `True` に設定されたままになり、`AttributeHierarchyVisible` プロパティを `False` に設定します。|  
|ディメンション内のテーブルに、ディメンションに存在しないテーブルへの外部キーが含まれている場合|ウィザードでは、属性として含める外部キーが選択されますが、 **[参照を有効にする]** は選択されません。 これらの設定をそのまま使用すると、属性の `AttributeHiearchyEnabled` プロパティは `True` に設定され、`AttributeHierarchyVisible` プロパティは `False` に設定されます。|  
|NULL 値が許容された外部キー列を使用してアクセスできるスノーフレーク テーブルがディメンションに含まれている場合<br /><br /> \- と -<br /><br /> スノーフレーク テーブルのキーに基づいた属性の [参照を有効にする] が選択されていない場合|ウィザードでは、`AttributeHiearchyEnabled` プロパティが `True` に設定され、`AttributeHierarchyVisible` プロパティが `False` に設定されている新しい属性が作成されます。|  
  
 **属性の型**  
 属性の型を設定します (省略可)。 既定値は **Regular**です。 属性の型によって、クライアント アプリケーションは、属性にどのような情報が含まれているかを判別できます。  
  
## <a name="see-also"></a>参照  
 [ディメンション ウィザードの F1 ヘルプ](dimension-wizard-f1-help.md)   
 [ディメンション&#40;Analysis Services - 多次元データ&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多次元モデル内のディメンション](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
