---
title: DirectQuery デザイン モード (SSAS テーブル) を有効にする |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 71fc7ebd-2e86-4a76-994b-66d3a57bcc9b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 965a3a7c1bfa9549793690e92760ce39f147e0d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067196"
---
# <a name="enable-directquery-design-mode-ssas-tabular"></a>DirectQuery デザイン モードの有効化 (SSAS テーブル)
  DirectQuery モードでモデルを作成するには、最初にデザイン時環境を変更して、DirectQuery モードのユーザーがサポートされるようにする必要があります。 この場合、デザイナーで以下の操作も行われます。  
  
-   DirectQuery の配置プロパティの使用を有効にします。  
  
-   デザインにキャッシュを使用するハイブリッド モードで稼働するようにワークスペース データベースを変更します。 実際にモデルを配置すると、モードはプロジェクトの配置プロパティで指定された値に戻されます。  
  
-   DirectQuery モードと互換性のないデザイン機能を無効にします。  
  
-   既存のモデルを検証します。  
  
 この手順では、デザイナーで DirectQuery モードを有効にする方法について説明します。  
  
### <a name="to-enable-use-of-directquery-in-a-model"></a>モデルで DirectQuery の使用を有効にするには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、ソリューション ファイルを開きます。  
  
2.  オブジェクト エクスプローラーで、Model.bim ファイルをダブルクリックします。  
  
3.  **[プロパティ]** ペインで、 **DirectQueryMode**プロパティを **On**に変更します。  
  
4.  Visual Studio で、エラーがある場合は、開く、**エラー一覧**とモデルが DirectQuery モードに切り替わる妨げている問題を解決します。  
  
## <a name="see-also"></a>参照  
 [DirectQuery モード &#40;SSAS テーブル&#41;](directquery-mode-ssas-tabular.md)  
  
  
