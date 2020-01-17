---
title: 多次元モデルの計算 |Microsoft Docs
ms.custom: ''
ms.date: 12/10/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- calculations [Analysis Services], creating
- deleting calculations
- calculations [Analysis Services], scripts
- Cube Designer
- modifying scripts
- removing calculations
- calculations [Analysis Services], deleting
- scripts [Analysis Services], calculations
- cubes [Analysis Services], calculations
- solve orders [Analysis Services]
ms.assetid: c21b3459-9bef-45a2-aba5-c992eba5b66e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 838e3a8d2df72d1589fdf76198671fee571e2e62
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75229423"
---
# <a name="calculations-in-multidimensional-models"></a>多次元モデルの計算
  キューブ デザイナーの **[計算]** タブを使用して、計算されるメンバー、名前付きセット、およびその他の多次元式 (MDX) 計算を作成します。  
  
 
  **[計算]** タブには、次の 3 つのペインがあります。  
  
-   
  **[スクリプト オーガナイザー]** ペインには、キューブ内の計算が一覧表示されます。 このペインを使用して、編集する計算を作成、整理、および選択します。  
  
-   
  **[計算ツール]** ペインには、計算を作成するためのメタデータ、関数、およびテンプレートが用意されています。  
  
-   計算式ペインでは、フォーム ビューおよびスクリプト ビューがサポートされています。  
  
> [!NOTE]  
>  MDX スクリプティングの詳細については、「 [Microsoft SQL Server 2005 での Mdx スクリプトの概要](https://go.microsoft.com/fwlink/?LinkId=81892)」を参照してください。また、Microsoft TechNet Web サイトの[SQL Server 2005-Analysis Services](https://go.microsoft.com/fwlink/?LinkId=80853)のページにある「その他のリソース」セクションを参照してください。 キューブ デザインに関連するパフォーマンスの問題の詳細については、「 [SQL Server 2005 Analysis Services パフォーマンス ガイド](https://download.microsoft.com/download/8/5/e/85eea4fa-b3bb-4426-97d0-7f7151b2011c/ssas2005perfguide.doc)」を参照してください。  
  
## <a name="creating-a-new-calculation"></a>新しい計算の作成  
 新しい計算を作成するには、キューブ デザイナーの **[計算]** タブの **[キューブ]** メニューで、作成する計算の種類に応じて、 **[新しい計算されるメンバー]**、 **[新しい名前付きセット]**、または **[新しいスクリプト コマンド]** をクリックします。 また、ツール バーで対応するいずれかのボタンをクリックするか、 **[スクリプト オーガナイザー]** ペイン内を右クリックし、ショートカット メニューのいずれかのコマンドをクリックすることもできます。 この操作により、新しい計算が **[スクリプト オーガナイザー]** ペインに追加され、計算式ペインの計算フォームにそのフィールドが表示されます。 新しいスクリプトを作成すると、この操作により計算式ペインに [スクリプト ビュー] が開きます。 3 種類の計算を作成する方法の詳細については、「 [計算されるメンバーの作成](create-calculated-members.md)」、「 [名前付きセットの作成](create-named-sets.md)」、および「 [割り当てとその他のスクリプト コマンドの定義](define-assignments-and-other-script-commands.md)」を参照してください。  
  
## <a name="editing-scripts"></a>スクリプトの編集  
 [**計算**] タブの計算式ペインでスクリプトを編集します。計算式ペインには、スクリプトビューとフォームビューの2つのビューがあります。 フォーム ビューには、1 つのコマンドの式およびプロパティが表示されます。 MDX スクリプトを編集する場合、式ボックスがフォーム ビュー全体に表示されます。  
  
 スクリプト ビューには、スクリプトを編集するためのコード エディターが用意されています。 計算式ペインがスクリプト ビューにある場合、 **[スクリプト オーガナイザー]** ペインは表示されません。 スクリプト ビューには、色分け表示、かっこの対応、オートコンプリート、MDX コード領域などの機能が用意されています。 MDX コード領域は、編集しやすいように折りたたんだり展開したりできます。  
  
 
  **[キューブ]** メニューをクリックし、 **[計算を表示]** をポイントして、 **[スクリプト]** または **[フォーム]** をクリックして、フォーム ビューとスクリプト ビューを切り替えることができます。 また、ツール バーの **[フォーム ビュー]** または **[スクリプト ビュー]** をクリックすることもできます。  
  
## <a name="changing-solve-order"></a>解決順序の変更  
 計算は、 **[スクリプト オーガナイザー]** ペインに一覧表示されている順序で解決されます。 計算を右クリックし、ショートカット メニューの **[上へ移動]** または **[下へ移動]** をクリックして、計算の順序を変更できます。 また、計算をクリックし、ツール バーの **[上へ移動]** ボタンまたは **[下へ移動]** ボタンをクリックすることもできます。  
  
 計算されるセルおよび計算されるメンバーについて、この順序を手動でオーバーライドできます。 パス順序と解決順序の詳細については、「[パス順序と解決順序の概要 (MDX)](mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md)」を参照してください。  
  
## <a name="deleting-a-calculation"></a>計算の削除  
 既存の計算を削除するには、 **[スクリプト オーガナイザー]** ペインの **[計算]** タブで、削除する計算を選択し、 **[編集]** メニューの **[削除]** をクリックするか、ツール バーの **[削除]** アイコンをクリックします。 また、 **[スクリプト オーガナイザー]** ペインで計算を右クリックし、ショートカット メニューから **[削除]** を選択することもできます。  
  
  
