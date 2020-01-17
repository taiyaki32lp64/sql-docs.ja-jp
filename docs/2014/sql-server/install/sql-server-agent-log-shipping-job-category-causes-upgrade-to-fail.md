---
title: SQL Server エージェントのログ配布ジョブ カテゴリがアップグレードが失敗すると、|Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server Agent]
- job categories [SQL Server Agent]
ms.assetid: ef05ce53-c6ce-42ec-9df8-46c951626424
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7145d846657613b50706ebe75c9832f40f49383e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092040"
---
# <a name="sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail"></a>SQL Server エージェントのログ配布ジョブ カテゴリが原因でアップグレードに失敗する
  "ログ配布" という名前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ カテゴリがある場合、アップグレード プロセスは失敗します。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント  
  
## <a name="description"></a>説明  
 "ログ配布" という名前のシステム ジョブ カテゴリがあります。 アップグレード対象のインストールにユーザーが作成した "ログ配布" という名前のジョブ カテゴリが含まれている場合、アップグレードする前にそのジョブ カテゴリの名前を変更する必要があります。名前を変更しないと、アップグレード プロセスは失敗します。  
  
## <a name="see-also"></a>参照  
 [ログ配布は、アップグレードした後は実行されません。](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)   
 [アップグレードと SQL Server エージェント ユーザー プロキシ アカウントが一時的な UpgradedProxyAccount に変更されます。](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md)   
 [SQL Server エージェントのアップグレードに関する問題](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
