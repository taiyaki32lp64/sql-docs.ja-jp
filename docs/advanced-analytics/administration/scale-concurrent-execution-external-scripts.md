---
title: スクリプトの同時実行のスケーリング
description: SQL Server Machine Learning Services をスケーリングするために、ユーザー アカウント プールで R および Python スクリプトの並列または同時実行を構成します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: c10f92bcb0f8b64441ad4b088c4b8b3e2f62236b
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727694"
---
# <a name="scale-concurrent-execution-of-external-scripts-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services での外部スクリプトの同時実行のスケーリング
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server Machine Learning Services のワーカー アカウントについて、および外部スクリプトの同時実行数をスケーリングするよう既定の構成を変更する方法について説明します。

[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] サービスによるタスクの実行をサポートするために、Machine Learning Services のインストール プロセスの一部として、新しい Windows "*ユーザー アカウント プール*" が作成されました。 これらのワーカー アカウントの目的は、異なる SQL Server ユーザーによる外部スクリプトの同時実行を隔離することです。

> [!Note]
> SQL Server 2019 では、**SQLRUserGroup** には、複数のワーカー アカウントではなく、1 つの SQL Server Launchpad サービス アカウントであるメンバーが 1 つだけあります。 この記事では、SQL Server 2016 および 2017 のワーカー アカウントについて説明します。

## <a name="worker-account-group"></a>ワーカー アカウント グループ

Windows アカウント グループは、機械学習がインストールされて有効になっているインスタンスごとに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップによって作成されます。

- 既定のインスタンスでは、グループ名は **SQLRUserGroup** です。 この名前は、Python と R のうちの一方を使用している場合も、これらの両方を使用している場合も同じです。
- 名前付きインスタンスでは、既定のグループ名にインスタンス名が付加されます: たとえば、 **SQLRUserGroupMyInstanceName**。

既定では、ユーザー アカウント プールには 20 個のユーザー アカウントが含まれています。 ほとんどの場合、20 個で機械学習タスクを十分サポートできますが、アカウント数を変更することもできます。 アカウントの最大数は 100 です。

- 既定のインスタンスでは、個々のアカウントは **MSSQLSERVER01** ～ **MSSQLSERVER20** と命名されます。
- 名前付きインスタンスの場合、個々のアカウントはインスタンス名に基づいて命名されます。たとえば、 **MyInstanceName01** ～ **MyInstanceName20**。

複数のインスタンスが機械学習を使用する場合、コンピューターには複数のユーザー グループが存在します。 グループはインスタンス間で共有できません。

<a name = "HowToChangeGroup"> </a>

## <a name="number-of-worker-accounts"></a>ワーカー アカウントの数

アカウント プール内のユーザー数を変更するには、以下に示すように、[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] サービスのプロパティを編集する必要があります。

各ユーザー アカウントに関連付けられるパスワードはランダムに生成されますが、アカウントの作成後に変更することもできます。

1. SQL Server 構成マネージャーを開き、 **[SQL Server のサービス]** をクリックします。
2. SQL Server スタート パッド サービスをダブルクリックし、サービスが実行されている場合は、サービスを停止します。
3.  **[サービス]** タブで、[開始モード] が [自動] に設定されていることを確認します。 Launchpad が実行されていない場合、外部スクリプトは開始できません。
4.  **[詳細設定]** タブをクリックし、必要であれば、 **[外部ユーザーの数]** の値を編集します。 この設定により、外部スクリプト セッションを同時に実行できる SQL ユーザーの数を制御します。 既定値は、20 アカウントです。 ユーザーの最大数は 100 です。
5. パスワードを定期的に変更するポリシーが組織で実施されている場合は、オプションで、 **[外部ユーザーのパスワードのリセット]** を _[はい]_ に設定できます。 これを行うと、ユーザー アカウントに対してスタート パッドが保持している暗号化パスワードが再生成されます。 詳しくは、「[パスワード ポリシーの実施](../security/sql-server-launchpad-service-account.md#bkmk_EnforcePolicy)」をご覧ください。
6.  Launchpad サービスを再起動します。

## <a name="managing-workloads"></a>ワークロードの管理

このプール内のアカウントの数によって、同時にアクティブにできる外部スクリプト セッションの数が決まります。  既定では、20 個のアカウントが作成されます。つまり、20 名のユーザーが、アクティブな Python または R セッションを同時に利用できます。 同時に 20 個を超えるスクリプトを実行することが予想される場合は、ワーカー アカウントの数を増やすことができます。

同じユーザーが複数の外部スクリプトを同時に実行した場合、そのユーザーが実行したすべてのセッションで同じワーカー アカウントが使用されます。 たとえば、リソースが許す限り、1 名のユーザーが 100 個の Python または R スクリプトを同時に実行しても、1 つのワーカー アカウントを使用してすべてのスクリプトが実行されます。

サポートできるワーカー アカウントの数と、1 名のユーザーが同時に実行できるセッションの数は、サーバーのリソースによってのみ制限されます。 通常、Python または R ランタイムの使用時に遭遇する最初のボトルネックは、メモリです。

Python または R スクリプトで使用できるリソースは SQL Server によって管理されます。 SQL Server の DMV を使用してリソースの使用状況を監視するか、または関連する Windows ジョブ オブジェクトのパフォーマンス カウンターを見て、サーバー メモリの使用量を必要に応じて調整することをお勧めします。 SQL Server Enterprise Edition を使用している場合は、[外部リソース プール](how-to-create-a-resource-pool.md)を構成することで、外部スクリプトの実行に使用されるリソースを割り当てることができます。

## <a name="next-steps"></a>次の手順

- [SQL Server Management Studio のカスタム レポートを使用して Python および R のスクリプトの実行を監視する](../../advanced-analytics/administration/monitor-sql-server-machine-learning-services-using-custom-reports-management-studio.md)
- [動的管理ビュー (DMV) を使用して SQL Server Machine Learning Services を監視する](../../advanced-analytics/administration/monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)