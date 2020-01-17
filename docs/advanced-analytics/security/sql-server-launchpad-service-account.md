---
title: Launchpad アカウントの構成
description: SQL Server で外部スクリプトを実行するために使用される、SQL Server Launchpad サービス アカウントを変更する方法。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f05181e1a3069ec56f079751e43bd739424ce92
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727363"
---
# <a name="sql-server-launchpad-service-configuration"></a>SQL Server Launchpad のサービスの構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] は外部スクリプトを管理および実行するサービスで、フルテキスト インデックス作成およびクエリ サービスが、フルテキスト クエリを処理するために別のホストを起動する方法に似ています。

詳細については、「[SQL Server Machine Learning Services の機能拡張アーキテクチャ](../../advanced-analytics/concepts/extensibility-framework.md#launchpad)」および「[SQL Server Machine Learning Services の機能拡張フレームワークのセキュリティの概要](../../advanced-analytics/concepts/security.md#launchpad)」に関するページの Launchpad のセクションを参照してください。

## <a name="account-permissions"></a>アカウントのアクセス許可

既定では、SQL Server Launchpad は **NT Service\MSSQLLaunchpad** で実行されるように構成されています。これは、外部スクリプトの実行に必要なすべてのアクセス許可によりプロビジョニングされています。 このアカウントからアクセス許可を削除すると、Launchpad が起動に失敗するか、外部スクリプトを実行するはずの SQL Server インスタンスにアクセスできなくなる可能性があります。

サービス アカウントを変更する場合は、必ず [[ローカル セキュリティ ポリシー] コンソール](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings)を使用してください。

このアカウントに必要なアクセス許可を次の表に示します。

| グループ ポリシー設定 | 定数名 |
|----------------------|---------------|
| [プロセスのメモリ クォータの増加](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/adjust-memory-quotas-for-a-process) | SeIncreaseQuotaPrivilege | 
| [走査チェックのバイパス](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/bypass-traverse-checking) | SeChangeNotifyPrivilege | 
| [サービスとしてログオン](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) | SeServiceLogonRight | 
| [プロセス レベル トークンを置き換える](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/replace-a-process-level-token) | SeAssignPrimaryTokenPrivilege | 

SQL Server サービスの実行に必要なアクセス許可の詳細については、「[Configure Windows Service Accounts and Permissions (Windows サービス アカウントとアクセス許可の構成)](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」をご覧ください。

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>構成プロパティ

通常、サービス構成を変更する理由はありません。 変更できるプロパティには、サービス アカウント、外部プロセスの数 (既定では 20)、またはワーカー アカウントのパスワードのリセット ポリシーなどがあります。

1. [[SQL Server 構成マネージャー](../../relational-databases/sql-server-configuration-manager.md)] を開きます。

2. [SQL Server Services] で [SQL Server Launchpad] を右クリックし、 **[プロパティ]** を選択します。
  + サービス アカウントを変更するには、 **[ログオン]** タブをクリックします。
  + ユーザー数を増やすには、 **[詳細設定]** タブをクリックし、 **[セキュリティ コンテキスト カウント]** を変更します。

> [!Note]
> SQL Server 2016 R Services の初期バージョンでは、[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 構成ファイルを編集することで、サービスの一部のプロパティを変更することが可能でした。 このファイルは、もはや構成の変更には使用されません。 SQL Server 構成マネージャーが、サービス アカウントやユーザーの数などのサービス構成を変更するための適切な方法です。

## <a name="debug-settings"></a>デバッグの設定

いくつかのプロパティは、Launchpad の構成ファイルを使用することによってのみ変更できます。これは、デバッグなどの限られたケースで役立つ場合があります。 構成ファイルは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ中に作成され、既定では `<instance path>\binn\rlauncher.config` にプレーン テキスト ファイルとして保存されます。

このファイルを変更するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているコンピューターの管理者になる必要があります。 ファイルを編集する場合は、変更を保存する前に、バックアップ コピーを作成することをお勧めします。

次の表に、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の詳細設定と、許容される値を示します。

|**設定名**|**型**|**[説明]**|
|----|----|----|
|JOB\_CLEANUP\_ON\_EXIT|Integer |これは内部用の設定です。この値は変更しないでください。 </br></br>外部ランタイム セッションごとに作成された一時作業フォルダーを、セッションの完了後にクリーンアップするかどうかを指定します。 この設定はデバッグに便利です。 </br></br>サポートされる値は、**0** (無効) または **1** (有効) です。 </br></br>既定値は 1 です。これは、終了時にログ ファイルが削除されることを意味します。|
|TRACE\_LEVEL|Integer |デバッグのために MSSQLLAUNCHPAD のトレースの詳細レベルを設定します。 これは、LOG_DIRECTORY 設定によって指定されたパスのトレース ファイルに影響します。 </br></br>サポートされている値は次のとおりです。**1** (エラー)、**2** (パフォーマンス)、**3** (警告)、**4** (情報)。 </br></br>既定値は 1 で、エラーのみの出力を意味します。|

すべての設定が、キーと値のペアの形をとり、各設定は個別の行に表示されます。 たとえば、トレース レベルを変更するには、`Default: TRACE_LEVEL=4` と記載した行を追加します。

<a name="bkmk_EnforcePolicy"></a>

## <a name="enforcing-password-policy"></a>パスワード ポリシーの適用

パスワードを定期的に変更するポリシーが組織で実施されている場合は、ユーザー アカウントに対してスタート パッドが保持している暗号化パスワードを、強制的に再生成しなければならない場合があります。

この設定を有効にし、パスワードの更新を強制するには、SQL Server 構成マネージャーでスタート パッド サービスの **[プロパティ]** ペインを開き、 **[詳細設定]** をクリックして、 **[外部ユーザーのパスワードのリセット]** を **[はい]** に変更します。 この変更を適用すると、すべてのユーザー アカウントのパスワードが直ちに再生成されます。 この変更後に外部スクリプトを実行するには、Launchpad サービスを再起動する必要があります。このとき、新しく生成されたパスワードが読み取られます。

パスワードを定期的にリセットするには、このフラグを手動で設定するか、スクリプトを使用します。

## <a name="next-steps"></a>次の手順

+ [機能拡張フレームワーク](../concepts/extensibility-framework.md)
+ [セキュリティの概要](../concepts/security.md)
