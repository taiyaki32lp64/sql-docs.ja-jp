---
title: 統合メンバー ステージング テーブル
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- database [Master Data Services], attributes staging table
- attributes staging table [Master Data Services]
ms.assetid: 070681ed-be99-49ae-93bd-6402f2134ace
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: b7b700f4bcdd453f6a2ec6f437fe29370423d5ac
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729616"
---
# <a name="consolidated-member-staging-table-master-data-services"></a>統合メンバー ステージング テーブル (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの統合メンバー ステージング テーブル (stg.name_Consolidated) を使用して、統合メンバーを作成、更新、非アクティブ化、および削除します。 このテーブルを使用して、統合メンバーの属性値を更新することも可能です。  
  
##  <a name="TableColumns"></a> テーブルの列  
 次の表は、統合ステージング テーブルの各フィールドの用途を説明しています。  
  
|列名|[説明]|  
|-----------------|-----------------|  
|**ID**|自動的に割り当てられる ID。 このフィールドには値を入力しないでください。 バッチが未処理の場合、このフィールドは空白です。|  
|**ImportType**<br /><br /> 必須|ステージング データが [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースに既に存在するデータと一致する場合の処理を決定します。<br /><br /> **0**: 新しいメンバーを作成します。 既存の MDS データをステージング データに置き換えます。ただし、ステージング データが NULL の場合は除きます。 NULL 値は無視されます。 属性値を NULL に変更するには、 **~NULL~** を使用します。<br /><br /> **1**: 新しいメンバーのみを作成します。 既存の MDS データに対する更新はすべて失敗します。<br /><br /> **2**: 新しいメンバーを作成します。 既存の MDS データをステージング データに置き換えます。 NULL 値をインポートする場合、既存の MDS 値が上書きされます。<br /><br /> **3**: コード値に基づいて、メンバーを非アクティブにします。 すべての属性、階層とコレクションのメンバーシップ、およびトランザクションは維持されますが、UI では利用できなくなります。 メンバーが別のメンバーのドメイン ベースの属性値として使用されている場合、非アクティブ化は失敗します。<br /><br /> **4**: コード値に基づいて、メンバーを完全に削除します。 すべての属性、階層とコレクションのメンバーシップ、およびトランザクションが、完全に削除されます。 メンバーが別のメンバーのドメイン ベースの属性値として使用されている場合、削除は失敗します。|  
|**ImportStatus_ID**<br /><br /> 必須|インポート処理の状態。 指定できる値は次のとおりです。<br /><br /> **0**: レコードがステージング準備済みであることを示すために指定します。<br /><br /> **1**: 自動的に割り当てられ、レコードのステージング処理が正常に完了したことを示します。<br /><br /> **2**: 自動的に割り当てられ、レコードのステージング処理に失敗したことを示します。|  
|**Batch_ID**<br /><br /> Web サービスでのみ必須|ステージング用のレコードをグループ化する、自動的に割り当てられる識別子。 バッチ内のメンバーすべてにこの識別子が割り当てられます。これは、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ユーザー インターフェイスの **[ID]** 列に表示されます。<br /><br /> バッチが未処理の場合、このフィールドは空白です。|  
|**BatchTag**<br /><br /> Web サービス以外は必須|バッチの一意名 (最大 50 文字)。|  
|**HierarchyName**<br /><br /> 必須|明示的階層の名前。 各統合メンバーは、1 つの階層にのみ所属することができます。|  
|**ErrorCode**|エラー コードを表示します。 **ImportStatus_ID** が **2** のすべてのレコードについては、「[ステージング処理のエラー (マスター データ サービス)](../master-data-services/staging-process-errors-master-data-services.md)」を参照してください。|  
|**コード**<br /><br /> 必須。**ImportType1** や **2** でコードが自動的に生成される場合は除きます。詳しくは、「[コードの自動作成 (マスター データ サービス)](../master-data-services/automatic-code-creation-master-data-services.md)」を参照してください。|メンバーの一意コード。|  
|**名前**<br /><br /> 省略可|メンバーの名前。|  
|**NewCode**|メンバー コードを変更する場合にのみ使用します。|  
|\<属性名>|エンティティ内の属性ごとに列が存在します。 **ImportType** が **0** または **2**の場合に、これを使用します。 自由形式属性の場合、属性の新しいテキストまたは文字列値を指定します。 ドメイン ベース属性の場合は、属性となるメンバーのコードを指定します。 リンク属性の場合、URL は **https://** で始まる必要があります。<br /><br /> <br /><br /> 注: ファイル属性をステージングすることはできません。|  
  
## <a name="see-also"></a>参照  
 [概要: テーブルからデータをインポートする (マスター データ サービス)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [ステージング中に発生したエラーの表示 (マスター データ サービス)](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [ステージング処理のエラー (マスター データ サービス)](../master-data-services/staging-process-errors-master-data-services.md)  
  
  
