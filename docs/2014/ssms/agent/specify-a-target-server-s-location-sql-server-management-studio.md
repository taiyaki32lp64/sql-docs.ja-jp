---
title: ターゲット サーバーを指定&#39;場所 (SQL Server Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], location
ms.assetid: 511ff311-21f5-4f2f-839f-b4deee26ec98
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e1d08c7f660d4deee887f95a06a7848f6d40b2d4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211333"
---
# <a name="specify-a-target-server39s-location-sql-server-management-studio"></a>対象サーバーの場所を指定する (SQL Server Management Studio)
  このトピックでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のマルチサーバー管理の構成でターゲット サーバーの場所を指定する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **対象サーバーの場所を指定する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 このアクションを実行すると、レジストリが編集されます。 レジストリは手動で編集しないでください。不適切または不正確な変更を加えると、システム構成に重大な問題が生じる場合があります。 熟練したユーザーのみがレジストリ エディターを使用してレジストリを編集することをお勧めします。 詳細については、Microsoft Windows のドキュメントを参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-specify-a-target-servers-location"></a>ターゲット サーバーの場所を指定するには  
  
1.  **オブジェクト エクスプローラー**で、対象サーバーの場所として指定するマスター サーバーをプラス記号をクリックして展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[マルチ サーバーの管理]** をポイントして、 **[対象サーバーの管理]** を選択します。  
  
3.  ターゲット サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[場所]** ボックスにサーバーの場所を入力し、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-specify-a-target-servers-location"></a>ターゲット サーバーの場所を指定するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
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
  
 詳細については、次を参照してください。 [sp_msx_enlist &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)します。  
  
  
