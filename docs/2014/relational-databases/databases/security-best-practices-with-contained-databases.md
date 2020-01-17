---
title: 包含データベースでのセキュリティのベスト プラクティス | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- contained database, threats
ms.assetid: 026ca5fc-95da-46b6-b882-fa20f765b51d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 89a988a5d664e460a3148cf910c0be31ba07a5dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62916761"
---
# <a name="security-best-practices-with-contained-databases"></a>包含データベースでのセキュリティのベスト プラクティス
  包含データベースには固有の脅威があるので、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] の管理者はそれを理解し、危険性を軽減する必要があります。 脅威の多くは `USER WITH PASSWORD` 認証プロセスと関連しており、このプロセスでは認証の境界を[!INCLUDE[ssDE](../../includes/ssde-md.md)]のレベルからデータベースのレベルへと移します。  
  
## <a name="threats-related-to-users"></a>ユーザーに関連する脅威  
 持つ包含データベースのユーザー、`ALTER ANY USER`のメンバーなど、アクセス許可、 **db_owner**と**db_securityadmin**固定データベース ロールでなくても、データベースへのアクセスを与えることができます、知識、許可場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]管理者。 ユーザーに包含データベースへのアクセスを許可すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス全体に対する潜在的な攻撃の危険性が高まります。 管理者はこのアクセス制御の委任について理解し、包含データベースのユーザーへの `ALTER ANY USER` 権限の許可については十分に注意する必要があります。 すべてのデータベース所有者は `ALTER ANY USER` 権限を持ちます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者は、包含データベースのユーザーを定期的に監査する必要があります。  
  
### <a name="accessing-other-databases-using-the-guest-account"></a>guest アカウントによる他のデータベースへのアクセス  
 `ALTER ANY USER` 権限を持つデータベース所有者とデータベース ユーザーは、包含データベースのユーザーを作成できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの包含データベースに接続した後で、包含データベースのユーザーは [!INCLUDE[ssDE](../../includes/ssde-md.md)]上の、 **guest** アカウントを有効にしている他のデータベースにアクセスできます。  
  
### <a name="creating-a-duplicate-user-in-another-database"></a>別のデータベースへの重複するユーザーの作成  
 アプリケーションによっては、1 人のユーザーが複数のデータベースにアクセスできるようにすることが必要な場合があります。 この操作を行うには、各データベースに同一の包含データベース ユーザーを作成します。 パスワードを持つ 2 番目のユーザーを作成するときは、SID オプションを使用します。 次の例では、2 つのデータベースに 2 人の同一ユーザーを作成します。  
  
```  
USE DB1;  
GO  
CREATE USER Carlo WITH PASSWORD = '<strong password>';   
-- Return the SID of the user  
SELECT SID FROM sys.database_principals WHERE name = 'Carlo';  
  
-- Change to the second database  
USE DB2;  
GO  
CREATE USER Carlo WITH PASSWORD = '<same password>', SID = <SID from DB1>;  
GO  
```  
  
 データベースをまたがるクエリを実行するには、呼び出し元のデータベースに対して `TRUSTWORTHY` オプションを設定する必要があります。 たとえば、上で定義したユーザー (Carlo) が DB1 に存在する場合、`SELECT * FROM db2.dbo.Table1;` を実行するには、データベース DB1 に対して `TRUSTWORTHY` 設定が ON である必要があります。 `TRUSTWORHTY` 設定を ON に設定するには、次のコードを実行します。  
  
```  
ALTER DATABASE DB1 SET TRUSTWORTHY ON;  
```  
  
### <a name="creating-a-user-that-duplicates-a-login"></a>ログインが重複するユーザーの作成  
 パスワードを持つ包含データベース ユーザーが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと同じ名前を使用して作成された場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインが包含データベースを初期カタログとして指定して接続しようとすると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインは接続できません。 その接続は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに基づくユーザーとしてではなく、包含データベース上のパスワード プリンシパル付きの包含データベース ユーザーとして評価されます。 このことは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに対する意図的または偶発的なサービス拒否を引き起こす可能性があります。  
  
-   ベスト プラクティスとして、 **sysadmin** 固定サーバー ロールのメンバーは常に、初期カタログ オプションを使用せずに接続することを検討してください。 このようにすると、ログインが master データベースに接続されるので、データベースの所有者によるログイン試行の悪用を回避できます。 管理者を使用して、包含データベースに変更でき、 `USE` *\<データベース >* ステートメント。 また、ログインの既定のデータベースを包含データベースに設定することもできます。この場合、まず **master**へのログインが行われ、その後、ログインが包含データベースに転送されます。  
  
-   ベスト プラクティスとして、パスワードを持つ包含データベース ユーザーを作成する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと同じ名前にしないようにしてください。  
  
-   重複するログインが存在する場合に接続、**マスター** 、初期カタログを指定せずにデータベースし、実行、`USE`包含データベースに変更するコマンド。  
  
-   包含データベースが存在する場合、包含データベースではないデータベースのユーザーは、初期カタログを使用せずに [!INCLUDE[ssDE](../../includes/ssde-md.md)] に接続するか、初期カタログとして非包含データベースの名前を指定する必要があります。 こうすることで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の管理者による直接的な制御が及ばない部分のある包含データベースへの接続を回避できます。  
  
### <a name="increasing-access-by-changing-the-containment-status-of-a-database"></a>データベースの包含状態の変更によるアクセスの増加  
 ログインを持つ、`ALTER ANY DATABASE`のメンバーなど、アクセス許可、 **dbcreator**固定サーバー ロールを持つ、非包含データベースのユーザー、`CONTROL DATABASE`のメンバーなど、アクセス許可、 **db_owner**固定データベース ロール、データベースの包含設定を変更することができます。 データベースの包含設定が `NONE` から `PARTIAL` または `FULL` に変更された場合、パスワードを持つ包含データベース ユーザーを作成することで、ユーザー アクセスを許可できるようになります。 これは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者が認識せず、同意していないアクセスが可能になることを意味しています。 すべてのデータベースが、含まれていることをするを防ぐためには、設定、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] `contained database authentication`オプションを 0 にします。 パスワードを持つ包含データベース ユーザーによる選択された包含データベースへの接続を防ぐには、ログイン トリガーを使用して、パスワードを持つ包含データベース ユーザーによるログイン試行を取り消します。  
  
### <a name="attaching-a-contained-database"></a>包含データベースのインポート  
 包含データベースをアタッチすることにより、管理者が意図していないユーザーに [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスへのアクセスを許可する可能性があります。 この危険性を懸念する管理者は、データベースを `RESTRICTED_USER` モードでオンラインにすることができます。このモードでは、パスワードを持つ包含データベース ユーザーの認証を防ぐことができます。 ログインによって承認されたプリンシパルだけが、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]にアクセスできます。  
  
 ユーザーの作成時にはパスワード要件が有効で、パスワードが確認されますが、データベースがアタッチされるときにはパスワードの再確認が行われません。 包含データベースをアタッチすることによって、厳しいパスワード ポリシーのシステムで脆弱なパスワードが許可されるため、管理者はアタッチする [!INCLUDE[ssDE](../../includes/ssde-md.md)]での現在のパスワード ポリシーに準拠していないパスワードを許可する可能性があります。 管理者は、アタッチされているデータベースのすべてのパスワードのリセットを要求することによって、脆弱なパスワードの保持を回避できます。  
  
### <a name="password-policies"></a>パスワード ポリシー  
 データベースのパスワードを強力なパスワードにするように要求することはできますが、強固なパスワード ポリシーで保護することはできません。 Windows で使用可能なより広範なパスワード ポリシーを活用するために、できる限り Windows 認証を使用してください。  
  
### <a name="kerberos-authentication"></a>Kerberos 認証  
 パスワードを持つ包含データベース ユーザーは、Kerberos 認証を使用することはできません。 可能であれば、Windows 認証を使用して、Kerberos などの Windows の機能を利用してください。  
  
### <a name="offline-dictionary-attack"></a>オフライン辞書攻撃  
 パスワードを持つ包含データベース ユーザーのパスワード ハッシュは、包含データベースに格納されます。 データベース ファイルにアクセスできるユーザーはだれでも、パスワードを持つ包含データベース ユーザーに対する辞書攻撃を、監査されないシステム上で実行できます。 この脅威を軽減するには、データベース ファイルへのアクセスを制限するか、Windows 認証を使用する場合にのみ包含データベースへの接続を許可します。  
  
## <a name="escaping-a-contained-database"></a>包含データベースのエスケープ  
 データベースが部分的に包含されている場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者は包含データベースのユーザーとモジュールの機能を定期的に監査する必要があります。  
  
## <a name="denial-of-service-through-autoclose"></a>AUTO_CLOSE によるサービス拒否  
 包含データベースを自動終了するように構成しないでください。 自動終了すると、ユーザーの認証のためにデータベースを開くことで追加のリソースが消費されたり、サービス拒否攻撃が容易になったりします。  
  
## <a name="see-also"></a>関連項目  
 [包含データベース](contained-databases.md)   
 [部分的包含データベースへの移行](migrate-to-a-partially-contained-database.md)  
  
  
