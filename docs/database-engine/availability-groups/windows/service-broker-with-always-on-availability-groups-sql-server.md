---
title: Service Broker と可用性グループ
description: SQL Server Always On 可用性グループでの Service Broker の構成に関する情報が含まれます。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Service Broker, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 881c20e5-1c99-44eb-b393-09fc5ea0f122
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8845f69e619c8cd2cc7a194b6f03a4dec5f592c1
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822613"
---
# <a name="service-broker-with-always-on-availability-groups-sql-server"></a>Service Broker と Always On 可用性グループ (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックでは、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] で Service Broker を [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]と共に使用できるように構成する方法について説明します。  
  
  
##  <a name="ReceiveRemoteMessages"></a> 可用性グループのサービスでリモート メッセージを受信するための要件  
  
1.  **可用性グループにリスナーが存在している。**  
  
     詳細については、「 [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)が存在する必要があります。  
  
2.  **Service Broker エンドポイントが存在し、正しく構成されている。**  
  
     可用性グループの可用性レプリカをホストするすべての [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスで、次のように Service Broker エンドポイントを構成します。  
  
    -   LISTENER_IP を "ALL" に設定します。 この設定により、可用性グループ リスナーにバインドされている有効な IP アドレスに接続できるようになります。  
  
    -   すべてのホスト サーバー インスタンスで Service Broker の PORT を同じポート番号に設定します。  
  
        > [!TIP]  
        >  特定のサーバー インスタンスの Service Broker エンドポイントのポート番号を確認するには、 **sys.tcp_endpoints** カタログ ビューの [port](../../../relational-databases/system-catalog-views/sys-tcp-endpoints-transact-sql.md) 列に対してクエリを実行します ( **type_desc** = 'SERVICE_BROKER')。  
  
     次の例では、既定の Service Broker ポート (4022) を使用し、有効なすべての IP アドレスをリッスンする Windows 認証済みの Service Broker エンドポイントを作成します。  
  
    ```  
    CREATE ENDPOINT [SSBEndpoint]  
        STATE = STARTED  
        AS TCP  (LISTENER_PORT = 4022, LISTENER_IP = ALL )  
        FOR SERVICE_BROKER (AUTHENTICATION = WINDOWS)  
    ```  
  
     詳細については、「[CREATE ENDPOINT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-endpoint-transact-sql.md)」を参照してください。  

    > [!NOTE]  
    SQL Server Broker はマルチサブネット対応ではありません。 0 に設定されている "registerallprovidersip" を必ず使用してください。また、DNS で静的 IP を使用し、 https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server で定義されているように、DNS のクラスターに必要な許可を与えていないことを確認してください。 無効になっている IP を使用しようとして Broker がメッセージを送らせることがあります。そのとき、ステータスは "CONVERSING" になります。

3.  **エンドポイントに対する CONNECT 権限を許可する。**  
  
     Service Broker エンドポイントに対する CONNECT 権限を PUBLIC またはログインに許可します。  
  
     次の例では、 `broker_endpoint` という名前の Service Broker エンドポイントに対する接続を PUBLIC に許可します。  
  
    ```  
    GRANT CONNECT ON ENDPOINT::[broker_endpoint] TO [PUBLIC]  
    ```  
  
     詳細については、「 [GRANT &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-transact-sql.md)と共に使用できるように構成する方法について説明します。  
  
4.  **msdb に AutoCreatedLocal ルートまたは特定のサービスへのルートが含まれている。**  
  
    > [!NOTE]  
    >  **msdb**を含む各ユーザー データベースには、既定で **AutoCreatedLocal**というルートが含まれています。 このルートは、どのサービス名および任意のブローカー インスタンスにも適用でき、現在のインスタンス内でメッセージを配信するように指定します。 **AutoCreatedLocal** の優先度は、リモート インスタンスと通信する特定のサービスを明示的に指定したルートよりも低くなります。  
  
     ルートの作成の詳細については、「 [Service Broker のルーティングの例](https://msdn.microsoft.com/library/ms166090\(SQL.105\).aspx) 」( [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] バージョンのオンライン ブック) および「 [CREATE ROUTE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-route-transact-sql.md)と共に使用できるように構成する方法について説明します。  
  
##  <a name="SendRemoteMessages"></a> 可用性グループのリモート サービスにメッセージを送信するための要件  
  
1.  **対象サービスへのルートを作成する。**  
  
     次のようにルートを構成します。  
  
    -   ADDRESS を、サービス データベースをホストする可用性グループのリスナーの IP アドレスに設定します。  
  
    -   PORT を、各リモート SQL Server インスタンスの Service Broker エンドポイントに指定したポートに設定します。  
  
     次の例では、 `RouteToTargetService` サービスに対する `ISBNLookupRequestService` という名前のルートを作成します。 ルートの対象は、ポート 4022 を使用している可用性グループ リスナー `MyAgListener`です。  
  
    ```  
    CREATE ROUTE [RouteToTargetService] WITH   
    SERVICE_NAME = 'ISBNLookupRequestService',   
    ADDRESS = 'TCP://MyAgListener:4022';  
  
    ```  
  
     詳細については、「 [CREATE ROUTE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-route-transact-sql.md)と共に使用できるように構成する方法について説明します。  
  
2.  **msdb に AutoCreatedLocal ルートまたは特定のサービスへのルートが含まれている。** (詳細については、このトピックの前の「 [可用性グループのサービスでリモート メッセージを受信するための要件](#ReceiveRemoteMessages)」を参照してください)。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-endpoint-transact-sql.md)  
  
-   [CREATE ROUTE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-route-transact-sql.md)  
  
-   [GRANT &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-transact-sql.md)  
  
-   [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [可用性グループの作成と構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [データベース ミラーリングまたは Always On 可用性グループのログイン アカウントの設定 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [SQL Server Service Broker (SQL Server Service Broker)](../../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
