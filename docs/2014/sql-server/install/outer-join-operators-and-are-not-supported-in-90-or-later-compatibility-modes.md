---
title: 外部結合演算子 *= および =* 互換性モード 90 以上でサポートされていません |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- outer joins
- =* join
- '*= join'
- joins [SQL Server]
ms.assetid: ca4aa11f-1048-411f-9c6c-3d0a8e319f2f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 62a6f9e016abf24f28660b04e7a6242fdd6606ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093684"
---
# <a name="outer-join-operators--and--are-not-supported-in-90-or-later-compatibility-modes"></a>互換性モード 90 以上では外部結合演算子 \*= および =\* がサポートされない
  アップグレード アドバイザーには、外部結合演算子の使用が検出しました\*= および =\*します。 このような演算子は互換性モード 90 以上ではサポートされません。 アップグレードすると、ユーザー データベースでは互換性モードが維持されます。 これらの演算子を使用するステートメントは失敗します。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>修正措置  
 データベース互換性モード 90 以上に変更すると、前に変更して、外部結合演算子を使用するステートメント\*= および =\*同等の OUTER JOIN キーワードを使用します。 次の例では、`\*=` 演算子を使用するクエリと、`LEFT OUTER JOIN` キーワードを使用する同等のクエリを示しています。  
  
```  
-- This query uses an old-style outer join operator.  
USE pubs  
SELECT employee.job_id, employee.emp_id,  
   employee.fname, employee.minit, jobs.job_desc  
FROM employee, jobs   
WHERE employee.job_id *= jobs.job_id  
ORDER BY employee.job_id  
  
-- This query uses the ANSI standard keywords LEFT OUTER JOIN.  
USE pubs;  
SELECT employee.job_id, employee.emp_id,  
   employee.fname, employee.minit, jobs.job_desc  
FROM employee LEFT OUTER JOIN jobs ON   
    employee.job_id = jobs.job_id  
ORDER BY employee.job_id  
```  
  
 詳細については、SQL Server オンライン ブックの「外部結合の使用」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 アップグレード アドバイザー&#91;新規&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
