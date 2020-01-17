---
title: パブリケーション アクセス リストのログインの管理 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server replication], publication access list
- publications [SQL Server replication], publication access lists
- publication access list (PAL)
- PAL (publication access list)
- logins [SQL Server replication], managing
ms.assetid: fceb216b-0b18-4e3b-8ae0-13e35920dcbc
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: b8a72455aafbf31f5a926719e821f3d15393d953
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710779"
---
# <a name="manage-logins-in-the-publication-access-list"></a>パブリケーション アクセス リストのログインの管理
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、パブリケーション アクセス リストのログインを管理する方法について説明します。 パブリケーションへのアクセスは、パブリケーション アクセス リスト (PAL) によって制御されます。 ログインおよびグループの PAL への追加および PAL からの削除を実行できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [前提条件](#Prerequisites)  
  
-   **パブリケーション アクセス リストのログインを管理するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> 前提条件  
  
-   PAL にログインを追加する前に、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインをパブリケーション データベースのデータベース ユーザーに関連付ける必要があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[パブリケーション アクセス リスト]** ページでパブリケーション アクセス リスト (PAL) を使用します。 このダイアログ ボックスへのアクセス方法の詳細については、「[パブリケーション プロパティの表示および変更](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」を参照してください。  
  
#### <a name="to-manage-logins-in-the-pal"></a>PAL のログインを管理するには  
  
1.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[パブリケーション アクセス リスト]** ページでは、 **[追加]** 、 **[削除]** 、および **[すべて削除]** の各ボタンを使用して、PAL のログインやグループを追加および削除します。 PAL から **distributor_admin** を削除しないでください。 このアカウントはレプリケーションで使用されます。  
  
    > [!NOTE]  
    >  リモート ディストリビューターを使用する場合、PAL 内のアカウントは、パブリッシャーとディストリビューターの両方で使用できる必要があります。 このアカウントは、どちらのサーバーでも定義されているドメイン アカウントまたはローカル アカウントにする必要があります。 両方のログインに関連付けられているパスワードは、同じにする必要があります。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-view-groups-and-logins-that-belong-to-the-pal"></a>PAL に登録されているグループおよびログインを表示するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_help_publication_access](../../../relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql.md)を実行します。 `@publication` には、パブリケーション名を指定します。 これで、PAL のグループおよびログインに関する情報が表示されます。  
  
#### <a name="to-add-groups-and-logins-to-the-pal"></a>グループおよびログインを PAL に追加するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_grant_publication_access](../../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)を実行します。 `@publication` には、パブリケーション名を指定し、`@login` には、追加するログインまたはグループの名前を指定します。  
  
#### <a name="to-remove-groups-and-logins-from-the-pal"></a>グループおよびログインを PAL から削除するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_revoke_publication_access](../../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)を実行します。 `@publication` には、パブリケーション名を指定し、`@login` には、削除するログインまたはグループの名前を指定します。  
  
## <a name="see-also"></a>参照  
 [パブリケーション アクセス リストのログインの管理](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md)   
 [レプリケーション エージェントのセキュリティ モデル](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [レプリケーション トポロジのセキュリティ保護](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [パブリッシャーのセキュリティ保護](../../../relational-databases/replication/security/secure-the-publisher.md)  
  
  
