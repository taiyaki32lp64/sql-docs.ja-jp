---
title: 非推奨のマスター データ サービス機能
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d8506bda-66dd-45a4-bfc9-3a10fa665acc
author: lrtoyou1223
ms.author: lle
manager: erikre
ms.openlocfilehash: e6e2247cd3648e78df0349ec8de2b63f29e52e94
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729347"
---
# <a name="deprecated-master-data-services-features"></a>非推奨のマスター データ サービス機能

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  このトピックでは、[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] でまだ使用できるものの、非推奨とされた [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]の機能について説明します。 これらの機能は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の今後のリリースで削除される予定です。 非推奨の機能を新しいアプリケーションで使用しないでください。  
  
## <a name="explicit-hierarchies-collections-and-related-components"></a>明示的階層、コレクション、および関連コンポーネント  
 明示的階層、コレクション、および関連コンポーネントは非推奨とされます。 以前統合メンバーの種類 (明示的階層の親) およびコレクション メンバーの種類としてモデル化されていたメンバーは、派生階層のリーフ メンバーとしてモデル化されます。 次の新機能により、派生階層を、明示的階層の代わりに使用できます。  
  
-   再帰型派生階層を使用して、メンバーのセキュリティ アクセス許可を割り当てることができます。  
  
     明示的階層は、再帰レベルの下位に単一の非再帰レベルがある再帰型派生階層に似ています。 再帰型派生階層は、再帰レベルの上下にレベルを追加して複雑にすることができます。  
  
-   エクスプローラーの派生階層ページに、割り当てられていない (未使用) メンバーが階層レベルごとに表示されます。 また、未使用ノードが、階層レベルごとにグループ化されています。 未使用ノードとルート ノードの間のメンバーの移動は、ドラッグ アンド ドロップまたは切り取りと貼り付けで行うことができます。  
  
     [システム管理] の **[プレビュー]** ウィンドウには、未使用ノードが表示されます。 未使用ノードは、[セキュリティ] の **[階層メンバーの権限]** ウィンドウにも表示されます。 **ルート** ノード、 **未使用** ノードにかかわらず、すべてのメンバーにアクセス許可を割り当てることができます。 **ルート**、 **未使用**、および **未使用** 疑似メンバーにも、アクセス許可を割り当てることができます。  
  
-   ストアド プロシージャである mdm.udpConvertCollectionAndConsolidatedMembersToLeaf は、明示的階層を再帰型派生階層に、統合メンバーとコレクション メンバーをリーフ メンバーに変換します。  
  
     明示的階層、統合、およびコレクションの各メンバーの種類は引き続きサポートされるため、このストアド プロシージャの実行は任意です。 ただし、これらの項目は非推奨であるため、これを使用する場合は、ストアド プロシージャを実行することをお勧めします。  
  
 明示的階層、コレクション、および統合メンバーについては、次のトピックを参照してください。  
  
-   [明示的階層 (マスター データ サービス)](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [コレクション (マスター データ サービス)](../master-data-services/collections-master-data-services.md)  
  
-   [メンバー (マスター データ サービス)](../master-data-services/members-master-data-services.md)  
  
## <a name="attribute-entity-transaction-log-type"></a>属性のエンティティのトランザクション ログの種類  
エンティティのトランザクション ログの種類 "属性" 非推奨とされました。"メンバー" というエンティティのトランザクション ログの種類に移行してください。 エンティティのトランザクション ログの種類については、次のトピックを参照してください。
* [エンティティのトランザクション ログの種類の変更 (マスター データ サービス)](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)
* [メンバー リビジョン履歴](../master-data-services/member-revision-history-master-data-services.md)
  
## <a name="external-resources"></a>外部リソース  
 msdn.com のブログ投稿「 [Deprecated: Explicit Hierarchies and Collections (非推奨: 明示的階層とコレクション)](https://go.microsoft.com/fwlink/p/?LinkId=615373)」  
  
## <a name="see-also"></a>参照  
 [提供が中止されたマスター データ サービス機能](../master-data-services/discontinued-master-data-services-features.md)  
  
  
