---
title: トリガーの入れ子が OFF の場合に入れ子になった AFTER トリガーが起動されます |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- DML triggers, nested
- nested triggers option
- triggers [SQL Server], nested
ms.assetid: 94d72960-676e-40d9-81bc-08bffe778110
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0675c412d753a1ce60fa41c7ced40528b3c58f75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093826"
---
# <a name="nested-after-trigger-fires-even-when-trigger-nesting-is-off"></a>トリガーの入れ子がオフになっている場合でも、入れ子になった AFTER トリガーが起動される
  アップグレード アドバイザーによって、1 つ以上のテーブルで定義されている INSTEAD OF トリガー内に入れ子になった AFTER トリガーが検出されました。 入れ子になった AFTER トリガーは、`nested triggers` サーバー構成オプションが 0 に設定されている場合でも起動されることがあります。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>説明  
 最初の AFTER トリガーが INSTEAD OF トリガーが起動場合であっても内部で入れ子になった、`nested triggers`サーバー構成オプションが 0 に設定します。 ただし、この設定では、後続の AFTER トリガーは起動されません。  
  
## <a name="corrective-action"></a>修正措置  
 アプリケーションに入れ子になったトリガーがないかどうかを調査し、`nested triggers` サーバー構成オプションが 0 に設定されている場合の新しい動作に関して、アプリケーションがビジネス ルールに従っているかどうかを判断します。その後、適切な変更を加えてください。  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 アップグレード アドバイザー&#91;新規&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
