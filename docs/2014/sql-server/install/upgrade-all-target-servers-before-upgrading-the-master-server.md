---
title: マスター サーバーをアップグレードする前にすべての対象サーバーのアップグレード |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- TSX [SQL Server Agent]
- target servers [SQL Server Agent]
- MSX [SQL Server Agent]
- master servers [SQL Server Agent]
ms.assetid: 2c231793-3878-4a5e-a425-1fa0d787ba84
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2b6e08a384e20d64a7002171059db0d35dfd94a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091472"
---
# <a name="upgrade-all-target-servers-before-upgrading-the-master-server"></a>マスター サーバーをアップグレードする前にすべてのターゲット サーバーをアップグレードする
  マスター サーバーをアップグレードする前に、ターゲット サーバーとして構成され、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているすべてのコンピューターをアップグレードしてください。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント  
  
## <a name="description"></a>説明  
 マルチサーバー環境で管理を自動化するには、マスター サーバーとターゲット サーバーが少なくとも 1 台ずつ必要です。 マスター サーバーは、ターゲット サーバーに対してジョブを分散し、ターゲット サーバーからイベントを受け取ります。 また、マスター サーバーは、ターゲット サーバーで実行されるジョブについて、ジョブ定義の中央コピーも保存します。  
  
 現在のサーバーがマスター サーバーとして構成されている場合、最初にすべてのターゲット サーバーをアップグレードしてから、マスター サーバーをアップグレードしてください。  
  
## <a name="corrective-action"></a>修正措置  
 マスター サーバーをアップグレードする前に、すべてのターゲット サーバーをアップグレードできない場合は、アップグレード後に、すべてのターゲット サーバーの参加を解除してからもう一度参加させる必要があります。  
  
 詳細については、「を自動化するエンタープライズ全体の管理、」のトピックを参照してください。"する方法。マスター サーバーから対象サーバーの参加を解除"と"する方法。マスター ターゲット サーバー"に参加[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server エージェントのアップグレードに関する問題](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)   
 [SQL Server エージェントのアップグレードに関する問題](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
