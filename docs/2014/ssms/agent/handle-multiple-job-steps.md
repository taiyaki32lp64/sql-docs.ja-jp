---
title: 複数のジョブ ステップの処理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [SQL Server Agent]
- ordering job steps [SQL Server]
- multiple job steps
- SQL Server Agent jobs, job steps
- control of flow for jobs [SQL Server]
ms.assetid: 7aba19ff-72b3-45f6-8e54-23f4988d63a8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 379877d3a08c60a293b96c5c57d55a2894ba0a79
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63074057"
---
# <a name="handle-multiple-job-steps"></a>複数のジョブ ステップの処理
  ジョブに複数のジョブ ステップがある場合、ジョブ ステップを実行する順序を指定する必要があります。 この順序指定を*フロー制御*と呼びます。 いつでも新しいジョブ ステップを追加して、フローを再構成できます。変更が有効になるのは、次にジョブを実行するときです。 次の図は、データベース バックアップ ジョブのフロー制御を示しています。  
  
 ![SQL Server エージェントのジョブ ステップのフロー制御](../../database-engine/media/dbflow01.gif "SQL Server エージェントのジョブ ステップのフロー制御")  
  
 最初のステップは "データベースのバックアップ" です。 このステップが失敗すると、通知を受け取るオペレーターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントから失敗が報告されます。 "データベースのバックアップ" ステップに成功すると、次のステップの "顧客データのスクラビング" に進みます。 このステップに失敗すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントにより "データベースの復元" までスキップされます。 "顧客データのスクラビング" に成功すると、次のステップの "統計の更新" に進みます。以降、最後のステップが "レポート成功" または "レポート失敗" になるまで続きます。  
  
 各ジョブ ステップの成功と失敗に対して、フロー制御アクションを定義します。 ジョブ ステップが成功した場合のアクション、およびジョブ ステップが失敗した場合のアクションを指定する必要があります。 また、失敗したジョブ ステップに対して、再試行の回数とその間隔を定義することもできます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのグラフィカル ユーザー インターフェイス (GUI) を使用し、複数のステップのジョブから 1 つ以上のステップを削除する場合、GUI では、すべてのジョブ ステップを削除してから、修正された成功時または失敗時の参照で、残りのステップを戻します。 たとえば 5 つのステップのジョブがあり、最初のステップが正常に終了した場合には、ステップ 4 に移動するように構成されているとします。 ステップ 3 を削除する場合、GUI ではこのジョブのすべてのステップを削除し、残りの 4 つのステップ (1、2、4、および 5) を修正した参照と共に追加します。 この場合、ステップ 1 の参照は、ステップ 1 が正常に終了したらステップ 3 に移動するように再構成されます。  
  
 ジョブ ステップは自己完結型である必要があります。 つまり、ジョブ ステップ間でブール値、データ、または数値を受け渡すことはできません。 ただし、パーマネント テーブルまたはグローバル一時テーブルを使用することで、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ジョブ ステップ間で値を受け渡すことができます。 実行可能プログラムを実行するジョブ ステップの値をジョブ ステップ間で受け渡すには、ファイルを使用します。 たとえば、あるジョブ ステップで実行される実行可能プログラムでファイルに書き込み、後続のジョブ ステップで実行される実行可能プログラムでそのファイルを読み取ります。  
  
> [!NOTE]  
>  ジョブ ステップ 1 の次にジョブ ステップ 2 が続き、ジョブ ステップ 2 の次にジョブ ステップ 1 に戻るような、ループするジョブ ステップを作成した場合は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でそのジョブを作成したときに警告メッセージが表示されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントにより、ジョブとジョブ ステップの情報がジョブ履歴に記録されます。  
  
## <a name="see-also"></a>関連項目  
 [sp_add_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql)   
 [dbo.sysjobhistory &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-tables/dbo-sysjobhistory-transact-sql)   
 [dbo.sysjobs &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-tables/dbo-sysjobs-transact-sql)   
 [dbo.sysjobsteps &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-tables/dbo-sysjobsteps-transact-sql)   
 [ジョブの実装](implement-jobs.md)   
 [ジョブ ステップの管理](manage-job-steps.md)  
  
  
