---
title: SQL Server 監査ログの表示 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- audits [SQL Server], viewing logs
- viewing audit logs
- logs [SQL Server], audit
ms.assetid: e8feaca0-7852-422b-895a-319b965d8d9b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: fa30824e32faae5feee1612305c1ca292d44e8e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63012019"
---
# <a name="view-a-sql-server-audit-log"></a>SQL Server 監査ログの表示
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] を使用して [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で SQL Server 監査ログを表示する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **SQL Server 監査ログを表示する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 `CONTROL SERVER` アクセス許可が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-a-sql-server-audit-log"></a>SQL Server 監査ログを表示するには  
  
1.  オブジェクト エクスプローラーで、 **[セキュリティ]** フォルダーを展開します。  
  
2.  **[監査]** フォルダーを展開します。  
  
3.  表示する監査ログを右クリックし、 **[監査ログの表示]** をクリックします。 開き、**ログ ファイルの表示 -** _server_name_  ダイアログ ボックス。 詳細については、「 [Log File Viewer F1 Help](../../logs/log-file-viewer-f1-help.md)」を参照してください。  
  
4.  完了したら、 **[閉じる]** をクリックします。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] では、[ログ ファイルの表示] を使用して監査ログを表示することをお勧めします。 ただし、自動監視システムを作成している場合、[sys.fn_get_audit_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql) 関数を使用して監査ファイルの情報を直接読み取ることができます。 ファイルを直接読み取ると、わずかに異なる (処理されていない) 形式でデータが返されます。 詳細については、 **sys.fn_get_audit_file** を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server Audit &#40;データベース エンジン&#41;](sql-server-audit-database-engine.md)   
 [セキュリティ ログへの SQL サーバー監査イベントの書き込み](write-sql-server-audit-events-to-the-security-log.md)  
  
  
