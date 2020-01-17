---
title: パブリッシャーのセキュリティ保護 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server replication], publication access list
- publications [SQL Server replication], publication access lists
- publication access list (PAL)
- PAL (publication access list)
- Publishers [SQL Server replication], security
- publications [SQL Server replication], security
ms.assetid: 4513a18d-dd6e-407a-b009-49dc9432ec7e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 201b1496444888b207a1a72be640b9705ff1059d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62960149"
---
# <a name="secure-the-publisher"></a>パブリッシャーのセキュリティ保護
  次のレプリケーション エージェントはパブリッシャーに接続します。  
  
-   ログ リーダー エージェント (Log Reader Agent)  
  
-   スナップショット エージェント  
  
-   キュー リーダー エージェント (Queue Reader Agent)  
  
-   [マージ エージェント]  
  
 最低限必要な権限のみを与え、かつ、すべてのパスワードの格納を保護するという原則に従って、これらの各エージェントに対し適切なログインを提供することをお勧めします。 各エージェントに必要な権限の詳細については、「 [Replication Agent Security Model](replication-agent-security-model.md)」を参照してください。  
  
 ログインとパスワードの適切な管理以外にも、パブリケーション アクセス リスト (PAL) の役割を理解しておく必要があります。 PAL は、パブリッシャーのデータベースへのアドホック アクセスを制限すると同時に、ログインしてパブリケーション データへのアクセスを可能にするために使用されます。  
  
## <a name="publication-access-list"></a>パブリケーション アクセス リスト  
 PAL は、パブリッシャーでパブリケーションの安全を確保する主要なメカニズムです。 PAL は、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows のアクセス制御リストによく似た機能を備えています。 パブリケーションを作成すると、レプリケーションによってそのパブリケーションから PAL が作成されます。 PAL は、パブリケーションへのアクセスを許可されているログインとグループのリストを含めるように構成できます。 エージェントがパブリッシャーまたはディストリビューターに接続し、パブリケーションへのアクセスを要求すると、PAL 内の認証情報が、エージェントによって提供されるパブリッシャー ログインと比較されます。 このプロセスでは、クライアント ツールがパブリッシャーとディストリビューターのログインを使用してパブリッシャー側で直接変更を行う危険性を回避できるので、パブリッシャーのセキュリティを向上できます。  
  
> [!NOTE]  
>  PAL のメンバーに含めるため、レプリケーションによって、各パブリケーションに対してパブリッシャー上にロールが作成されます。 ロールには、マージ レプリケーションの場合は **Msmerge_** _\<PublicationID>_ という形式、トランザクション レプリケーションとスナップショット レプリケーションの場合は **MSReplPAL_** _\<PublicationDatabaseID>_ **_** _\<PublicationID>_ という形式で名前が付けられます。  
  
 既定で PAL に含まれるログインは、パブリケーションが作成された時点の **sysadmin** 固定サーバー ロールのメンバー、およびパブリケーションを作成するために使用されるログインです。 既定で、パブリケーション データベース上の **sysadmin** 固定サーバー ロールまたは **db_owner** 固定データベース ロールのメンバーであるすべてのログインは、明示的に PAL に追加しなくても、パブリケーションに対してサブスクライブできます。  
  
 PAL を使用する場合は、次のガイドラインを考慮してください。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインを PAL に追加する前に、そのログインをパブリケーション データベースのデータベース ユーザーに関連付ける必要があります。  
  
-   最小特権の原則に従って、PAL 内のログインに、レプリケーション タスクを実行するために必要な権限のみを許可します。 レプリケーションに必要のない固定データベース ロールやサーバー ロールに、ログインを追加しないでください。 必要な権限の詳細については、「 [Replication Agent Security Model](replication-agent-security-model.md) 」および「 [Replication Security Best Practices](replication-security-best-practices.md)」を参照してください。  
  
-   リモート ディストリビューターを使用する場合、PAL 内のアカウントは、パブリッシャーとディストリビューターの両方で使用できる必要があります。 このアカウントは、どちらのサーバーでも定義されているドメイン アカウントまたはローカル アカウントにする必要があります。 両方のログインに関連付けられているパスワードは、同じにする必要があります。  
  
-   PAL に Windows アカウントが含まれており、ドメインで Active Directory が使用されている場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行する際に使用するアカウントが Active Directory から読み取りを行う権限を持っている必要があります。 Windows アカウントに関する問題が発生した場合は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行する際に使用するアカウントが十分な権限を持っていることを確認します。 詳細については、Windows のマニュアルを参照してください。  
  
 PAL を管理する場合は、「[パブリケーション アクセス リストのログインの管理](manage-logins-in-the-publication-access-list.md)」を参照してください。  
  
## <a name="snapshot-agent"></a>スナップショット エージェント  
 パブリケーションごとに 1 つのスナップショット エージェントがあります。 詳細については、「 [Create a Publication](../publish/create-a-publication.md)」を参照してください。  
  
## <a name="ftp-snapshot-delivery"></a>FTP スナップショット配信  
 UNC 共有ではなく FTP 共有によりスナップショットを使用できるように指定する場合、FTP アクセスの構成時にログインおよびパスワードを指定する必要があります。 詳細については、「[FTP でのスナップショットの配信](../publish/deliver-a-snapshot-through-ftp.md)」を参照してください。  
  
## <a name="log-reader-agent"></a>ログ リーダー エージェント (Log Reader Agent)  
 トランザクション レプリケーション用にパブリッシュされるデータベースには、それぞれ 1 つのログ リーダー エージェントがあります。 詳細については、「 [Create a Publication](../publish/create-a-publication.md)」を参照してください。  
  
## <a name="queue-reader-agent"></a>キュー リーダー エージェント (Queue Reader Agent)  
 あるディストリビューターに関連付けられたすべてのパブリッシャーおよびパブリケーション (キュー更新サブスクリプションを許可するパブリケーション) に対し、1 つのキュー リーダー エージェントがあります。 詳細については、「[トランザクション パブリケーションの更新可能なサブスクリプションの有効化](../publish/enable-updating-subscriptions-for-transactional-publications.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [SQL Server レプリケーションのセキュリティ](view-and-modify-replication-security-settings.md)  
  
  
