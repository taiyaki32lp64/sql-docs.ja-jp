---
title: 使用してマークされたトランザクションが一貫して関連するデータベースを回復する (完全復旧モデル) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- transaction marks [SQL Server]
- marked transactions [SQL Server]
- database restores [SQL Server], inserting transaction marks for
- recovery [SQL Server], related databases
- restoring databases [SQL Server], related database recovery
- database restores [SQL Server], related databases
- marked transactions [SQL Server], creating
- BEGIN TRAN...WITH MARK statement
- two-phase commit
ms.assetid: 50a73574-1a69-448e-83dd-9abcc7cb7e1a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 37b4a53461b2ebd485941ecad89e3672e7c31b62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62877071"
---
# <a name="use-marked-transactions-to-recover-related-databases-consistently-full-recovery-model"></a>マークされたトランザクションを使用して関連するデータベースを一貫した状態に復元する方法 (完全復旧モデル)
  このトピックは、完全復旧モデルまたは一括ログ復旧モデルを使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのみに関連しています。  
  
 関連する更新を複数のデータベース ( *関連データベース*) に対して実行する場合、トランザクション マークを使用して、それらのデータベースを論理的に一貫した状態に復旧できます。 ただし、この復旧により、復旧ポイントとして使用されていたマークより後にコミットされたトランザクションはすべて失われます。 マークされたトランザクションの使用が適しているのは、関連データベースをテストする場合や、最近コミットされたトランザクションが失われてもよい場合のみです。  
  
 すべての関連データベースの関連トランザクションに定期的にマークを付けることにより、これらのデータベースに共通する一連の復旧ポイントが作成されます。 これらのトランザクション マークはトランザクション ログに記録され、ログ バックアップに格納されます。 障害が発生した場合、各データベースを同じトランザクション マークまで復元し、一貫性のある状態に復旧できます。  
  
> [!NOTE]  
>  データベースのログ バックアップは、各データベースで別々に作成できるため、同時に作成する必要はありません。  
  
 次のシナリオで関連データベースを復旧するには、既にすべての関連データベースにマークされたトランザクションが含まれている必要があります。  
  
-   1 つ以上のトランザクション ログが壊れている。 データベースのセットを、最後のログ バックアップの時点の一貫性のある状態に復元する必要がある。  
  
-   データベースのセット全体を、以前の特定の時点の相互に一貫性のある状態に復元する必要がある。  
  
> [!IMPORTANT]  
>  関連データベースを復旧できるのは、特定の時点までではなく、マークが付けられたトランザクションまでに限られます。  
  
 マークされたトランザクションの作成方法の詳細については、このトピックの「マーク付きトランザクションの作成」を参照してください。  
  
## <a name="typical-scenario-for-using-marked-transactions"></a>マークされたトランザクションを使用するための一般的なシナリオ  
 マークされたトランザクションを使用するための一般的なシナリオでは、次の手順が実行されます。  
  
1.  各関連データベースの完全バックアップまたは差分バックアップを作成します。  
  
2.  すべてのデータベースのトランザクション ブロックにマークを付けます。  
  
3.  すべてのデータベースのトランザクション ログをバックアップします。  
  
4.  WITH NORECOVERY を指定してデータベース バックアップを復元します。  
  
5.  WITH STOPATMARK を指定してログを復元します。  
  
## <a name="considerations-for-using-marked-transactions"></a>マークされたトランザクションの使用に関する考慮事項  
 名前付きマークをトランザクション ログに挿入する前に、次の点を考慮してください。  
  
-   トランザクション マークはログ領域を使用するので、データベース復旧ストラテジにおいて重要な役割を果たすトランザクションだけに使用する必要があります。  
  
-   マークされたトランザクションのコミットが完了したら、 [msdb](/sql/relational-databases/system-tables/logmarkhistory-transact-sql) の **logmarkhistory**テーブルに 1 行が挿入されます。  
  
-   マークされたトランザクションが同じデータベース サーバーまたは異なるサーバー上の複数のデータベースと関係している場合は、影響を受けたすべてのデータベースのログにそのマークが記録される必要があります。  
  
## <a name="creating-the-marked-transactions"></a>マーク付きトランザクションの作成  
 マーク付きトランザクションを作成するには、 [BEGIN TRANSACTION](/sql/t-sql/language-elements/begin-transaction-transact-sql) ステートメントと WITH MARK [*description*] 句を使用します。 省略可能な *description* は、マークの説明テキストです。 トランザクションのマーク名が必要です。 マーク名は再利用できます。 トランザクション ログには、マーク名、説明、データベース、ユーザー、datetime 情報、および LSN (ログ シーケンス番号) が記録されます。 マーク名と共に datetime 情報を使用することで、マークが一意に識別されます。  
  
 **データベースのセットでマーク付きトランザクションを作成するには**  
  
1.  BEGIN TRAN ステートメントでトランザクションに名前を付け、WITH MARK 句を使用します。  
  
     BEGIN TRAN *new_mark_name* WITH MARK ステートメントは、既存のトランザクション内で入れ子にすることができます。 トランザクションに名前が付いている場合でも、 *new_mark_name* の値がそのトランザクションのマーク名になります。  
  
    > [!NOTE]  
    >  入れ子にした 2 番目の BEGIN TRAN...WITH MARK を実行すると、このステートメントはスキップされますが、警告メッセージは生成されます。  
  
2.  セット内のすべてのデータベースに対して更新を実行します。  
  
     BEGIN TRAN...WITH MARK ステートメントが実行されるサーバー インスタンス上でのみ、特定のトランザクションのマークがトランザクション ログに挿入されます。 トランザクション マークは、そのサーバー インスタンス上のマーク付きトランザクションによって更新されたすべてのデータベースのトランザクション ログに配置されます。 データベースが他のサーバー インスタンス上にある場合は、それらのサーバー インスタンスで同一のマークを作成する必要があります。  
  
### <a name="examples"></a>使用例  
 次の例では、トランザクション ログを `ListPriceUpdate`というマーク付きトランザクションのマークまで復元します。  
  
```sql  
USE AdventureWorks  
GO  
BEGIN TRANSACTION ListPriceUpdate  
   WITH MARK 'UPDATE Product list prices';  
GO  
  
UPDATE Production.Product  
   SET ListPrice = ListPrice * 1.10  
   WHERE ProductNumber LIKE 'BK-%';  
GO  
  
COMMIT TRANSACTION ListPriceUpdate;  
GO  
  
-- Time passes. Regular database   
-- and log backups are taken.  
-- An error occurs in the database.  
USE master  
GO  
  
RESTORE DATABASE AdventureWorks  
FROM AdventureWorksBackups  
WITH FILE = 3, NORECOVERY;  
GO  
  
RESTORE LOG AdventureWorks  
   FROM AdventureWorksBackups   
   WITH FILE = 4,  
   RECOVERY,   
   STOPATMARK = 'ListPriceUpdate';  
```  
  
## <a name="forcing-a-mark-to-spread-to-other-servers"></a>他のサーバーへのマークの強制波及  
 トランザクションが別のサーバーに波及しても、トランザクション マーク名はそのサーバーに自動的には分散されません。 他のサーバーにマークが広まるようにするには、BEGIN TRAN *name* WITH MARK ステートメントを含むストアド プロシージャを記述する必要があります。 このストアド プロシージャは、元のサーバーのトランザクションの範囲内においてリモート サーバー上で実行されなければなりません。  
  
 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の複数のインスタンスに存在するパーティション データベースを考えてください。 各インスタンスには、 `coyote`という名前のデータベースがあります。 まず、すべてのデータベースで `sp_SetMark`などのストアド プロシージャを作成します。  
  
```sql  
CREATE PROCEDURE sp_SetMark  
@name nvarchar (128)  
AS  
BEGIN TRANSACTION @name WITH MARK  
UPDATE coyote.dbo.Marks SET one = 1  
COMMIT TRANSACTION;  
GO  
```  
  
 次に、すべてのデータベースにマークを挿入するトランザクションを含んでいる、 `sp_MarkAll` というストアド プロシージャを作成します。 `sp_MarkAll` は、任意のインスタンスから実行できます。  
  
```sql  
CREATE PROCEDURE sp_MarkAll  
@name nvarchar (128)  
AS  
BEGIN TRANSACTION  
EXEC instance0.coyote.dbo.sp_SetMark @name  
EXEC instance1.coyote.dbo.sp_SetMark @name  
EXEC instance2.coyote.dbo.sp_SetMark @name  
COMMIT TRANSACTION;  
GO  
```  
  
### <a name="two-phase-commit"></a>2 フェーズ コミット (two-phase commit)  
 分散トランザクションのコミットは、準備とコミットという 2 つのフェーズで発生します。 マーク付きトランザクションがコミットされると、マーク付きトランザクション内の各データベースに関するコミット ログ レコードは、状況不明トランザクションがどのログにも含まれていない時点のログに挿入されます。 これにより、トランザクションのコミット状態がログごとに異なるなどの問題がなくなります。  
  
 この処理は、マーク付きトランザクションのコミット中に次の順で行われます。  
  
1.  マーク付きトランザクションの準備フェーズで、すべての新しい準備とコミットが停止します。  
  
2.  既に準備が完了しているトランザクションのコミットのみが、継続を許可されます。  
  
3.  マーク付きトランザクションは、タイムアウトによってすべての準備されたトランザクションがなくなるのを待ちます。  
  
4.  マーク付きのトランザクションが準備され、コミットされます。  
  
5.  新しい準備とコミットの停止が解除されます。  
  
 複数のデータベースにまたがるマーク付きトランザクションによって引き起こされた機能停止は、サーバーのトランザクション処理パフォーマンスを低下させる可能性があります。  
  
 複数のマーク付きトランザクションを同時に実行しないことをお勧めします。 実際にはあまりないことですが、分散されたマーク付きトランザクションのコミットが、同時にコミットされる他のマーク付き分散トランザクションによってデッドロックに陥ることがあります。 その場合、マーク付きトランザクションは、デッドロックの対象として選択され、ロールバックされます。 このエラーが発生した場合、アプリケーションではマーク付きトランザクションを再試行できます。 複数のマーク付きトランザクションのコミットが同時に試行されると、デッドロックが生じる可能性が高くなります。  
  
## <a name="recovering-to-a-marked-transaction"></a>マークされたトランザクションへの復旧  
 マークされたトランザクションを含むデータベースを特定のマークかその直前まで復旧する方法の詳細については、「 [マークされたトランザクションを使用して関連するデータベースを一貫した状態に復元する方法](recovery-of-related-databases-that-contain-marked-transaction.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/begin-distributed-transaction-transact-sql)   
 [システム データベースのバックアップと復元 &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/begin-transaction-transact-sql)   
 [トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [データベースの完全バックアップ &#40;SQL Server&#41;](full-database-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [マークされたトランザクションを使用して関連するデータベースを一貫した状態に復元する方法](recovery-of-related-databases-that-contain-marked-transaction.md)  
  
  
