---
title: Azure Key Vault のカスタマー マネージド キーでよく発生するエラー
description: Transparent Data Encryption (TDE) と Azure Key Vault (AKV) のカスタマー マネージド キーでよく発生するエラーを解決します。
ms.custom: seo-lt-2019
helpviewer_keywords:
- troublshooting, tde akv
- tde akv configuration, troubleshooting
- tde troubleshooting
author: jaszymas
ms.prod: sql
ms.technology: security
ms.reviewer: vanto
ms.topic: conceptual
ms.date: 11/06/2019
ms.author: jaszymas
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 40584dda23d36af385b9cae5457377838694be6e
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558468"
---
# <a name="common-errors-for-transparent-data-encryption-with-customer-managed-keys-in-azure-key-vault"></a>Azure Key Vault のカスタマー マネージド キーを使った透過的なデータ暗号化に関する一般的なエラー

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md.md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]
この記事では、[Azure Key Vault のカスタマー マネージド キーで Transparent Data Encryption (TDE)](/azure/sql-database/transparent-data-encryption-byok-azure-sql) を使用するように構成されたデータベースがアクセスできなくなる原因となった、Azure Key Vault キーのアクセスに関する問題を特定して解決する方法について説明します。

## <a name="introduction"></a>はじめに
Azure Key Vault のカスタマー マネージド キーを使用するように TDE が構成されている場合、データベースをオンラインに保つには、この TDE 保護機能への継続的なアクセスが必要です。  論理 SQL サーバーが Azure Key Vault のカスタマー マネージド TDE 保護機能にアクセスできなくなった場合、データベースでは該当するエラー メッセージが表示されてすべての接続の拒否が始まり、Azure portal でその状態が *Inaccessible* になります。

最初の 8 時間以内に基になっている Azure Key Vault のキー アクセスの問題が解決されると、データベースは自動修復され、自動的にオンラインになります。 つまり、間欠的および一時的なネットワーク停止のシナリオでは、ユーザーによる対応は必要なく、データベースは自動的にオンラインになります。 ほとんどの場合、基になっている Key Vault のキー アクセスの問題を解決するには、ユーザーによる対応が必要です。 

アクセスできないデータベースがもう必要ない場合は、すぐに削除してコストを抑えることができます。 Azure Key Vault キーへのアクセスが復元され、データベースがオンラインに戻るまで、データベースに対する他のすべての操作は許可されません。 カスタマー マネージド キーで暗号化されたデータベースにアクセスできない間は、サーバーで TDE のオプションをカスタマー マネージド キーからサービス マネージド キーに変更することもできません。 これは、TDE 保護機能へのアクセス許可が取り消されているときに、データを不正アクセスから保護するために必要です。 

データベースにアクセスできない期間が 8 時間を超えると、自動修復は行われなくなります。 この期間の後に必要な Azure Key Vault のキー アクセスが復元された場合は、手動でアクセスを再検証して、データベースをオンラインに戻す必要があります。 この状況でデータベースをオンラインに戻す場合は、データベースのサイズによってはかなり時間がかかることがあり、現在はサポート チケットが必要になります。 データベースがオンラインに戻ると、Geo-DR が構成されていた場合の geo リンク、PITR 履歴、タグなどの以前に構成した設定は失われます。 そのため、基になっている Key Vault のキー アクセスの問題にできる限り早く気付き、対処できるように、[アクション グループ](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups)を使用して通知システムを実装することをお勧めします。 

## <a name="common-errors-causing-databases-to-become-inaccessible"></a>データベースにアクセスできなくなる原因となる一般的なエラー

Key Vault による TDE を使用しているときに発生する問題のほとんどは、次の構成ミスのいずれかが原因です。

### <a name="the-key-vault-is-unavailable-or-doesnt-exist"></a>キー コンテナーが使用できない、または存在しない

- キー コンテナーが誤って削除された。
- Azure Key Vault に対してファイアウォールが構成されたが、そこで Microsoft サービスへのアクセスが許可されていない。
- 間欠的なネットワーク エラーのために、キー コンテナーを使用できない。

### <a name="no-permissions-to-access-the-key-vault-or-the-key-doesnt-exist"></a>キー コンテナーへのアクセス許可がない、またはキーが存在しない

- キーが誤って削除された、無効にされた、またはキーの有効期限が切れた。
- 論理 SQL Server インスタンスの AppId が誤って削除された。
- 論理 SQL Server インスタンスが別のサブスクリプションに移動された。 論理サーバーが別のサブスクリプションに移動された場合、新しい AppId を作成する必要があります。
- キー用の AppId に付与されているアクセス許可が不十分 (取得、ラップ、ラップ解除が含まれていない)。
- 論理 SQL Server インスタンスの AppId に対するアクセス許可が取り消された。

## <a name="identify-and-resolve-common-errors"></a>一般的なエラーの識別と解決

このセクションでは、最も一般的なエラーに対するトラブルシューティング手順の一覧を示します。

### <a name="missing-server-identity"></a>サーバー ID がない

**エラー メッセージ**

"_401 AzureKeyVaultNoServerIdentity - サーバーでサーバー ID が正しく構成されていません。サポートにお問い合わせください。_ "

**検出**

次のコマンドレットまたはコマンドを使用して、論理 SQL Server インスタンスに ID が割り当てられていることを確認します。

- Azure PowerShell:[Get-AzureRMSqlServer](https://docs.microsoft.com/powershell/module/AzureRM.Sql/Get-AzureRmSqlServer?view=azurermps-6.13.0) 

- Azure CLI: [az-sql-server-show](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-show)

**軽減策**

次のコマンドレットまたはコマンドを使用して、論理 SQL Server インスタンス用の Azure AD ID (AppId) を構成します。

- Azure PowerShell:`-AssignIdentity` オプションを指定した [Set-AzureRmSqlServer](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqlserver?view=azurermps-6.13.0)。

- Azure CLI: `--assign_identity` オプションを指定した [az sql server update](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-update)。

Azure portal では、キー コンテナーに移動してから、 **[アクセス ポリシー]** に移動します。 以下の手順を実行します。 

 1. **[新規追加]** ボタンを使用して、前の手順で作成したサーバーの AppId を追加します。 
 1. 次のキー アクセス許可を割り当てます。取得、ラップ、ラップ解除 

詳細については、「[サーバーに Azure AD ID を割り当てる](/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure#assign-an-azure-ad-identity-to-your-server)」をご覧ください。

> [!IMPORTANT]
> Key Vault による TDE の初期構成後に論理 SQL Server インスタンスが新しいテナントに移動された場合、Azure AD ID を構成する手順を繰り返して、新しい AppId を作成します。 その後、その AppId をキー コンテナーに追加し、キーに適切なアクセス許可を割り当てます。 
>

### <a name="missing-key-vault"></a>キー コンテナーがない

**エラー メッセージ**

"_503 AzureKeyVaultConnectionFailed - Azure Key Vault への接続の試みが失敗したため、サーバーでの操作を完了できませんでした_"

**検出**

キー URI とキー コンテナーを識別するには:

1. 次のコマンドレットまたはコマンドを使用して、特定の論理 SQL Server インスタンスのキー URI を取得します。

    - Azure PowerShell:[Get-AzureRmSqlServerKeyVaultKey](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey?view=azurermps-6.13.0)

    - Azure CLI: [az-sql-server-tde-key-show](https://docs.microsoft.com/cli/azure/sql/server/tde-key?view=azure-cli-latest#az-sql-server-tde-key-show) 

1. キー URI を使用して、キー コンテナーを識別します。

    - Azure PowerShell:$MyServerKeyVaultKey 変数のプロパティを検査して、キー コンテナーの詳細を取得できます。

    - Azure CLI:キー コンテナーの詳細について、返されるサーバー暗号化プロテクターを検査します。

**軽減策**

キー コンテナーを使用できることを確認します。

- キー コンテナーを使用でき、論理 SQL Server インスタンスにアクセス権があることを確認します。
- キー コンテナーがファイアウォールの背後にある場合は、Microsoft サービスによるキー コンテナーへのアクセスを許可するチェック ボックスがオンになっていることを確認します。
- キー コンテナーが誤って削除された場合は、最初から構成を完了する必要があります。


### <a name="missing-key"></a>キーがない

**エラー メッセージ**

"_404 ServerKeyNotFound - The requested server key was not found on the current subscription._ " (404 ServerKeyNotFound - 要求されたサーバー キーは、現在のサブスクリプションで使用できません。) 

"_409 ServerKeyDoesNotExists - The server key does not exist._ " (409 ServerKeyDoesNotExists - サーバー キーは存在しません。)

**検出**

キー URI とキー コンテナーを識別するには:

- 「[キー コンテナーがない](#missing-key-vault)」のコマンドレットまたはコマンドを使用して、論理 SQL Server インスタンスに追加されたキー URI を識別します。 コマンドを実行すると、キーの一覧が返されます。

**軽減策**

TDE プロテクターが Key Vault に存在することを確認します。

1. キー コンテナーを識別した後、Azure portal でそのキー コンテナーに移動します。
1. キー URI によって識別されたキーが存在することを確認します。

### <a name="missing-permissions"></a>アクセス許可がない

**エラー メッセージ**

"_401 AzureKeyVaultMissingPermissions - The server is missing required permissions on the Azure Key Vault._ " (401 AzureKeyVaultMissingPermissions - サーバーには Azure Key Vault に必要なアクセス許可がありません。)

**検出**

キー URI とキー コンテナーを識別するには: 

- 「[キー コンテナーがない](#missing-key-vault)」のコマンドレットまたはコマンドを使用して、論理 SQL Server インスタンスによって使用されるキー コンテナーを識別します。

**軽減策**

論理 SQL Server インスタンスにキー コンテナーへのアクセス許可と、キーにアクセスするための適切なアクセス許可があることを確認します。

- Azure portal で、キー コンテナー > **[アクセス ポリシー]** の順に移動します。 論理 SQL Server インスタンスの AppId を探します。  
- AppId が存在する場合は、その AppId に次のキー アクセス許可があることを確認します。取得、ラップ、ラップ解除。
- AppId が存在しない場合は、 **[新規追加]** ボタンを使用して、それを追加します。 

## <a name="getting-tde-status-from-the-activity-log"></a>アクティビティ ログから TDE の状態を取得する

Azure Key Vault のキー アクセスの問題によるデータベースの状態を監視できるように、Azure Resource Manager の URL と Subscription+Resourcegroup+ServerName+DatabseName に基づいて、次のイベントがリソース ID の[アクティビティ ログ](https://docs.microsoft.com/azure/service-health/alerts-activity-log-service-notifications)に記録されます。 

**サービスが Azure Key Vault のキーにアクセスできなくなったときのイベント**

イベント名: MakeDatabaseInaccessible 

状態:Started 

説明:データベースは、Azure Key Vault のキーにアクセスできなくなったため、現在はアクセスできません: <error message>   

 

**自己修復の 8 時間の待機時間が開始したときのイベント** 

イベント名: MakeDatabaseInaccessible 

状態:InProgress 

説明:データベースは、8 時間以内にユーザーによって Azure Key Vault のキー アクセスが再確立されるのを待機しています。   

 

**データベースが自動的にオンラインに戻ったときのイベント**

イベント名: MakeDatabaseAccessible 

状態:成功 

説明:Azure Key Vault のキーへのデータベース アクセスが再確立され、データベースがオンラインになりました。 

 

**8 時間以内に問題が解決されず、Azure Key Vault のキー アクセスを手動で検証する必要がある場合のイベント** 

イベント名: MakeDatabaseInaccessible 

状態:成功 

説明:データベースはアクセスできない状態であり、ユーザーは Azure Key Vault のエラーを解決し、再検証キーを使用して Azure Key Vault のキーへのアクセスを再確立する必要があります。 

 

**手動によるキーの再検証後にデータベースがオンラインになったときのイベント**

イベント名: MakeDatabaseAccessible 

状態:成功 

説明:Azure Key Vault のキーへのデータベース アクセスが再確立され、データベースがオンラインになりました。 

 

**Azure Key Vault のキー アクセスの再検証が成功し、データベースがオンラインに戻ったときのイベント**

イベント名: MakeDatabaseAccessible 

状態:Started 

説明:Azure Key Vault のキーへのデータベース アクセスの復元が開始されました。 

 

**Azure Key Vault のキー アクセスの再検証が失敗したときのイベント**

イベント名: MakeDatabaseAccessible 

状態:失敗 

説明:Azure Key Vault のキーへのデータベース アクセスの復元が失敗しました。 


## <a name="next-steps"></a>次のステップ

- [Azure Resource Health](https://docs.microsoft.com/azure/service-health/resource-health-overview) について学習する。
- 電子メール/SMS/プッシュ/音声、ロジック アプリ、Webhook、ITSM、Automation Runbook などの設定に基づいて、通知とアラートを受け取る[アクション グループ](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups)を設定します。 


