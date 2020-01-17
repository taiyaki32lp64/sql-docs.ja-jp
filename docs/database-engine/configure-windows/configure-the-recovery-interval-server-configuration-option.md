---
title: recovery interval サーバー構成オプションの構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- restoring recovery interval [SQL Server]
- checkpoints [SQL Server]
- recovery interval option [SQL Server]
- default recovery interval option
- time [SQL Server], recovery interval
- interval for recovery [SQL Server]
- maximum number of minutes per database recovery
- recovery [SQL Server], recovery interval option
ms.assetid: e4734b3b-8fbe-4b65-9c48-91b5a3dd18e1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4014060d393e4af5ec9739cdd2487d7920195266
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68012347"
---
# <a name="configure-the-recovery-interval-server-configuration-option"></a>recovery interval サーバー構成オプションの構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックでは、 **または** を使用して、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] recovery interval [!INCLUDE[tsql](../../includes/tsql-md.md)]サーバー構成オプションを構成する方法について説明します。 **recovery interval** オプションは、データベースの復旧に必要な時間の上限を定義します。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] は、このオプションに指定された値を使って、[自動チェックポイント](../../relational-databases/logs/database-checkpoints-sql-server.md)が特定のデータベースに対して発行されるおおよその頻度を決定します。  
  
 recovery-interval の既定値は 0 で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] によって自動的に復旧間隔が構成されます。 既定の recovery interval では、通常、アクティブなデータベースの自動チェックポイントの発生間隔は約 1 分、復旧時間は 1 分未満になります。 既定値より大きな値は、おおよその最大リカバリ時間 (分単位) を示します。 たとえば、recovery interval を '3' に設定した場合は、最大リカバリ時間は約 3 分になります。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
     [セキュリティ](#Security)  
  
-   **recovery interval サーバー構成オプションを構成する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [recovery interval オプションを構成した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   recovery interval が作用するのは、既定のターゲット復旧時間 (0) を使用するデータベースだけです。 データベース上のサーバー復旧間隔をオーバーライドするには、データベースの既定のターゲット復旧時間を既定以外の値に変更します。 詳細については、「 [データベースのターゲットの復旧時間の変更 &#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)サーバー構成オプションを構成する方法について説明します。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   このオプションは詳細設定オプションであるため、熟練したデータベース管理者または認定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロフェッショナルだけが変更するようにしてください。  
  
-   通常は、パフォーマンス上の問題が発生する場合を除いて、recovery interval は 0 のままにすることをお勧めします。 recovery interval 設定を長くする場合には、少しずつ値を増やして、そのたびに復旧のパフォーマンスへの影響を評価することをお勧めします。  
  
-   **sp_configure** を使用し、**recovery interval** オプションの値を 60 (分) よりも大きくするには、RECONFIGURE WITH OVERRIDE を指定する必要があります。 WITH OVERRIDE は、構成値のチェック (無効な値や非推奨値のチェック) を無効にします。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 パラメーターなしで、または最初のパラメーターだけを指定して **sp_configure** を実行する権限は、既定ですべてのユーザーに付与されます。 両方のパラメーターを指定して **sp_configure** を実行し構成オプションを変更したり RECONFIGURE ステートメントを実行したりするには、ALTER SETTINGS サーバーレベル権限がユーザーに付与されている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **復旧間隔を設定するには**  
  
1.  オブジェクト エクスプローラーでサーバー インスタンスを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[データベースの設定]** ノードをクリックします。  
  
3.  **[復旧]** の **[復旧間隔 (分単位)]** ボックスで、0 ～ 32767 の値を入力するか選択して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が起動時に各データベースの復旧に要する最大時間を分単位で設定します。 既定値は 0 です。0 の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって自動的に構成されます。 実際には、復旧時間が 1 分未満で、アクティブなデータベースのチェックポイントは約 1 分間隔になります。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-set-the-recovery-interval"></a>復旧間隔を設定するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) を使用して、 `recovery interval` オプションの値を `3` 分に設定する方法を示します。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'recovery interval', 3 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 詳細については、「 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)」を参照してください。  
  
##  <a name="FollowUp"></a>補足情報: recovery internal オプションを構成した後  
 新しい設定は、サーバーを再起動しなくてもすぐに有効になります。  
  
## <a name="see-also"></a>参照  
 [データベースのターゲットの復旧時間の変更 &#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)   
 [データベース チェックポイント &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [show advanced options サーバー構成オプション](../../database-engine/configure-windows/show-advanced-options-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
