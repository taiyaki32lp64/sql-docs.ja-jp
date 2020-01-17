---
title: ALTER DATABASE SET HADR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET HADR
- SET_HADR_TSQL
- HADR_TSQL
- HADR
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER DATABASE statement, AlwaysOn Availability Group
- ALTER DATABASE statement, SET HADR options
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], Transact-SQL statements
- Availability Groups [SQL Server], databases
ms.assetid: 20e6e803-d6d5-48d5-b626-d1e0a73d174c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 43970780903aa0a4d5aef84f971ac230f2f26358
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065731"
---
# <a name="alter-database-transact-sql-set-hadr"></a>ALTER DATABASE (Transact-SQL) SET HADR 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  このトピックには、セカンダリ データベースで [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] オプションを設定するための ALTER DATABASE 構文が含まれています。 ALTER DATABASE ステートメントごとに SET HADR オプションが 1 つだけ許可されます。 これらのオプションは、セカンダリ レプリカ上でのみサポートされます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER DATABASE database_name  
   SET HADR   
   {  
        { AVAILABILITY GROUP = group_name | OFF }  
   | { SUSPEND | RESUME }  
   }  
[;]  
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 変更するセカンダリ データベースの名前です。  
  
 SET HADR  
 指定したデータベース上で指定した [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] コマンドを実行します。  
  
 { AVAILABILITY GROUP **=** _group_name_ | OFF }  
 次のように、指定した可用性グループから可用性データベースを削除するか、指定した可用性グループに参加させます。  
  
 *group_name*  
 指定したデータベースをセカンダリ レプリカ上で参加させます。このレプリカは、group_name で指定された可用性グループに対してコマンドを実行するサーバー インスタンスによってホストされています。  
  
 この操作の前提条件は以下のとおりです。  
  
-   データベースは既にプライマリ レプリカ上の可用性グループに追加されている必要があります。  
  
-   プライマリ レプリカがアクティブになっている必要があります。 非アクティブなプライマリ レプリカのトラブルシューティング方法の詳細については、「[AlwaysOn 可用性グループの構成のトラブルシューティング (SQL Server)](https://go.microsoft.com/fwlink/?LinkId=225834)」を参照してください。  
  
-   プライマリ レプリカがオンラインになっており、セカンダリ レプリカがプライマリ レプリカに接続されている必要があります。  
  
-   セカンダリ データベースは、プライマリ データベースの最新のデータベースとログ バックアップから WITH NORECOVERY を使用して復元されている必要があります。これは、セカンダリ データベースがプライマリ データベースからの遅れを取り戻せるように最新のログ バックアップで終わっている必要があります。  
  
    > [!NOTE]  
    >  データベースを可用性グループに追加するには、プライマリ レプリカをホストするサーバー インスタンスに接続し、[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)*group_name* ADD DATABASE *database_name* ステートメントを使用します。  
  
 詳細については、「 [可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)のインスタンスに AlwaysOn 可用性グループを作成する方法について説明します。  
  
 OFF  
 指定したセカンダリ データベースを可用性グループから削除します。  
  
 セカンダリ データベースがプライマリ データベースから大幅に遅れており、セカンダリ データベースが遅れを取り戻すまで待てない場合は、セカンダリ データベースを削除することをお勧めします。 セカンダリ データベースを削除した後、最新のログ バックアップで終わる一連のバックアップを復元することで、セカンダリ データベースを更新できます (次の構文を使用: RESTORE ...WITH NORECOVERY)。  
  
> [!IMPORTANT]  
>  可用性グループから可用性データベースを完全に削除するには、プライマリ可用性レプリカをホストするサーバー インスタンスに接続し、[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)*group_name* REMOVE DATABASE *availability_database_name* ステートメントを使用します。 詳細については、「[可用性グループからのプライマリ データベースの削除 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)」をご覧ください。  
  
 SUSPEND  
 セカンダリ データベース上でデータ移動を中断します。 SUSPEND コマンドは、対象のデータベースをホストするレプリカによって受け付けられるとすぐに戻りますが、実際にはデータベースの中断が非同期に行われます。  
  
 その影響の範囲は、ALTER DATABASE ステートメントを実行する場所によって異なります。  
  
-   セカンダリ レプリカ上のセカンダリ データベースを中断した場合、ローカルのセカンダリ データベースのみが中断されます。 読み取り可能なセカンダリ上の既存の接続は、引き続き使用できます。 読み取り可能なセカンダリ上で中断されたデータベースに対する新しい接続は、データ移動が再開されるまでは許可されません。  
  
-   プライマリ レプリカ上のデータベースを中断した場合、すべてのセカンダリ レプリカ上の対応するセカンダリ データベースへのデータ移動が中断されます。 読み取り可能なセカンダリの既存の接続は引き続き利用できます。新しい読み取り目的の接続は、読み取り可能なセカンダリ レプリカに接続しません。  
  
-   データ移動が強制的な手動フェールオーバーによって中断された場合、新しいセカンダリ レプリカへの接続は、データ移動が中断している間は許可されません。  
  
 セカンダリ レプリカ上のデータベースを中断した場合、データベースとレプリカは同期されなくなり、NOT SYNCHRONIZED とマークされます。  
  
> [!IMPORTANT]  
>  セカンダリ データベースが中断されている間、対応するプライマリ データベースの送信キューが未送信トランザクション ログ レコードに蓄積されます。 セカンダリ レプリカへの接続では、データ移動が中断されたときに使用可能であったデータが返されます。  
  
> [!NOTE]  
>  AlwaysOn セカンダリ データベースの中断と再開は、プライマリ データベースの可用性に直接は影響しませんが、セカンダリ データベースの中断から再開までに、プライマリ データベースの冗長性とフェールオーバー機能に影響する場合があります。 ミラーリングの場合はこれと異なり、ミラーリングが再開されるまで、ミラーリングの状態はミラー データベースでもプリンシパル データベースでも中断になります。 Always On プライマリ データベースを中断すると、対応するすべてのセカンダリ データベースでデータ移動が中断され、そのデータベースの冗長性とフェールオーバー機能はプライマリ データベースが再開されるまで停止されます。  
  
 詳細については、「[可用性データベースの中断 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/suspend-an-availability-database-sql-server.md)」を参照してください。  
  
 RESUME  
 指定したセカンダリ データベース上で中断されたデータ移動を再開します。 RESUME コマンドは、対象のデータベースをホストするレプリカによって受け付けられるとすぐに戻りますが、実際にはデータベースの再開が非同期に行われます。  
  
 その影響の範囲は、ALTER DATABASE ステートメントを実行する場所によって異なります。  
  
-   セカンダリ レプリカ上のセカンダリ データベースを再開した場合、ローカルのセカンダリ データベースのみが再開されます。 データ移動は、データベースがプライマリ レプリカでも中断されている場合を除き、再開されます。  
  
-   プライマリ レプリカ上のデータベースを再開した場合、対応するセカンダリ データベースがローカルに中断されていないすべてのセカンダリ レプリカへのデータ移動が再開されます。 セカンダリ レプリカ上で個別に中断されたセカンダリ データベースを再開するには、セカンダリ レプリカをホストするサーバー インスタンスに接続し、そこでデータベースを再開します。  
  
     同期コミット モードでは、データベースの状態が SYNCHRONIZING に変わります。 他のデータベースが現在中断されていない場合は、レプリカの状態も SYNCHRONIZING に変わります。  
  
     詳細については、このトピックの「 [可用性データベースの再開 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/resume-an-availability-database-sql-server.md)の可用性データベースを中断できます。  
  
## <a name="database-states"></a>データベースの状態  
 セカンダリ データベースを可用性グループに参加させると、ローカル セカンダリ レプリカのセカンダリ データベースの状態が RESTORING から ONLINE に変わります。 セカンダリ データベースを可用性グループから削除すると、その状態はローカル セカンダリ レプリカによって RESTORING に戻ります。 これにより、プライマリ データベースからの後続のログ バックアップをそのセカンダリ データベースに適用できます。  
  
## <a name="restrictions"></a>制限  
 トランザクションとバッチの外で ALTER DATABASE ステートメントを実行します。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 データベースに対する ALTER 権限が必要です。 データベースを可用性グループに参加させるには、**db_owner** 固定データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、セカンダリ データベース `AccountsDb1` を、`AccountsAG` 可用性グループのローカル セカンダリ レプリカに参加させます。  
  
```  
ALTER DATABASE AccountsDb1 SET HADR AVAILABILITY GROUP = AccountsAG;  
```  
  
> [!NOTE]  
>  コンテキストで使用するこの [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを確認するには、「[可用性グループの作成 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) [AlwaysOn 可用性グループの構成のトラブルシューティング &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md) 
  
  
