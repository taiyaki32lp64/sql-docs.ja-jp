---
title: remote access サーバー構成オプションの構成 | Microsoft Docs
ms.custom: ''
ms.date: 08/11/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- remote servers [SQL Server], stored procedure execution
ms.assetid: f5de748d-1c55-4714-9661-38fe62e5095f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 52d6f73b585f3d0857186bef9c6c440e8655adc1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68012343"
---
# <a name="configure-the-remote-access-server-configuration-option"></a>remote access サーバー構成オプションの構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックは、"リモート アクセス"機能に関するものです。 この構成オプションは、わかりにくい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への通信機能であり、非推奨であるため、使用すべきではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]への接続で問題があるため、それを解決するためにこのページに至った場合は、代わりに次のいずれかのページを参照してください。  
  
-   [チュートリアル: データベース エンジンの概要](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)  
  
-   [SQL Server へのログイン](../../database-engine/configure-windows/logging-in-to-sql-server.md)  
  
-   [システム管理者がロックアウトされた場合の SQL Server への接続](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)  
  
-   [登録済みサーバーへの接続 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/connect-to-a-registered-server-sql-server-management-studio.md)  
  
-   [SQL Server Management Studio から SQL Server コンポーネントへの接続](../../ssms/f1-help/connect-to-any-sql-server-component-from-sql-server-management-studio.md)  
  
-   [sqlcmd によるデータベース エンジンへの接続](../../relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md)  
  
-   [SQL Server データベース エンジンへの接続のトラブルシューティングの方法](https://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)  
  
 プログラマーの方には次のトピックも参考になる可能性があります。  
  
-   [方法: ASP.NET 2.0 で SQL 認証を使用して SQL Server へ接続する](https://msdn.microsoft.com/library/ff648340.aspx)  
  
-   [SQL Server のインスタンスへの接続](../../relational-databases/server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md)  
  
-   [方法:SQL Server データベースへの接続を作成する](https://msdn.microsoft.com/library/s4yys16a.aspx)  
  
 **このトピックの本文は、ここから始まります。**  
  
 このトピックでは、 **または** を使用して、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] remote access [!INCLUDE[tsql](../../includes/tsql-md.md)]サーバー構成オプションを構成する方法について説明します。 **remote access** オプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが実行されているローカル サーバーまたはリモート サーバーからストアド プロシージャの実行を制御します。 このオプションの既定値は 1 です。 この場合、リモート サーバーからローカル ストアド プロシージャを実行する権限、またはローカル サーバーからリモート ストアド プロシージャを実行する権限が許可されます。 リモート サーバーからローカル ストアド プロシージャを、ローカル サーバーからリモート ストアド プロシージャを実行できないようにするには、このオプションを 0 に設定します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 代わりに [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) を使用してください。
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **以下を使用して remote access オプションを構成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [remote access オプションを構成した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   **remote access** オプションは [sp_addserver](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)を使用して追加されたサーバーにのみ適用でき、旧バージョンとの互換性のために用意されています。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 パラメーターなしで、または最初のパラメーターだけを指定して **sp_configure** を実行する権限は、既定ですべてのユーザーに付与されます。 両方のパラメーターを指定して **sp_configure** を実行し構成オプションを変更したり RECONFIGURE ステートメントを実行したりするには、ALTER SETTINGS サーバーレベル権限がユーザーに付与されている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-configure-the-remote-access-option"></a>remote access オプションを構成するには  
  
1.  オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[接続]** ノードをクリックします。  
  
3.  **[リモート サーバー接続]** で、 **[このサーバーへのリモート接続を許可する]** チェック ボックスをオンまたはオフにします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-configure-the-remote-access-option"></a>remote access オプションを構成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) を使用して、 `remote access` オプションの値を `0`に設定する方法を示します。  
  
```sql  
EXEC sp_configure 'remote access', 0 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
 詳細については、「 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)」を参照してください。  
  
##  <a name="FollowUp"></a>補足情報: remote access オプションを構成した後  
 この設定は、SQL Server の再起動後に反映されます。  
  
## <a name="see-also"></a>参照  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
