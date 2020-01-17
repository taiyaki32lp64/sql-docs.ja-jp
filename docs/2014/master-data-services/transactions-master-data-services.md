---
title: トランザクション (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Master Data Services], about transactions
- transactions [Master Data Services]
ms.assetid: 4cd2fa6f-9c76-4b7a-ae18-d4e5fd2f03f5
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8eebb47569a4ccc96437a3e16379c794b83642dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478506"
---
# <a name="transactions-master-data-services"></a>トランザクション (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、メンバーに対してアクションが行われるたびに、トランザクションが記録されます。 すべてのユーザーがトランザクションを表示でき、管理者はトランザクションを破棄できます。 日付、時刻、アクションを行ったユーザーが、その他の詳細と共にトランザクションによって表示されます。 ユーザーは、トランザクションが行われた理由を示す注釈をトランザクションに追加できます。  
  
## <a name="when-transaction-are-recorded"></a>トランザクションが記録されるタイミング  
 トランザクションは、次のタイミングで記録されます。  
  
-   メンバーが作成、削除、または再アクティブ化されたとき。  
  
-   メンバーが属性値を変更したとき。  
  
-   メンバーが階層内で移動されたとき。  
  
 ビジネス ルールによって属性値が変更された場合、トランザクションは記録されません。  
  
## <a name="view-and-manage-transactions"></a>トランザクションの表示および管理  
 **[エクスプローラー]** 機能領域では、自分で作成したトランザクションを表示したり、自分で作成したトランザクションに注釈を設定 (コメントを追加) したりできます。  
  
 **[バージョン管理]** 機能領域では、管理者は、アクセス権を持っているモデルに対する全ユーザーのトランザクションをすべて表示したり、それらのトランザクションを破棄したりできます。  
  
> [!NOTE]  
>  **[バージョン管理]** 機能領域で読み取り専用アクセス許可レベルが適用されていない限り、管理者は全ユーザーの全トランザクションを表示できます。 たとえば、読み取り専用アクセス許可と更新アクセス許可レベルが管理者に設定されている場合、読み取り専用アクセス許可が更新アクセス許可よりも優先されるため、管理者は他のユーザーのトランザクションを表示できません。

## <a name="system-settings"></a>システム設定  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] には、レコードがステージングされたときにトランザクションが記録されるかどうかに影響する設定があります。 この設定は SQL Server 2008 R2 にのみ影響します。 この設定は、 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] で調整するか、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの System Settings テーブルで直接調整することができます。 詳細については、「[システム設定 &#40;マスター データ サービス&#41;](system-settings-master-data-services.md)」を参照してください。  
  
 このバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]にデータをインポートする場合に、ストアド プロシージャを開始するときにトランザクションをログに記録するかどうかを指定できます。 詳細については、「[ステージング ストアド プロシージャ (マスター データ サービス)](../../2014/master-data-services/staging-stored-procedure-master-data-services.md)」を参照してください。  
  
## <a name="concurrency"></a>コンカレンシー  
 複数のエクスプローラー セッションで特定のエンティティの値が同時に表示される場合、同じ値を同時に編集している可能性があります。 同時編集は、MDS によって自動的に検出されません。 これは、複数のユーザーが複数のセッション (たとえば、複数のコンピューター、複数のブラウザーのタブやウィンドウ、複数のユーザー アカウントなど) から Web ブラウザー内で MDS エクスプローラーを使用している場合に発生します。  
  
 トランザクションが有効になっているにもかかわらず、複数のユーザーがエラーなく、同じエンティティの値を更新できます。 通常、時間順で最後に編集した値が優先されます。 トランザクションの履歴で、重複する編集の競合を手動で観察することができ、管理者によって手動で取り消すことができます。 トランザクションの履歴は、各セッションの問題の属性に対する **[以前の値]** と **[新しい値]** の個々のトランザクションを表示しますが、複数の **[新しい値]** が同一の古い値に対して存在しても、競合を自動的には解決しません。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|トランザクションを破棄してアクションを元に戻す (管理者のみ)。|[トランザクションを破棄する (マスター データ サービス)](../../2014/master-data-services/reverse-a-transaction-master-data-services.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [管理者 (マスター データ サービス)](../../2014/master-data-services/administrators-master-data-services.md)  
  
-   [注釈 (マスター データ サービス)](../../2014/master-data-services/annotations-master-data-services.md)  
  
  
