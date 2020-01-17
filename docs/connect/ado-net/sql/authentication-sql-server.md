---
title: SQL Server での認証
description: SQL Server のログインと認証について説明し、その他のリソースへのリンクを示します。
ms.date: 09/26/2019
dev_langs:
- csharp
ms.assetid: 646ddbf5-dd4e-4285-8e4a-f565f666c5cc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: eb528eb1045788469b0eb31491fd654997831468
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452311"
---
# <a name="authentication-in-sql-server"></a>SQL Server での認証

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server は、Windows 認証モードと混合モードという 2 つの認証モードをサポートしています。  
  
- Windows 認証は既定の認証モードです。この SQL Server セキュリティ モデルは Windows と緊密に統合されているため、多くの場合、統合セキュリティと呼ばれます。 特定の Windows ユーザーアカウントとグループアカウントは、SQL Server にログインするために信頼されています。 既に認証されている Windows ユーザーは、追加の資格情報を提示する必要はありません。  
  
- 混合モードは、Windows による認証と SQL Server による認証の両方がサポートされます。 ユーザー名とパスワードの組み合わせは、SQL Server 内で管理されます。  
  
> [!IMPORTANT]
> 可能な限り、Windows 認証を使用することをお勧めします。 Windows 認証では、暗号化された一連のメッセージを使用して SQL Server のユーザーを認証します。 SQL Server ログインを使用した場合、SQL Server のログイン名と暗号化されたパスワードがネットワーク経由で渡されるためセキュリティが低下します。  
  
Windows 認証では、既に Windows にログオンしているユーザーが別途 SQL Server にログオンする必要はありません。 次の `SqlConnection.ConnectionString` では Windows 認証が指定されるため、ユーザー名もパスワードもユーザーに要求させません。  
  
```csharp
"Server=MSSQL1;Database=AdventureWorks;Integrated Security=true;  
```  
  
> [!NOTE]
> ログインはデータベースユーザーとは異なります。 ログインまたは Windows グループは、別の操作でデータベースユーザーまたはロールにマップする必要があります。 次に、データベースオブジェクトにアクセスするためのアクセス許可をユーザーまたはロールに付与します。  
  
## <a name="authentication-scenarios"></a>認証シナリオ  
Windows 認証は、通常、次のような場合に最適な選択肢です。  
  
- ドメインコントローラーがあります。  
  
- アプリケーションとデータベースが同じコンピューター上にある。  
  
- SQL Server Express または LocalDB のインスタンスを使用している。  
  
SQL Server のログインは、次の状況でよく使用されます。  
  
- ワークグループがある場合。  
  
- ユーザーは、信頼されていない別のドメインから接続します。  
  
- ASP.NET などのインターネットアプリケーション。  
  
> [!NOTE]
> Windows 認証を指定しても、SQL Server ログインは無効になりません。 高い権限を持つ SQL Server ログインを無効にするには、Transact-SQL ステートメント ALTER LOGIN DISABLE を使用します。  
  
## <a name="login-types"></a>ログインの種類  
SQL Server では、次の 3 種類のログインがサポートされています。  
  
- ローカル Windows ユーザーアカウントまたは信頼されたドメインアカウント。 SQL Server が Windows に依存する形で Windows ユーザー アカウントを認証します。  
  
- Windows グループ。 Windows グループへのアクセス権を付与すると、そのグループのメンバーであるすべての Windows ユーザーログインへのアクセス権が付与されます。  
  
- SQL Server ログイン SQL Server はユーザー名およびパスワードのハッシュを master データベースに格納し、内部の認証方法を使ってログイン試行を検証します。  
  
> [!NOTE]
> SQL Server では、証明書または非対称キーから作成されたログインが提供されています。このログインはコード署名にのみ使用されます。 SQL Server への接続には使用できません。  
  
## <a name="mixed-mode-authentication"></a>混合モード認証  
混合モード認証を使用する場合は、SQL Server に格納される SQL Server ログインを作成する必要があります。 さらに、SQL Server のユーザー名とパスワードを実行時に指定する必要があります。  
  
> [!IMPORTANT]
> SQL Server は、`sa` という名前の SQL Server ログイン ("システム管理者" の省略形) を使用してインストールされます。 `sa` ログインに強力なパスワードを割り当て、アプリケーションで `sa` ログインを使用しないようにします。 `sa` ログインは `sysadmin` 固定サーバーロールにマップされます。このロールには、サーバー全体で後管理者の資格情報が割り当てられています。 攻撃者がシステム管理者としてアクセス権を獲得した場合、潜在的な損害に対する制限はありません。 既定では、Windows `BUILTIN\Administrators` グループ (ローカル管理者のグループ) のすべてのメンバーが `sysadmin` ロールに所属しますが、そのロールから削除することもできます。  
  
> [!IMPORTANT]
> 接続文字列をユーザー入力から連結すると、接続文字列インジェクション攻撃に対して脆弱なままになる可能性があります。 実行時に構文的に有効な接続文字列を作成するには、<xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> を使用します。 
  
## <a name="external-resources"></a>外部リソース  
詳細については、次のリソースを参照してください。  
  
|リソース|[説明]|  
|--------------|-----------------|  
|[プリンシパル](../../../relational-databases/security/authentication-access/principals-database-engine.md)|SQL Server のログインおよびその他のセキュリティ プリンシパルについて説明します。|  
  
## <a name="next-steps"></a>次の手順
- [SQL Server におけるアプリケーション セキュリティのシナリオ](application-security-scenarios-sql-server.md)
