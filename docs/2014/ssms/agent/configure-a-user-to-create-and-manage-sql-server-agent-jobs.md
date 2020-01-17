---
title: SQL Server エージェント ジョブ ステップを作成および管理するユーザーの構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, user configuration
- jobs [SQL Server Agent], user configuration
- SQLAgentUserRole database role
- proxy accounts [SQL Server Agent]
ms.assetid: 67897e3e-b7d0-43dd-a2e2-2840ec4dd1ef
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a62f6c2e1ef86a6fcd5e532b2ef413d8142698e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63253559"
---
# <a name="configure-a-user-to-create-and-manage-sql-server-agent-jobs"></a>SQL Server エージェント ジョブ ステップを作成および管理するユーザーの構成
  このトピックでは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを作成または実行するユーザーを構成する方法について説明します。  
  
-   **作業を開始する準備:** [Security](#Security)  
  
-   **SQL Server エージェント ジョブを作成および管理するユーザーを構成するために使用するもの:** [SQL Server Management Studio](#SSMS)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを作成または実行するユーザーを構成するには、まず、msdb データベース内の次のいずれかの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールに、既存の SQL Server ログインまたは msdb ロールを追加する必要があります: SQLAgentUserRole、SQLAgentReaderRole、または SQLAgentOperatorRole。  
  
 既定では、これらのデータベース ロールのメンバーは、メンバー自身が実行する独自のジョブ ステップを作成できます。 このような管理者権限のないユーザーが他の種類のジョブ ステップ ( [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージなど) を実行するには、プロキシ アカウントへのアクセスが必要です。 sysadmin 固定サーバー ロールのすべてのメンバーには、プロキシ アカウントを作成、変更、および削除する権限があります。 これら [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定のデータベース ロールに関連付けられている権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
####  <a name="Permissions"></a> Permissions  
 詳細については、「 [SQL Server エージェントのセキュリティの実装](implement-sql-server-agent-security.md)」をご覧ください。  
  
##  <a name="SSMS"></a> SQL Server Management Studio の使用  
 **SQL ログインまたは msdb ロールを SQL Server エージェント固定データベース ロールに追加するには**  
  
1.  **オブジェクト エクスプローラー**で、サーバーを展開します。  
  
2.  **[セキュリティ]** を展開し、 **[ログイン]** を展開します。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールに追加するログインを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **ユーザー マッピング**のページ、**ログインのプロパティ** ダイアログ ボックスを含む行を選択します。`msdb`します。  
  
5.  **[データベース ロールのメンバーシップ: msdb]** で、該当する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールのチェック ボックスをオンにします。  
  
 **SQL Server エージェント ジョブ ステップを作成および管理できるようにプロキシ アカウントを構成するには**  
  
1.  **オブジェクト エクスプローラー**で、サーバーを展開します。  
  
2.  **[SQL Server エージェント]** を展開します。  
  
3.  **[プロキシ]** を右クリックして **[新しいプロキシ]** をクリックします。  
  
4.  **[新しいプロキシ アカウント]** ダイアログの **[全般]** ページで、新しいプロキシのプロキシ名、資格情報名、および説明を指定します。 SQL Server エージェントのプロキシを作成する前に、まず資格情報を作成する必要があることに注意してください。 資格情報の作成の詳細については、次を参照してください。[資格情報を作成](../../relational-databases/security/authentication-access/create-a-credential.md)と[CREATE CREDENTIAL &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)します。  
  
5.  このプロキシに適したサブシステムを確認します。  
  
6.  **[プリンシパル]** ページで、プロキシ アカウントへのアクセスを許可するログインまたはロールを追加するか、あるいは拒否するログインまたはロールを削除します。  
  
## <a name="see-also"></a>参照  
 [SQL Server エージェントのセキュリティの実装](implement-sql-server-agent-security.md)  
  
  
