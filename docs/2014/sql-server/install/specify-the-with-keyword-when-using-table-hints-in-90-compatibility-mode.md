---
title: 互換性モードが 90 でテーブル ヒントを使用する場合は、WITH キーワードを指定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- WITH keyword
- table hints [SQL Server]
ms.assetid: 7636cc85-5155-44db-baf6-df807761adb8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ff2fee26c6f71cc398f8dbacf91f3ad8dbdb3358
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092158"
---
# <a name="specify-the-with-keyword-when-using-table-hints-in-90-compatibility-mode"></a>互換性モード 90 ではテーブル ヒントを使用するときに WITH キーワードを指定する
  例外がいくつかありますが、テーブル ヒントは WITH キーワードを使用して指定された場合のみクエリの FROM 句でサポートされます。 詳細については、[!INCLUDE[tsql](../../includes/tsql-md.md)] オンライン ブックの「FROM ([!INCLUDE[tsql](../../includes/tsql-md.md)])」および「テーブル ヒント ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])」を参照してください。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>修正措置  
 テーブル ヒントの前に WITH キーワードを含めることによって、テーブル ヒントを FROM 句に含めてクエリを変更します。  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 アップグレード アドバイザー&#91;新規&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
