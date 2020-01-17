---
title: フェールオーバー クラスター インスタンスの管理とメンテナンス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- user accounts [SQL Server], failover clustering
- clusters [SQL Server], maintaining
- nodes [Faillover Clustering]
- failover clustering [SQL Server], maintaining
- adding nodes
- virtual servers [SQL Server], removing nodes
- clustered instance of SQL Server
- nodes [Faillover Clustering], removing
- nodes [Faillover Clustering], adding
- service accounts [SQL Server]
- removing nodes
- virtual servers [SQL Server], adding nodes
ms.assetid: 2d5c63e9-8061-45c3-94db-8dd3100b8a91
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 46b895dcc560a6e42e9ba5abce39ee22b4075bde
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002480"
---
# <a name="failover-cluster-instance-administration-and-maintenance"></a>フェールオーバー クラスター インスタンスの管理とメンテナンス
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  既存の AlwaysOn フェールオーバー クラスター インスタンス (FCI) に対するノードの追加または削除のようなメンテナンス タスクは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のセットアップ プログラムを使用して行います。 IP アドレス リソースの変更や、特定の FCI シナリオからの復元が必要になった場合など、その他の管理タスクについては、Windows Server フェールオーバー クラスタリング (WSFC) サービスの管理スナップインであるフェールオーバー クラスター マネージャー スナップインを使用して行います。  
  
## <a name="maintaining-a-failover-cluster-instance"></a>フェールオーバー クラスター インスタンスの管理  
 FCI をインストールすると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のセットアップ プログラムを使用して、フェールオーバー クラスターを変更または修復できます。 たとえば、FCI に別のノードを追加したり、FCI をスタンドアロン インスタンスとして実行したり、FCI 構成からノードを削除したりできます。  
  
### <a name="adding-a-node-to-an-existing-failover-cluster-instance"></a>既存のフェールオーバー クラスター インスタンスへのノードの追加  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップ プログラムには、既存の FCI を維持するオプションが含まれています。 このオプションを選択すると、FCI を追加するコンピューター上で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップ プログラムを実行することによって、FCI に他のノードを追加できます。 詳細については、「[新しい SQL Server フェールオーバー クラスターの作成 &#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)」と「[SQL Server フェールオーバー クラスターでのノードの追加または削除 &#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)」を参照してください。  
  
### <a name="removing-a-node-from-an-existing-failover-cluster-instance"></a>既存のフェールオーバー クラスター インスタンスからのノードの削除  
 FCI からノードを削除するコンピューター上で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップ プログラムを実行すると、FCI からノードを削除できます。 FCI の各ノードは、FCI 上で他のノードと依存関係のないピア (同等) と見なされるので、どのノードでも削除できます。 損傷したノードは、使用できない場合でも削除できます。ただし、その削除プロセスで、使用できないノードから [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] バイナリがアンインストールされることはありません。 削除したノードは、いつでも FCI に戻すことができます。 詳細については、「[SQL Server フェールオーバー クラスターでのノードの追加または削除 &#40;Setup&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)」を参照してください。  
  
### <a name="changing-service-accounts"></a>サービス アカウントの変更  
 FCI ノードがダウンしている、またはオフラインになっているときは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントのパスワードを変更しないでください。 変更する必要がある場合は、すべてのノードがオンラインに戻ったときに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーを使用してパスワードを再設定してください。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のサービス アカウントがクラスター内で管理者でない場合は、クラスターのどのノードでも管理共有を削除できません。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が動作するためには、クラスター内で管理共有を利用できる必要があります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントと WSFC サービス アカウントに同じアカウントを使用しないでください。 WSFC サービス アカウントのパスワードを変更すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストールが失敗します。  
  
 [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]では、サービス SID が [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントに使用されます。 詳細については、「 [Windows サービス アカウントと権限の構成](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。  
  
## <a name="administering-a-failover-cluster-instance"></a>フェールオーバー クラスター インスタンスの管理  
  
|タスクの説明|トピック|  
|----------------------|----------------|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースに依存関係を追加する方法について説明します。|[SQL Server リソースへの依存関係の追加](../../../sql-server/failover-clusters/windows/add-dependencies-to-a-sql-server-resource.md)|  
|Kerberos は、クライアント/サーバー アプリケーションで強力な認証を行うためにデザインされたネットワーク認証プロトコルです。 企業全体のネットワーク認証のセキュリティ強化に役立つ、相互運用性の基盤となるプロトコルです。 Kerberos 認証は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のスタンドアロンのインスタンス、または AlwaysOn FCI と共に使用できます。|[Kerberos 接続用のサービス プリンシパル名を登録します](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。|  
|Kerberos 認証を有効にする方法について説明したコンテンツへのリンクを提供します。||  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターの障害から復旧する手順について説明します。|[フェールオーバー クラスター インスタンス障害からの復旧](../../../sql-server/failover-clusters/windows/recover-from-failover-cluster-instance-failure.md)|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスの IP アドレス リソースを変更する手順について説明します。|[フェールオーバー クラスター インスタンスの IP アドレスの変更](../../../sql-server/failover-clusters/windows/change-the-ip-address-of-a-failover-cluster-instance.md)|  
  
## <a name="see-also"></a>参照  
 [HealthCheckTimeout プロパティ設定の構成](../../../sql-server/failover-clusters/windows/configure-healthchecktimeout-property-settings.md)   
 [FailureConditionLevel プロパティ設定の構成](../../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md)   
 [フェールオーバー クラスター インスタンスの診断ログを表示して読む方法](../../../sql-server/failover-clusters/windows/view-and-read-failover-cluster-instance-diagnostics-log.md)  
  
  
