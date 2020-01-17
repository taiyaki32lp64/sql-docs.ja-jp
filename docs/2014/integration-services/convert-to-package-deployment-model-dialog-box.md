---
title: パッケージ配置モデル ダイアログ ボックスへの変換 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.bids.converttolegacydeployment.f1
ms.assetid: 9e60a34a-10f7-48d1-966f-b3ff236ab4b7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dfe1f6e5b752284b6bb0feec96f4f3dfd67cc4f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060347"
---
# <a name="convert-to-package-deployment-model-dialog-box"></a>[パッケージ配置モデルに変換] ダイアログ ボックス
  **[パッケージ配置モデルに変換]** コマンドを使用すると、パッケージをパッケージ配置モデルに変換できます。この変換は、プロジェクトおよびプロジェクト内の各パッケージとそのモデルとの互換性を確認した後に行います。 パラメーターなど、プロジェクト配置モデルに固有の機能をパッケージで使用する場合は、パッケージを変換できません。  
  
## <a name="task-list"></a>タスク一覧  
 パッケージをパッケージ配置モデルに変換するには、2 つの手順を実行する必要があります。  
  
1.  **[プロジェクト]** メニューの **[パッケージ配置モデルに変換]** をクリックすると、プロジェクトおよび各パッケージとこのモデルとの互換性が確認されます。 結果は **[結果]** テーブルに表示されます。  
  
     互換性テストに失敗したプロジェクトまたはパッケージがある場合は、 **[結果]** 列の **[失敗]** をクリックして詳細を確認します。 この情報のコピーをテキスト ファイルに保存するには、 **[レポートの保存]** をクリックします。  
  
2.  プロジェクトとすべてのパッケージの互換性テストが成功した場合は、 **[OK]** をクリックしてパッケージを変換します。  
  
> [!NOTE]  
>  プロジェクトをプロジェクト配置モデルに変換するには、**Integration Services プロジェクト変換ウィザード**を使用します。 詳細については、「 [Integration Services プロジェクトの変換ウィザード](../../2014/integration-services/integration-services-project-conversion-wizard.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [プロジェクトとパッケージの展開](packages/deploy-integration-services-ssis-projects-and-packages.md)   
 [パッケージの配置&#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)   
 [Integration Services プロジェクト変換ウィザード](../../2014/integration-services/integration-services-project-conversion-wizard.md)  
  
  
