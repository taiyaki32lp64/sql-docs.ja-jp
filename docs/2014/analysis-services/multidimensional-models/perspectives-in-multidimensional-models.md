---
title: 多次元モデルのパースペクティブ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- default members
- hiding objects from perspective
- renaming perspectives
- attributes [Analysis Services], default members
- removing perspectives
- perspectives [Analysis Services]
- names [Analysis Services], perspectives
- cubes [Analysis Services], perspectives
- deleting perspectives
ms.assetid: 5a3d6577-6833-4c24-820c-b65bb856157b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d9c408f79dcecd0a7850c7361716cc29b07f4cf9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073345"
---
# <a name="perspectives-in-multidimensional-models"></a>多次元モデルのパースペクティブ
  パースペクティブは、特定のアプリケーションまたはユーザーのグループに対して作成されるキューブのサブセットです。 キューブ自体は既定のパースペクティブになります。 パースペクティブは、キューブとしてクライアントに表示されます。 ユーザーがパースペクティブを表示すると、キューブと同じように表示されます。 パースペクティブで書き戻しによりキューブ データに行われる変更は、元のキューブに対して行われます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のビューの詳細については、「 [パースペクティブ](../multidimensional-models-olap-logical-cube-objects/perspectives.md)」を参照してください。  
  
 キューブのパースペクティブを作成または変更するには、キューブ デザイナーの **[パースペクティブ]** タブを使用します。 **[パースペクティブ]** タブの最初の列は **[キューブ オブジェクト]** 列で、この列にはキューブ内のオブジェクトがすべて一覧表示されます。 これは、キューブ自体である、キューブの既定のパースペクティブに対応しています。  
  
## <a name="creating-or-deleting-perspectives"></a>パースペクティブの作成または削除  
 パースペクティブを **[パースペクティブ]** タブに追加するには、 **[キューブ]** メニューの **[新しいパースペクティブ]** をクリックします。 ツール バーの **[新しいパースペクティブ]** ボタンをクリックするか、ペイン内を右クリックしてショートカット メニューの **[新しいパースペクティブ]** をクリックすることもできます。 キューブに追加できるパースペクティブの数に制限はありません。  
  
 パースペクティブを削除するには、削除するパースペクティブの列内の任意のセルをクリックします。 次に、 **[キューブ]** メニューで、 **[パースペクティブの削除]** をクリックします。 ツール バーの **[パースペクティブの削除]** ボタンをクリックするか、削除するパースペクティブ内の任意のセルを右クリックし、ショートカット メニューの **[パースペクティブの削除]** をクリックすることもできます。  
  
## <a name="renaming-perspectives"></a>パースペクティブ名の変更  
 各パースペクティブの最初の行には、パースペクティブの名前が表示されます。 パースペクティブを作成したときの初期の名前は「パースペクティブ」になります (「パースペクティブ」という名前が既に存在する場合は、1 から始まる序数が名前の後に付けられます)。 この名前をクリックすると、名前を編集できます。  
  
## <a name="hiding-objects-from-a-perspective"></a>パースペクティブのオブジェクトの非表示  
 パースペクティブのオブジェクトを非表示にするには、パースペクティブの列にあるオブジェクトに対応する行のチェック ボックスをオフにします。 パースペクティブで非表示にできるキューブ オブジェクトは次のとおりです。  
  
-   メジャー グループ  
  
-   メジャー  
  
-   ディメンション  
  
-   階層  
  
-   名前付きセット  
  
-   KPI  
  
-   アクション  
  
-   計算されるメンバー  
  
 オブジェクトを表示するには、 **[キューブ オブジェクト]** の下にあるオブジェクトの種類のカテゴリ ( **[メジャー グループ]** 、 **[ディメンション]** 、 **[KPI]** 、 **[計算]** 、または **[アクション]** ) を展開します。 ディメンション内の階層または属性を表示するには、まず、ディメンションを展開してから、 **[階層]** または **[属性]** 行を展開します。 メジャー グループ内のメジャーを表示するには、メジャー グループを展開します。  
  
## <a name="see-also"></a>関連項目  
 [多次元モデルのキューブ](cubes-in-multidimensional-models.md)  
  
  
