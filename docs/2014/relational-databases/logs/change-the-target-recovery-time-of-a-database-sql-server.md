---
title: データベースのターゲットの復旧時間の変更 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: e466419a-d8a4-48f7-8d97-13a903ad6b15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 72ac6ac92da531d0f653e0fc03d88d170b7706e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62743218"
---
# <a name="change-the-target-recovery-time-of-a-database-sql-server"></a>データベースのターゲットの復旧時間の変更 (SQL Server)
  このトピックでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の [!INCLUDE[tsql](../../includes/tsql-md.md)] データベースのターゲットの復旧時間を変更する方法について説明します。 既定では、ターゲットの復旧時間は 0 で、データベースは *自動チェックポイント* ( **復旧間隔** サーバー オプションによって制御されます) を使用します。 ターゲットの復旧時間を 0 より大きい値に設定すると、データベースは *間接的なチェックポイント* を使用するようになり、このデータベースの復旧時間に上限を設定します。  
  
> [!NOTE]  
>  ターゲットの復旧時間の設定によって特定のデータベースに対して指定された上限は、実行時間の長いトランザクションによって UNDO が過度に繰り返される場合には超過することがあります。  
  
-   **作業を開始する準備:** [制限事項と制約事項](#Restrictions)、[セキュリティ](#Security)  
  
-   **ターゲットの復旧時間を変更するには:** [SQL Server Management Studio](#SSMSProcedure) または [Transact-SQL](#TsqlProcedure) を使用  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a>  
  
> [!CAUTION]  
>  間接チェックポイントが構成されたデータベースでオンライン トランザクション ワークロードが生じると、パフォーマンスが低下することがあります。 間接チェックポイントは、ターゲットの復旧時間内でデータベースの回復が完了するように、ダーティ ページの数が特定のしきい値を下回るようにします。 復旧間隔構成オプションは、ダーティ ページ数を使用する間接チェックポイントとは異なり、トランザクション数を使用して復旧時間を決定します。 DML 操作の受信数が多いデータベースで間接チェックポイントが有効な場合、バックグラウンド ライターは積極的にディスクにダーティ バッファーのフラッシュを開始し、回復を実行するのに必要な時間をデータベースのターゲット復旧時間内にすることができます。 これにより、ディスクのサブシステムが I/O のしきい値よりも高い動作をするかまたはその値に近づいた場合、パフォーマンス ボトルネックの原因となる追加の I/O アクティビティが特定のシステムで発生する可能性があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 データベースに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **ターゲットの復旧時間を変更するには**  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  変更するデータベースを右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[データベースのプロパティ]** ダイアログ ボックスで、 **[オプション]** ページをクリックします。  
  
4.  **[復旧]** パネルの **[ターゲットの復旧時間 (秒)]** フィールドで、このデータベースの復旧時間の上限にする秒数を指定します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **ターゲットの復旧時間を変更するには**  
  
1.  データベースがある [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続します。  
  
2.  次の [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options)ステートメントを、次のように使用します。  
  
     TARGET_RECOVERY_TIME **=** _target_recovery_time_ { SECONDS | MINUTES }  
  
     *target_recovery_time*  
     0 (既定値) より大きい値の場合は、指定されたデータベースでクラッシュが発生したときの復旧時間に上限を指定します。  
  
     SECONDS  
     *target_recovery_time* が秒単位で表されていることを示します。  
  
     MINUTES  
     *target_recovery_time* が分単位で表されていることを示します。  
  
     次の例では、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースのターゲットの復旧時間を `60` 秒に設定します。  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET TARGET_RECOVERY_TIME = 60 SECONDS;  
    ```  
  
## <a name="see-also"></a>参照  
 [データベース チェックポイント &#40;SQL Server&#41;](database-checkpoints-sql-server.md)   
 [ALTER DATABASE SET Options &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
  
