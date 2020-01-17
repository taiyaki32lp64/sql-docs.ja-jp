---
title: backup compression default サーバー構成オプションの表示または構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], backup compression default option
- backup compression [SQL Server], backup compression default Option
ms.assetid: 23029395-3e93-4c29-b7d6-e5a47a3526ff
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 139d5e3b2ec72917ed021fba005cacc306bce191
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945673"
---
# <a name="view-or-configure-the-backup-compression-default-server-configuration-option"></a>backup compression default サーバー構成オプションの表示または構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックでは、 **で** または [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] backup compression default [!INCLUDE[tsql](../../includes/tsql-md.md)]サーバー構成オプションを確認または構成する方法について説明します。 **backup compression default** オプションは、圧縮されたバックアップを既定で作成するかどうかを決定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールした場合、 **backup compression default** オプションはオフになっています。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
     [セキュリティ](#Security)  
  
-   **以下を使用して backup compression default オプションを表示および構成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [backup compression default オプションを構成した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   バックアップ圧縮は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディッションで使用できるわけではありません。 詳細については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
-   既定の設定では、圧縮によって CPU 使用率が著しく増加し、圧縮処理によって CPU がさらに消費されるために、同時に実行される操作が悪影響を受ける場合があります。 このため、 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)によって CPU 使用率が制限されるセッションでは、優先度の低い圧縮バックアップを作成することができます。 詳細については、「 [リソース ガバナーを使用してバックアップの圧縮による CPU 使用率を制限する方法 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)」を参照してください。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   個別のバックアップを作成する場合、ログ配布構成を構成する場合、またはメンテナンス プランを作成する場合は、サーバー レベルの既定値をオーバーライドできます。  
  
-   バックアップの圧縮は、ディスク バックアップ デバイスとテープ バックアップ デバイスの両方でサポートされています。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 パラメーターなしで、または最初のパラメーターだけを指定して **sp_configure** を実行する権限は、既定ですべてのユーザーに付与されます。 両方のパラメーターを指定して **sp_configure** を実行し構成オプションを変更したり RECONFIGURE ステートメントを実行したりするには、ALTER SETTINGS サーバーレベル権限がユーザーに付与されている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-or-configure-the-backup-compression-default-option"></a>backup compression default オプションを表示および構成するには  
  
1.  オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[データベースの設定]** ノードをクリックします。  
  
3.  **[バックアップと復元]** の **[バックアップを圧縮する]** に、 **backup compression default** オプションの現在の設定が表示されます。 この設定によって、バックアップの圧縮についてのサーバー レベルの既定値が次のように決定されます。  
  
    -   **[バックアップを圧縮する]** チェック ボックスがオフの場合、既定では新しいバックアップは圧縮されません。  
  
    -   **[バックアップを圧縮する]** チェック ボックスがオンの場合、既定で新しいバックアップが圧縮されます。  
  
     **sysadmin** 固定サーバー ロールまたは **serveradmin** 固定サーバー ロールのメンバーである場合は、 **[バックアップを圧縮する]** チェック ボックスをクリックして既定の設定を変更することもできます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-view-the-backup-compression-default-option"></a>backup compression default オプションを表示するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) カタログ ビューをクエリして、 `backup compression default`の値を判定しています。 値 0 はバックアップの圧縮がオフであることを示し、値 1 はバックアップの圧縮が有効であることを示します。  
  
```sql  
SELECT value   
FROM sys.configurations   
WHERE name = 'backup compression default' ;  
GO  
```  
  
#### <a name="to-configure-the-backup-compression-default-option"></a>backup compression default オプションを構成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) を使用して、圧縮されたバックアップが既定で作成されるようにサーバー インスタンスを構成する方法を示します。  
  
```sql  
EXEC sp_configure 'backup compression default', 1 ;  
RECONFIGURE;  
GO 
```  
  
 詳細については、「 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)」を参照してください。  
  
##  <a name="FollowUp"></a>補足情報: backup compression default オプションを構成した後  
 新しい設定は、サーバーを再起動しなくてもすぐに有効になります。  
  
## <a name="see-also"></a>参照  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [バックアップの概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)  
  
  

