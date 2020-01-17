---
title: '[IP アドレスの追加] ダイアログ ボックス (SQL Server Management Studio) | Microsoft Docs'
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygrouplistener.addipaddress.f1
ms.assetid: 98c9ad3b-ff3c-4c1d-b344-59a72fca137c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 68bd85258bd3fd259386f020394ffb5bc70a9781
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62791916"
---
# <a name="add-ip-address-dialog-box-sql-server-management-studio"></a>[IP アドレスの追加] ダイアログ ボックス (SQL Server Management Studio)
  この F1 ヘルプ トピックでは、 **[IP アドレスの追加]** ダイアログ ボックスのオプションについて説明します。 このダイアログ ボックスには、 **[新しい可用性グループ リスナー]** ダイアログ ボックスと **[リスナー]** タブ ( **の** または [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] の [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] [レプリカの指定] [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]ページ上) からアクセスできます。  
  
## <a name="prerequisites"></a>前提条件  
 サブネットを可用性グループ リスナーに追加するには、サブネットごとの IP アドレスと、IPv4 アドレスのサブネット マスクを把握している必要があります。  
  
##  <a name="PageOptions"></a> [IP アドレスの追加] オプション  
 **[サブネット]**  
 ドロップダウン リストを使用して、可用性グループ リスナーに追加するサブネットのアドレスを選択します。 既定では、サブネットには IPv4 アドレスと IPv6 アドレスの両方があります。 **[IP アドレスの追加]** ダイアログを初めて使用するときは、 **[サブネット]** ボックスの一覧に、可用性グループのレプリカをホストするサブネットごとに両方のサブネット アドレスが表示されます。 特定のサブネットをリスナーに追加するには、そのサブネット アドレスのいずれかを選択します。  
  
 **[IP アドレスの追加]** ダイアログ ボックスで作業を終え、 **[OK]** をクリックして、選択したサブネット アドレスをリスナーに追加すると、 **[サブネット]** ボックスの一覧でそのサブネット アドレスが除外されます。 選択されなかったすべてのサブネット アドレスは、ドロップダウン リストに残ります。 サブネットごとにサブネット アドレスを 1 つだけリスナーに追加したことを確認してください。それ以外の場合、リスナーの作成に失敗します。  
  
 **[アドレス]**  
 このフィールドを使用して、選択したサブネット アドレスの静的 IP アドレスを入力します。 この IP アドレスは、ネットワーク管理者に問い合わせてください。 選択したサブネット アドレスの有効なアドレスを入力したことを確認します。アドレスが無効な場合、リスナーの作成に失敗します。  
  
 **[IPv4 アドレス]**  
 サブネットの IPv4 サブネット アドレスを選択した場合は、有効な IPv4 静的アドレスをここに入力します。  
  
 **[サブネット マスク]**  
 IPv4 アドレスの場合は、この読み取り専用フィールドに、選択したサブネットのサブネット マスクが表示されます。  
  
 **[IPv6 アドレス]**  
 サブネットの IPv6 サブネット アドレスを選択した場合は、有効な IPv6 静的アドレスをここに入力します。  
  
 **[OK]**  
 クリックすると、選択したアドレスのサブネットと指定した静的 IP アドレスが追加されます。 これらの値が含まれる行は、 **[新しい可用性グループ リスナー]** または **[レプリカの指定]** ダイアログ ボックスのサブネット グリッドに追加されます。  
  
> [!IMPORTANT]  
>  **[IP アドレスの追加]** ダイアログでは、IP アドレスは検証されません。 また、既に可用性グループ リスナーに追加されているサブネットのサブネット アドレスを追加できないようになっていません。  
  
 **Cancel**  
 クリックすると、選択が取り消され、 **[新しい可用性グループ リスナー]** ダイアログ ボックスまたは **[リスナー]** タブに戻ります。サブネットの静的 IP アドレスは追加されません。  
  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [可用性グループへのレプリカ追加ウィザードの使用 &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [AlwaysOn クライアント接続 (SQL Server)](always-on-client-connectivity-sql-server.md)  
  
  
