---
title: 包含データベース ユーザー - データベースの可搬性を確保する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- contained database, users
- user [SQL Server], about contained database users
ms.assetid: e57519bb-e7f4-459b-ba2f-fd42865ca91d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a10f892c8fd635892d76061e9f33649340e69593
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62655472"
---
# <a name="contained-database-users---making-your-database-portable"></a>包含データベース ユーザー - データベースの可搬性を確保する
  包含データベース ユーザーを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[ssSDS](../../includes/sssds-md.md)] のデータベース レベルでの接続が認証されます。 包含データベースは、他のデータベース、およびデータベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/[!INCLUDE[ssSDS](../../includes/sssds-md.md)] (および master データベース) のインスタンスから分離されたデータベースです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、Windows 認証と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証の両方で包含データベース  ユーザーがサポートされます。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]を使用して、包含データベース ユーザーとデータベース レベルのファイアウォール規則を結合します。 このトピックでは、従来のログイン/ユーザー モデルおよび Windows またはサーバー レベルのファイアウォール規則と比較して、包含データベース モデルの相違点とこれを使用する利点について説明します。 特定のシナリオ、管理の容易性、アプリケーションのビジネス ロジックでは、従来のログイン / ユーザー モデルとサーバー レベルのファイアウォール規則を引き続き使用する必要があります。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] の [!INCLUDE[ssSDS](../../includes/sssds-md.md)] サービスが向上し、SLA の保証が高度になると、包含データベース ユーザー モデルとデータベース用ファイアウォール規則に切り替え、特定のデータベースに対する SLA の可用性と最大ログイン レートをさらに高める必要があります。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] は、今すぐこのような変化に対応することをお勧めします。  
  
## <a name="traditional-login-and-user-model"></a>従来のログイン / ユーザー モデル  
 従来の接続モデルでは、Windows ユーザーまたは Windows グループのメンバーが [!INCLUDE[ssDE](../../includes/ssde-md.md)] に接続する際、Windows によって認証されているユーザーまたはグループの資格情報を指定します。 または、名前とパスワードが接続から指定され、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して接続します ([!INCLUDE[ssSDS](../../includes/sssds-md.md)] に接続するときは、これが唯一の選択肢となります)。 どちらの場合も、接続ユーザーの資格情報に対応するログインが master データベースに格納されている必要があります。 通常、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] で Windows 認証の資格情報が確認されるか、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証の資格情報で本人性が確認されると、ユーザー データベースへの接続が試行されます。 ユーザー データベースに接続するには、そのデータベース内のユーザーに対してログインをマップ (関連付けることが) できなければなりません。 また、特定のデータベースへの接続を接続文字列で指定する方法もあります。この方法は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では任意ですが、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]では必須です。  
  
 重要なのは、(master データベース内の) ログインと (ユーザー データベース内の) ユーザーの両方が存在し、かつ相互に関連付けられていなければならない、ということです。 これは、ユーザー データベースへの接続が、master データベース内のログインに依存していることを意味します。そのことが、データベースのホストを別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] や [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] サーバーに切り替えることを困難にしています。 また、なんらかの理由で、master データベースへの接続が利用できないと (フェールオーバーが進行中であるなど)、全体的な接続時間が増えたり、接続がタイムアウトしたりする可能性もあります。そのため、接続のスケーラビリティが低下します。  
  
## <a name="contained-database-user-model"></a>包含データベース ユーザー モデル  
 包含データベース ユーザー モデルでは、ログインが master データベースには存在しません。 認証プロセスはユーザー データベースで実行されます。master データベースには、ユーザー データベース内のデータベース ユーザーに関連付けられたログインは存在しません。 包含データベース ユーザー モデルでは、Windows 認証 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[ssSDS](../../includes/sssds-md.md)] の両方) がどちらもサポートされます。 包含データベース ユーザーとして接続するには必ず、ユーザー データベースのパラメーターが接続文字列に含まれている必要があります。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] はそれを基に、認証プロセスがどちらのデータベースで管理されるかを判別します。 包含データベース ユーザーのアクティビティは、そのユーザーを認証するデータベースに限定されます。そのため包含データベース ユーザーとして接続しているときは、そのユーザーが必要とする個々のデータベースに、ユーザー アカウントを別々に作成する必要があります。 データベースを切り替えるには、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ユーザー側で新しい接続を作成する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内の包含データベース ユーザーは、別のデータベースに同一ユーザーが存在する場合、データベースを切り替えることができます。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]に関しては、従来のモデルから包含データベース ユーザー モデルに切り替える際、接続文字列に対する変更は不要です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続の場合は、データベースの名前を接続文字列に追加する必要があります (既に存在する場合は不要)。  
  
> [!IMPORTANT]  
>  従来型のモデルを使用した場合、サーバー レベルのロールとサーバー レベルの権限ですべてのデータベースに対するアクセスを制限できます。 包含データベース モデルを使用した場合、データベース所有者と ALTER ANY USER 権限を持ったデータベース ユーザーとがデータベースに対するアクセス権を付与できます。 これにより高い権限を与えられたサーバー ログインのアクセス制御範囲は狭められ、高い権限を与えられたデータベース ユーザーのアクセス制御範囲は拡大します。  
  
## <a name="firewalls"></a>ファイアウォール  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Windows ファイアウォール ルールはすべての接続に適用され、ログイン (従来のモデルの接続) と包含データベース ユーザーに同じ影響を及ぼします。 Windows ファイアウォールの詳細については、「 [データベース エンジン アクセスを有効にするための Windows ファイアウォールを構成する](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)」を参照してください。  
  
### <a name="includesssdsincludessssds-mdmd-firewalls"></a>[!INCLUDE[ssSDS](../../includes/sssds-md.md)] ファイアウォール  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] では、サーバー レベルの接続 (ログイン) 用とデータベース レベルの接続 (包含データベース ユーザー) 用にファイアウォール規則を切り離すことができます。 ユーザー データベースに接続すると、最初にデータベースのファイアウォール規則がチェックされます。 データベースへのアクセスを許可する規則が存在しない場合は、サーバー レベルのファイアウォール規則がチェックされます。これには、論理サーバーのマスター データベースへのアクセスが必要です。 データベース レベルのファイアウォール規則と包含データベース ユーザーを組み合わせることで、接続中にサーバーのマスター データベースにアクセスする必要がなくなり、接続のスケーラビリティが向上します。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] のファイアウォール規則の詳細については、次のトピックを参照してください。  
  
-   [Azure SQL Database ファイアウォール](https://msdn.microsoft.com/library/azure/ee621782.aspx)  
  
-   [方法:ファイアウォール設定を構成する (Azure SQL Database)](https://msdn.microsoft.com/library/azure/jj553530.aspx)  
  
-   [sp_set_firewall_rule &#40;Azure SQL データベース&#41;](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)  
  
-   [sp_set_database_firewall_rule &#40;Azure SQL データベース&#41;](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)  
  
## <a name="syntax-differences"></a>構文上の違い  
  
|従来のモデル|包含データベース ユーザー モデル|  
|-----------------------|-----------------------------------|  
|master データベースに接続する場合:<br /><br /> `CREATE LOGIN login_name  WITH PASSWORD = 'strong_password';`<br /><br /> 次にユーザー データベースに接続する場合:<br /><br /> `CREATE USER 'user_name' FOR LOGIN 'login_name';`|ユーザー データベースにする場合:<br /><br /> `CREATE USER user_name  WITH PASSWORD = 'strong_password';`|  
  
|従来のモデル|包含データベース ユーザー モデル|  
|-----------------------|-----------------------------------|  
|master データベースのコンテキストでパスワードを変更するには:<br /><br /> `ALTER LOGIN login_name  WITH PASSWORD = 'strong_password';`|ユーザー データベースのコンテキストでパスワードを変更するには:<br /><br /> `ALTER USER user_name  WITH PASSWORD = 'strong_password';`|  
  
## <a name="remarks"></a>コメント  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに対して包含データベース ユーザーを有効にする必要があります。 詳細については、「 [contained database authentication Server Configuration Option](../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md)」を参照してください。  
  
-   包含データベース ユーザーとログインの名前が重複しない場合は、アプリケーションで共存させることができます。  
  
-   **name1** という名前のログインが master データベースに存在し、なおかつ **name1**という名前の包含データベース ユーザーを作成した場合、接続文字列でデータベース名を指定すると、そのデータベースに接続するときのログイン コンテキストよりも、データベース ユーザーのコンテキストが優先されます。 つまり、包含データベース ユーザーは、同じ名前のログインに優先します。  
  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)] では、包含データベース ユーザーの名前を、サーバーの管理者アカウントと同じ名前にすることはできません。  
  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーの管理者アカウントは、包含データベース ユーザーにできません。 サーバー管理者は、包含データベース ユーザーを作成し、管理するための十分な権限を持っています。 サーバー管理者は、ユーザー データベースの包含データベース ユーザーに権限を付与できます。  
  
-   包含データベース ユーザーはデータベース レベル プリンシパルであるため、使用するすべてのデータベースで包含データベース ユーザーを作成する必要があります。 ID はデータベースに限定され、同じサーバー内の別のデータベースで同じ名前とパスワードを持つユーザーとは完全に独立しています。  
  
-   通常のログインで使用するパスワードと同じ強度のパスワードを使用します。  
  
## <a name="see-also"></a>参照  
 [包含データベース](../databases/contained-databases.md)   
 [包含データベースでのセキュリティのベスト プラクティス](../databases/security-best-practices-with-contained-databases.md)   
 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)  
  
  
