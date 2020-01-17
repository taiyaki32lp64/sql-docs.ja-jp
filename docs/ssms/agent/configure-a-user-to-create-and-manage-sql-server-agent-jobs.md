---
title: SQL Server エージェント ジョブ ステップを作成および管理するユーザーの構成 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, user configuration
- jobs [SQL Server Agent], user configuration
- SQLAgentUserRole database role
- proxy accounts [SQL Server Agent]
ms.assetid: 67897e3e-b7d0-43dd-a2e2-2840ec4dd1ef
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: eae65b8c68d001c2a9c0a7abbd43801870191410
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68251423"
---
# <a name="configure-a-user-to-create-and-manage-sql-server-agent-jobs"></a>Configure a User to Create and Manage SQL Server Agent Jobs
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを作成または実行するユーザーを構成する方法について説明します。  
  
-   **作業を開始する準備:** [セキュリティ](#Security)  
  
-   **SQL Server エージェント ジョブを作成および管理するユーザーを構成するために使用するもの:** [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Security"></a>セキュリティ  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを作成または実行するユーザーを構成するには、まず、msdb データベース内の次のいずれかの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールに、既存の SQL Server ログインまたは msdb ロールを追加する必要があります: SQLAgentUserRole、SQLAgentReaderRole、または SQLAgentOperatorRole。  
  
既定では、これらのデータベース ロールのメンバーは、メンバー自身が実行する独自のジョブ ステップを作成できます。 このような管理者権限のないユーザーが他の種類のジョブ ステップ ( [!INCLUDE[ssIS](../../includes/ssis_md.md)] パッケージなど) を実行するには、プロキシ アカウントへのアクセスが必要です。 sysadmin 固定サーバー ロールのすべてのメンバーには、プロキシ アカウントを作成、変更、および削除する権限があります。 これら [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定のデータベース ロールに関連付けられている権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
#### <a name="Permissions"></a>アクセス許可  
詳細については、「 [SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)」をご覧ください。  
  
## <a name="SSMS"></a>SQL Server Management Studio の使用  
**SQL ログインまたは msdb ロールを SQL Server エージェント固定データベース ロールに追加するには**  
  
1.  **オブジェクト エクスプローラー**で、サーバーを展開します。  
  
2.  **[セキュリティ]** を展開し、 **[ログイン]** を展開します。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールに追加するログインを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[ログインのプロパティ]** ダイアログ ボックスの **[ユーザー マッピング]** ページで、 **msdb**を含む行を選択します。  
  
5.  **[データベース ロールのメンバーシップ: msdb]** で、該当する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールのチェック ボックスをオンにします。  
  
**SQL Server エージェント ジョブ ステップを作成および管理できるようにプロキシ アカウントを構成するには**  
  
1.  **オブジェクト エクスプローラー**で、サーバーを展開します。  
  
2.  **[SQL Server エージェント]** を展開します。  
  
3.  **[プロキシ]** を右クリックして **[新しいプロキシ]** をクリックします。  
  
4.  **[新しいプロキシ アカウント]** ダイアログの **[全般]** ページで、新しいプロキシのプロキシ名、資格情報名、および説明を指定します。 SQL Server エージェントのプロキシを作成する前に、まず資格情報を作成する必要があることに注意してください。 資格情報の作成の詳細については、「[資格情報の作成方法 (SQL Server Management Studio)](https://msdn.microsoft.com/c1e77e91-2a69-40d9-b8b3-97cffc710586)に関するページおよび「[CREATE CREDENTIAL (Transact-SQL)](https://msdn.microsoft.com/d5e9ae69-41d9-4e46-b13d-404b88a32d9d)」を参照してください。  
  
5.  このプロキシに適したサブシステムを確認します。  
  
6.  **[プリンシパル]** ページで、プロキシ アカウントへのアクセスを許可するログインまたはロールを追加するか、あるいは拒否するログインまたはロールを削除します。  
  
## <a name="see-also"></a>参照  
[SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)  
  
