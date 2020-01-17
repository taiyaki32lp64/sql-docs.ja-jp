---
title: スクリプトに関する権限の付与
description: SQL Server Machine Learning Services で R および Python スクリプトの実行に対するデータベース ユーザーの権限を付与する方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9b8d3ea5c52c5c18f09097322fdc1e1b2321494e
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727309"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services にユーザー 権限を付与する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、SQL Server Machine Learning Services で外部スクリプトを実行する権限をユーザーに付与する方法とデータベースに対する読み取り、書き込み、またはデータ定義言語 (DDL) の権限を付与する方法について説明します。

詳細については、「[機能拡張フレームワークのセキュリティ概要](../../advanced-analytics/concepts/security.md#permissions)」の「権限」セクションを参照してください。

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>スクリプトを実行する権限

自分で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールし、独自のインスタンスで R または Python スクリプトを実行している場合は、通常、管理者としてスクリプトを実行します。 そのため、データベース内のさまざまな操作とすべてのデータに対して暗黙的な権限を持っています。

ただし、ほとんどのユーザーには、このような管理者権限はありません。 たとえば、SQL ログインを使用してデータベースにアクセスする組織内のユーザーには、通常、管理者権限がありません。 そのため、R または Python を使用している毎ユーザーに対して、言語が使用されている各データベースで外部スクリプトを実行する権限を Machine Learning Services のユーザーに付与する必要があります。 その方法は次のとおりです。

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> サポートされているスクリプト言語には、権限が固有ではありません。 言い換えると、R スクリプトと Python スクリプトには個別の権限レベルがありません。 これらの言語に対して個別の権限を保持する必要がある場合は、R と Python を別々のインスタンスにインストールします。

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>データベースの権限の許可

ユーザーがスクリプトを実行している間、ユーザーは他のデータベースからデータを読み取ることが必要になる場合があります。 ユーザーは、結果を格納したり、テーブルにデータを書き込んだりするために、新しいテーブルを作成することが必要になる場合もあります。

R または Python スクリプトを実行している Windows ユーザー アカウントまたは SQL ログインごとに、特定のデータベースに対する適切なアクセス許可を持っていることを確認します。これには、データを読み取るための `db_datareader`、オブジェクトをデータベースに保存するための `db_datawriter`、およびトレーニングおよびシリアル化されたデータを含むストアド プロシージャまたはテーブルなどのオブジェクトを作成する `db_ddladmin` が含まれます。

たとえば、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでは、SQL ログインである *MySQLLogin* に、*ML_Samples* データベースで T-SQL クエリを実行する権限を与えています。 このステートメントを実行するには、SQL ログインがサーバーのセキュリティ コンテキストに既に存在している必要があります。

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>次の手順

各ロールに含まれる権限の詳細については、「[データベース レベルのロール](../../relational-databases/security/authentication-access/database-level-roles.md)」をご覧ください。