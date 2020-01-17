---
title: ディストリビューション エージェント セキュリティ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.DA.f1
helpviewer_keywords:
- Distribution Agent Security dialog box
ms.assetid: de40cc21-2e58-4464-9be7-b5b90c925e9b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 08a4a90580a00e3ab4f2c38c7dfa3cf81b331d08
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768618"
---
# <a name="distribution-agent-security"></a>[ディストリビューション エージェント セキュリティ]
::: moniker range=">=sql-server-2014||=sqlallproducts-allversions" 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
**[ディストリビューション エージェント セキュリティ]** ダイアログ ボックスを使用すると、ディストリビューション エージェントを実行する Windows アカウントを指定できます。 ディストリビューション エージェントは、プッシュ サブスクリプションのディストリビューターと、プル サブスクリプションのサブスクライバーで動作します。 エージェント プロセスはこのアカウントで実行されるため、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントは、 *プロセス アカウント*としても参照されます。 ダイアログ ボックスで使用できる追加オプションは、次に示すアクセスの方法によって異なります。  
  
-   サブスクリプションの新規作成ウィザードからこのダイアログ ボックスにアクセスする場合、サブスクライバー (プッシュ サブスクリプション) またはディストリビューター (プル サブスクリプション) への接続を作成するディストリビューション エージェントのコンテキストを指定することもできます。 接続は、Windows アカウントの権限を借用するか、指定した [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントのコンテキストで作成します。  
  
-   **[サブスクリプションのプロパティ]** ダイアログ ボックスからこのダイアログ ボックスにアクセスする場合、 **[サブスクライバー接続]** 行または **[ディストリビューター接続]** 行のプロパティ ボタン ( **[...]** ) をクリックして、ディストリビューション エージェントが接続を作成するコンテキストを指定します。 **[サブスクリプションのプロパティ]** ダイアログ ボックスへのアクセスの詳細については、「[プッシュ サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)」および「[プル サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)」を参照してください。  
  
 各アカウントに正しいパスワードが指定され、すべてのアカウントが有効である必要があります。 アカウントとパスワードは、エージェントが実行されるまで検証されません。  
  
## <a name="options"></a>オプション  
 **Process Account**  
 ディストリビューション エージェントが実行される Windows アカウントを入力します。  
  
-   プッシュ サブスクリプションでは、アカウントには次のことが必要です。  
  
    -   最低でも、ディストリビューション データベースで **db_owner** 固定データベース ロールのメンバーである。  
  
    -   パブリケーション アクセス リスト (PAL) のメンバーになれる。  
  
    -   スナップショット共有の読み取り権限を持っている。  
  
    -   サブスクリプションが非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバーの場合、サブスクライバーの OLE DB プロバイダーのインストール ディレクトリへの読み取り権限を持つ。  
  
-   プル サブスクリプションでは、アカウントは少なくとも、サブスクリプション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。  
  
 接続を作成するときにプロセス アカウントを借用する場合、追加の権限が必要です。 後述の **[ディストリビューターに接続]** と **[サブスクライバーに接続]** を参照してください。  
  
 ディストリビューション エージェントは [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] のインスタンスでは実行できないため、 **[プロセス アカウント]** は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] へのプル サブスクリプションには指定できません。  
  
 **[パスワード]** と **[パスワードの確認入力]**  
 Windows アカウントのパスワードを入力します。  
  
 **[ディストリビューターに接続]**  
 プッシュ サブスクリプションでは、ディストリビューターへの接続は常に **[プロセス アカウント]** テキスト ボックスに指定されたアカウントを借用することによって作成されます。  
  
 プル サブスクリプションでは、ディストリビューション エージェントが、 **[プロセス アカウント]** テキスト ボックスに指定されたアカウントを借用するか、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアカウントを使用してディストリビューターへの接続を作成する必要があるかどうかを選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントの使用を選択した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインとパスワードを入力します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントの使用ではなく、Windows アカウントの借用を選択することをお勧めします。  
  
 接続に使用する Windows アカウントまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントには次のことが必要です。  
  
-   PAL のメンバーである。  
  
-   スナップショット共有の読み取り権限を持っている。  
  
 **[サブスクライバーに接続]**  
 プル サブスクリプションでは、サブスクライバーへの接続は常に **[プロセス アカウント]** テキスト ボックスに指定されたアカウントを借用することによって作成されます。  
  
 プッシュ サブスクリプションでは、次のように、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバーと非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバーのオプションが異なります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバーでは、ディストリビューション エージェントが、 **[プロセス アカウント]** テキスト ボックスに指定されたアカウントを借用するか、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアカウントを使用してサブスクライバーへの接続を作成する必要があるかどうかを選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントの使用を選択した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインとパスワードを入力します。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントの使用ではなく、Windows アカウントの借用を選択することをお勧めします。  
  
     サブスクライバーへの接続に使用される Windows アカウントまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントは、少なくとも、サブスクリプション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。  
  
-   非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバーでは、ディストリビューション エージェントがサブスクライバーに接続するときに使用する必要のあるサブスクライバーでデータベース ログインを指定します。 ログインは、サブスクリプション データベースにオブジェクトを作成するための十分な権限を持つ必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバの詳細については、「[SQL Server 以外のサブスクライバーのサブスクリプションの作成](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)」を参照してください。  
  
 **[追加の接続オプション]**  
 非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバーのみです。 接続文字列の形式で、サブスクライバーの任意の接続オプションを指定します (Oracle では追加のオプションは不要)。 各オプションはセミコロンで区切る必要があります。 次は、IBM DB2 接続文字列の例です (読みやすくするために改行されています)。  
  
```  
Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
Persist Security Info=False;Connection Pooling=True;  
```  
  
 文字列内のオプションの多くは、接続する DB2 サーバーに固有のものですが、 **Process Binary as Character** オプションは常に **False**に設定する必要があります。 サブスクリプション データベースを識別するため、 **Initial Catalog** オプションに値が必要です。 詳細については、「 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ID およびアクセス制御 (レプリケーション)](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [レプリケーション エージェントのセキュリティ モデル](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [レプリケーション エージェントの概要](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)  
::: moniker-end
  
::: monikerRange="azuresqldb-mi-current"
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
**[ディストリビューション エージェント セキュリティ]** ダイアログ ボックスを使用すると、ディストリビューション エージェントを実行する SQL 認証アカウントを指定できます。 ディストリビューション エージェントは、プッシュ サブスクリプションのディストリビューターと、プル サブスクリプションのサブスクライバーで動作します。  ダイアログ ボックスで使用できる追加オプションは、次に示すアクセスの方法によって異なります。  
  
-   サブスクリプションの新規作成ウィザードからこのダイアログ ボックスにアクセスする場合、サブスクライバー (プッシュ サブスクリプション) またはディストリビューター (プル サブスクリプション) への接続を作成するディストリビューション エージェントのコンテキストを指定することもできます。 接続は、SQL Server 認証アカウントを使用して行う必要があります。 
  
-   **[サブスクリプションのプロパティ]** ダイアログ ボックスからこのダイアログ ボックスにアクセスする場合、 **[サブスクライバー接続]** 行または **[ディストリビューター接続]** 行のプロパティ ボタン ( **[...]** ) をクリックして、ディストリビューション エージェントが接続を作成するコンテキストを指定します。 **[サブスクリプションのプロパティ]** ダイアログ ボックスへのアクセスの詳細については、「[プッシュ サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)」および「[プル サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)」を参照してください。  
  
 各アカウントに正しいパスワードが指定され、すべてのアカウントが有効である必要があります。 アカウントとパスワードは、エージェントが実行されるまで検証されません。  
  
## <a name="options"></a>オプション  
 **Process Account**  
 ディストリビューション エージェントを実行する SQL Server 認証アカウントを入力します。  
  
-   プッシュ サブスクリプションでは、アカウントには次のことが必要です。  
  
    -   最低でも、ディストリビューション データベースで **db_owner** 固定データベース ロールのメンバーである。  
  
    -   パブリケーション アクセス リスト (PAL) のメンバーになれる。  
  
    -   スナップショット共有の読み取り権限を持っている。  
  
    -   サブスクリプションが非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバーの場合、サブスクライバーの OLE DB プロバイダーのインストール ディレクトリへの読み取り権限を持つ。  
  
-   プル サブスクリプションでは、アカウントは少なくとも、サブスクリプション データベースの **db_owner** 固定データベース ロールのメンバーである必要があります。  
  
    
**[パスワード]** と **[パスワードの確認入力]**  
Windows アカウントのパスワードを入力します。  
  
**[ディストリビューターに接続]**  
プッシュ サブスクリプションでは、ディストリビューターへの接続は常に **[プロセス アカウント]** テキスト ボックスに指定されたアカウントを借用することによって作成されます。  
  
プル サブスクリプションでは、ディストリビューション エージェントが、 **[プロセス アカウント]** テキスト ボックスに指定されたアカウントを借用するか、SQL Server 認証アカウントを使用してディストリビューターへの接続を作成する必要があるかどうかを選択します。 
  
  
 **[サブスクライバーに接続]**  
 プル サブスクリプションでは、サブスクライバーへの接続は常に **[プロセス アカウント]** テキスト ボックスに指定されたアカウントを借用することによって作成されます。  
  
 プッシュ サブスクリプションでは、次のように、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバーと非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバーのオプションが異なります。

  
-   非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバーでは、ディストリビューション エージェントがサブスクライバーに接続するときに使用する必要のあるサブスクライバーでデータベース ログインを指定します。 ログインは、サブスクリプション データベースにオブジェクトを作成するための十分な権限を持つ必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバの詳細については、「[SQL Server 以外のサブスクライバーのサブスクリプションの作成](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)」を参照してください。  
  
 **[追加の接続オプション]**  
 非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバーのみです。 接続文字列の形式で、サブスクライバーの任意の接続オプションを指定します (Oracle では追加のオプションは不要)。 各オプションはセミコロンで区切る必要があります。 次は、IBM DB2 接続文字列の例です (読みやすくするために改行されています)。  
  
```  
Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
Persist Security Info=False;Connection Pooling=True;  
```  
  
 文字列内のオプションの多くは、接続する DB2 サーバーに固有のものですが、 **Process Binary as Character** オプションは常に **False**に設定する必要があります。 サブスクリプション データベースを識別するため、 **Initial Catalog** オプションに値が必要です。 詳細については、「 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Azure SQL Database を使用したトランザクションのレプリケーション](/azure/sql-database/sql-database-managed-instance-transactional-replication) [マネージド インスタンスのレプリケーションを構成する](/azure/sql-database/replication-with-sql-database-managed-instance)
::: moniker-end


