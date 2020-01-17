---
title: 管理者以外のユーザーがレプリケーション モニターを使用できるようにする
description: SQL Server Management Studio (SSMS) で管理者以外のユーザーにレプリケーション モニターへのアクセス権を付与する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, non-administrators access
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: ee5905259958b1b396b1b9c2726ca3a74b24a7d6
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75320625"
---
# <a name="allow-non-administrators-to-use-replication-monitor"></a>管理者以外のユーザーがレプリケーション モニターを使用できるようにする
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、管理者以外のユーザーがレプリケーション モニターを使用できるようにする方法について説明します。 レプリケーション モニターは、次のロールのメンバーになっているユーザーが使用できます。  
  
-   **sysadmin** 固定サーバー ロール  
  
     これらのユーザーはレプリケーションを監視することができ、また、エージェント スケジュール、エージェント プロファイルなどのレプリケーション プロパティの変更に対するフル コントロール権限を持っています。  
  
-   ディストリビューション データベースの **replmonitor** データベース ロール  
  
     これらのユーザーはレプリケーションを監視できますが、レプリケーション プロパティは変更できません。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [セキュリティ](#Security)  
  
-   **管理者以外のユーザーがレプリケーション モニターを使用できるようにするために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 管理者以外のユーザーがレプリケーション モニターを使用できるようにするには、 **sysadmin** 固定サーバー ロールのメンバーがディストリビューション データベースにユーザーを追加して、そのユーザーを **replmonitor** ロールに割り当てる必要があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-allow-non-administrators-to-use-replication-monitor"></a>管理者以外のユーザーがレプリケーション モニターを使用できるようにするには  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で、ディストリビューターに接続し、サーバー ノードを展開します。  
  
2.  **[データベース]** 、 **[システム データベース]** の順に展開してから、ディストリビューション データベース (既定の名前は **distribution** ) を展開します。  
  
3.  **[セキュリティ]** を展開し、 **[ユーザー]** を右クリックしてから、 **[新しいユーザー]** をクリックします。  
  
4.  ユーザー名とユーザーのログインを入力します。  
  
5.  既定のスキーマ **[replmonitor]** を選択します。  
  
6.  **[データベース ロールのメンバーシップ]** の **[replmonitor]** チェック ボックスをオンにします。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-add-a-user-to-the-replmonitor-fixed-database-role"></a>固定データベース ロール replmonitor にユーザーを追加するには  
  
1.  ディストリビューターのディストリビューション データベースで [sp_helpuser (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md) を実行します。 対象のユーザーが結果セットの **UserName** に含まれていなかった場合は、そのユーザーに対し、[CREATE USER (Transact-SQL)](../../../t-sql/statements/create-user-transact-sql.md) ステートメントを使って、ディストリビューション データベースへのアクセスを許可する必要があります。  
  
2.  ディストリビューターのディストリビューション データベースで [sp_helprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md) を実行します。このとき、`@rolename` パラメーターには値 **replmonitor** を指定します。 対象のユーザーが結果セットの **MemberName** に含まれていた場合、そのユーザーは既にこのロールに所属しています。  
  
3.  ユーザーが **replmonitor** ロールに属していなかった場合は、ディストリビューターのディストリビューション データベースで [sp_addrolemember (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) を実行します。 `@rolename` には値 **replmonitor** を、`@membername` には、追加するデータベース ユーザーの名前または [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows ログイン名を指定します。  
  
#### <a name="to-remove-a-user-from-the-replmonitor-fixed-database-role"></a>固定データベース ロール replmonitor からユーザーを削除するには  
  
1.  ユーザーが **replmonitor** ロールに属しているかどうかを確認するには、ディストリビューターのディストリビューション データベースで [sp_helprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md) を実行します。このとき、`@rolename` に値 **replmonitor** を指定します。 対象のユーザーが結果セットの **MemberName** に含まれていなかった場合、そのユーザーは現在、このロールに所属していません。  
  
2.  ユーザーが **replmonitor** ロールに属している場合は、ディストリビューターのディストリビューション データベースで [sp_droprolemember (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) を実行します。 `@rolename` には値 **replmonitor** を、`@membername` には、削除するデータベース ユーザーの名前または Windows ログイン名を指定します。 
  
  
