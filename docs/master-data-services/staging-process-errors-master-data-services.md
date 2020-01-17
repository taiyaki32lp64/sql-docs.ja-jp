---
title: ステージング処理のエラー
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- staging process [Master Data Services], error messages
ms.assetid: 0d9be0dd-638f-4dd4-92b2-253fda655455
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e719a0a96545bdc69134e42facca9bb4ad79069c
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728922"
---
# <a name="staging-process-errors-master-data-services"></a>ステージング処理のエラー (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  ステージング処理が完了すると、ステージング テーブル内のすべての処理済みレコードの [ErrorCode] 列に値が格納されます。 これらの値を次の表に示します。  
  
|Code|エラー|発生時/詳細|テーブルへの適用|  
|----------|-----------|--------------------------|----------------------|  
|210001|ステージング テーブルに同じメンバー コードが複数回出現します。|ステージング バッチに、同じメンバー コードが複数回含まれます。 メンバーは作成も更新もされません。|リーフ<br /><br /> [統合]<br /><br /> [リレーションシップ]|  
|210003|属性値は、存在しないメンバーまたは非アクティブなメンバーを参照しています。|ドメイン ベースの属性をステージングするときは、名前ではなく、コードを使用する必要があります。 **ImportType0**、 **1**、および **2**に適用されます。|リーフ<br /><br /> [統合]|  
|210006|メンバー コードが非アクティブです。|**ImportType** = **1** で、存在しないメンバー コードを指定しました。|リーフ<br /><br /> [統合]<br /><br /> [リレーションシップ]|  
|210032|階層名が指定されていないか、無効です。|明示的階層が見つからなかったか、 **HierarchyName** の値が空白でした。|[統合]<br /><br /> [リレーションシップ]|  
|210035|コード生成のビジネス ルールが存在しないので、 **MemberCode** は必須です。|メンバーを作成または更新するとき、自動コード生成を使用しない場合は、 **MemberCode** が常に必須です。 詳細については、「[コードの自動作成 (マスター データ サービス)](../master-data-services/automatic-code-creation-master-data-services.md)」を参照してください。|リーフ<br /><br /> [統合]|  
|210036|コード生成のビジネス ルールが存在するため、 **MemberCode** を指定する必要はありません。|メンバーを作成または更新するとき、自動コード生成を使用している場合は、 **MemberCode** は必要ありません。 ただし、指定してもかまいません。 詳細については、「[コードの自動作成 (マスター データ サービス)](../master-data-services/automatic-code-creation-master-data-services.md)」を参照してください。|リーフ<br /><br /> [統合]|  
|210041|"ROOT" は有効なメンバー コードではありません。|**MemberCode** の値に、単語 "ROOT" が含まれています。|リーフ<br /><br /> [統合]<br /><br /> [リレーションシップ]|  
|210042|"MDMUNUSED" は有効なメンバー コードではありません。|**MemberCode** の値に、単語 "MDMUNUSED" が含まれています。|リーフ<br /><br /> [統合]<br /><br /> [リレーションシップ]|  
|210052|MemberCode は、ドメイン ベースの属性値として使用されているため、非アクティブ化できません。|**ImportType** = **3** または **4**のとき、メンバーが他のメンバーの属性値として使用されている場合、ステージングは失敗します。 **ImportType5** または **6** のいずれかを使用して、値を NULL に設定するか、ステージング プロセスを実行する前に値を変更してください。|リーフ<br /><br /> [統合]|  
|300002|メンバー コードが無効です。|リレーションシップ: 親または子のどちらかのメンバー コードが存在しません。<br /><br /> リーフまたは統合: **ImportType** = **3** または **4** で、メンバー コードが存在しません。|リーフ<br /><br /> [統合]<br /><br /> [リレーションシップ]|  
|300004|このメンバー コードは既に存在します。|**ImportType** = **1** で、エンティティに既に存在するメンバー コードを使用しました。|リーフ<br /><br /> [統合]|  
|210011|**RelationshipType** が **1**の場合、 **ParentCode** はリーフ メンバーにできません。|**ParentCode** の値が統合メンバー コードであることを確認してください。|[リレーションシップ]|  
|210015|階層およびバッチのステージング テーブルに、メンバー コードが複数回出現します。|明示的階層の場合に、同じバッチ内で同じメンバーの位置を複数回指定しました。|[リレーションシップ]|  
|210016|循環参照が発生するため、リレーションシップを作成できませんでした。|子を親として割り当てようとした場合に、このエラーが発生します。|[リレーションシップ]|  
|210046|Root の兄弟をメンバーにすることはできません。|**RelationshipType** = **2** (兄弟) で、 **ParentCode** または **ChildCode** のどちらかが **Root**の場合に、このエラーが発生します。 メンバーは、ルート ノードと同じレベルに存在することはできません (子しかメンバーになれません)。|[リレーションシップ]|  
|210047|Unused の兄弟をメンバーにすることはできません。|**RelationshipType** = **2** (兄弟) で、 **ParentCode** または **ChildCode** のどちらかが **Unused**の場合に、このエラーが発生します。 未使用ノードの子しかメンバーになれません。|[リレーションシップ]|  
|210048|**ParentCode** と **ChildCode** を同じにすることはできません。|**ParentCode** の値は **ChildCode** の値と同じです。 これらの値は別にする必要があります。|[リレーションシップ]|  
  
## <a name="see-also"></a>参照  
 [ステージング中に発生したエラーの表示 (マスター データ サービス)](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [概要: テーブルからデータをインポートする (マスター データ サービス)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)  
  
  
