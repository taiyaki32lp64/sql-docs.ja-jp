---
title: インターネット経由のレプリケーションのセキュリティ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], Internet
- Internet [SQL Server replication], security
ms.assetid: 25b7af05-2721-4b24-9083-fb671e8bf4e0
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 42a070f35f6e9dce8a79e2c647ec290aac1adccc
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769600"
---
# <a name="securing-replication-over-the-internet"></a>インターネット経由のレプリケーションのセキュリティ
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  インターネット経由のレプリケーションを利用すると、特にモバイルのサブスクライバーで必要とされるような柔軟性を実現できます。ただし、適切に構成して十分なセキュリティを確保する必要があります。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] では、インターネット経由で情報を安全に共有するために、次のいずれかの技術を使用することを推奨しています。  
  
-   仮想プライベート ネットワーク (VPN)  
  
-   マージ レプリケーション用の Web 同期オプション  
  
## <a name="virtual-private-network"></a>仮想プライベート ネットワーク  
 仮想プライベート ネットワークを使用すると、複数の層を使ったシンプルかつ安全な方法で、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のデータをインターネット経由でレプリケートできます。 インターネットを介しての VPN 接続は、論理的にはサイト間のワイド エリア ネットワーク (WAN) リンクとして動作します。  
  
 これは、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows&#xA0;NT Version&#xA0;4.0 または [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows&#xA0;2000 オペレーティング システムで使用できる [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Point-to-Point トンネリング プロトコル (PPTP)、または Windows&#xA0;2000 オペレーティング システムで使用できるレイヤー 2 トンネリング プロトコル (L2TP) などのプロトコルを使用して、ユーザーがインターネットや他のパブリック ネットワークをトンネリングできるようにすることで実現します。 これにより、プライベート ネットワークとほぼ同等のセキュリティと機能が実現されます。  
  
 VPN の設定の詳細については、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows のマニュアルを参照してください。  
  
## <a name="web-synchronization-through-iis"></a>IIS による Web 同期  
 マージ レプリケーション用の Web 同期オプションを使用すると、HTTPS プロトコルを使用してデータをレプリケートできます。この方法は、ファイアウォール越しにデータをレプリケートする場合に便利です。 詳細については、「[Web 同期の構成](../../../relational-databases/replication/configure-web-synchronization.md)」および「[Web 同期のセキュリティ アーキテクチャ](../../../relational-databases/replication/security/security-architecture-for-web-synchronization.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [レプリケーションのセキュリティ設定の表示および変更](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
