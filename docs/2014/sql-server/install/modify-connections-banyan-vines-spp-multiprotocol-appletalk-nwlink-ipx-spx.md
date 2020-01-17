---
title: Banyan VINES Sequenced Packet Protocol (SPP)、Multiprotocol、AppleTalk、または NWLink IPX/SPX ネットワーク プロトコルを使用する接続の変更 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- network protocols [SQL Server], modifying connections
- SPP [SQL Server]
- NWLink IPX/SPX [SQL Server]
- connections [SQL Server]
- AppleTalk [SQL Server]
- Sequenced Packet Protocol [SQL Server]
- Multiprotocol Net-Library [SQL Server]
- Banyan VINES Sequenced Package Protocol [SQL Server]
- IPX/SPX [SQL Server]
- protocols [SQL Server], modifying connections
- RPC [SQL Server]
ms.assetid: 5c5ae453-cc5b-4898-95c7-ad34157b1f60
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cdbcaa39e3d9630bd4ea50919f31cdbb15a36d14
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093899"
---
# <a name="modify-connections-that-use-banyan-vines-sequenced-packet-protocol-spp-multiprotocol-appletalk-or-nwlink-ipx-spx-network-protocols"></a>Banyan VINES Sequenced Packet Protocol (SPP)、Multiprotocol、AppleTalk、または NWLink IPX/SPX ネットワーク プロトコルを使用する接続を変更する
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] でサポートされていないクライアント サーバー接続プロトコルをアップグレード アドバイザーが検出しました。 Banyan VINES Sequenced Packet Protocol (SPP)、Multiprotocol (RPC)、AppleTalk、または NWLink IPX/SPX ネットワーク プロトコルを使用するクライアント接続は、サポート対象のプロトコルを使用して接続する必要があります。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>説明  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、Banyan VINES Sequenced Packet Protocol (SPP)、Multiprotocol、AppleTalk、または NWLink IPX/SPX ネットワーク プロトコルはサポートされていません。 以前にこれらのプロトコルを使用して接続していたクライアントの場合、別のプロトコルを選択する必要があります。  
  
## <a name="corrective-action"></a>修正措置  
 サポートされているプロトコルを使用してサーバーに接続するように、クライアント アプリケーションを変更します。 サポートされていないプロトコルを使用するように別名を設定している場合は、サポートされるいずれかのプロトコルを使用するように別名を変更する必要があります。  
  
 指定するかネットワークでの RPC、ネットワークの DBMSRPCN = アプリケーションの接続文字列の使用または次のいずれかのプロトコルの負荷具体的には場合、= Appletalk、またはネットワーク用に DBMSADSN、Banyan VINES プロパティにまたは明示的なプレフィックスを使用して、DBMSVINN を ="spx:*server \instance*"SPX などの"bv:*サーバー*"の Banyan VINES、"adsp:*サーバー*"appletalk の場合または"rpc:*サーバー*"forマルチ プロトコル、しする必要がありますを変更するアプリケーションでサポートされているプロトコルのいずれかを使用します。  
  
 詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「ネットワーク プロトコルの選択」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 アップグレード アドバイザー&#91;新規&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
