---
title: MSSQL_ENG024070 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG024070 error
ms.assetid: 23ac7e00-fab6-429b-9f85-2736a322aa65
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: c45c23cd93cfda524f9987ae8b2181aece99f9fa
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770292"
---
# <a name="mssqleng024070"></a>MSSQL_ENG024070
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|24070|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|クライアントには必要な特権がありません。|  
  
## <a name="explanation"></a>説明  
 このエラーは、レプリケーションが使用されたかどうかにかかわらず発生する一般エラーです。 一般に、レプリケーション トポロジ内のサーバーでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーではなく [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows サービス コントロール マネージャーで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントが変更された場合に、このエラーが発生します。 サービス アカウントの変更後にエージェント ジョブを実行しようとすると、次のようなエラー メッセージが表示されてジョブが失敗する場合があります。  
  
 `Executed as user: \<UserAccount>. Replication-Replication Snapshot Subsystem: agent \<AgentName> failed. Executed as user: \<UserAccount>. A required privilege is not held by the client. The step failed. [SQLSTATE 42000] (Error 14151). The step failed.`  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの新しいサービス アカウントに必要な権限を Windows サービス コントロール マネージャーが付与できないので、この問題が発生します。  
  
## <a name="user-action"></a>ユーザーの操作  
 今後この問題を回避するには、サービス アカウントおよびパスワードを変更する場合に、Windows サービス コントロール マネージャーではなく [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを必ず使用してください。  
  
 この問題を解決するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、サービス アカウントを元のアカウントに戻します。 その後、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、新しいアカウントに変更します。 このとき、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーは、新しいアカウントを次のセキュリティ グループに追加します。  
  
 SQLServer2008SQLAgentUser$ComputerName$InstanceName  
  
 このセキュリティ グループのメンバーになると、レプリケーション エージェント ジョブを実行するために必要な権限が新しいアカウントに付与されます。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [レプリケーションのログインとパスワードの管理](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [SQL Server 構成マネージャー](../../relational-databases/sql-server-configuration-manager.md)  
  
  
