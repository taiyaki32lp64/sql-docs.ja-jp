---
title: レプリケーションのパブリッシング モデルの概要 | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], publishing model
- subscriptions [SQL Server replication], about subscriptions
- articles [SQL Server replication]
- publications [SQL Server replication]
- Publishers [SQL Server replication], about Publishers
- Subscribers [SQL Server replication]
- Distributors [SQL Server replication], about Distributors
- Subscribers [SQL Server replication], about Subscribers
- articles [SQL Server replication], about articles
- publications [SQL Server replication], about publications
- Distributors [SQL Server replication]
ms.assetid: b9567832-e6a8-45b2-a3ed-ea12aa002f4b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 95d2a3538cb775efb346d59e7db75c238e35c5d6
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769802"
---
# <a name="replication-publishing-model-overview"></a>レプリケーションのパブリッシング モデルの概要
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  レプリケーションでは、パブリッシャー (出版社)、ディストリビューター (流通業者)、サブスクライバー (購読者)、パブリケーション (出版物)、アーティクル (記事)、サブスクリプション (定期購読物) など、レプリケーション トポロジ内のコンポーネントを出版業界にたとえて表しています。 雑誌を例にとって考えると、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のレプリケーションを理解しやすくなります。  
  
-   雑誌のパブリッシャー (出版社) は、1 つ以上のパブリケーション (出版物) を発行します。  
  
-   パブリケーションにはアーティクル (記事) が含まれています。  
  
-   パブリッシャーは、雑誌を直接または、ディストリビューター (流通業者) を使用して配布します。  
  
-   サブスクライバー (購読者) は、サブスクライブする (定期購読する) パブリケーションを受け取ります。  
  
 雑誌にたとえると、レプリケーションを理解する上で役に立ちますが、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のレプリケーションには、この例で表されない機能 (特に、サブスクライバーが更新を行ったり、パブリッシャーがパブリケーション内のアーティクルに増分変更を送信する機能など) もあるので注意が必要です。  
  
 *レプリケーション トポロジ* は、サーバーとデータのコピー間のリレーションシップを定義し、サーバー間のデータ フローを決定する論理を明白にします。 パブリッシャーとサブスクライバーの間でデータのコピーや移動を行ういくつかのレプリケーション処理 ( *エージェント*) があります。 次の図は、レプリケーションに関係するコンポーネントと処理の概要を表しています。  
  
 ![レプリケーション コンポーネントとデータ フロー](../../../relational-databases/replication/publish/media/replintro1.gif "レプリケーション コンポーネントとデータ フロー")  
  
## <a name="publisher"></a>パブリッシャー  
 パブリッシャーは、レプリケーションを介して他の場所でデータを使用できるようにするデータベース インスタンスです。 パブリッシャーは、1 つ以上のパブリケーションを持つことができ、各パブリケーションに、論理的に関連するレプリケート対象のオブジェクトとデータのセットが定義されています。  
  
## <a name="distributor"></a>ディストリビューター  
 ディストリビューターは、1 つ以上のパブリッシャーに関連付けられたレプリケーション固有のデータの保存場所として機能するデータベース インスタンスです。 各パブリッシャーは、ディストリビューターの単一のデータベース (ディストリビューション データベース) と関連付けられます。 ディストリビューション データベースには、レプリケーション状態データ、パブリケーションに関するメタデータが保存され、場合によっては、パブリッシャーからサブスクライバーへ移動するデータのキューとしても機能します。 多くの場合、単一のデータベース サーバー インスタンスが、パブリッシャーとディストリビューター両方の役割を果たします。 これを、 *ローカル ディストリビューター*と呼びます。 パブリッシャーとディストリビューターが別のデータベース サーバー インスタンス上で構成される場合、このディストリビューターを *リモート ディストリビューター*と呼びます。  
  
## <a name="subscribers"></a>[サブスクライバー]  
 サブスクライバーは、レプリケートされたデータを受信するデータベース インスタンスです。 サブスクライバーは、複数のパブリッシャーおよびパブリケーションからデータを受信できます。 選択したレプリケーションの種類に応じて、サブスクライバーはパブリッシャーにデータの変更を戻したり、データを他のサブスクライバーに再パブリッシュしたりできます。  
  
## <a name="article"></a>[アーティクル]  
 アーティクルは、パブリケーションに含まれている 1 つのデータベース オブジェクトを表します。 パブリケーションには、テーブル、ビュー、ストアド プロシージャ、その他のオブジェクトなどさまざまな種類のアーティクルを含めることができます。 テーブルがアーティクルとしてパブリッシュされている場合は、フィルターを使用してサブスクライバーに送信するデータの列と行を制限することができます。  
  
## <a name="publication"></a>パブリケーション  
 パブリケーションは、1 つのデータベースからの 1 つ以上のアーティクルの集合です。 複数のアーティクルを 1 つのパブリケーションにグループ化すると、1 つの単位としてレプリケートされる論理的に関連するデータベース オブジェクトとデータのセットを簡単に指定できます。  
  
## <a name="subscription"></a>サブスクリプション  
 サブスクリプションは、サブスクライバーに配信されるパブリケーションのコピーの要求です。 サブスクリプションでは、どのパブリケーションをいつ、どこで受信するのかが定義されます。 サブスクリプションには、プッシュとプルの 2 つの種類があります。 プッシュ サブスクリプションとプル サブスクリプションの詳細については、「[パブリケーションのサブスクライブ](../../../relational-databases/replication/subscribe-to-publications.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェントの概要](../../../relational-databases/replication/agents/replication-agents-overview.md)   
 [レプリケーションの種類](../../../relational-databases/replication/types-of-replication.md)   
 [AlwaysOn 可用性グループ用のレプリケーションの構成 (SQL Server)](../../../database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server.md)   
 [AlwaysOn パブリケーション データベースのメンテナンス (SQL Server)](../../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md)  
  
  
