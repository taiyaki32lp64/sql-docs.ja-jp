---
title: 機能拡張のセキュリティの概要
description: SQL Server Machine Learning Services の機能拡張フレームワークのセキュリティの概要。 ログイン アカウントとユーザー アカウント、SQL Server Launchpad サービス、ワーカー アカウント、実行中の複数のスクリプト、およびファイルのアクセス許可のセキュリティ。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f2e2d696a09e5b5bb321da583efd76f580759ce6
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727669"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services の機能拡張フレームワークのセキュリティの概要

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、SQL Server データベース エンジンおよび関連するコンポーネントと機能拡張フレームワークを統合するために使用されるセキュリティ アーキテクチャ全体について説明します。 セキュリティ保護可能なリソース、サービス、プロセス ID、およびアクセス許可について詳しく説明します。 SQL Server での機能拡張の主要概念とコンポーネントについて詳しくは、「[SQL Server Machine Learning Services の機能拡張アーキテクチャ](extensibility-framework.md)」を参照してください。

## <a name="securables-for-external-script"></a>外部スクリプトでのセキュリティ保護可能リソース

R または Python で記述された外部スクリプトは、この目的のために作成された[システム ストアド プロシージャ](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)に入力パラメーターとして送信されるか、または定義したストアド プロシージャでラップされます。 または、事前にトレーニングされ、バイナリ形式でデータベース テーブルに格納され、T-SQL [PREDICT](../../t-sql/queries/predict-transact-sql.md) 関数で呼び出し可能なモデルを使用することもできます。

スクリプトは、既存のデータベース スキーマ オブジェクト、ストアド プロシージャ、およびテーブルによって提供されるため、SQL Server Machine Learning Services では新しい[セキュリティ保護可能なリソース](../../relational-databases/security/securables.md)はありません。

スクリプトの使用方法や、スクリプトが何で構成されているかにかかわらず、データベース オブジェクトは作成され、多くの場合、保存されますが、スクリプトを格納するための新しいオブジェクト型は導入されていません。 このため、データベース オブジェクトを使用、作成、および保存できるかどうかは、ユーザーに対して既に定義されているデータベースのアクセス許可に大きく依存します。

<a name="permissions"></a>

## <a name="permissions"></a>アクセス許可

SQL Server のデータベース ログインとロールのデータ セキュリティ モデルは、R および Python スクリプトにまで拡張されています。 SQL Server データを使用する外部スクリプトまたはコンピューティング コンテキストとして SQL Server で実行される外部スクリプトを実行する場合、SQL Server ログインまたは Windows ユーザー アカウントが必要です。 アドホック クエリを実行するアクセス許可を持つデータベース ユーザーは、R または Python スクリプトから同じデータにアクセスできます。

ログインまたはユーザー アカウントによって、外部スクリプトの要件に応じて、複数レベルのアクセスを必要とする場合のある*セキュリティ プリンシパル*が特定されます。

+ 外部スクリプトが有効になっているデータベースにアクセスするためのアクセス許可。
+ テーブルなどのセキュリティで保護されたオブジェクトからデータを読み取るためのアクセス許可。
+ モデルやスコア付けの結果など、新しいデータをテーブルに書き込むための許可。
+ テーブル、外部スクリプトを使用するストアド プロシージャ、R または Python ジョブを使用するカスタム関数など、新しいオブジェクトを作成するための許可。
+ SQL Server コンピューターに新しいパッケージをインストールする権限、またはユーザーのグループに提供されるパッケージを使用する権限。

実行コンテキストとして SQL Server を使用して外部スクリプトを実行する各ユーザーを、データベース内のユーザーにマップする必要があります。 データベース ユーザーのアクセス許可を個別に設定するのではなく、アクセス許可のセットを管理するロールを作成し、それらのロールにユーザーを割り当てることができます。

詳細については、「[SQL Server Machine Learning Services にユーザー アクセス許可を付与する](../../advanced-analytics/security/user-permission.md)」を参照してください。

## <a name="permissions-when-using-an-external-client-tool"></a>外部クライアント ツールを使用する場合のアクセス許可

外部クライアント ツールで R または Python を使用するユーザーは、データベース内で外部スクリプトを実行したり、データベース オブジェクトやデータにアクセスしたりする必要がある場合、ログインまたはアカウントをデータベース内のユーザーにマップする必要があります。 外部スクリプトを、リモート データ サイエンス クライアントから送信するか、T-SQL ストアド プロシージャを使用して実行するかにかかわらず、同じアクセス許可が必要です。

たとえば、ローカル コンピューターで実行される外部スクリプトを作成し、そのスクリプトを SQL Server で実行したいとします。 次の条件が満たされていることを確認する必要があります。

+ データベースがリモート接続を許可します。
+ データベース アクセスに使用した SQL ログインまたは Windows アカウントが、インスタンス レベルで SQL Server に追加されています。
+ SQL ログインまたは Windows ユーザーには、外部スクリプトを実行するためのアクセス許可が必要です。 一般に、このアクセス許可を追加できるのはデータベース管理者のみです。
+ SQL ログインまたは Window ユーザーが、適切なアクセス許可を持つユーザーとして、外部スクリプトによって次の操作が実行される各データベースに追加されている必要があります。
  + データの取得。
  + データの書き込みまたは更新。
  + 新しいオブジェクト (テーブルやストアド プロシージャなど) の作成。

ログインまたは Windows ユーザー アカウントがプロビジョニングされ、必要なアクセス許可が付与された後、R のデータ ソース オブジェクトまたは Python の **revoscalepy** ライブラリを使用することで、あるいは外部スクリプトを含むストアド プロシージャを呼び出すことで、SQL Server で外部スクリプトを実行できます。

外部スクリプトが SQL Server から起動されるたびに、データベース エンジンのセキュリティによって、ジョブを開始したユーザーのセキュリティ コンテキストが取得され、セキュリティ保護可能なオブジェクトへのユーザーまたはログインのマッピングが管理されます。

このため、リモート クライアントから開始されるすべての外部スクリプトで、接続文字列の一部として、ログインまたはユーザーの情報を指定する必要があります。

<a name="launchpad"></a>

## <a name="services-used-in-external-processing-launchpad"></a>外部処理で使用されるサービス (Launchpad)

機能拡張フレームワークによって、SQL Server のインストールで[サービスの一覧](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details)に次の新しい NT サービスが追加されます:[**SQL Server Launchpad (MSSSQLSERVER)** ](extensibility-framework.md#launchpad)。

データベース エンジンは、SQL Server Launchpad サービスを使用して、R または Python セッションを別個のプロセスとしてインスタンス化します。 プロセスは、SQL Server、Launchpad 自体、およびストアド プロシージャまたはホスト クエリの実行に使用されたユーザー ID とは異なる低い特権のアカウントで実行されます。 スクリプトを、低い特権のアカウント下の別のプロセスで実行することは、SQL Server での R と Python のセキュリティと分離モデルの基礎です。

Launchpad は、外部プロセスを起動するだけでなく、呼び出し元ユーザーの ID を追跡し、その ID をプロセスの始動に使用される低い特権のワーカー アカウントにマッピングする役割も担います。 スクリプトまたはコードによって、データおよび操作のために SQL Server に対してコールバックが行われる一部の状況では、Launchpad によって、通常、ID 転送をシームレスに管理できます。 SELECT ステートメントや呼び出し元関数、およびその他のプログラミング オブジェクトを含むスクリプトは通常、呼び出し元のユーザーが十分な権限を持っていれば成功します。

> [!NOTE]
> 既定では、[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] は **NT Service\MSSQLLaunchpad** で実行されるように構成されています。これは、外部スクリプトの実行に必要なすべてのアクセス許可がプロビジョニングされています。 構成可能なオプションについて詳しくは、「[SQL Server Launchpad のサービスの構成](../security/sql-server-launchpad-service-account.md)」を参照してください。

<a name="sqlrusergroup"></a>

## <a name="identities-used-in-processing-sqlrusergroup"></a>処理で使用される ID (SQLRUserGroup)

**SQLRUserGroup** (SQL 制限ユーザー グループ) は、SQL Server セットアップによって作成され、低い特権のローカル Windows ユーザー アカウントのプールを含みます。 外部プロセスが必要な場合、Launchpad は使用可能なワーカー アカウントを取得し、それを使用してプロセスを実行します。 具体的には、Launchpad は使用可能なワーカー アカウントをアクティブ化し、呼び出し元ユーザーの ID にマップして、そのワーカー アカウントでスクリプトを実行します。

+ **SQLRUserGroup** は、特定のインスタンスにリンクされます。 Machine Learning が有効になっているインスタンスごとに、ワーカー アカウントの個別プールが必要です。 インスタンス間でアカウントを共有することはできません。

+ ユーザー アカウント プールのサイズは静的であり、既定値は 20 です。これにより、20 の同時セッションがサポートされます。 同時に起動できる外部ランタイム セッションの数は、このユーザー アカウント プールのサイズによって制限されます。 

+ プール内のワーカー アカウント名の形式は、SQLInstanceName*nn* です。 たとえば、既定のインスタンスの場合、**SQLRUserGroup** には、MSSQLSERVER01、MSSQLSERVER02 (MSSQLSERVER20 まで以後同様) という名前のアカウントが含まれます。

並列化されたタスクでは、追加のアカウントは使用されません。 たとえば、ユーザーが並列処理を使用するスコアリング タスクを実行する場合、同じワーカー アカウントがすべてのスレッドで再利用されます。 Machine Learning を頻繁に使用する場合、外部スクリプトの実行に使用するアカウントの数を増やすことができます。 詳細については、[Machine Learning のユーザー アカウント プールの変更](../../advanced-analytics/administration/modify-user-account-pool.md)に関する記事を参照してください。

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>SQL Server 2019 での AppContainer の分離

SQL Server 2019 では、セットアップで **SQLRUserGroup** のワーカー アカウントが作成されなくなりました。 代わりに、[AppContainer](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation) によって分離が実現されます。 実行時に、ストアド プロシージャまたはクエリで外部スクリプトが検出されると、SQL Server は拡張機能固有の起動ツールの要求を使用して Launchpad を呼び出します。 Launchpad は、その ID 下のプロセスで適切なランタイム環境を呼び出し、AppContainer をインスタンス化して、そのランタイム環境を含めます。 ローカル アカウントとパスワードの管理が不要になったため、これは有益な変更です。 また、ローカル ユーザー アカウントが禁止されているインストールでは、ローカル ユーザー アカウントの依存関係を削除することで、この機能を使用できるようになります。

AppContainer は、SQL Server に実装されているため、内部メカニズムです。 プロセス モニターには AppContainer の物理的な証拠は表示されませんが、セットアップによって作成された、プロセスによるネットワーク呼び出しを防ぐための送信ファイアウォール規則で AppContainer を見つけることができます。 詳細については、「[SQL Server Machine Learning Services のファイアウォール構成](../../advanced-analytics/security/firewall-configuration.md)」を参照してください。

> [!Note]
> SQL Server 2019 では、**SQLRUserGroup** には、複数のワーカー アカウントではなく、1 つの SQL Server Launchpad サービス アカウントであるメンバーが 1 つだけあります。
::: moniker-end

### <a name="permissions-granted-to-sqlrusergroup"></a>SQLRUserGroup に付与されるアクセス許可

既定では、**SQLRUserGroup** のメンバーには、SQL Server の **Binn**、**R_SERVICES**、および **PYTHON_SERVICES** ディレクトリ内のファイルに対する読み取りおよび実行アクセス許可が付与され、さらに SQL Server とともにインストールされる R および Python ディストリビューションの実行可能ファイル、ライブラリ、および組み込みデータセットへのアクセス権が付与されます。 

SQL Server の機密性の高いリソースを保護するために、**SQLRUserGroup** へのアクセスを拒否するアクセス制御リスト (ACL) を必要に応じて定義できます。 逆に、SQL Server 自体とは別のホスト コンピューターに存在するローカル データ リソースへのアクセス許可を付与することもできます。 

仕様により、**SQLRUserGroup** には、データベース ログインまたはデータへのアクセス許可はありません。 特定の状況、特に信頼された Windows ID が呼び出し元のユーザーである場合、ループバック接続を許可するログインを作成できます。 この機能は、[*暗黙の認証*](#implied-authentication)と呼ばれます。 詳細については、[データベース ユーザーとしての SQLRUserGroup の追加](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)に関する記事を参照してください。

## <a name="identity-mapping"></a>ID のマッピング

セッションが開始されると、Launchpad は、呼び出し元のユーザーの ID をワーカー アカウントにマップします。 ワーカー アカウントに対する外部の Windows ユーザーまたは有効な SQL ログインのマッピングは、外部スクリプトを実行する SQL ストアド プロシージャの有効期間中のみ有効です。 同じログインからの並列クエリは、同じユーザー ワーカー アカウントにマップされます。

実行中、Launchpad はセッション データを格納する一時フォルダーを作成し、セッションの終了時にそれらを削除します。 ディレクトリへのアクセスは制限されます。 R の場合、RLauncher がこのタスクを実行します。 Python の場合、PythonLauncher がこのタスクを実行します。 個々のワーカー アカウントは、その所有フォルダーに制限され、その所有レベルを超えているフォルダー内のファイルにはアクセスできません。 ただし、ワーカー アカウントは、作成されたセッション作業フォルダーの下位にある子の読み取り、書き込み、または削除を行うことができます。 コンピューターの管理者であれば、各プロセスによって作成されたディレクトリを表示できます。 各ディレクトリはセッション GUID によって識別されます。

<a name="implied-authentication"></a>

## <a name="implied-authentication-loop-back-requests"></a>暗黙の認証 (ループバック要求)

*暗黙の認証*では、接続要求の動作が示されます。この動作では、データまたは操作のループバック要求で、低い特権のワーカー アカウントとして実行されている外部プロセスが信頼されたユーザー ID として SQL Server に提示されます。 暗黙の認証は、R または Python スクリプトなどの外部プロセスから送信される要求で、SQL Server 接続文字列によって信頼関係接続が指定されるという点で、概念として Windows 認証に固有です。 これは、*ループバック*と呼ばれることもあります。

信頼関係接続は R および Python スクリプトから使用できますが、構成を追加した場合のみ使用できます。 機能拡張アーキテクチャでは、R および Python プロセスはワーカー アカウントで実行され、親 **SQLRUserGroup** からアクセス許可を継承します。 接続文字列で `Trusted_Connection=True` が指定されると、ワーカー アカウントの ID が接続要求で提示されます。これは、既定では SQL Server には通知されません。

信頼関係接続を正常に確立するには、**SQLRUserGroup** のデータベース ログインを作成する必要があります。 これを行った後、**SQLRUserGroup** のメンバーからのすべての信頼関係接続に SQL Server へのログイン権限が与えられます。 詳しい手順については、[データベース ログインへの SQLRUserGroup の追加](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)に関する記事を参照してください。

信頼関係接続は、最も広く使用されている接続要求の形式ではありません。 R または Python スクリプトで接続を指定するとき、ODBC データ ソースへの接続の場合には、SQL ログインを使用するか、または完全指定のユーザー名とパスワードを使用するのが一般的です。

### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>R および Python セッションでの暗黙の認証のしくみ

次の図は、SQL Server コンポーネントと R ランタイムの相互作用、および R で暗黙の認証が行われる方法を示しています。

![R での暗黙の認証](../security/media/implied-auth-rsql.png)

次の図は、SQL Server コンポーネントと Python ランタイムの相互作用、および Python で暗黙の認証が行われる方法を示しています。

![Python での暗黙の認証](../security/media/implied-auth-python2.png)

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>透過的なデータ暗号化はサポートされない

[透過的なデータ暗号化 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) は、外部スクリプト ランタイムとの間で送受信されるデータに対してはサポートされません。 これは、外部プロセス (R または Python) が SQL Server プロセスの外部で実行されるためです。 このため、外部ランタイムによって使用されるデータは、データベース エンジンの暗号化機能によって保護されません。 この動作は、データベースからデータを読み取り、コピーを作成する、SQL Server コンピューターで実行される他のクライアントと同様です。

このため、TDE は、R または Python スクリプトで使用するデータ、ディスクに保存されるデータ、または保存される中間結果のいずれにも適用**されません**。 ただし、Windows BitLocker 暗号化や、ファイルまたはフォルダー レベルで適用されるサード パーティ暗号化など、その他の種類の暗号化は引き続き適用されます。

[Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md) の場合、外部ランタイムは暗号化キーにアクセスできません。 そのため、スクリプトにデータを送信できません。

## <a name="next-steps"></a>次の手順

この記事では、[機能拡張フレームワーク](../../advanced-analytics/concepts/extensibility-framework.md)に組み込まれたセキュリティ アーキテクチャのコンポーネントと相互作用モデルについて学習しました。 この記事で取り上げた主なポイントは、Launchpad、SQLRUserGroup、およびワーカー アカウントの目的、R と Python のプロセス分離、ユーザー ID をワーカーアカウントにマップする方法です。 

次の手順として、[アクセス許可付与](../../advanced-analytics/security/user-permission.md)の手順を確認してください。 Windows 認証を使用するサーバーの場合、追加の構成が必要になるタイミングを確認するために、[データベース ログインへの SQLRUserGroup の追加](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)に関する記事も参照する必要があります。