---
title: マークされたトランザクションを含む関連データベースの復旧
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], marks
- STOPBEFOREMARK option [RESTORE statement]
- STOPATMARK option [RESTORE statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
- recovery [SQL Server], databases
- restoring [SQL Server], point in time
- transactions [SQL Server], recovering to a mark
- database recovery [SQL Server]
- marked transactions [SQL Server], restoring
- database restores [SQL Server], point in time
ms.assetid: 77a0d9c0-978a-4891-8b0d-a4256c81c3f8
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 002b5e92c94abece7ea935cb06985a51b78e98c4
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75238890"
---
# <a name="recovery-of-related--databases-that-contain-marked-transaction"></a>マークされたトランザクションを含む関連データベースの復旧
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックは、マークされたトランザクションが含まれており、完全復旧モデルまたは一括ログ復旧モデルを使用するデータベースのみに関連しています。  
  
 特定の復旧ポイントまでの復元するための要件については、「 [SQL Server データベースを特定の時点に復元する &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] トランザクション ログに名前付きマークを挿入することによって、その特定のマークの時点に復旧できます。 ログ マークはトランザクションに固有で、関連するトランザクションがコミットされる場合のみ挿入されます。 このため、マークを特定の操作に結び付けることが可能で、この操作を含む時点または含まない時点に復旧できます。  
  
 名前付きマークをトランザクション ログに挿入する前に、次の点を考慮してください。  
  
-   トランザクション マークはログ領域を使用するので、データベース復旧ストラテジにおいて重要な役割を果たすトランザクションだけに使用する必要があります。  
  
-   マークされたトランザクションのコミットが完了したら、 [msdb](../../relational-databases/system-tables/logmarkhistory-transact-sql.md) の **logmarkhistory**テーブルに 1 行が挿入されます。  
  
-   マークされたトランザクションが同じデータベース サーバーまたは異なるサーバー上の複数のデータベースと関係している場合は、影響を受けたすべてのデータベースのログにそのマークが記録される必要があります。 詳細については、「 [マークされたトランザクションを使用して関連するデータベースを一貫した状態に復元する方法 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)」を参照してください。  
  
> [!NOTE]  
>  トランザクションをマークする方法の詳細については、「 [マークされたトランザクションを使用して関連するデータベースを一貫した状態に復元する方法 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)」を参照してください。  
  
## <a name="transact-sql-syntax-for-inserting-named-marks-into-a-transaction-log"></a>名前付きマークをトランザクション ログに挿入するための Transact-SQL 構文  
 トランザクション ログにマークを挿入するには、 [BEGIN TRANSACTION](../../t-sql/language-elements/begin-transaction-transact-sql.md) ステートメントと WITH MARK [*description*] 句を使用します。 マークの名前はトランザクションの名前と同じです。 省略可能な *description* は、マークの名前ではなく、マークの説明テキストです。 たとえば、次の `BEGIN TRANSACTION` ステートメントで作成されるトランザクションとマークは、いずれも名前が `Tx1`になります。  
  
```wmimof  
BEGIN TRANSACTION Tx1 WITH MARK 'not the mark name, just a description'    
```  
  
 トランザクション ログには、マーク名 (トランザクション名)、説明、データベース、ユーザー、 **datetime** 情報、および LSN (ログ シーケンス番号) が記録されます。 マーク名に **datetime** 情報を使用することで、マークが一意に識別されます。  
  
 複数のデータベースに関係するトランザクションにマークを挿入する方法については、「 [マークされたトランザクションを使用して関連するデータベースを一貫した状態に復元する方法 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)」を参照してください。  
  
## <a name="transact-sql-syntax-for-recovering-to-a-mark"></a>特定のマークの時点へ復旧するための Transact-SQL 構文  
 マークされたトランザクションを[RESTORE LOG](../../t-sql/statements/restore-statements-transact-sql.md)ステートメントで指定する場合、次のいずれかの句を使用して、マークに到達した時点またはマークの直前まで復旧できます。  
  
-   WITH STOPATMARK = **'** _<mark_name>_ **'** 句を使用して、マークされたトランザクションが復旧ポイントであることを指定します。  
  
     STOPATMARK では、マークまでロールフォワードされます。ロールフォワードには、マークされたトランザクションも含まれます。  
  
-   WITH STOPBEFOREMARK = **'** _<mark_name>_ **'** 句を使用して、マークの直前のログ レコードが復旧ポイントであることを指定します。  
  
     STOPBEFOREMARK では、マークまでロールフォワードされますが、マークされたトランザクションは含まれません。  
  
 STOPATMARK オプションと STOPBEFOREMARK オプションは両方とも、省略可能な AFTER *datetime* 句をサポートしています。 *datetime* を使用する場合、マーク名を一意にする必要はありません。  
  
 AFTER *datetime* の指定を省略すると、指定した名前を持つ最初のマークでロールフォワードが停止します。 AFTER *datetime* を指定すると、 *datetime*以降の指定した名前を持つ最初のマークでロールフォワードが停止します。  
  
> [!NOTE]  
>  時間を指定したすべての復元操作と同様に、一括ログ記録の対象となる操作がデータベースで実行されている場合は、マーク時点に復旧できません。  
  
 **マークされたトランザクションまで復旧するには**  
  
 [マークされたトランザクションへのデータベースの復元 &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
### <a name="preparing-the-log-backups"></a>ログ バックアップの準備  
 この例の場合、関連データベースに適切なバックアップ方法は次のようになります。  
  
1.  両方のデータベースで完全復旧モデルを使用します。  
  
2.  各データベースの完全バックアップを作成します。  
  
     データベースは順次と同時の両方でバックアップできます。  
  
3.  トランザクション ログをバックアップする前に、すべてのデータベースで実行されるトランザクションにマークを付けます。 マークされたトランザクションを作成する方法の詳細については、「 [マークされたトランザクションを使用して関連するデータベースを一貫した状態に復元する方法 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)」を参照してください。  
  
4.  各データベースでトランザクション ログをバックアップします。  
  
### <a name="recovering-the-database-to-a-marked-transaction"></a>マークされたトランザクションへのデータベースの復旧  
 **バックアップを復元するには**  
  
1.  可能であれば、壊れていないデータベースの [ログ末尾のバックアップ](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) を作成します。  
  
2.  各データベースの最新の完全バックアップを復元します。  
  
3.  すべてのトランザクション ログ バックアップで使用できるマークされた最新のトランザクションを識別します。 この情報は、各サーバー上の **msdb** データベースの **logmarkhistory** テーブルに格納されています。  
  
4.  そのマークが格納されているすべての関連データベースのログ バックアップを識別します。  
  
5.  それぞれのログ バックアップを復元し、マーク付きトランザクションで停止します。  
  
6.  各データベースを復旧します。  
  
## <a name="see-also"></a>参照  
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [マークされたトランザクションを使用して関連するデータベースを一貫した状態に復元する方法 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)   
 [復元と復旧の概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [SQL Server データベースを特定の時点に復元する方法 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [復元シーケンスの計画と実行 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/plan-and-perform-restore-sequences-full-recovery-model.md)  
  
  
