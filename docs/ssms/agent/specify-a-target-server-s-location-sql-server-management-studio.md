---
title: ターゲット サーバーの場所を指定する | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], location
ms.assetid: 511ff311-21f5-4f2f-839f-b4deee26ec98
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 99c67c3d0e3afbda0c05e3feb3ed1e0d6951f870
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69552466"
---
# <a name="specify-a-target-server39s-location-sql-server-management-studio"></a>ターゲット サーバーの場所を指定する (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のマルチサーバー管理の構成でターゲット サーバーの場所を指定する方法について説明します。  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Restrictions"></a>制限事項と制約事項  
このアクションを実行すると、レジストリが編集されます。 レジストリは手動で編集しないでください。不適切または不正確な変更を加えると、システム構成に重大な問題が生じる場合があります。 熟練したユーザーのみがレジストリ エディターを使用してレジストリを編集することをお勧めします。 詳細については、Microsoft Windows のドキュメントを参照してください。  
  
### <a name="Security"></a>セキュリティ  
  
#### <a name="Permissions"></a>アクセス許可  
**sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-specify-a-target-servers-location"></a>ターゲット サーバーの場所を指定するには  
  
1.  **オブジェクト エクスプローラー**で、ターゲット サーバーの場所として指定するマスター サーバーをプラス記号をクリックして展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[マルチ サーバーの管理]** をポイントして、 **[ターゲット サーバーの管理]** を選択します。  
  
3.  ターゲット サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[場所]** ボックスにサーバーの場所を入力し、 **[OK]** をクリックします。  
  
## <a name="TsqlProcedure"></a>Transact-SQL の使用  
  
#### <a name="to-specify-a-target-servers-location"></a>ターゲット サーバーの場所を指定するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE msdb ;  
    GO  
    -- enlists the current server into the AdventureWorks1 master server.   
    -- The location for the current server is Building 21, Room 309, Rack 5  
    EXEC dbo.sp_msx_enlist N'AdventureWorks2012',   
        N'Building 21, Room 309, Rack 5' ;  
    GO  
    ```  
  
詳細については、「 [sp_msx_enlist (Transact-SQL)](https://msdn.microsoft.com/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f)」を参照してください。  
  
