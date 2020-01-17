---
title: 可用性グループ リスナーのプロパティの表示 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygrouplistenerproperties.general.f1
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
ms.assetid: aca0d016-3228-40b8-bdc3-285ed6d9b280
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bdec432699b7d0a6152509ec6a53ddf452376d5c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62788028"
---
# <a name="view-availability-group-listener-properties-sql-server"></a>可用性グループ リスナーのプロパティの表示 (SQL Server)
  このトピックでは、 *で* または [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] を使用して、AlwaysOn [!INCLUDE[tsql](../../../includes/tsql-md.md)] 可用性グループ リスナー [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]のプロパティを表示する方法について説明します。  
  
-   **リスナーのプロパティを表示する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **リスナーのプロパティを表示するには**  
  
1.  オブジェクト エクスプローラーで、リスナーを表示する可用性グループの任意の可用性レプリカをホストするサーバー インスタンスに接続します。 サーバー名をクリックし、サーバー ツリーを展開します。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  可用性グループのノード、 **[可用性グループ リスナー]** ノードの順に展開します。  
  
4.  表示するリスナーを右クリックし、 **[プロパティ]** をクリックします。  
  
5.  これにより、 **[可用性グループ リスナーのプロパティ]** ダイアログ ボックスが開きます。 詳細については、このトピックの「 [[可用性グループ リスナーのプロパティ] (ダイアログ ボックス)](#AgListenerPropertiesDialog)」を参照してください。  
  
###  <a name="AgListenerPropertiesDialog"></a> [可用性グループ リスナーのプロパティ] (ダイアログ ボックス)  
 **[リスナーの DNS 名]**  
 可用性グループ リスナーのネットワーク名。  
  
 **ポート**  
 このリスナーで使用される TCP ポート。  
  
> [!NOTE]  
>  プライマリ レプリカに接続している場合は、このフィールドを使用してリスナーのポート番号を変更できます。 それには、可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。  
  
 **[ネットワーク モード]**  
 リスナーで使用される TCP プロトコルを指定します。次のいずれかです。  
  
 **[DHCP]**  
 リスナーは、動的ホスト構成プロトコル (DHCP) を実行しているサーバーによって割り当てられる動的 IP アドレスを使用します。  
  
 **[静的 IP]**  
 リスナーは、1 つまたは複数の静的 IP アドレスを使用します。 別のサブネットにアクセスするには、可用性グループ リスナーは静的 IP アドレスを使用する必要があります。  
  
 グリッドには、リスナーがリッスンする各サブネットと、そのサブネットに関連付けられた IP アドレスが表示されます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **リスナーのプロパティを表示するには**  
  
 可用性グループ リスナーを監視するには、次のビューを使用します。  
  
 [sys.availability_group_listener_ip_addresses](/sql/relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql)  
 可用性グループ リスナーに対してオンラインになっている準拠仮想 IP アドレスごとに 1 行のデータを返します。  
  
 **列名:** listener_id、ip_address、ip_subnet_mask、is_dhcp、network_subnet_ip、network_subnet_prefix_length、network_subnet_ipv4_mask、state, state_desc  
  
 [sys.availability_group_listeners](/sql/relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql)  
 特定の可用性グループについて、可用性グループにネットワーク名が関連付けられていないことを示すゼロ行を返すか、WSFC クラスター内の可用性グループ リスナーの構成ごとに 1 行のデータを返します。  
  
 **列名** : group_id、listener_id、dns_name、port、is_conformant、ip_configuration_string_from_cluster  
  
 [sys.dm_tcp_listener_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql)  
 各 TCP リスナーの動的状態情報を含む行を返します。  
  
 **列名** : listener_id、ip_address、is_ipv4、port、type、type_desc、state、state_desc、start_time  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../../includes/tsql-md.md)] を使用した [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 環境の監視の詳細については、「[可用性グループの監視 &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [可用性グループ リスナーの削除 &#40;SQL Server&#41;](remove-an-availability-group-listener-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
  
  
