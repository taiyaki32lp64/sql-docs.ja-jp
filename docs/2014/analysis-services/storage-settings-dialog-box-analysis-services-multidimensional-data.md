---
title: ストレージ設定 ダイアログ ボックス (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.f1
- sql12.asvs.cubeeditor.cubebuilder.measuregroupstoragesettings.f1
ms.assetid: 80c41c71-226c-45fe-b9cf-af824b592fe1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ecd796d2fb2bc37c4c2ad6d9fac00ef4258ec038
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068029"
---
# <a name="storage-settings-dialog-box-analysis-services---multidimensional-data"></a>[ストレージ設定] ダイアログ ボックス (Analysis Services - 多次元データ)
  **の** [ストレージ設定] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ダイアログ ボックスを使用すると、ディメンション、キューブ、メジャー グループ、およびパーティションのプロアクティブ キャッシュ、ストレージ、および通知設定を指定できます。 **で** [ストレージ設定] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ダイアログ ボックスを表示するには、次の手順に従います。  
  
-   省略記号ボタンをクリックすると ( **.** ) の`ProactiveCaching`ディメンション、キューブ、メジャー グループ、またはパーティションのプロパティの値、**プロパティ**のウィンドウ[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]します。  
  
-   **キューブ デザイナー** の **[パーティション]** タブでメジャー グループを展開し、 **[ストレージ設定]** をクリックします。  
  
-   **キューブ デザイナー** の **[パーティション]** タブで、メジャー グループを展開し、メジャー グループのグリッド内でパーティションを選択します。次に、 **[ストレージ設定]** をクリックします。  
  
-   **キューブ デザイナー** の **[パーティション]** タブで、メジャー グループを展開し、メジャー グループのグリッド内でパーティションを選択します。次に、 **キューブ デザイナー** の **[パーティション]** タブの **ツール バー** 上にある、 **[ストレージ設定]** をクリックします。  
  
## <a name="options"></a>および  
  
|項目|定義|値|  
|----------|----------------|------------|  
|**標準の設定**|**標準設定のスライダー** を有効にして、ストレージ モードとプロアクティブ キャッシュ機能で、定義済みの設定を使用します。||  
|**標準設定スライダー**|次の定義済み設定のいずれかに設定します。<br /><br /> **リアルタイム ROLAP**<br /><br /> 次のストレージとプロアクティブ キャッシュ設定を使用します。|ROLAP ストレージ モードに設定します。<br /><br /> プロアクティブ キャッシュを有効にします。<br /><br /> 古くなったキャッシュを待機時間 0 秒で削除します。<br /><br /> オブジェクトを直ちにオンラインにします。|  
||**リアルタイム HOLAP**<br /><br /> 次のストレージとプロアクティブ キャッシュ設定を使用します。|HOLAP ストレージ モードに設定します。<br /><br /> プロアクティブ キャッシュを有効にします。<br /><br /> 古くなったキャッシュを待機時間 0 秒で削除します。<br /><br /> データが変更されると、アクティビティがない状態の間隔 0 秒、アクティビティがない状態のオーバーライド間隔なしでキャッシュを更新します。<br /><br /> オブジェクトを直ちにオンラインにします。|  
||**低待機時間 MOLAP**<br /><br /> 次のストレージとプロアクティブ キャッシュ設定を使用します。|MOLAP ストレージ モードに設定します。<br /><br /> プロアクティブ キャッシュを有効にします。<br /><br /> 古くなったキャッシュを待機時間 30 分で削除します。<br /><br /> アクティビティがない状態の間隔 10 秒、アクティビティがない状態のオーバーライド間隔 10 分でキャッシュを更新します。<br /><br /> オブジェクトを直ちにオンラインにします。|  
||**中待機時間 MOLAP**<br /><br /> 次のストレージとプロアクティブ キャッシュ設定を使用します。|MOLAP ストレージ モードに設定します。<br /><br /> プロアクティブ キャッシュを有効にします。<br /><br /> 古くなったキャッシュを待機時間 4 時間で削除します。<br /><br /> アクティビティがない状態の間隔 10 秒、アクティビティがない状態のオーバーライド間隔 10 分でキャッシュを更新します。<br /><br /> オブジェクトを直ちにオンラインにします。|  
||**自動 MOLAP**<br /><br /> 次のストレージとプロアクティブ キャッシュ設定を使用します。|MOLAP ストレージ モードに設定します。<br /><br /> プロアクティブ キャッシュを有効にします。<br /><br /> データが変更されると、アクティビティがない状態の間隔 0 秒、アクティビティがない状態のオーバーライド間隔なしでキャッシュを更新します。|  
||**定期 MOLAP**<br /><br /> 次のストレージとプロアクティブ キャッシュ設定を使用します。|MOLAP ストレージ モードに設定します。<br /><br /> プロアクティブ キャッシュを有効にします。<br /><br /> キャッシュを定期的に更新します。再構築間隔は 1 日です。|  
||**MOLAP**<br /><br /> 次のストレージとプロアクティブ キャッシュ設定を使用します。|MOLAP ストレージ モードに設定します。|  
|**カスタム設定**|ストレージ モード、プロアクティブ キャッシュ、通知の各オプションを明示的に設定します。||  
|**[オプション]**|**[ストレージのオプション]** ダイアログ ボックスを表示し、ストレージ モード、プロアクティブ キャッシュ、通知の各オプションを明示的に設定します。 **[ストレージ設定]** ダイアログ ボックスの詳細については、「[[ストレージ設定] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)」を参照してください。||  
  
## <a name="see-also"></a>参照  
 [Analysis Services のデザイナーおよびダイアログ ボックス&#40;多次元データ&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [プロアクティブ キャッシュ&#40;パーティション&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)   
 [キューブのストレージ&#40;Analysis Services - 多次元データ&#41;](multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)  
  
  
