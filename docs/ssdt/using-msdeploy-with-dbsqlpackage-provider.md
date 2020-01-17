---
title: dbSqlPackage プロバイダーでの MSDeploy の使用 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 04/26/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 213b91ab-03e9-431a-80f0-17eed8335abe
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e9279a433d848108b204cadc6990803695f9e82d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140984"
---
# <a name="using-msdeploy-with-dbsqlpackage-provider"></a>dbSqlPackage プロバイダーでの MSDeploy の使用
**DbSqlPackage** は SQL Server/SQL Azure データベースとのやり取りを可能にする **MSDeploy** プロバイダーです。 **DbSqlPackage** は次の操作をサポートしています。  
  
-   **Extract**: ライブ SQL Server または SQL Azure の各データベースからデータベース スナップショット (.dacpac) ファイルを作成します。  
  
-   **Publish**: ソース .dacpac ファイルのスキーマに合わせてデータベース スキーマの増分更新を行います。  
  
-   **DeployReport**: 公開操作によって行われる変更の XML レポートを作成します。  
  
-   **Script**: 公開操作によって実行されるスクリプトに対応する Transact\-SQL スクリプトを作成します。  
  
DACFx について詳しくは、[https://msdn.microsoft.com/library/microsoft.sqlserver.dac.aspx](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.aspx) または [SqlPackage.exe](../tools/sqlpackage.md) (DACFx コマンド ライン ツール) の DACFx マネージド API のドキュメントをご覧ください。  
  
> [!IMPORTANT]  
> dbSqlPackage のプロバイダー機能は、Visual Studio の次回メジャー リリースから削除される予定です。 Web Deploy を使用してデータベースの公開を処理する方法については、「[増分データベース公開のための dbDacFx プロバイダー (英語)](https://www.iis.net/learn/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing)」を参照してください。  
  
## <a name="command-line-syntax"></a>コマンド ラインの構文  
**MSDeploy** で **dbSqlPackage** プロバイダーを使用する場合は、次の形式でコマンド ラインを指定します。  
  
```  
  
MSDeploy -verb: MSDeploy-verb -source:dbSqlPackage="Input"[,dbSqlPackage-source-parameters] -dest:dpSqlPackage="Input"[,dbSqlPackage-target-parameters]  
```  
  
## <a name="ms-deploy-verbs"></a>MS-Deploy 動詞  
MS-Deploy 動詞は、MS-Deploy コマンド ラインに **-verb** スイッチを使用して指定します。 **dbSqlPackage** プロバイダーでは、次の **MSDeploy** 動詞がサポートされています。  
  
|動詞|[説明]|  
|--------|---------------|  
|ダンプ (dump)|.dacpac ファイルに含まれるソース データベースに関する名前、バージョン番号、説明などの情報を提供します。 ソース データベースは、コマンド ラインで次の形式を使用して指定します。<br /><br />**msdeploy -verb:dump -source:dbSqlPackage="** _.dacpac-file-path_ **"**|  
|sync|dbSqlPackage 操作は、コマンド ラインで次の形式を使用して指定します。<br /><br />**msdeploy -verb:sync -source:dbSqlPackage**="input" _[,DbSqlPackage-source-parameters] -_ **dest:dbSqlPackage**="input" *[,DbSqlPackage-destination-parameters]*<br /><br />sync 動詞の有効なソースおよびターゲットのパラメーターの詳細については、以下のセクションを参照してください。|  
  
## <a name="dbsqlpackage-source"></a>dbSqlPackage ソース  
**dbSqlPackage** は、有効な SQL Server または SQL Azure 接続文字列か、ディスク上にある .dacpac ファイルのパスのどちらかを入力として取得します。  プロバイダーの入力ソースを指定する構文は次のとおりです。  
  
|入力|既定|[説明]|  
|---------|-----------|---------------|  
|**-source:dbSqlPackage=** {*input*}|**N/A**|*input* は、有効な SQL Server または SQL Azure 接続文字列か、ディスク上にある .dacpac ファイルのパスです。<br /><br />**注:** 入力ソースとして接続文字列を使用する場合、サポートされる接続文字列プロパティは *InitialCatalog、DataSource、UserID、Password、IntegratedSecurity、Encrypt、TrustServerCertificate* および *ConnectionTimeout* のみです。|  
  
入力ソースがライブ SQL Server/Azure データベースへの接続文字列の場合、**dbSqlPackage** はライブ SQL Server/Azure データベースから .dacpac ファイルの形式でデータベース スナップショットを抽出します。  
  
**Source** パラメーターは次のとおりです。  
  
|パラメーター|既定|[説明]|  
|-------------|-----------|---------------|  
|**Profile**:{ *string*}|なし|DAC 公開プロファイルのファイル パスを指定します。 結果の dacpac の生成時に使用するプロパティと変数のコレクションをプロファイルで定義します。 **Publish**、**Script**、または **DeployReport** 操作の 1 つが実行される場合、公開プロファイルはターゲットに渡されて既定のオプションとして使用されます。|  
|**DacApplicationName**={ *string* }|データベース名|DACPAC メタデータに格納されるアプリケーション名を定義します。 既定の文字列は、データベース名です。|  
|**DacMajorVersion** ={*integer*}|**1**|DACPAC メタデータに格納されるメジャー バージョンを定義します。|  
|**DacMinorVersion**={*integer*}|**0**|DACPAC メタデータに格納されるマイナー バージョンを定義します。|  
|**DacApplicationDescription**={ *string* }|なし|DACPAC メタデータに格納されるアプリケーションの説明を定義します。|  
|**ExtractApplicationScopedObjectsOnly={True &#124; False}**|**True**|**True** の場合は、ソースからアプリケーション スコープのオブジェクトのみを抽出します。 **False** の場合は、アプリケーション スコープのオブジェクトとアプリケーション スコープでないオブジェクトの両方を抽出します。|  
|**ExtractReferencedServerScopedElements={True &#124; False}**|**True**|**True** の場合、ソース データベース オブジェクトによって参照されるログイン オブジェクト、サーバー監査オブジェクト、および資格情報オブジェクトを抽出します。|  
|**ExtractIgnorePermissions={True &#124; False}**|**False**|**True** の場合は、抽出されたすべてのオブジェクトのアクセス許可の抽出は無視されます。**False** の場合は、無視されません。|  
|**ExtractStorage={File&#124;Memory}**|**[最近使ったファイル]**|抽出時に使用されるスキーマ モデルのバックアップ用ストレージの種類を指定します。|  
|**ExtractIgnoreExtendedProperties={True&#124;False}**|**False**|拡張プロパティを無視するかどうかを指定します。|  
|**VerifyExtraction = {True&#124;False}**|**False**|抽出された DACPAC を検証するかどうかを指定します。|  
  
## <a name="dbsqlpackage-destination"></a>DbSqlPackage ターゲット  
**dbSqlPackage** プロバイダーは、有効な SQL Server または SQL Azure 接続文字列か、ターゲット入力としてディスク上にある .dacpac ファイルのパスのどちらかを受け入れます。  プロバイダーのターゲットを指定する構文は次のとおりです。  
  
|入力|既定|[説明]|  
|---------|-----------|---------------|  
|-**dest:dbSqlPackage**={*input*}|なし|*input* は、有効な SQL Server または SQL Azure 接続文字列か、ディスク上にある .dacpac ファイルの完全パスまたは部分パスです。 *input* がファイル パスの場合、他のパラメーターは指定できません。|  
  
次の **Destination** パラメーターは、すべての **dbSqlPackage** 操作に使用できます。  
  
|プロパティ|既定|[説明]|  
|------------|-----------|---------------|  
|**Action={Publish&#124;DeployReport&#124;Script}**|なし|オプション パラメーターは、**Destination** で実行する操作を指定します。|  
|**AllowDropBlockingAssemblies ={True &#124; False}**|**False**|**SqlClr** による公開で、ブロックしているアセンブリを配置計画から削除するかどうかを指定します。 既定では、参照しているアセンブリを削除する必要がある場合、ブロックしているアセンブリまたは参照しているアセンブリによって、アセンブリの更新がブロックされます。|  
|**AllowIncompatiblePlatform={True &#124; False}**|**False**|互換性がない可能性のある SQL Server プラットフォームであっても公開操作を続行するかどうかを指定します。|  
|**BackupDatabaseBeforeChanges={True &#124; False}**|**False**|変更を配置する前にデータベースをバックアップします。|  
|**BlockOnPossibleDataLoss={ True &#124; False}**|**True**|公開操作によってデータが失われる可能性がある場合に公開エピソードを終了するかどうかを指定します。|  
|**BlockWhenDriftDetected={ True &#124; False}**|**True**|スキーマがその登録と一致しないか、スキーマが登録されていないデータベースの更新をブロックするかどうかを指定します。|  
|**CommentOutSetVarDeclarations= {True &#124; False}**|**False**|生成する公開スクリプト内で **SETVAR** 変数の宣言をコメント アウトするかどうかを指定します。 このようなコメント アウトが必要になるのは、**SQLCMD.exe** などのツールを使用して、公開時にコマンド ラインで値を指定する予定がある場合などです。|  
|**CompareUsingTargetCollation={ True &#124; False}**|**False**|この設定では、配置の際にデータベースの照合順序をどのように処理するかを指定します。既定では、ソースで指定されている照合順序と異なる場合にターゲット データベースの照合順序が更新されます。  このオプションを設定した場合、ターゲット データベース (またはサーバー) の照合順序が使用されます。|  
|**CreateNewDatabase={ True &#124; False}**|**False**|データベースへの公開時に、ターゲット データベースを更新するか、削除して再作成するかを指定します。|  
|**DeployDatabaseInSingleUserMode={ True &#124; False}**|**False**|**True** の場合、データベースは配置前にシングル ユーザー モードに設定されます。|  
|**DisableAndReenableDdlTriggers={True &#124; False}**|**True**|公開プロセスの開始時にデータ定義言語 (DDL) トリガーを無効にして、公開操作の最後に再度有効にするかどうかを指定します。|  
|**DoNotAlterChangeDataCaptureObjects={ True &#124; False}**|**True**|**True** の場合、Change Data Capture オブジェクトは変更されません。|  
|**DoNotAlterReplicatedObjects=( True &#124; False}**|**True**|レプリケートされたオブジェクトが、検証時に識別されるかどうかを指定します。|  
|**DropConstraintsNotInSource= {True &#124; False}**|**True**|公開操作で、データベースへの公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) に存在しない制約を削除するかどうかを指定します。|  
|**DropDmlTriggersNotInSource= {True &#124; False}**|**True**|公開操作で、データベースへの公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) に存在しないデータ操作言語 (DML) トリガーを削除するかどうかを指定します。|  
|**DropExtendedPropertiesNotInSource= {True &#124; False}**|**True**|公開操作で、データベースへの公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) に存在しない拡張プロパティを削除するかどうかを指定します。|  
|**DropIndexesNotInSource= {True &#124; False}**|**True**|公開操作で、データベースへの公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) に存在しないインデックスを削除するかどうかを指定します。|  
|**DropObjectsNotInSource= {True &#124; False}**|**False**|データベースへの公開時に、データベース スナップショット (.dacpac) ファイルに存在しないオブジェクトをターゲット データベースから削除するかどうかを指定します。|  
|**DropPermissionsNotInSource= {True &#124; False}**|**False**|公開操作で、データベースへの公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) に存在しないアクセス許可を削除するかどうかを指定します。|  
|**DropRoleMembersNotInSource= {True &#124; False}**|**False**|公開操作で、データベースへの公開時に、ターゲット データベースのデータベース スナップショット (.dacpac) に存在しないロール メンバーを削除するかどうかを指定します。|  
|**GenerateSmartDefaults={True &#124; False}**|**False**|**SqlPackage.exe** で、null 値が許可されない列を含むデータが格納されているテーブルを更新する際に、自動的に既定値を提供するかどうかを指定します。|  
|**IgnoreAnsiNulls= {True &#124; False}**|**False**|データベースへの公開時に、**ANSI NULLS** 設定の相違を無視するか更新するかを指定します。|  
|**IgnoreAuthorizer= {True &#124; False}**|**False**|データベースへの公開時に、Authorizer の相違を無視するか更新するかを指定します。|  
|**IgnoreColumnCollation= {True &#124; False}**|**False**|データベースへの公開時に、列の照合順序の相違を無視するか更新するかを指定します。|  
|**IgnoreComments= {True &#124; False}**|**False**|データベースへの公開時に、コメントの順序の相違を無視するか更新するかを指定します。|  
|**IgnoreCryptographicProviderFile= {True &#124; False}**|**True**|データベースへの公開時に、暗号化サービス プロバイダーのファイル パスの相違を無視するか更新するかを指定します。|  
|**IgnoreDdlTriggerOrder= {True &#124; False}**|**False**|データベースへの公開時に、データ定義言語 (DDL) トリガーの順序の相違を無視するか更新するかを指定します。|  
|**IgnoreDdlTriggerState={True &#124; False}**|**False**|データベースへの公開時に、DDL トリガーの有効/無効状態の相違を無視するか更新するかを指定します。|  
|**IgnoreDefaultSchema={True &#124; False}**|**False**|データベースへの公開時に、既定のスキーマの相違を無視するか更新するかを指定します。|  
|**IgnoreDmlTriggerOrder= {True &#124; False}**|**False**|データベースへの公開時に、DML トリガーの順序の相違を無視するか更新するかを指定します。|  
|**IgnoreDmlTriggerState= {True &#124; False}**|**False**|データベースへの公開時に、DML トリガーの有効/無効状態の相違を無視するか更新するかを指定します。|  
|**IgnoreExtendedProperties= {True &#124; False}**|**False**|データベースへの公開時に、拡張プロパティの相違を無視するか更新するかを指定します。|  
|**IgnoreFileAndLogFilePath={True &#124; False}**|**True**|データベースへの公開時に、ファイルおよびログ ファイルのパスの相違を無視するか更新するかを指定します。|  
|**IgnoreFilegroupPlacement= {True &#124; False}**|**True**|データベースへの公開時に、**FILEGROUP** の配置の相違を無視するか更新するかを指定します。|  
|**IgnoreFileSize= {True &#124; False}**|**True**|データベースへの公開時に、ファイル サイズの相違を無視するか更新するかを指定します。|  
|**IgnoreFillFactor= {True &#124; False}**|**True**|データベースへの公開時に、FILL FACTOR の相違を無視するか更新するかを指定します。|  
  
|プロパティ|既定|[説明]|  
|------------|-----------|---------------|  
|**IgnoreFullTextCatalogFilePath= {True &#124; False}**|**True**|データベースへの公開時に、フルテキスト インデックス ファイルのパスの相違を無視するか更新するかを指定します。|  
|**IgnoreIdentitySeed= {True &#124; False}**|**False**|データベースへの公開時に、ID 列のシードの相違を無視するか更新するかを指定します。|  
|**IgnoreIncrement= {True &#124; False}**|**False**|データベースへの公開時に、ID 列の増分の相違を無視するか更新するかを指定します。|  
|**IgnoreIndexOptions ={True &#124; False}**|**False**|データベースへの公開時に、インデックス オプションの相違を無視するか更新するかを指定します。|  
|**IgnoreIndexPadding= {True &#124; False}**|**True**|データベースへの公開時に、インデックスの埋め込みの相違を無視するか更新するかを指定します。|  
|**IgnoreKeywordCasing= {True &#124; False}**|**True**|データベースへの公開時に、キーワードの大文字と小文字の設定の相違を無視するか更新するかを指定します。|  
|**IgnoreLockHintsOnIndexes= {True &#124; False}**|**False**|データベースへの公開時に、インデックスのロック ヒントの相違を無視するか更新するかを指定します。|  
|**IgnoreLoginSids= {True &#124; False}**|**True**|データベースへの公開時に、セキュリティ識別子 (SID) の相違を無視するか更新するかを指定します。|  
|**IgnoreNotForReplication= {True &#124; False}**|**False**|データベースへの公開時に、Not For Replication 設定の相違を無視するか更新するかを指定します。|  
|**IgnoreObjectPlacementOnPartitionScheme= {True &#124; False}**|**True**|データベースへの公開時に、パーティション構成のオブジェクト配置の相違を無視するのか更新するのかを指定します。|  
|**IgnorePartitionSchemes= {True &#124; False}**|**False**|データベースへの公開時に、パーティション構成およびパーティション関数の相違を無視するか更新するかを指定します。|  
|**IgnorePermissions= {True &#124; False}**|**False**|データベースへの公開時に、アクセス許可の相違を無視するか更新するかを指定します。|  
|**IgnoreQuotedIdentifiers= {True &#124; False}**|**False**|データベースへの公開時に、Quoted Identifier 設定の相違を無視するか更新するかを指定します。|  
|**IgnoreRoleMembership={True &#124; False}**|**False**|データベースへの公開時に、ログインのロール メンバーシップの相違を無視するか更新するかを指定します。|  
|**IgnoreRouteLifetime= {True &#124; False}**|**True**|データベースへの公開時に、ログインのロール メンバーシップの相違を無視するか更新するかを指定します。|  
|**IgnoreSemicolonBetweenState= {True &#124; False}**|**True**|データベースへの公開時に、Transact-SQL ステートメント間のセミコロンの相違を無視するか更新するかを指定します。|  
|**IgnoreTableOptions= {True &#124; False}**|**False**|データベースへの公開時に、テーブル オプションの相違を無視するか更新するかを指定します。|  
|**IgnoreUserSettingsObjects= {True &#124; False}**|**False**|データベースへの公開時に、ユーザー設定オプションの相違を無視するか更新するかを指定します。|  
|**IgnoreWhitespace= {True &#124; False}**|**True**|データベースへの公開時に、空白の相違を無視するか更新するかを指定します。|  
|**IgnoreWithNocheckOnCheckConstraints={True &#124; False}**|**False**|データベースへの公開時に、CHECK 制約に対する **WITH NOCHECK** 句の値の相違を無視するか更新するかを指定します。|  
|**IgnoreWithNocheckOnForeignKeys={True &#124; False}**|**False**|データベースへの公開時に、外部キーに対する **WITH NOCHECK** 句の値の相違を無視するか更新するかを指定します。|  
|**IncludeCompositeObjects= {True &#124; False}**|**False**|単一の公開操作の一部としてすべての複合要素を含めるかどうかを指定します。|  
|**IncludeTransactionalScripts={True &#124; False}**|**False**|データベースへの公開時に、可能であれば常にトランザクション ステートメントを使用するかどうかを指定します。|  
|**NoAlterStatementsToChangeClrTypes={True &#124; False}**|**False**|公開で、相違がある場合に ALTER ASSEMBLY ステートメントを発行するのではなく、常にアセンブリを削除して再作成することを指定します。|  
|**PopulateFilesOnFilegroups= {True &#124; False}**|**True**|ターゲット データベース内に新しい **FileGroup** を作成する際に、新しいファイルも作成するかどうかを指定します。|  
|**RegisterDataTierApplication={True &#124; False}**|**False**|スキーマがデータベース サーバーに登録されるかどうかを指定します。|  
|**ScriptDatabaseCollation {True &#124; False}**|**False**|データベースへの公開時に、データベースの照合順序の相違を無視するか更新するかを指定します。|  
|**ScriptDatabaseCompatibility= {True &#124; False}**|**True**|データベースへの公開時に、データベース互換性の相違を無視するか更新するかを指定します。|  
|**ScriptDatabaseOptions= {True &#124; False}**|**True**|データベースへの公開時に、ターゲット データベースのプロパティを設定するか更新するかを指定します。|  
|**ScriptFileSize={True &#124; False}**|**False**|ファイル グループにファイルを追加するときに、サイズを指定するかどうかを制御します。|  
|**ScriptNewConstraintValidation= {True &#124; False}**|**True**|公開操作の途中で CHECK 制約または外部キー制約によるデータ エラーが生じないように、公開操作の最後にすべての制約を 1 つのセットとして確認するかどうかを指定します。 このオプションが **False** の場合、対応するデータを確認せずに制約が公開されます。|  
|**ScriptDeployStateChecks={True &#124; False}**|**False**|データベース プロジェクト内で指定されている名前にデータベース名およびサーバー名が一致することを確認するために、公開スクリプト内にステートメントを生成するかどうかを指定します。|  
|**ScriptRefreshModule= {True &#124; False}**|**True**|公開スクリプトの末尾に REFRESH ステートメントを含めるかどうかを指定します。|  
|**Storage={File&#124;Memory}**|**[メモリ]**|データベース モデルの構築時に要素をどのように格納するかを指定します。 パフォーマンス上の理由から、既定値は **Memory** です。 非常に大規模なデータベースの場合は、ファイルを使用するストレージが必要です。|  
|**TreatVerificationErrorsAsWarnings= {True &#124; False}**|**False**|公開の検証中に発生したエラーを警告として扱うかどうかを指定します。 配置計画をターゲット データベースに対して実行する前に、生成された配置計画がチェックされます。 計画の検証では、変更を加えるためには取り除く必要のある、ターゲットのみのオブジェクト (インデックスなど) の損失などの問題が検出されます。 また、複合プロジェクトへの参照のためテーブルやビューなどに依存関係が存在するのに、その関係がターゲット データベースに存在しない状況も検出されます。 すべての問題の一覧を取得するには、最初のエラー発生時に公開操作を停止するのではなく、検証エラーを警告として扱うことをお勧めします。|  
|**UnmodifiableObjectWarnings= {True &#124; False}**|**True**|修正できない相違がオブジェクトで見つかった場合 (たとえば、同じファイルのファイル サイズまたはファイル パスが異なる場合) に警告を生成するかどうかを指定します。|  
|**VerifyCollationCompatibility={True &#124; False}**|**True**|照合順序の互換性を検証するかどうかを指定します。|  
|**VerifyDeployment={True &#124; False}**|**True**|正常な公開がブロックされる可能性のある問題が存在する場合には公開操作を停止するようなチェックを、公開前に行うかどうかを指定します。 たとえば、ターゲット データベースの外部キーがデータベース プロジェクトに存在しないために公開時にエラーが発生する場合、公開操作は停止します。|  
  
> [!NOTE]  
> 指定されたすべてのターゲット パラメーターは、ソース公開プロファイルでのこれらの指定をオーバーライドします。  
  
> [!NOTE]  
> **SQLCMD** の変数および値は、ターゲット パラメーターとして指定できないため、公開プロファイルのソース プロファイルで指定する必要があります。  
  
次の **Destination** パラメーターは、**DeployReport** および **Script** 操作にのみ使用できます。  
  
|パラメーター|既定|[説明]|  
|-------------|-----------|---------------|  
|**OutputPath**={ *string* }|なし|省略可能なパラメーターです。*string* で指定されたディスク上の場所に DeployReport XML 出力ファイルまたは Script SQL 出力ファイルを作成することを **dbSqlPackage** に対して指定します。 この操作では、文字列で指定された場所にある現在のスクリプトが上書きされます。|  
  
> [!NOTE]  
> **OutputPath** パラメーターが **DeployReport** または **Script** 操作に対して指定されない場合、出力はメッセージとして返されます。  
  
## <a name="examples"></a>使用例  
次は、**dbSqlPackage** を使用する **Extract** 操作の構文の例です。  
  
```  
MSDeploy.exe -verb:sync -source:dbSqlPackage="<source connection string>",<source parameter> -dest:dbSqlPackage="<target dacpac file path>"  
```  
  
次は、**dbSqlPackage** を使用する **Publish** 操作の構文の例です。  
  
```  
MSDeploy.exe -verb:sync -source:dbSqlPackage="<source dacpac file path>" -dest:dbSqlPackage="<target SQL Server/SQL Azure connection string>",Action=Publish,<destination parameters>  
```  
  
次は、**dbSqlPackage** を使用する **DeployReport** 操作の構文の例です。  
  
```  
MSDeploy.exe -verb:sync -source:dbSqlPackage="<source dacpac file path>" -dest:dbSqlPackage="<target SQL Server/SQL Azure connection string>",Action=DeployReport,OutputPath="<path to output XML file>",<destination parameters>  
```  
  
次は、**dbSqlPackage** を使用する **Script** 操作の構文の例です。  
  
```  
MSDeploy.exe -verb:sync -source:dbSqlPackage="<source dacpac file path>" -dest:dbSqlPackage="<target SQL Server/SQL Azure connection string>",Action=Script,OutputPath="<path to output sql script>",<destination parameters>  
```  
  
