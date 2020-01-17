---
title: SSIS カタログ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 24bd987e-164a-48fd-b4f2-cbe16a3cd95e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 14de3fa15fa5a648c2d41824d237040b5aa085e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771578"
---
# <a name="ssis-catalog"></a>SSIS カタログ
  `SSISDB`カタログが操作するための中心点[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)](SSIS) プロジェクトを展開している、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]サーバー。 たとえば、プロジェクト パラメーターとパッケージ パラメーターの設定、パッケージに合わせたランタイム値を指定するための環境の構成、パッケージの実行およびトラブルシューティング、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバー操作の管理を行います。  
  
 オブジェクトに格納されている、`SSISDB`カタログには、プロジェクト、パッケージ、パラメーター、環境、および操作履歴が含まれます。  
  
 オブジェクト、設定、およびに格納されているオペレーション データを検査する、`SSISDB`カタログ ビューでは、クエリを実行して、`SSISDB`データベース。 ストアド プロシージャを呼び出すことによって、オブジェクトを管理する、`SSISDB`データベースかの UI を使用して、`SSISDB`カタログ。 多くの場合、UI でもストアド プロシージャの呼び出しでも同じタスクを実行できます。  
  
 `SSISDB` データベースを保守するには、ユーザー データベースの管理に標準的なエンタープライズ ポリシーを適用することをお勧めします。 メンテナンス プランの作成については、「 [Maintenance Plans](../../relational-databases/maintenance-plans/maintenance-plans.md)」をご覧ください。  
  
 `SSISDB`カタログと`SSISDB`データベースは Windows PowerShell をサポートします。 Windows PowerShell による SQL Server の使用の詳細については、「 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)」をご覧ください。 Windows PowerShell を使用してプロジェクトの配置などのタスクを実行する方法の例については、blogs.msdn.com のブログ エントリ「 [SQL Server 2012 での SSIS と PowerShell](https://go.microsoft.com/fwlink/?LinkId=242539)」をご覧ください。  
  
 オペレーション データを表示する方法についての詳細については、次を参照してください。[パッケージの実行とその他の操作の監視を](../performance/monitor-running-packages-and-other-operations.md)します。  
  
 アクセスする、`SSISDB`のカタログに[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]に接続して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース エンジンとし、展開、 **Integration Services カタログ**オブジェクト エクスプ ローラーでノード。 アクセスする、`SSISDB`データベース[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]オブジェクト エクスプ ローラーでデータベース ノードを展開します。  
  
> [!NOTE]  
>  名前を変更することはできません、`SSISDB`データベース。  
  
> [!NOTE]  
>  場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスが、`SSISDB`データベースに接続されて、停止するか、ISServerExec.exe が応答しないプロセスが終了します。 メッセージが Windows イベント ログに書き込まれます。  
>   
>  クラスター フェールオーバーの一環として [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソースがフェールオーバーした場合、実行中のパッケージは再開されません。 チェックポイントを使用してパッケージを再開できます。 詳しくは、「 [Restart Packages by Using Checkpoints](../packages/restart-packages-by-using-checkpoints.md)」をご覧ください。  
  
## <a name="catalog-object-identifiers"></a>カタログ オブジェクト識別子  
 カタログに新しいオブジェクトを作成するときは、オブジェクトに名前を割り当てる必要があります。 オブジェクト名が識別子となります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、識別子に使用できる文字のルールが定義されています。 次のオブジェクトの名前は、識別子のルールに従っている必要があります。  
  
-   フォルダー  
  
-   Project  
  
-   環境  
  
-   パラメーター  
  
-   環境変数  
  
### <a name="folder-project-environment"></a>フォルダー、プロジェクト、環境  
 フォルダー、プロジェクト、または環境の名前を変更するときは、次のルールを考慮します。  
  
-   無効な文字には、ASCII/Unicode 文字 1 - 31、引用符 (")、小なり (\<)、大なり (>)、パイプ (|)、バックスペース (\b)、null (\0)、タブ (\t) などがあります。  
  
-   名前の先頭または末尾にスペースを含めることはできません。  
  
-   名前を \@ で始めることはできませんが、先頭以外では \@ を使用できます。  
  
-   名前の長さは 1 ～ 128 文字にする必要があります。  
  
### <a name="parameter"></a>パラメーター  
 パラメーターに名前を付けるときは、次のルールを考慮します。  
  
-   名前の最初の文字は、Unicode Standard 2.0 に定義されている文字か、アンダースコア (_) である必要があります。  
  
-   2 番目以降の文字では、Unicode Standard 2.0 に定義されている文字または数字と、アンダースコア (_) を使用できます。  
  
### <a name="environment-variable"></a>環境変数  
 環境変数に名前を付けるときは、次のルールを考慮します。  
  
-   無効な文字には、ASCII/Unicode 文字 1 - 31、引用符 (")、小なり (\<)、大なり (>)、パイプ (|)、バックスペース (\b)、null (\0)、タブ (\t) などがあります。  
  
-   名前の先頭または末尾にスペースを含めることはできません。  
  
-   名前を \@ で始めることはできませんが、先頭以外では \@ を使用できます。  
  
-   名前の長さは 1 ～ 128 文字にする必要があります。  
  
-   名前の最初の文字は、Unicode Standard 2.0 に定義されている文字か、アンダースコア (_) である必要があります。  
  
-   2 番目以降の文字では、Unicode Standard 2.0 に定義されている文字または数字と、アンダースコア (_) を使用できます。  
  
## <a name="catalog-configuration"></a>カタログの構成  
 カタログ プロパティを調整することによって、カタログの動作を微調整します。 カタログ プロパティは、機微なデータを暗号化する方法と、操作およびプロジェクトのバージョン管理データを保持する方法を定義します。 カタログ プロパティを設定するには、 **[カタログのプロパティ]** ダイアログ ボックスを使用するか、[catalog.configure_catalog (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database) ストアド プロシージャを呼び出します。 プロパティを表示するには、ダイアログ ボックスまたはクエリ [catalog.catalog_properties (SSISDB Database)](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database) を使用します。 ダイアログ ボックスには、オブジェクト エクスプローラーで `SSISDB` を右クリックしてアクセスできます。  
  
### <a name="operations-and-project-version-cleanup"></a>操作とプロジェクト バージョンのクリーンアップ  
 カタログの多くの操作の状態データは、内部データベース テーブルに格納されます。 たとえば、カタログではパッケージの実行とプロジェクトの配置の状態が追跡されます。 操作データのサイズを維持するには、 **の** SSIS サーバー メンテナンス ジョブ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して古いデータを削除します。 この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のインストール時に作成されます。  
  
 同じ名前の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトをカタログの同じフォルダーに配置することで、このプロジェクトを更新または再配置できます。 既定では、毎回再デプロイするプロジェクトを`SSISDB`カタログは、プロジェクトの以前のバージョンを保持します。 操作データのサイズを維持するには、 **SSIS サーバー メンテナンス ジョブ** を使用して古いバージョンのプロジェクトを削除します。  
  
 次`SSISDB`カタログのプロパティを定義する方法、この[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント ジョブの動作します。 **[カタログ プロパティ]** ダイアログ ボックスを利用するか、[catalog.catalog_properties (SSISDB データベース)](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database) と [catalog.configure_catalog (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database) を利用し、プロパティを表示し、変更できます。  
  
 **ログを定期的に消去する**  
 このプロパティが `True` に設定されている場合は、操作のクリーンアップのジョブ ステップが実行されます。  
  
 **保有期間 (日)**  
 操作データの最大保有期間を日数で定義します。 この期間を経過したデータは削除されます。  
  
 最小値は 1 日です。 最大値はの最大値によってのみ制限されます、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `int`データ。 このデータ型に関する詳細については、「[int、bigint、smallint、および tinyint (Transact-SQL)](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)」を参照してください。  
  
 **古いバージョンを定期的に削除する**  
 このプロパティが `True` に設定されている場合は、プロジェクト バージョンのクリーンアップのジョブ ステップが実行されます。  
  
 **プロジェクトごとのバージョンの最大数**  
 カタログに格納されるプロジェクトのバージョンの数を定義します。 この数を超える古いバージョンのプロジェクトは削除されます。  
  
### <a name="encryption-algorithm"></a>暗号化アルゴリズム  
 **[暗号化アルゴリズム]** プロパティでは、秘密性の高いパラメーター値を暗号化するために使用される暗号化の種類を指定します。 次の暗号化の種類から選択できます。  
  
-   AES_256 (既定値)  
  
-   AES_192  
  
-   AES_128  
  
-   DESX  
  
-   TRIPLE_DES_3KEY  
  
-   TRIPLE_DES  
  
-   DES  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]サーバーに配置する場合、カタログは自動的にパッケージのデータと重要な値を暗号化します。 また、ユーザーがデータを取得するときには、自動的に暗号化を解除します。 SSISDB カタログは、`ServerStorage` 保護レベルを使用します。 詳しくは、「 [Access Control for Sensitive Data in Packages](../security/access-control-for-sensitive-data-in-packages.md)」をご覧ください。  
  
 暗号化アルゴリズムの変更は、時間のかかる操作です。 最初に、サーバーで以前に指定したアルゴリズムを使用して、すべての構成値の暗号化を解除する必要があります。 次に、新しいアルゴリズムを使用して、その値を再暗号化する必要があります。 この間、サーバーで他の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 操作を実行できません。 そのため、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 操作を途切れることなく続行できるように、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]では、暗号化アルゴリズムが読み取り専用の値になっています。  
  
 変更する、**暗号化アルゴリズム**プロパティの設定は、設定、`SSISDB`データベースをシングル ユーザー モードとし、catalog.configure_catalog ストアド プロシージャを呼び出します。 *property_name* 引数の ENCRYPTION_ALGORITHM を使用します。 プロパティの値の詳細については、「[catalog.catalog_properties (SSISDB データベース)](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database)」を参照してください。 ストアド プロシージャの詳細については、「[catalog.configure_catalog (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database)」を参照してください。  
  
 シングル ユーザー モードの詳細については、「[データベースをシングル ユーザー モードに設定する](../../relational-databases/databases/set-a-database-to-single-user-mode.md)」を参照してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の暗号化と暗号化アルゴリズムの詳細については、「 [SQL Server の暗号化](../../relational-databases/security/encryption/sql-server-encryption.md)」のトピックを参照してください。  
  
 暗号化にはデータベース マスター キーが使用されます。 このキーは、カタログの作成時に作成されます。 詳細については、「 [SSIS カタログの作成](ssis-catalog.md)」を参照してください。  
  
 次の表では、 **[カタログのプロパティ]** ダイアログ ボックスに示されるプロパティ名と、データベース ビュー内の対応するプロパティについて説明します。  
  
|プロパティ名 ( **[カタログのプロパティ]** ダイアログ ボックス)|プロパティ名 (データベース ビュー)|  
|---------------------------------------------------------|-------------------------------------|  
|暗号化アルゴリズムの名前|ENCRYPTION_ALGORITHM|  
|ログを定期的に消去する|OPERATION_CLEANUP_ENABLED|  
|保有期間 (日)|RETENTION_WINDOW|  
|古いバージョンを定期的に削除する|VERSION_CLEANUP_ENABLED|  
|プロジェクトごとのバージョンの最大数|MAX_PROJECT_VERSIONS|  
|サーバー全体の既定のログ記録レベル|SERVER_LOGGING_LEVEL|  
  
## <a name="permissions"></a>アクセス許可  
 プロジェクト、環境、およびパッケージは、セキュリティ保護可能なオブジェクトであるフォルダーに格納されます。 MANAGE_OBJECT_PERMISSIONS 権限などのフォルダーに対する権限を許可することができます。 MANAGE_OBJECT_PERMISSIONS を許可すると、ユーザーに ssis_admin ロールのメンバーシップを許可しなくても、フォルダー内容の管理をユーザーに委任できます。 プロジェクト、環境、および操作に権限を付与することもできます。 操作には、初期化が含まれます[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、展開プロジェクト、作成し実行を開始、プロジェクトおよびパッケージの検証、構成、`SSISDB`カタログ。  
  
 データベース ロールの詳細については、「 [データベース レベルのロール](../../relational-databases/security/authentication-access/database-level-roles.md)」を参照してください。  
  
 SSISDB カタログでは、DDL トリガーの ddl_cleanup_object_permissions を使用して、SSIS のセキュリティ保護可能なリソースの権限情報の整合性を保ちます。 このトリガーは、データベース ユーザー、データベース ロール、データベース アプリケーション ロールなどのデータベース プリンシパルが SSISDB データベースから削除されたときに起動します。  
  
 このプリンシパルによって他のプリンシパルに権限が許可または拒否されている場合は、プリンシパルを削除する前に、権限の許可者が付与した権限を取り消してください。 取り消していない場合は、プリンシパルの削除が試行されるとエラー メッセージが返されます。 トリガーでは、データベース プリンシパルが権限付与対象ユーザーであるすべての権限レコードが削除されます。  
  
 トリガーは無効にしないことを後が存在しない孤立した権限レコードから、データベース プリンシパルが削除されるようにするためお勧めしますが、`SSISDB`データベース。  
  
### <a name="managing-permissions"></a>権限の管理  
 権限は、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の UI、ストアド プロシージャ、<xref:Microsoft.SqlServer.Management.IntegrationServices> 名前空間を使って管理できます。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の UI を使って権限を管理するには、次のダイアログ ボックスを使用します。  
  
-   フォルダーを使用して、 **権限** のページ、 [Folder Properties Dialog Box](folder-properties-dialog-box.md)します。  
  
-   プロジェクトの場合は、 **権限** の [Project Properties Dialog Box](project-properties-dialog-box.md)します。  
  
 Transact-SQL を利用して権限を管理するには、[catalog.grant_permission (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database)、[catalog.deny_permission (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database)、[catalog.revoke_permission (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database) を呼び出します。 すべてのオブジェクトの現在のプリンシパルで有効な権限を表示するには、[catalog.effective_object_permissions (SSISDB データベース)](/sql/integration-services/system-views/catalog-effective-object-permissions-ssisdb-database) にクエリを実行します。 このトピックでは、さまざまな種類の権限について説明します。 ユーザーに明示的に割り当てられている権限を表示するには、[catalog.explicit_object_permissions (SSISDB データベース)](/sql/integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database) にクエリを実行します。  
  
## <a name="folders"></a>フォルダー  
 1 つまたは複数のプロジェクトおよび環境のフォルダーに含まれる、`SSISDB`カタログ。 [catalog.folders (SSISDB データベース)](/sql/integration-services/system-views/catalog-folders-ssisdb-database) ビューを使用して、カタログのフォルダーに関する情報にアクセスできます。 次のストアド プロシージャを使用して、フォルダーを管理することができます。  
  
-   [catalog.create_folder &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database)  
  
-   [catalog.delete_folder &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database)  
  
-   [catalog.rename_folder &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database)  
  
-   [catalog.set_folder_description &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database)  
  
## <a name="projects-and-packages"></a>プロジェクトとパッケージ  
 各プロジェクトには、複数のパッケージを含めることができます。 プロジェクトとパッケージの両方に、パラメーターおよび環境への参照を含めることができます。 [Configure Dialog Box](configure-dialog-box.md)を使用して、パラメーターおよび環境への参照にアクセスできます。  
  
 次のストアド プロシージャを呼び出して、他のプロジェクト タスクを実行することができます。  
  
-   [catalog.delete_project &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database)  
  
-   [catalog.deploy_project &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database)  
  
-   [catalog.get_project &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-get-project-ssisdb-database)  
  
-   [catalog.move_project &#40;&#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-move-project-ssisdb-database)  
  
-   [catalog.restore_project &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database)  
  
 次のビューには、パッケージ、プロジェクト、およびプロジェクトのバージョンに関する詳細が表示されます。  
  
-   [catalog.projects &#40;SSISDB データベース&#41;](/sql/integration-services/system-views/catalog-projects-ssisdb-database)  
  
-   [catalog.packages &#40;SSISDB データ&#41;](/sql/integration-services/system-views/catalog-packages-ssisdb-database)  
  
-   [catalog.object_versions &#40;SSISDB データベース&#41;](/sql/integration-services/system-views/catalog-object-versions-ssisdb-database)  
  
## <a name="parameters"></a>パラメーター  
 パラメーターを使用して、パッケージの実行時にパッケージ プロパティに値を割り当てます。 パッケージまたはプロジェクト パラメーターの値を設定したり、値を消去したりするには、[catalog.set_object_parameter_value (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database) と [catalog.clear_object_parameter_value (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database) を呼び出します。 実行のインスタンスのパラメーターの値を設定するには、[catalog.set_execution_parameter_value (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database) を呼び出します。 [catalog.get_parameter_values (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database) を呼び出すことで既定のパラメーター値を取得できます。  
  
 次のビューには、すべてのパッケージとプロジェクトのパラメーター、および実行のインスタンスに使用されるパラメーター値が表示されます。  
  
-   [catalog.object_parameters &#40;SSISDB データベース&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database)  
  
-   [catalog.execution_parameter_values &#40;SSISDB データベース&#41;](/sql/integration-services/system-views/catalog-execution-parameter-values-ssisdb-database)  
  
## <a name="server-environments-server-variables-and-server-environment-references"></a>サーバー環境、サーバー変数、およびサーバー環境参照  
 サーバー環境にはサーバー変数が含まれます。 変数値は、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーでパッケージを実行または検証するときに使用できます。  
  
 次のストアド プロシージャを使用すると、環境と変数の他の多くの管理タスクを実行することができます。  
  
-   [catalog.create_environment &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database)  
  
-   [catalog.delete_environment &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database)  
  
-   [catalog.move_environment &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database)  
  
-   [catalog.rename_environment &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database)  
  
-   [catalog.set_environment_property &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database)  
  
-   [catalog.create_environment_variable &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database)  
  
-   [catalog.delete_environment_variable &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database)  
  
-   [catalog.set_environment_variable_property &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database)  
  
-   [catalog.set_environment_variable_value &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database)  
  
 [catalog.set_environment_variable_protection (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database) ストアド プロシージャを呼び出すことで、変数のセンシティビティ ビットを設定できます。  
  
 サーバー変数の値を使用するには、プロジェクトとサーバー環境間の参照を指定します。 次のストアド プロシージャを使用して、参照を作成したり削除したりすることができます。 環境をプロジェクトと同じフォルダーに配置できるか、または別のフォルダーに配置できるかを示すこともできます。  
  
-   [catalog.create_environment_reference &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database)  
  
-   [catalog.delete_environment_reference &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database)  
  
-   [catalog.set_environment_reference_type &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database)  
  
 環境と変数の詳細については、次のビューに対してクエリを実行します。  
  
-   [catalog.environments &#40;SSISDB データベース&#41;](/sql/integration-services/system-views/catalog-environments-ssisdb-database)  
  
-   [catalog.environment_variables &#40;SSISDB データベース&#41;](/sql/integration-services/system-views/catalog-environment-variables-ssisdb-database)  
  
-   [catalog.environment_references &#40;SSISDB データベース&#41;](/sql/integration-services/system-views/catalog-environment-references-ssisdb-database)  
  
## <a name="executions-and-validations"></a>実行と検証  
 実行はパッケージ実行のインスタンスです。 実行を作成し、開始するには、[catalog.create_execution (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database) と [catalog.start_execution (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) を呼び出します。 実行またはパッケージ/プロジェクト検証を停止するには、[catalog.stop_operation (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database) を呼び出します。  
  
 実行中のパッケージを一時停止してダンプ ファイルを作成するには、catalog.create_execution_dump ストアド プロシージャを呼び出します。 ダンプ ファイルは、実行に関する問題のトラブルシューティングに役立つ、パッケージの実行に関する情報を提供します。 ダンプ ファイルの生成および構成の詳細については、「 [Generating Dump Files for Package Execution](../troubleshooting/generating-dump-files-for-package-execution.md)」をご覧ください。  
  
 実行、検証、操作中にログに記録されたメッセージ、およびエラーに関するコンテキスト情報の詳細については、次のビューに対してクエリを実行します。  
  
-   [catalog.executions &#40;SSISDB データベース&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database)  
  
-   [catalog.operations &#40;SSISDB データベース&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database)  
  
-   [catalog.operation_messages &#40;SSISDB データベース&#41;](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database)  
  
-   [catalog.extended_operation_info &#40;SSISDB データベース&#41;](/sql/integration-services/system-views/catalog-extended-operation-info-ssisdb-database)  
  
-   [catalog.event_messages](/sql/integration-services/system-views/catalog-event-messages)  
  
-   [catalog.event_message_context](/sql/integration-services/system-views/catalog-event-message-context)  
  
 [catalog.validate_project (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database) および [catalog.validate_package (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database) ストアド プロシージャを呼び出すことで、プロジェクトとパッケージを検証できます。 [catalog.validations (SSISDB データベース)](/sql/integration-services/system-views/catalog-validations-ssisdb-database) ビューには、検証で考慮されるサーバー環境参照、検証が依存関係の検証であるか完全検証であるか、32 ビット ランタイムと 64 ビット ランタイムのどちらをパッケージの実行に使用するかなどの、検証に関する詳細が表示されます。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [SSIS カタログの作成](ssis-catalog.md)  
  
-   [SSIS カタログのバックアップ、復元、および移動](../backup-restore-and-move-the-ssis-catalog.md)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   blogs.msdn.com のブログ「 [SQL Server 2012 での SSIS と PowerShell](https://go.microsoft.com/fwlink/?LinkId=242539)」  
  
-   blogs.msdn.com のブログ エントリ「 [SSIS カタログのアクセス制御のヒント](https://go.microsoft.com/fwlink/?LinkId=246669)」  
  
-   blogs.msdn.com のブログ エントリ「 [SSIS カタログ マネージド オブジェクト モデルの概要](https://go.microsoft.com/fwlink/?LinkId=254267)」  
  
  
