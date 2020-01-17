---
title: アップグレード処理中にすべてのファイル グループが書き込み可能なことを確認 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- filegroups [SQL Server], writeable
- writeable filegroups [SQL Server]
ms.assetid: 2985efc1-4b14-46c3-abbd-a656b159f23c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 758207977c8ddf92d6696dda71a8943e6a596d4d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091184"
---
# <a name="verify-all-filegroups-are-writeable-during-the-upgrade-process"></a>アップグレード処理中にすべてのファイル グループが書き込み可能であることを確認する
  アップグレード アドバイザーによって、1 つ以上の読み取り専用のファイル グループを含むデータベースが検出されました。 アップグレードする前に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内のすべてのデータベースでファイル グループを READ_WRITE に設定しておく必要があります。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>修正措置  
 ALTER DATABASE を使用してファイル グループを READ_WRITE に設定してください。  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 アップグレード アドバイザー&#91;新規&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
