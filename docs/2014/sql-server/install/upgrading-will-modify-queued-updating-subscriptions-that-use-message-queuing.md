---
title: アップグレードすると、メッセージ キューを使用するキュー更新サブスクリプションが変更されます |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication]
- MSMQ [SQL Server replication]
- queues [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
ms.assetid: 97944de3-fbad-4db1-939a-dcd550bf5893
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1c723050f9e860534c5298df9a487337e319ff91
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091412"
---
# <a name="upgrading-will-modify-queued-updating-subscriptions-that-use-message-queuing"></a>アップグレードすると、メッセージ キューを使用するキュー更新サブスクリプションが変更される
  アップグレード アドバイザーによって、[!INCLUDE[msCoName](../../includes/msconame-md.md)] メッセージ キュー (MSMQ) を使用する 1 つ以上のキュー更新サブスクリプションが存在する可能性があることが検出されました。 レプリケーションでは、メッセージ キューがサポートされないため、キュー更新サブスクリプションが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] キューを使用するように変更されます。  
  
 値しか**sql**は許可されています。 メッセージ キューを使用する既存のパブリケーションは、アップグレード時に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] キューを使用するよう修正されます。 使用するアプリケーションがメッセージ キューによるキュー更新を必要とする場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] キューに対応するようにこれらのアプリケーションを記述し直す必要があります。 キュー更新サブスクリプションの詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「トランザクション レプリケーションの更新可能なサブスクリプション」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアップグレード中にメッセージ キュー サービスを実行していると、既存のメッセージ キュー サブスクリプション キューは削除されます。  
  
 メッセージ キュー サービスを実行していない場合は、アップグレード完了後にキューを手動で削除してください。 キューの削除方法の詳細については、Windows のマニュアルを参照してください。  
  
## <a name="see-also"></a>関連項目  
 [レプリケーションのアップグレードに関する問題](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
  
