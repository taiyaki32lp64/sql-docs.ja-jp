---
title: 双方向トランザクション レプリケーション | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 85ab0f993e919b491376ff3d9ffa44afefd42603
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710689"
---
# <a name="bidirectional-transactional-replication"></a>双方向トランザクション レプリケーション
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  双方向トランザクション レプリケーションとは、トランザクション レプリケーションの中でも特に、2 台のサーバーが互いに変更内容を交換し合うことのできるトポロジのことです。各サーバーはデータをパブリッシュすると共に、同じデータを含んだパブリケーションをもう一方のサーバーからサブスクライブします。 変更が確実にサブスクライバーに対してのみ送信され、サブスクライバーからパブリッシャーには送信されないようにするには、[sp_addsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) の `@loopback_detection` パラメーターを TRUE に設定します。  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降では、ピア ツー ピア トランザクション レプリケーションでもこのトポロジがサポートされますが、双方向レプリケーションを使用するとパフォーマンスが向上します。  
  
## <a name="see-also"></a>参照  
 [ピア ツー ピア トランザクション レプリケーション](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
