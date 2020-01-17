---
title: 中央管理サーバーとグループを作成する
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- configuration server
ms.assetid: da265482-3953-440a-ac23-0ab7e42a55eb
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 17c1e63789e9c2069d8fdecd8bd62b64bf8a886d
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244656"
---
# <a name="create-a-central-management-server-and-server-group-sql-server-management-studio"></a>中央管理サーバーとサーバー グループの作成 (SQL Server Management Studio)
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用して、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインスタンスを [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の中央管理サーバーとして指定する方法について説明します。 中央管理サーバーには、1 つ以上の中央管理サーバー グループに編成される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの一覧が格納されます。 中央管理サーバー グループを使用して実行したアクションは、サーバー グループ内のすべてのサーバーに影響します。 これには、オブジェクト エクスプローラーを使用したサーバーへの接続と、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントやポリシー ベースの管理ポリシーの複数サーバーでの同時実行が含まれます。  
  
> [!NOTE]  
>  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] よりも前のバージョンの [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] では、中央管理サーバーを指定できません。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [保護](#Security)  
  
-   **中央管理サーバーとサーバーグループを作成するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a>開始する前に  
  
###  <a name="Security"></a>保護  
  
####  <a name="Permissions"></a>許可  
 中央管理サーバーへのアクセスは、msdb データベースの 2 つのデータベース ロールによって許可されます。 中央管理サーバーを管理できるのは、ServerGroupAdministratorRole ロールのメンバーだけです。 中央管理サーバーに接続するには、ServerGroupReaderRole ロールのメンバーシップが必要です。  
  
 中央管理サーバーによって保持される接続は、ユーザーのコンテキスト内で Windows 認証を使用して実行されるため、登録済みサーバーでの有効な権限が変わることがあります。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A のインスタンスでは sysadmin 固定サーバー ロールのメンバーであるユーザーでも、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] B のインスタンスでは権限が限られていることがあります。  
  
##  <a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
 ここでは、以下の作業の手順について説明します。  
  
1.  中央管理サーバーを作成する。  
  
2.  中央管理サーバーに対してサーバー グループを 1 つ以上追加し、そのサーバー グループに登録済みサーバーを 1 つ以上追加する。  
  
#### <a name="create-a-central-management-server"></a>中央管理サーバーを作成する  
  
1.  
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 **[表示]** メニューの **[登録済みサーバー]** をクリックします。  
  
2.  [登録済みサーバー] で、 **[データベース エンジン]** を展開して **[中央管理サーバー]** を右クリックし、 **[中央管理サーバーの登録]** をクリックします。  
  
3.  
  **[新規サーバーの登録]** ダイアログ ボックスで、ドロップダウン リストにあるサーバーから、中央管理サーバーにする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを選択します。 中央管理サーバーに対して Windows 認証を使用する必要があります。  
  
4.  
  **[登録済みサーバー]** で、サーバー名と説明 (省略可) を入力します。  
  
5.  
  **[接続プロパティ]** タブで、ネットワークと接続のプロパティを確認または変更します。 詳細については、「[[サーバーへの接続] &#40;[接続プロパティ] ページ&#41; データベース エンジン](../f1-help/connect-to-server-connection-properties-page-database-engine.md)」を参照してください。  
  
6.  
  **[テスト]** をクリックして接続をテストします。  
  
7.  
  **[保存]** をクリックします。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが **[中央管理サーバー]** フォルダーに表示されます。  
  
#### <a name="create-a-new-server-group-and-add-servers-to-the-group"></a>新しいサーバー グループを作成し、グループにサーバーを追加する  
  
1.  
  **[登録済みサーバー]** で、 **[中央管理サーバー]** を展開します。 上に挙げた手順で追加した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを右クリックし、 **[新しいサーバー グループ]** を選択します。  
  
2.  
  **[新しいサーバー グループのプロパティ]** で、グループの名前と説明 (省略可) を入力します。  
  
3.  
  **[登録済みサーバー]** で、サーバー グループを右クリックし、 **[新規サーバーの登録]** をクリックします。  
  
4.  [新規サーバーの登録] で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを選択します。 詳細については、「[新しい登録済みサーバーの作成 &#40;SQL Server Management Studio&#41;](create-a-new-registered-server-sql-server-management-studio.md)」を参照してください。 必要に応じてサーバーを追加します。  
  
#### <a name="to-execute-queries-against-several-configuration-targets-at-the-same-time"></a>複数の構成対象に対してクエリを同時に実行するには  
  
-   1 つの中央管理サーバー、1 つ以上のサーバー グループ、および 1 つ以上の登録済みサーバーを作成すると、グループ全体に対してクエリを同時に実行できるようになります。 サーバー グループ内の複数サーバーで [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを同時に実行する方法の詳細については、「[複数のサーバーに対してステートメントを同時に実行する方法 &#40;SQL Server Management Studio&#41;](execute-statements-against-multiple-servers-simultaneously.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [中央管理サーバーを使用して複数のサーバーを管理する](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
