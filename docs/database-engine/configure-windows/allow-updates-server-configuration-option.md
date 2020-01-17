---
title: allow updates サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3cccccebcbbd9054752aa8aa4e65f3f2bc17b342
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68013151"
---
# <a name="allow-updates-server-configuration-option"></a>allow updates サーバー構成オプション
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このオプションは **sp_configure** ストアド プロシージャにまだ含まれていますが、その機能を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で使用することはできません。 設定しても何の影響もありません。 システム テーブルの直接更新はサポートされていません。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 **allow updates** オプションを変更すると、RECONFIGURE ステートメントが失敗します。 **allow updates** オプションへの変更は、すべてのスクリプトから削除する必要があります。  
  
## <a name="see-also"></a>参照  
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
