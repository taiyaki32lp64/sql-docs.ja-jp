---
title: ユーザー データベースの対称キー | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3333ab5b-2518-4753-a0a8-57df5e5af74f
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 71e52cf9d65eb21df0553f5601bd4aefb3727175
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021507"
---
# <a name="symmetric-keys-on-user-databases"></a>ユーザー データベースの対称キー
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このルールでは、長さが 128 バイト未満のキーが RC2 または RC4 暗号化アルゴリズムを使用していないかどうかを確認します。  
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスと推奨事項  
 データ暗号化用の対称キーを作成する場合は、AES 128 ビット以上を使用します。 AES がオペレーティング システムでサポートされていない場合は、3DES を使用します。  
  
## <a name="for-more-information"></a>詳細情報  
 [暗号化アルゴリズムの選択](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したベスト プラクティスの監視と実行](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
