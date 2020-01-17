---
title: サブスクリプションの初期化 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.initializesubscriptions.f1
ms.assetid: 7b170e4e-470d-4828-a9ed-7435b0b03514
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: a205577bb53e7b0aa690dbb8cf77e7bb7d01590e
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768491"
---
# <a name="initialize-subscriptions"></a>サブスクリプションの初期化
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  レプリケートされたデータをサブスクライバーで受信するためには、あらかじめサブスクライバーを初期化する必要があります。 初期データセットは必要ありませんが、少なくともサブスクライバーは、レプリケートされたそれぞれのオブジェクトのスキーマと、レプリケーションに必要なメタデータ テーブルおよびプロシージャを持つ必要があります。  
  
## <a name="options"></a>オプション  
 **[サブスクリプションのプロパティ]**  
 初期データセットを必要とするそれぞれのサブスクライバーの **[初期化]** 列のチェック ボックスをオンにします。 チェック ボックスがオフの場合は、レプリケーション メタデータおよびプロシージャのみが初期化されます。 スナップショットを使用せずにサブスクリプションを初期化する方法については、「[Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)」 (スナップショットを使用しないトランザクション サブスクリプションの初期化) を参照してください。  
  
 このウィザードが完了した後にマージ エージェントまたはディストリビューション エージェントによってスナップショット ファイルがサブスクライバーに転送されるようにするには、 **[次の場合に初期化]** 列のドロップダウン リストから **[今すぐ]** を選択します。 エージェントの次回の実行時にファイルが転送されるようにするには、 **[初回同期時]** を選択します。 **[今すぐ]** オプションは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]へのプル サブスクリプションに対して使用できません。 マージ エージェントおよびディストリビューション エージェントは、 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]のインスタンス上で実行されません。したがって、サブスクリプションを別の方法で初期化する必要があります。  
  
> [!NOTE]  
>  ディストリビューション エージェントまたはマージ エージェントの適切なジョブを開始するために、ウィザードによりディストリビューターへの接続が要求される場合があります。  
  
## <a name="see-also"></a>参照  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [サブスクリプションの初期化](../../relational-databases/replication/initialize-a-subscription.md)   
 [パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
