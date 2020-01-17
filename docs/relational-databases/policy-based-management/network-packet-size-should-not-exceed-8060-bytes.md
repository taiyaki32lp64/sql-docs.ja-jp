---
title: ネットワーク パケット サイズは 8060 バイトを超えることはできない | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 86db5da1-afe4-4fbb-8bf8-33cedc7e4361
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1b153ab4f5fa1e3443d29c195d6b60004dcab8e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087054"
---
# <a name="network-packet-size-should-not-exceed-8060-bytes"></a>ネットワーク パケット サイズは 8060 バイトを超えることはできない
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  sp_configure の 'network packet size' に指定された値またはログイン ユーザーのネットワーク パケット サイズが 8060 バイトを超えている場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、異なるメモリ割り当て操作が実行されます。 これにより、バッファー プールに予約されていない、プロセスの仮想アドレス空間が増加する可能性があります。  
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスと推奨事項  
 ネットワーク パケット サイズが 8060 バイトを超えないようにする必要があります。  
  
## <a name="for-more-information"></a>詳細情報  
 [サポート技術情報の資料 903002](https://go.microsoft.com/fwlink/?linkid=117749)  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したベスト プラクティスの監視と実行](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
