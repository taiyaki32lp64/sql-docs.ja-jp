---
title: 複数のジョブ ステップの処理 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 800318df9945b674f3e0777f6c53b67b71ba61a9
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262402"
---
# <a name="handle-multiple-job-steps"></a>複数のジョブ ステップの処理
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

ジョブに複数のジョブ ステップがある場合、ジョブ ステップを実行する順序を指定する必要があります。 この順序指定を "*フロー制御*" と呼びます。 いつでも新しいジョブ ステップを追加して、フローを再構成できます。変更が有効になるのは、次にジョブを実行するときです。 次の図は、データベース バックアップ ジョブのフロー制御を示しています。  
  
![SQL Server エージェントのジョブ ステップのフロー制御](../../ssms/agent/media/dbflow01.gif "SQL Server エージェントのジョブ ステップのフロー制御")  
  
最初のステップは "データベースのバックアップ" です。 このステップが失敗すると、通知を受け取るオペレーターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントから失敗が報告されます。 "データベースのバックアップ" ステップに成功すると、次のステップの "顧客データのスクラビング" に進みます。 このステップに失敗すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントにより "データベースの復元" までスキップされます。 "顧客データのスクラビング" に成功すると、次のステップの "統計の更新" に進みます。以降、最後のステップが "レポート成功" または "レポート失敗" になるまで続きます。  
  
各ジョブ ステップの成功と失敗に対して、フロー制御アクションを定義します。 ジョブ ステップが成功した場合のアクション、およびジョブ ステップが失敗した場合のアクションを指定する必要があります。 また、失敗したジョブ ステップに対して、再試行の回数とその間隔を定義することもできます。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのグラフィカル ユーザー インターフェイス (GUI) を使用し、複数のステップのジョブから 1 つ以上のステップを削除する場合、GUI では、すべてのジョブ ステップを削除してから、修正された成功時または失敗時の参照で、残りのステップを戻します。 たとえば 5 つのステップのジョブがあり、最初のステップが正常に終了した場合には、ステップ 4 に移動するように構成されているとします。 ステップ 3 を削除する場合、GUI ではこのジョブのすべてのステップを削除し、残りの 4 つのステップ (1、2、4、および 5) を修正した参照と共に追加します。 この場合、ステップ 1 の参照は、ステップ 1 が正常に終了したらステップ 3 に移動するように再構成されます。  
  
ジョブ ステップは自己完結型である必要があります。 つまり、ジョブ ステップ間でブール値、データ、または数値を受け渡すことはできません。 ただし、パーマネント テーブルまたはグローバル一時テーブルを使用することで、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ジョブ ステップ間で値を受け渡すことができます。 実行可能プログラムを実行するジョブ ステップの値をジョブ ステップ間で受け渡すには、ファイルを使用します。 たとえば、あるジョブ ステップで実行される実行可能プログラムでファイルに書き込み、後続のジョブ ステップで実行される実行可能プログラムでそのファイルを読み取ります。  
  
> [!NOTE]  
> ジョブ ステップ 1 の次にジョブ ステップ 2 が続き、ジョブ ステップ 2 の次にジョブ ステップ 1 に戻るような、ループするジョブ ステップを作成した場合は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でそのジョブを作成したときに警告メッセージが表示されます。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントにより、ジョブとジョブ ステップの情報がジョブ履歴に記録されます。  
  
## <a name="see-also"></a>参照  
[sp_add_job](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)  
[sysjobhistory](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
[sysjobs (Transact-SQL)](https://msdn.microsoft.com/e244a6a5-54c2-47a6-8039-dd1852b0ae59)  
[sysjobsteps](../../relational-databases/system-tables/dbo-sysjobsteps-transact-sql.md)  
[ジョブの実装](../../ssms/agent/implement-jobs.md)  
[ジョブ ステップの管理](../../ssms/agent/manage-job-steps.md)  
  
