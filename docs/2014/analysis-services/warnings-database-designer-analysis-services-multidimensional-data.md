---
title: 警告 (データベース デザイナー) (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.databasedesigner.warnings.f1
ms.assetid: 13f58b4d-f345-4fbc-ae2d-b3c8290a797d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 90eeca203c672c21551b8aff2e24feb164d8fda5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065427"
---
# <a name="warnings-database-designer-analysis-services---multidimensional-data"></a>[警告] (データベース デザイナー) (Analysis Services - 多次元データ)
  **[警告]** タブを使用すると、ルールをグローバルに表示および消去したり、消去された警告の特定のインスタンスを表示して再度有効にしたりできます。 **警告** タブには 2 つのグリッドが表示されます。**デザイン警告ルール**と**された警告**します。  
  
 **[警告] タブを表示するには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] プロジェクトを開きます。  
  
2.  **ソリューション エクスプローラー**で [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] プロジェクトを右クリックし、 **[データベースの編集]** をクリックして、 **[警告]** タブをクリックします。  
  
## <a name="design-warning-rules-grid"></a>[デザイン警告ルール] グリッド  
 **[デザイン警告ルール]** グリッドには、すべてのデザイン警告ルールが表示されます。 このグリッドでは、データベースに有効なルールも制御します。 警告ルールを有効または無効にするには、そのチェック ボックスをオンまたはオフにします。  
  
 **[デザイン警告ルール]** グリッドには、次の列があります。  
  
 **[説明]**  
 ルールの名前が表示されます。 ルールはカテゴリ別にグループ化されています。  
  
 **重要度**  
 ルールに割り当てられている重要度が表示されます。  
  
 **コメント**  
 ユーザーは警告を消去する理由を説明するコメントを入力できます (省略可)。  
  
## <a name="dismissed-warnings-grid"></a>[消去された警告] グリッド  
 **[消去された警告]** グリッドには、発生した警告のうち、 **[エラー一覧]** から消去された特定の警告がすべて表示されます。 警告を再度有効にするには、グリッドで警告を選択し、 **[再有効化]** をクリックします。  
  
 **[消去された警告]** グリッドには、次の列があります。  
  
 **Object**  
 オブジェクトの種類とオブジェクト名を表すアイコンが表示されます。  
  
 **型**  
 オブジェクトの種類が表示されます。  
  
 **[説明]**  
 ルールの名前が表示されます。  
  
 **重要度**  
 ルールに割り当てられている重要度が表示されます。  
  
 **コメント**  
 警告が消去されるときに入力されたコメントが表示されます。 ここでは、コメントを追加または変更できます。  
  
 **再度有効にします。**  
 選択した警告を再度有効にします。  
  
> [!NOTE]  
>  オブジェクトに警告が含まれていても、オブジェクトが無効な状態であったり、プロジェクトから手動で削除されたりすると、一覧にある警告の横にエラー アイコンが表示されます。 警告を消去するには、警告を選択し、 **[再有効化]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [警告ダイアログ ボックスを閉じます&#40;Analysis Services - 多次元データ&#41;](dismiss-warning-dialog-box-analysis-services-multidimensional-data.md)   
 [一般的な&#40;データベース デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](general-database-designer-analysis-services-multidimensional-data.md)  
  
  
