---
title: 管理者以外のユーザーがレプリケーション モニターを使用できるようにする | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, non-administrators access
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9e8f03d12d3ac1695d4f6d000c8eab89a42004fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667390"
---
# <a name="allow-non-administrators-to-use-replication-monitor"></a>管理者以外のユーザーがレプリケーション モニターを使用できるようにする
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、管理者以外のユーザーがレプリケーション モニターを使用できるようにする方法について説明します。 レプリケーション モニターは、次のロールのメンバーになっているユーザーが使用できます。  
  
-   **sysadmin** 固定サーバー ロール  
  
     これらのユーザーはレプリケーションを監視することができ、また、エージェント スケジュール、エージェント プロファイルなどのレプリケーション プロパティの変更に対するフル コントロール権限を持っています。  
  
-   `replmonitor`ディストリビューション データベース内のデータベース ロール。  
  
     これらのユーザーはレプリケーションを監視できますが、レプリケーション プロパティは変更できません。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **管理者以外のユーザーがレプリケーション モニターを使用できるようにするために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 管理者以外のユーザーがレプリケーション モニター, のメンバーを使用できるように、 **sysadmin**固定サーバー ロールがディストリビューション データベースにユーザーを追加し、そのユーザーを割り当てる必要があります、`replmonitor`ロール。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-allow-non-administrators-to-use-replication-monitor"></a>管理者以外のユーザーがレプリケーション モニターを使用できるようにするには  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で、ディストリビューターに接続し、サーバー ノードを展開します。  
  
2.  **[データベース]** 、 **[システム データベース]** の順に展開してから、ディストリビューション データベース (既定の名前は **distribution** ) を展開します。  
  
3.  **[セキュリティ]** を展開し、 **[ユーザー]** を右クリックしてから、 **[新しいユーザー]** をクリックします。  
  
4.  ユーザー名とユーザーのログインを入力します。  
  
5.  既定のスキーマを選択します。`replmonitor`します。  
  
6.  選択、 `replmonitor`  チェック ボックス、**データベース ロールのメンバーシップ**グリッド。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-add-a-user-to-the-replmonitor-fixed-database-role"></a>固定データベース ロール replmonitor にユーザーを追加するには  
  
1.  ディストリビューターのディストリビューション データベースで [sp_helpuser (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpuser-transact-sql) を実行します。 ユーザーが表示されていない場合`UserName`、結果セットで、ユーザー与える必要がありますを使って、ディストリビューション データベースへのアクセス、 [CREATE USER &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-user-transact-sql)ステートメント。  
  
2.  ディストリビューター、ディストリビューション データベースで、次のように実行します。 [sp_helprolemember &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql)、の値を指定する`replmonitor`の、 **@rolename** パラメーター。 ユーザーが表示されている場合`MemberName`結果セットで、ユーザー既にこのロールに属しています。  
  
3.  ユーザーが属していない場合、`replmonitor`ロール、実行[sp_addrolemember &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)ディストリビューターのディストリビューション データベースでします。 値を指定`replmonitor`の **@rolename** とデータベース ユーザーの名前または[!INCLUDE[msCoName](../../../includes/msconame-md.md)]を追加する Windows ログイン **@membername** します。  
  
#### <a name="to-remove-a-user-from-the-replmonitor-fixed-database-role"></a>固定データベース ロール replmonitor からユーザーを削除するには  
  
1.  ユーザーに属していることを確認する、`replmonitor`ロール、実行[sp_helprolemember &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql)ディストリビューター、ディストリビューション データベースでの値を指定して`replmonitor`の **@rolename** . 対象のユーザーが結果セットの `MemberName` に含まれていなかった場合、そのユーザーは現在、このロールに所属していません。  
  
2.  ユーザーが属している場合、`replmonitor`ロール、実行[sp_droprolemember &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)ディストリビューターのディストリビューション データベースでします。 値を指定`replmonitor`の **@rolename** データベース ユーザーまたは削除されている Windows ログインの名前と **@membername** します。  
  
  
