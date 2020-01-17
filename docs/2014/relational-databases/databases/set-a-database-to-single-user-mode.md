---
title: データベースをシングル ユーザー モードに設定する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- single-user mode [SQL Server], database option
ms.assetid: fb5254eb-b635-4b39-8361-136fd36f2b1f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ea6e37603ae997c218db196c14fe7831bef95e81
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871236"
---
# <a name="set-a-database-to-single-user-mode"></a>データベースをシングル ユーザー モードに設定する
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]のユーザー定義のデータベースをシングル ユーザー モードに設定する方法について説明します。 シングル ユーザー モードでは、一度に 1 人のユーザーだけがデータベースにアクセスでき、一般にはメンテナンス操作のために使用されます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [前提条件](#Prerequisites)  
  
     [Security](#Security)  
  
-   **以下を使用してデータベースをシングル ユーザー モードに設定するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   データベースをシングル ユーザー モードに設定したときに他のユーザーがデータベースに接続していると、データベースに対する接続は警告なく切断されます。  
  
-   このオプションを設定したユーザーがログオフしても、データベースはシングル ユーザー モードのままです。 そのユーザーがログオフした時点で、他のユーザーが 1 人だけデータベースに接続できます。  
  
###  <a name="Prerequisites"></a> 前提条件  
  
-   データベースを SINGLE_USER に設定する前に、AUTO_UPDATE_STATISTICS_ASYNC オプションが OFF に設定されていることを確認します。 このオプションが ON に設定されていると、統計の更新に使用されるバックグラウンド スレッドによってデータベースへの接続が使用されるため、シングル ユーザー モードではデータベースにアクセスできなくなります。 詳細については、「[ALTER DATABASE の SET オプション &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 データベースに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-set-a-database-to-single-user-mode"></a>データベースをシングル ユーザー モードに設定するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  変更するデータベースを右クリックして、 **[プロパティ]** をクリックします。  
  
3.  **[データベースのプロパティ]** ダイアログ ボックスで、 **[オプション]** ページをクリックします。  
  
4.  **[アクセスの制限]** オプションで、 **[Single]** をクリックします。  
  
5.  他のユーザーがデータベースに接続していると、 **"接続を開く"** というメッセージが表示されます。 プロパティを変更して他のすべての接続を閉じるには、 **[はい]** をクリックします。  
  
 この手順を使用して、データベースを複数アクセス モードまたは制限アクセス モードに設定することもできます。 [アクセス制限] オプションの詳細については、「[[データベースのプロパティ] &#40;[オプション] ページ&#41;](database-properties-options-page.md)」を参照してください。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-set-a-database-to-single-user-mode"></a>データベースをシングル ユーザー モードに設定するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、排他的アクセスを取得するために、データベースを `SINGLE_USER` モードに設定します。 次に、 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] データベースの状態を `READ_ONLY` に設定し、データベースへのアクセス権をすべてのユーザーに戻します。終了オプション `WITH ROLLBACK IMMEDIATE` は、最初の `ALTER DATABASE` ステートメントで指定しています。 これですべての未完了のトランザクションがロールバックされ、 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] データベースへの他のすべての接続は直ちに解除されます。  
  
 [!code-sql[DatabaseDDL#AlterDatabase8](../../snippets/tsql/SQL14/tsql/databaseddl/transact-sql/alterdatabase.sql#alterdatabase8)]  
  
## <a name="see-also"></a>関連項目  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
