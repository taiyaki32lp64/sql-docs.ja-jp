---
title: サービスの SID を使用してサービスにアクセス許可を付与する
ms.custom: seo-dt-2019
author: randomnote1
ms.author: dareist
ms.date: 05/02/2019
ms.topic: conceptual
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.openlocfilehash: 18ac490c514703d890f2a1075602494fff81749a
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095598"
---
# <a name="using-service-sids-to-grant-permissions-to-services-in-sql-server"></a>サービスの SID を使用して SQL Server のサービスにアクセス許可を付与する

SQL Server では、特定のサービスにアクセス許可を直接付与できるようにするために、[サービスごとのセキュリティ識別子 (SID)](https://support.microsoft.com/help/2620201/sql-server-uses-a-service-sid-to-provide-service-isolation) が使用されます。 この方法は、エンジン サービスおよびエージェント サービス (それぞれ、NT SERVICE\MSSQL$<InstanceName> および NT SERVICE\SQLAGENT$<InstanceName>) にアクセス許可を付与するために、SQL Server によって使用されます。 この方法を使用すると、それらのサービスからデータベース エンジンにアクセスできるのは、サービスが実行されている場合のみとなります。

その他のサービスにアクセス許可を付与する場合も、これと同じ方法を使用できます。 サービス SID を使用すると、サービス アカウントを管理および維持するのにかかるオーバーヘッドが不要になり、システム リソースに付与するアクセス許可をより厳密により細かく制御することができます。

サービス SID を使用できるサービスの例を次に示します。

- System Center Operations Manager ヘルス サービス (NT SERVICE\HealthService)
- Windows Server フェールオーバー クラスタリング (WSFC) サービス (NT SERVICE\ClusSvc)

一部のサービスには、既定ではサービス SID がありません。 サービス SID は、[SC.exe](/windows/desktop/services/configuring-a-service-using-sc) を使用して作成する必要があります。 [この方法](https://kevinholman.com/2016/08/25/sql-mp-run-as-accounts-no-longer-required/)は、SQL Server 内でヘルス サービスにアクセス許可を付与するために Microsoft System Center Operations Manager 管理者によって採用されています。

サービス SID を作成し確定したら、SQL Server 内でそれにアクセス許可を付与する必要があります。 アクセス許可を付与するには、[SQL Server Management Studio (SSMS)](/sql/ssms/download-sql-server-management-studio-ssms) またはクエリのいずれかを使用して Windows ログインを作成します。 ログインを作成したら、他の任意のログインと同様に、アクセス許可を付与し、ロールに追加し、データベースにマップすることがします。

> [!TIP]
> エラー `Login failed for user 'NT AUTHORITY\SYSTEM'` が返された場合は、目的のサービスに対してサービス SID が存在すること、SQL Server 内でサービス SID ログインが作成されていること、SQL Server 内でサービス SID に適切なアクセス許可が付与されていることを確認します。

## <a name="security"></a>Security

### <a name="eliminate-service-accounts"></a>サービス アカウントを不要にする

従来は、サービス アカウントを使用して、SQL Server へのログインをサービスに許可していました。 サービス アカウントを使用すると、サービス アカウントのパスワードを維持し定期的に更新する必要があるため、管理の複雑さがさらに増します。 さらに、インスタンス内でアクションを実行するときに自分のアクティビティをマスクしようとする個人によってサービス アカウントの資格情報が使用される可能性があります。

### <a name="granular-permissions-to-system-accounts"></a>システム アカウントに対するきめ細かいアクセス許可

これまで、システム アカウントにアクセス許可を付与するには、[LocalSystem](https://msdn.microsoft.com/library/windows/desktop/ms684190) ([en-us で NT AUTHORITY\SYSTEM](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions#Localized_service_names)) または [NetworkService](/windows/desktop/Services/networkservice-account) ([en-us で NT AUTHORITY\NETWORK SERVICE](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions?#Localized_service_names)) アカウント用のログインを作成し、それらのログインにアクセス許可を付与していました。 この方法では、システム アカウントとして実行されている SQL への任意のプロセスまたはサービスのアクセス許可が付与されます。

サービス SID を使用すると、特定のサービスにアクセス許可を付与することができます。 そのサービスは、実行時にアクセス許可を与えられたリソースにのみアクセスできます。 たとえば、`HealthService` が `LocalSystem` として実行されていて、それに `View Server State` が付与されている場合、`LocalSystem`アカウントは、`HealthService` のコンテキストで実行されているときに、`View Server State` に対してのみアクセスできます。 その他のどのプロセスが `LocalSystem` として SQL のサーバー状態にアクセスを試みても、アクセスは拒否されます。

## <a name="examples"></a>使用例

### <a name="a-create-a-service-sid"></a>A. サービス ID を作成する

次の PowerShell コマンドでは、System Center Operations Manager ヘルス サービス上にサービス SID が作成されます。

```PowerShell
sc.exe --% sidtype "HealthService" unrestricted
```

> [!IMPORTANT]
> `--%` は、コマンドの残りの部分の解析を停止するように PowerShell に指示します。 これは、レガシ コマンドとアプリケーションを使用する場合に便利です。

### <a name="b-query-a-service-sid"></a>B. サービス SID を照会する

サービス SID を確認する場合、またはサービス SID が存在することを確認する場合には、PowerShell で次のコマンドを実行します。

```PowerShell
sc.exe --% qsidtype "HealthService"
```

> [!IMPORTANT]
> `--%` は、コマンドの残りの部分の解析を停止するように PowerShell に指示します。 これは、レガシ コマンドとアプリケーションを使用する場合に便利です。

### <a name="c-add-a-newly-created-service-sid-as-a-login"></a>C. 新しく作成したサービス SID をログインとして追加する

次の例では、T-SQL を使用して、System Center Operations Manager ヘルス サービス用のログインを作成します。

```SQL
CREATE LOGIN [NT SERVICE\HealthService] FROM WINDOWS
GO
```

### <a name="d-add-an-existing-service-sid-as-a-login"></a>D. 既存のサービス SID をログインとして追加する

次の例では、T-SQL を使用して、クラスター サービス用のログインを作成します。 クラスター サービスにアクセス許可を直接付与すれば、SYSTEM アカウントに過剰なアクセス許可を付与する必要がなくなります。

```SQL
CREATE LOGIN [NT SERVICE\ClusSvc] FROM WINDOWS
GO
```

### <a name="e-grant-permissions-to-a-service-sid"></a>E. サービス SID にアクセス許可を付与する

可用性グループを管理するために必要なアクセス許可をクラスター サービスに付与します。

```SQL
GRANT ALTER ANY AVAILABILITY GROUP TO 'NT SERVICE\ClusSvc'
GO

GRANT CONNECT SQL TO 'NT SERVICE\ClusSvc'
GO

GRANT VIEW SERVER STATE TO 'NT SERVICE\ClusSvc'
GO
```

## <a name="next-steps"></a>次の手順

サービス SID 構造体の詳細について、「[SERVICE_SID_INFO structure](/windows/win32/api/winsvc/ns-winsvc-service_sid_info)」 (SERVICE_SID_INFO 構造体) を参照してください。

[ログインを作成](/sql/t-sql/statements/create-login-transact-sql)するときに使用できるその他のオプションについて確認してください。

ロール ベースのセキュリティをサービス SID と一緒に使用するために、SQL Server で[ロールを作成](/sql/t-sql/statements/create-role-transact-sql)する方法を確認してください。

SQL Server 内でサービス SID に[アクセス許可を付与](/sql/t-sql/statements/grant-transact-sql)するさまざまな方法について確認してください。
