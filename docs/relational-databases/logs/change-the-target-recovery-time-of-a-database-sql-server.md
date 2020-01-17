---
title: データベースのターゲットの復旧時間の変更
ms.custom: seo-lt-2019
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: e466419a-d8a4-48f7-8d97-13a903ad6b15
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 24a87adf77ea4217cb27b20d2452fcbd5ba26135
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056255"
---
# <a name="change-the-target-recovery-time-of-a-database-sql-server"></a>データベースのターゲットの復旧時間の変更 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の [!INCLUDE[tsql](../../includes/tsql-md.md)]データベースのターゲットの復旧時間を変更する方法について説明します。 既定では、ターゲットの復旧時間は 60 秒です。データベースで *間接チェックポイント*が使用されます。 ターゲットの復旧時間により、このデータベースの復旧時間に上限が設定されます。  
  
> [!NOTE]  
>  ターゲットの復旧時間の設定によって特定のデータベースに対して指定された上限は、実行時間の長いトランザクションによって UNDO が過度に繰り返される場合には超過することがあります。  
  
-   **作業を開始する準備:** [制限事項と制約事項](#Restrictions)、[セキュリティ](#Security)  
  
-   **ターゲットの復旧時間を変更するには:** [SQL Server Management Studio](#SSMSProcedure) または [Transact-SQL](#TsqlProcedure) を使用  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項 
  
> [!CAUTION]  
>  間接チェックポイントが構成されたデータベースでオンライン トランザクション ワークロードが生じると、パフォーマンスが低下することがあります。 間接チェックポイントは、ターゲットの復旧時間内でデータベースの回復が完了するように、ダーティ ページの数が特定のしきい値を下回るようにします。 復旧間隔構成オプションでは、ダーティ ページ数を使用する間接チェックポイントとは異なり、トランザクション数を使用して復旧時間を決定します。 DML 操作の受信数が多いデータベースで間接チェックポイントが有効な場合、バックグラウンド ライターでは積極的にディスクにダーティ バッファーのフラッシュを開始し、回復を実行するのに必要な時間をデータベースのターゲット復旧時間内にすることができます。 これにより、ディスクのサブシステムが I/O のしきい値を超えて、または近くで動作する場合にパフォーマンス ボトルネックの原因となる、追加の I/O アクティビティが特定のシステムで発生する可能性があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 データベースに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **ターゲットの復旧時間を変更するには**  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** コンテナーを展開してから、変更するデータベースを右クリックし、 **[プロパティ]** コマンドをクリックします。  
  
3.  **[データベースのプロパティ]** ダイアログ ボックスで、 **[オプション]** ページをクリックします。  
  
4.  **[復旧]** パネルの **[ターゲットの復旧時間 (秒)]** フィールドで、このデータベースの復旧時間の上限としての秒数を指定します。  

##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **ターゲットの復旧時間を変更するには**  
  
1.  データベースがある [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続します。  
  
2.  次の例に示すように、[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md) ステートメントを使用します。  
  
     TARGET_RECOVERY_TIME **=** _target_recovery_time_ { SECONDS | MINUTES }  
  
     *target_recovery_time*  
     [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]より、既定値は 1 分です。 0 (旧バージョンの既定値) より大きい値の場合は、指定されたデータベースでクラッシュが発生したときの復旧時間に上限を指定します。  
  
     SECONDS  
     *target_recovery_time* が秒単位で表されていることを示します。  
  
     MINUTES  
     *target_recovery_time* が分単位で表されていることを示します。  
  
     次の例では、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースのターゲットの復旧時間を `60` 秒に設定します。  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET TARGET_RECOVERY_TIME = 60 SECONDS;  
    ```  
  
## <a name="see-also"></a>参照  
 [データベース チェックポイント &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [ALTER DATABASE SET Options &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
