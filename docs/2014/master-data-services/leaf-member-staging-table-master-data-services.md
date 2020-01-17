---
title: リーフ メンバー ステージング テーブル (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members staging table [Master Data Services]
- database [Master Data Services], members staging table
ms.assetid: a8c953da-ec20-47dc-8656-ed5f0dfed89b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 272fdcee66a8e702ac1dfe6c2da3d408c93a5e49
ms.sourcegitcommit: 0818f6cc435519699866db07c49133488af323f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284973"
---
# <a name="leaf-member-staging-table-master-data-services"></a>リーフ メンバー ステージング テーブル (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースのリーフ メンバー ステージング テーブル (stg.name_Leaf) を使用して、リーフ メンバーを作成、更新、非アクティブ化、および削除します。 また、このテーブルを使用して、リーフ メンバーの属性値を更新できます。  
  
##  <a name="TableColumns"></a> テーブルの列  
 次の表は、リーフ ステージング テーブルの各フィールドの用途を説明しています。  
  
|列名|説明|  
|-----------------|-----------------|  
|**ID**|自動的に割り当てられる ID。 このフィールドには値を入力しないでください。 バッチが未処理の場合、このフィールドは空白です。|  
|**ImportType**<br /><br /> 必須|次**ID**ステージング データに既に存在するデータに一致する場合の対処方法を決定する値、[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]データベース。<br /><br /> **0**:新しいメンバーを作成します。 既存の MDS データをステージング データに置き換えます。ただし、ステージング データが NULL の場合は除きます。 NULL 値は無視されます。 文字列の属性値を NULL に変更するには、 **~NULL~** を設定します。 数値の属性値を NULL に変更するには、 **-98765432101234567890**に設定します。 DateTime 型の属性値を NULL に変更するには、 **5555-11-22T12:34:56**に設定します。<br /><br /> **1**:新しいメンバーのみを作成します。 既存の MDS データに対する更新はすべて失敗します。<br /><br /> **2**:新しいメンバーを作成します。 既存の MDS データをステージング データに置き換えます。 NULL 値をインポートする場合、既存の MDS 値が上書きされます。<br /><br /> **3**:コード値に基づいて、メンバーを非アクティブにします。 すべての属性、階層とコレクションのメンバーシップ、およびトランザクションは維持されますが、UI では利用できなくなります。 メンバーが別のメンバーのドメイン ベースの属性値として使用されている場合、非アクティブ化は失敗します。 代わりの方法については **ImportType5** を参照してください。<br /><br /> **4**:コード値に基づいて、メンバーを完全に削除します。 すべての属性、階層とコレクションのメンバーシップ、およびトランザクションが、完全に削除されます。 メンバーが別のメンバーのドメイン ベースの属性値として使用されている場合、削除は失敗します。 代わりの方法については **ImportType6** を参照してください。<br /><br /> **5**:**コード**値に基づいて、メンバーを非アクティブにします。 すべての属性、階層とコレクションのメンバーシップ、およびトランザクションは維持されますが、UI では利用できなくなります。 メンバーが他のメンバーのドメイン ベースの属性値として使用されている場合、関連する値は NULL に設定されます。 ImportType 5 はリーフ メンバー専用です。<br /><br /> **6**:**コード**値に基づいて、メンバーを完全に削除します。 すべての属性、階層とコレクションのメンバーシップ、およびトランザクションが、完全に削除されます。 メンバーが他のメンバーのドメイン ベースの属性値として使用されている場合、関連する値は NULL に設定されます。 ImportType 6 はリーフ メンバー専用です。|  
|**ImportStatus_ID**<br /><br /> 必須|インポート処理の状態。 有効な値は次のとおりです。<br /><br /> **0**: レコードがステージング準備済みであることを示すために指定します。<br /><br /> **1**: 自動的に割り当てられ、レコードのステージング処理が正常に完了したことを示します。<br /><br /> **2**: 自動的に割り当てられ、レコードのステージング処理に失敗したことを示します。|  
|**Batch_ID**<br /><br /> Web サービスでのみ必須|ステージング用のレコードをグループ化する、自動的に割り当てられる識別子。 バッチ内のメンバーすべてにこの識別子が割り当てられます。これは、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ユーザー インターフェイスの **[ID]** 列に表示されます。<br /><br /> バッチが未処理の場合、このフィールドは空白です。|  
|**BatchTag**<br /><br /> Web サービス以外は必須|バッチの一意名 (最大 50 文字)。|  
|**ErrorCode**|エラー コードを表示します。 **ImportStatus_ID** が **2** のすべてのレコードについては、「[ステージング処理のエラー (マスター データ サービス)](staging-process-errors-master-data-services.md)」を参照してください。|  
|**コード**<br /><br /> 必須。**ImportType1** や **2** でコードが自動的に生成される場合は除きます。詳しくは、「[コードの自動作成 (マスター データ サービス)](../../2014/master-data-services/automatic-code-creation-master-data-services.md)」を参照してください。|メンバーの一意コード。|  
|**名前**<br /><br /> 省略可|メンバーの名前。|  
|**NewCode**|メンバー コードを変更する場合にのみ使用します。|  
|\<属性名>|エンティティ内の属性ごとに列が存在します。 **ImportType** が **0** または **2**の場合に、これを使用します。 自由形式属性の場合、属性の新しいテキストまたは文字列値を指定します。 ドメイン ベース属性の場合は、属性となるメンバーのコードを指定します。 リンク属性の場合、URL は **http://** で始まる必要があります。<br /><br /> 注:ファイル属性をステージングすることはできません。|  
  
##  <a name="feedback"></a> この記事ではする方法でしょうか。 待ちしています  
 どのような情報をお探しでしたか? お探しの情報は見つかりましたか? コンテンツを向上させるためにお客様のフィードバックを受け付けています。 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Leaf%20Member%20Staging%20Table%20page) にコメントをお送りください  
  
## <a name="see-also"></a>参照  
 [読み込むか、ステージング処理を使用してマスター データ サービス内のメンバーを更新します。](add-update-and-delete-data-master-data-services.md)   
 [データのインポート&#40;マスター データ サービス&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [ステージング処理中に発生するエラーを表示する&#40;マスター データ サービス&#41;](view-errors-that-occur-during-staging-master-data-services.md)   
 [ステージング処理のエラー (マスター データ サービス)](staging-process-errors-master-data-services.md)  
  
  
