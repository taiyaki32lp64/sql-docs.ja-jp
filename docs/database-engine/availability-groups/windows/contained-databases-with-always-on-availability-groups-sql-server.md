---
title: 包含データベースと可用性グループを使用する
description: 包含データベースと Always On 可用性グループを使用する方法
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], interoperability
- contained database, AlwaysOnAvailabilityGroups
ms.assetid: cacce3ae-e940-4566-8298-6607c4268e74
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 26e92d38188b02c5a2ce0025cc2d33fccc5c6728
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988425"
---
# <a name="use-contained-databases-with-always-on-availability-groups"></a>包含データベースと Always On 可用性グループを使用する 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックには、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] で [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]と共に包含データベースを使用する方法に関する情報が含まれています。  
  
##  <a name="Prerequisites"></a> 前提条件  
  
-   包含データベースを可用性グループに追加する前に、その可用性グループの可用性レプリカをホストする各サーバー インスタンスで、 **contained database authentication** のサーバー オプションが **1** に設定されていることを確認してください。 詳細については、「 [contained database authentication サーバー構成オプション](../../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md) 」および「 [サーバー構成オプション &#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)と共に包含データベースを使用する方法に関する情報が含まれています。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [サーバー構成オプション &#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [包含データベース](../../../relational-databases/databases/contained-databases.md)  
  
  
