---
title: SSIS カタログ | Microsoft Docs
ms.custom: ''
ms.date: 11/12/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.iscreatecatalog.f1
- sql13.ssis.ssms.iscatalogprop.general.f1
- sql13.ssis.dbupgradewizard.f1
ms.assetid: 24bd987e-164a-48fd-b4f2-cbe16a3cd95e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1e240a53d86d66fdf81b53cae1ba55d41820befd
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294963"
---
# <a name="ssis-catalog"></a>SSIS カタログ

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **SSISDB** カタログは、[!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] サーバーに配置した [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] (SSIS) プロジェクトを操作するための中核となります。 たとえば、プロジェクト パラメーターとパッケージ パラメーターの設定、パッケージに合わせたランタイム値を指定するための環境の構成、パッケージの実行およびトラブルシューティング、 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] サーバー操作の管理を行います。  
 
> [!NOTE]
> この記事では、SSIS カタログ全般とオンプレミスで実行されている SSIS カタログについて説明します。 Azure SQL Database で SSIS カタログを作成し、Azure で SSIS パッケージをデプロイし、実行することもできます。 詳細については、「[Lift and shift SQL Server Integration Services workloads to the cloud](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)」 (SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする) を参照してください。
>
> Linux で SSIS パッケージを実行することもできますが、SSIS カタログは Linux ではサポートされていません。 詳しくは、「[SSIS で Linux 上のデータの抽出、変換、読み込みを行う](../../linux/sql-server-linux-migrate-ssis.md)」 をご覧ください。
 
 **SSISDB** カタログに格納されているオブジェクトには、プロジェクト、パッケージ、パラメーター、環境、および操作履歴があります。  
  
 **SSISDB** カタログに格納されているオブジェクト、設定、および業務データを検査するには、 **SSISDB** データベースのビューに対してクエリを実行します。 オブジェクトを管理するには、 **SSISDB** データベースのストアド プロシージャを呼び出すか、 **SSISDB** カタログの UI を使用します。 多くの場合、UI でもストアド プロシージャの呼び出しでも同じタスクを実行できます。  
  
 **SSISDB** データベースを保守するには、ユーザー データベースの管理に標準的なエンタープライズ ポリシーを適用することをお勧めします。 メンテナンス プランの作成については、「 [Maintenance Plans](../../relational-databases/maintenance-plans/maintenance-plans.md)」をご覧ください。  
  
 **SSISDB** カタログおよび **SSISDB** データベースは、Windows PowerShell をサポートしています。 Windows PowerShell による SQL Server の使用の詳細については、「 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)」をご覧ください。 Windows PowerShell を使用してプロジェクトの配置などのタスクを実行する方法の例については、blogs.msdn.com のブログ エントリ「 [SQL Server 2012 での SSIS と PowerShell](https://go.microsoft.com/fwlink/?LinkId=242539)」をご覧ください。  
  
 操作データの表示に関する詳細については、「 [パッケージとその他の操作を実行するモニター](../../integration-services/performance/monitor-running-packages-and-other-operations.md)」をご覧ください。  
  
 **の** SSISDB [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] カタログにアクセスするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース エンジンに接続し、オブジェクト エクスプローラーで **[Integration Services カタログ]** ノードを展開します。 **で** SSISDB [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] データベースにアクセスするには、オブジェクト エクスプローラーで [データベース] ノードを展開します。  
  
> [!NOTE]
> **SSISDB** データベースの名前は変更できません。  
  
> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSISDB **データベースがアタッチされている** インスタンスが停止したか、応答しない場合、ISServerExec.exe プロセスは終了します。 メッセージが Windows イベント ログに書き込まれます。  
>   
>  クラスター フェールオーバーの一環として [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソースがフェールオーバーした場合、実行中のパッケージは再開されません。 チェックポイントを使用してパッケージを再開できます。 詳細については、「 [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md)」を参照してください。  
  
## <a name="features-and-capabilities"></a>機能および能力  
  
-   [カタログ オブジェクト識別子](../../integration-services/catalog/ssis-catalog.md#CatalogObjectIdentifiers)  
  
-   [カタログの構成](../../integration-services/catalog/ssis-catalog.md#Configuration)  
  
-   [アクセス許可](../../integration-services/catalog/ssis-catalog.md#Permissions)  
  
-   [フォルダー](../../integration-services/catalog/ssis-catalog.md#Folders)  
  
-   [プロジェクトとパッケージ](../../integration-services/catalog/ssis-catalog.md#ProjectsAndPackages)  
  
-   [パラメーター](../../integration-services/catalog/ssis-catalog.md#Parameters)  
  
-   [サーバー環境、サーバー変数、およびサーバー環境参照](../../integration-services/catalog/ssis-catalog.md#ServerEnvironments)  
  
-   [実行と検証](../../integration-services/catalog/ssis-catalog.md#Executions)  

##  <a name="CatalogObjectIdentifiers"></a> カタログ オブジェクト識別子  
 カタログに新しいオブジェクトを作成するときは、オブジェクトに名前を割り当てる必要があります。 オブジェクト名が識別子となります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、識別子に使用できる文字のルールが定義されています。 次のオブジェクトの名前は、識別子のルールに従っている必要があります。  
  
-   フォルダー  
  
-   プロジェクト  
  
-   環境  
  
-   パラメーター  
  
-   環境変数  
  
###  <a name="Folder"></a> フォルダー、プロジェクト、環境  
 フォルダー、プロジェクト、または環境の名前を変更するときは、次のルールを考慮します。  
  
-   無効な文字には、ASCII/Unicode 文字 1 - 31、引用符 (")、小なり (\<)、大なり (>)、パイプ (|)、バックスペース (\b)、null (\0)、タブ (\t) などがあります。  
  
-   名前の先頭または末尾にスペースを含めることはできません。  
  
-   名前を \@ で始めることはできませんが、先頭以外では \@ を使用できます。  
  
-   名前の長さは 1 ～ 128 文字にする必要があります。  
  
###  <a name="Parameter"></a> パラメーター  
 パラメーターに名前を付けるときは、次のルールを考慮します。  
  
-   名前の最初の文字は、Unicode Standard 2.0 に定義されている文字か、アンダースコア (_) である必要があります。  
  
-   2 番目以降の文字では、Unicode Standard 2.0 に定義されている文字または数字と、アンダースコア (_) を使用できます。  
  
###  <a name="EnvironmentVariable"></a> 環境変数  
 環境変数に名前を付けるときは、次のルールを考慮します。  
  
-   無効な文字には、ASCII/Unicode 文字 1 - 31、引用符 (")、小なり (\<)、大なり (>)、パイプ (|)、バックスペース (\b)、null (\0)、タブ (\t) などがあります。  
  
-   名前の先頭または末尾にスペースを含めることはできません。  
  
-   名前を \@ で始めることはできませんが、先頭以外では \@ を使用できます。  
  
-   名前の長さは 1 ～ 128 文字にする必要があります。  
  
-   名前の最初の文字は、Unicode Standard 2.0 に定義されている文字か、アンダースコア (_) である必要があります。  
  
-   2 番目以降の文字では、Unicode Standard 2.0 に定義されている文字または数字と、アンダースコア (_) を使用できます。  
  
##  <a name="Configuration"></a> カタログの構成  
 カタログ プロパティを調整することによって、カタログの動作を微調整します。 カタログ プロパティは、機微なデータを暗号化する方法と、操作およびプロジェクトのバージョン管理データを保持する方法を定義します。 カタログ プロパティを設定するには、 **[カタログのプロパティ]** ダイアログ ボックスを使用するか、[catalog.configure_catalog (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md) ストアド プロシージャを呼び出します。 プロパティを表示するには、ダイアログ ボックスまたはクエリ [catalog.catalog_properties (SSISDB Database)](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) を使用します。 ダイアログ ボックスには、オブジェクト エクスプローラーで **SSISDB** を右クリックしてアクセスできます。  
  
###  <a name="Cleanup"></a> 操作とプロジェクト バージョンのクリーンアップ  
 カタログの多くの操作の状態データは、内部データベース テーブルに格納されます。 たとえば、カタログではパッケージの実行とプロジェクトの配置の状態が追跡されます。 操作データのサイズを維持するには、 **の** SSIS サーバー メンテナンス ジョブ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して古いデータを削除します。 この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のインストール時に作成されます。  
  
 同じ名前の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトをカタログの同じフォルダーに配置することで、このプロジェクトを更新または再配置できます。 既定では、プロジェクトを再配置するたびに、 **SSISDB** カタログには以前のバージョンのプロジェクトが保持されます。 操作データのサイズを維持するには、 **SSIS サーバー メンテナンス ジョブ** を使用して古いバージョンのプロジェクトを削除します。  
 
**SSIS サーバー メンテナンス ジョブ**を実行するために、SSIS で SQL Server ログイン **##MS_SSISServerCleanupJobLogin##** が作成されます。 このログインは SSIS による内部使用専用です。
  
 次の **SSISDB** カタログ プロパティで、この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブの動作を定義します。 **[カタログ プロパティ]** ダイアログ ボックスを利用するか、[catalog.catalog_properties (SSISDB データベース)](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) と [catalog.configure_catalog (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md) を利用し、プロパティを表示し、変更できます。  
  
 **ログを定期的に消去する**  
 このプロパティが **True**に設定されている場合は、操作のクリーンアップのジョブ ステップが実行されます。  
  
 **保有期間 (日)**  
 操作データの最大保有期間を日数で定義します。 この期間を経過したデータは削除されます。  
  
 最小値は 1 日です。 最大値は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **int** データ型の最大値によってのみ制限されます。 このデータ型に関する詳細については、「[int、bigint、smallint、および tinyint (Transact-SQL)](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)」を参照してください。  
  
 **古いバージョンを定期的に削除する**  
 このプロパティが **True**に設定されている場合は、プロジェクト バージョンのクリーンアップのジョブ ステップが実行されます。  
  
 **プロジェクトごとのバージョンの最大数**  
 カタログに格納されるプロジェクトのバージョンの数を定義します。 この数を超える古いバージョンのプロジェクトは削除されます。  
  
###  <a name="Encryption"></a> 暗号化アルゴリズム  
 **[暗号化アルゴリズム]** プロパティでは、秘密性の高いパラメーター値を暗号化するために使用される暗号化の種類を指定します。 次の暗号化の種類から選択できます。  
  
-   AES_256 (既定値)  
  
-   AES_192  
  
-   AES_128  
  
-   DESX  
  
-   TRIPLE_DES_3KEY  
  
-   TRIPLE_DES  
  
-   DES  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置する場合、カタログは自動的にパッケージのデータと機微な値を暗号化します。 また、ユーザーがデータを取得するときには、自動的に暗号化を解除します。 SSISDB カタログは、 **ServerStorage** 保護レベルを使用します。 詳しくは、「 [Access Control for Sensitive Data in Packages](../../integration-services/security/access-control-for-sensitive-data-in-packages.md)」をご覧ください。  
  
 暗号化アルゴリズムの変更は、時間のかかる操作です。 最初に、サーバーで以前に指定したアルゴリズムを使用して、すべての構成値の暗号化を解除する必要があります。 次に、新しいアルゴリズムを使用して、その値を再暗号化する必要があります。 この間、サーバーで他の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 操作を実行できません。 そのため、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 操作を途切れることなく続行できるように、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]では、暗号化アルゴリズムが読み取り専用の値になっています。  
  
 **[暗号化アルゴリズム]** プロパティの設定を変更するには、 **SSISDB** データベースをシングル ユーザー モードに設定し、catalog.configure_catalog ストアド プロシージャを呼び出します。 *property_name* 引数の ENCRYPTION_ALGORITHM を使用します。 プロパティの値の詳細については、「[catalog.catalog_properties (SSISDB データベース)](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)」を参照してください。 ストアド プロシージャの詳細については、「[catalog.configure_catalog (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)」を参照してください。  
  
 シングル ユーザー モードの詳細については、「[データベースをシングル ユーザー モードに設定する](../../relational-databases/databases/set-a-database-to-single-user-mode.md)」を参照してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の暗号化と暗号化アルゴリズムの詳細については、「 [SQL Server の暗号化](../../relational-databases/security/encryption/sql-server-encryption.md)」のトピックを参照してください。  
  
 暗号化にはデータベース マスター キーが使用されます。 このキーは、カタログの作成時に作成されます。  
  
 次の表では、 **[カタログのプロパティ]** ダイアログ ボックスに示されるプロパティ名と、データベース ビュー内の対応するプロパティについて説明します。  
  
|プロパティ名 ( **[カタログのプロパティ]** ダイアログ ボックス)|プロパティ名 (データベース ビュー)|  
|---------------------------------------------------------|-------------------------------------|  
|暗号化アルゴリズムの名前|ENCRYPTION_ALGORITHM|  
|ログを定期的に消去する|OPERATION_CLEANUP_ENABLEDâ€‹|  
|保有期間 (日)|RETENTION_WINDOW|  
|古いバージョンを定期的に削除する|VERSION_CLEANUP_ENABLED|  
|プロジェクトごとのバージョンの最大数|MAX_PROJECT_VERSIONS|  
|サーバー全体の既定のログ記録レベル|SERVER_LOGGING_LEVEL|  
  
##  <a name="Permissions"></a> Permissions  
 プロジェクト、環境、およびパッケージは、セキュリティ保護可能なオブジェクトであるフォルダーに格納されます。 MANAGE_OBJECT_PERMISSIONS 権限などのフォルダーに対する権限を許可することができます。 MANAGE_OBJECT_PERMISSIONS を許可すると、ユーザーに ssis_admin ロールのメンバーシップを許可しなくても、フォルダー内容の管理をユーザーに委任できます。 プロジェクト、環境、および操作に権限を付与することもできます。 操作には、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]の初期化、プロジェクトの配置、実行の作成および開始、プロジェクトおよびパッケージの検証、 **SSISDB** カタログの構成などがあります。  
  
 データベース ロールの詳細については、「 [データベース レベルのロール](../../relational-databases/security/authentication-access/database-level-roles.md)」を参照してください。  
  
 SSISDB カタログでは、DDL トリガーの ddl_cleanup_object_permissions を使用して、SSIS のセキュリティ保護可能なリソースの権限情報の整合性を保ちます。 このトリガーは、データベース ユーザー、データベース ロール、データベース アプリケーション ロールなどのデータベース プリンシパルが SSISDB データベースから削除されたときに起動します。  
  
 このプリンシパルによって他のプリンシパルに権限が許可または拒否されている場合は、プリンシパルを削除する前に、権限の許可者が付与した権限を取り消してください。 取り消していない場合は、プリンシパルの削除が試行されるとエラー メッセージが返されます。 トリガーでは、データベース プリンシパルが権限付与対象ユーザーであるすべての権限レコードが削除されます。  
  
 トリガーは無効にしないことをお勧めします。これは、データベース プリンシパルが **SSISDB** データベースから削除された後に孤立した権限レコードが存在しないようにするためです。  
  
### <a name="managing-permissions"></a>権限の管理  
 権限は、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の UI、ストアド プロシージャ、<xref:Microsoft.SqlServer.Management.IntegrationServices> 名前空間を使って管理できます。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の UI を使ってアクセス許可を管理するには、次のダイアログ ボックスを使用します。 
  
-   フォルダーを使用して、 **権限** のページ、 [Folder Properties Dialog Box](../../integration-services/catalog/folder-properties-dialog-box.md)します。  
  
-   プロジェクトの場合は、 **権限** の [Project Properties Dialog Box](../../integration-services/catalog/project-properties-dialog-box.md)します。  

 Transact-SQL を利用してアクセス許可を管理するには、[catalog.grant_permission (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md)、[catalog.deny_permission (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database.md)、[catalog.revoke_permission (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database.md) を呼び出します。 すべてのオブジェクトの現在のプリンシパルで有効な権限を表示するには、[catalog.effective_object_permissions (SSISDB データベース)](../../integration-services/system-views/catalog-effective-object-permissions-ssisdb-database.md) にクエリを実行します。 このトピックでは、さまざまな種類の権限について説明します。 ユーザーに明示的に割り当てられている権限を表示するには、[catalog.explicit_object_permissions (SSISDB データベース)](../../integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database.md) にクエリを実行します。  
  
##  <a name="Folders"></a> フォルダー  
 フォルダーには、 **SSISDB** カタログ内の 1 つ以上のプロジェクトおよび環境が含まれます。 [catalog.folders (SSISDB データベース)](../../integration-services/system-views/catalog-folders-ssisdb-database.md) ビューを使用して、カタログのフォルダーに関する情報にアクセスできます。 次のストアド プロシージャを使用して、フォルダーを管理することができます。  
  
-   [catalog.create_folder &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database.md)  
  
-   [catalog.delete_folder &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database.md)  
  
-   [catalog.rename_folder &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database.md)  
  
-   [catalog.set_folder_description &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database.md)  
  
##  <a name="ProjectsAndPackages"></a> プロジェクトとパッケージ  
 各プロジェクトには、複数のパッケージを含めることができます。 プロジェクトとパッケージの両方に、パラメーターおよび環境への参照を含めることができます。 [Configure Dialog Box](../../integration-services/catalog/configure-dialog-box.md)を使用して、パラメーターおよび環境への参照にアクセスできます。  
  
 次のストアド プロシージャを呼び出して、他のプロジェクト タスクを実行することができます。 
  
-   [catalog.delete_project &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database.md)  
  
-   [catalog.deploy_project &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md)  
  
-   [catalog.get_project &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md)  
  
-   [catalog.move_project &#40;&#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-move-project-ssisdb-database.md)  
  
-   [catalog.restore_project &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md)  
  
 次のビューには、パッケージ、プロジェクト、およびプロジェクトのバージョンに関する詳細が表示されます。  
  
-   [catalog.projects &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-projects-ssisdb-database.md)  
  
-   [catalog.packages &#40;SSISDB データ&#41;](../../integration-services/system-views/catalog-packages-ssisdb-database.md)  
  
-   [catalog.object_versions &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md)  
  
##  <a name="Parameters"></a> パラメーター  
 パラメーターを使用して、パッケージの実行時にパッケージ プロパティに値を割り当てます。 パッケージまたはプロジェクト パラメーターの値を設定したり、値を消去したりするには、[catalog.set_object_parameter_value (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md) と [catalog.clear_object_parameter_value (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md) を呼び出します。 実行のインスタンスのパラメーターの値を設定するには、[catalog.set_execution_parameter_value (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) を呼び出します。 [catalog.get_parameter_values (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md) を呼び出すことで既定のパラメーター値を取得できます。  
  
 次のビューには、すべてのパッケージとプロジェクトのパラメーター、および実行のインスタンスに使用されるパラメーター値が表示されます。  
  
-   [catalog.object_parameters &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)  
  
-   [catalog.execution_parameter_values &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)  
  
##  <a name="ServerEnvironments"></a> サーバー環境、サーバー変数、およびサーバー環境参照  
 サーバー環境にはサーバー変数が含まれます。 変数値は、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーでパッケージを実行または検証するときに使用できます。  
  
 次のストアド プロシージャを使用すると、環境と変数の他の多くの管理タスクを実行することができます。  
  
-   [catalog.create_environment &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database.md)  
  
-   [catalog.delete_environment &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database.md)  
  
-   [catalog.move_environment &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database.md)  
  
-   [catalog.rename_environment &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database.md)  
  
-   [catalog.set_environment_property &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database.md)  
  
-   [catalog.create_environment_variable &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database.md)  
  
-   [catalog.delete_environment_variable &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database.md)  
  
-   [catalog.set_environment_variable_property &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database.md)  
  
-   [catalog.set_environment_variable_value &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database.md)  
  
 [catalog.set_environment_variable_protection (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database.md) ストアド プロシージャを呼び出すことで、変数のセンシティビティ ビットを設定できます。  
  
 サーバー変数の値を使用するには、プロジェクトとサーバー環境間の参照を指定します。 次のストアド プロシージャを使用して、参照を作成したり削除したりすることができます。 環境をプロジェクトと同じフォルダーに配置できるか、または別のフォルダーに配置できるかを示すこともできます。  
  
-   [catalog.create_environment_reference &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database.md)  
  
-   [catalog.delete_environment_reference &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database.md)  
  
-   [catalog.set_environment_reference_type &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database.md)  
  
 環境と変数の詳細については、次のビューに対してクエリを実行します。  
  
-   [catalog.environments &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-environments-ssisdb-database.md)  
  
-   [catalog.environment_variables &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-environment-variables-ssisdb-database.md)  
  
-   [catalog.environment_references &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-environment-references-ssisdb-database.md)  
  
##  <a name="Executions"></a> 実行と検証  
 実行はパッケージ実行のインスタンスです。 実行を作成し、開始するには、[catalog.create_execution (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md) と [catalog.start_execution (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) を呼び出します。 実行またはパッケージ/プロジェクト検証を停止するには、[catalog.stop_operation (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md) を呼び出します。  
  
 実行中のパッケージを一時停止してダンプ ファイルを作成するには、catalog.create_execution_dump ストアド プロシージャを呼び出します。 ダンプ ファイルは、実行に関する問題のトラブルシューティングに役立つ、パッケージの実行に関する情報を提供します。 ダンプ ファイルの生成および構成の詳細については、「 [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)」をご覧ください。  
  
 実行、検証、操作中にログに記録されたメッセージ、およびエラーに関するコンテキスト情報の詳細については、次のビューに対してクエリを実行します。  
  
-   [catalog.executions &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)  
  
-   [catalog.operations &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)  
  
-   [catalog.operation_messages &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)  
  
-   [catalog.extended_operation_info &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md)  
  
-   [catalog.event_messages](../../integration-services/system-views/catalog-event-messages.md)  
  
-   [catalog.event_message_context](../../integration-services/system-views/catalog-event-message-context.md)  
  
 [catalog.validate_project (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database.md) および [catalog.validate_package (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database.md) ストアド プロシージャを呼び出すことで、プロジェクトとパッケージを検証できます。 [catalog.validations (SSISDB データベース)](../../integration-services/system-views/catalog-validations-ssisdb-database.md) ビューには、検証で考慮されるサーバー環境参照、検証が依存関係の検証であるか完全検証であるか、32 ビット ランタイムと 64 ビット ランタイムのどちらをパッケージの実行に使用するかなどの、検証に関する詳細が表示されます。  

## <a name="create-the-ssis-catalog"></a>SSIS カタログの作成
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]でパッケージをデザインしてテストしたら、パッケージを含むプロジェクトを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置できます。 プロジェクトを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置するには、まず、サーバーに **SSISDB** カタログを含める必要があります。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] のインストール プログラムでは、カタログは自動的に作成されません。次の手順を使用して、カタログを手動で作成する必要があります。  
  
 SSISDB カタログは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で作成できます。 Windows PowerShell を使用して、カタログをプログラムから作成することもできます。  
  
### <a name="to-create-the-ssisdb-catalog-in-sql-server-management-studio"></a>SQL Server Management Studio で SSISDB カタログを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を開きます。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース エンジンに接続します。  
  
3.  オブジェクト エクスプローラーで、サーバー ノードを展開します。次に、 **[Integration Services カタログ]** ノードを右クリックし、 **[カタログの作成]** をクリックします。  
  
4.  **[CLR 統合を有効にする]** をクリックします。  
  
     カタログは CLR ストアド プロシージャを使用します。  
  
5.  **サーバー インスタンスを再起動するたびに** catalog.startup [ストアド プロシージャが実行されるようにするには、](../../integration-services/system-stored-procedures/catalog-startup.md) [SQL Server のスタートアップ時に Integration Services ストアド プロシージャを自動実行できるようにする] [!INCLUDE[ssIS](../../includes/ssis-md.md)] をクリックします。  
  
     このストアド プロシージャは、SSISDB カタログに対する操作の状態のメンテナンスを実行します。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] サーバー インスタンスがダウンした場合に、実行されていたパッケージの状態を修正します。  
  
6.  パスワードを入力し、 **[OK]** をクリックします。  
  
     カタログ データを暗号化するために使用されるデータベース マスター キーがパスワードで保護されます。 パスワードは安全な場所に保管してください。 データベース マスター キーをバックアップすることもお勧めします。 詳細については、「 [データベース マスター キーのバックアップ](../../relational-databases/security/encryption/back-up-a-database-master-key.md)」を参照してください。  
  
### <a name="to-create-the-ssisdb-catalog-programmatically"></a>SSISDB カタログをプログラムから作成するには  
  
1.  次の PowerShell スクリプトを実行します。  
  
    ```  
    # Load the IntegrationServices Assembly  
    [Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices")  
  
    # Store the IntegrationServices Assembly namespace to avoid typing it every time  
    $ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"  
  
    Write-Host "Connecting to server ..."  
  
    # Create a connection to the server  
    $sqlConnectionString = "Data Source=localhost;Initial Catalog=master;Integrated Security=SSPI;"  
    $sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString  
  
    # Create the Integration Services object  
    $integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection  
  
    # Provision a new SSIS Catalog  
    $catalog = New-Object $ISNamespace".Catalog" ($integrationServices, "SSISDB", "P@assword1")  
    $catalog.Create()  
  
    ```  
  
     Windows PowerShell と <xref:Microsoft.SqlServer.Management.IntegrationServices> 名前空間の使用方法を紹介したその他の例については、blogs.msdn.com のブログ エントリ「[SQL Server 2012 での SSIS と PowerShell](https://go.microsoft.com/fwlink/?LinkId=242539)」を参照してください。 名前空間とコード例の概要については、blogs.msdn.com のブログ エントリ「 [SSIS カタログ マネージド オブジェクト モデルの概要](https://go.microsoft.com/fwlink/?LinkId=254267)」を参照してください。  

## <a name="catalog-properties-dialog-box"></a>[カタログのプロパティ] ダイアログ ボックス
  [カタログのプロパティ] ダイアログ ボックスを使用すると、SSISDB カタログを構成できます。 カタログ プロパティは、機微なデータを暗号化する方法、操作およびプロジェクトのバージョン管理データを保持する方法、および検証操作がタイムアウトするタイミングを定義します。SSISDB カタログは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクト、パッケージ、パラメーター、および環境のための中央のストレージと管理ポイントです。  
  
 また、カタログ プロパティを `catalog.catalog_properties` ビューで表示し、`catalog.configure_catalog` ストアド プロシージャを使用することで、これらのプロパティを設定することもできます。 詳細については、「[catalog.catalog_properties (SSISDB データベース)](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)」および「[catalog.configure_catalog (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)」を参照してください。  
  
 **目的に合ったトピックをクリックしてください**  
  
-   [[カタログのプロパティ] ダイアログ ボックスを開く](#open_dialog)  
  
-   [オプションの構成](#options)  
  
###  <a name="open_dialog"></a> [カタログのプロパティ] ダイアログ ボックスを開く  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]を開きます。  
  
2.  Microsoft SQL Server データベース エンジンに接続します。  
  
3.  オブジェクト エクスプローラーで、 **[Integration Services]** ノードを展開します。 **[SSISDB]** を右クリックし、 **[プロパティ]** をクリックします。  
  
###  <a name="options"></a> オプションの構成  
  
#### <a name="options"></a>オプション  
 次の表では、ダイアログ ボックスに示される特定のプロパティと、`catalog.catalog_properties` ビュー内の対応するプロパティについて説明します。  
  
|プロパティ名 ([カタログのプロパティ] ダイアログ ボックス)|プロパティ名 (catalog.catalog_properties ビュー)|[説明]|  
|-----------------------------------------------------|------------------------------------------------------|-----------------|  
|暗号化アルゴリズムの名前|ENCRYPTION_ALGORITHM|カタログ内の機密性の高いパラメーター値を暗号化するために使用される暗号化の種類を指定します。 使用できる値を次に示します。<br /><br /> DES<br /><br /> TRIPLE_DES<br /><br /> TRIPLE_DES_3KEY<br /><br /> DESPX<br /><br /> AES_128<br /><br /> AES_192<br /><br /> AES_256 (既定値)|  
|プロジェクトごとのバージョンの最大数|MAX_PROJECT_VERSIONS|カタログに格納されるプロジェクトのバージョンの数を指定します。 最大数を超えるプロジェクトの古いバージョンは、プロジェクト バージョンのクリーンアップ ジョブを実行したときに削除されます。|  
|ログを定期的に消去する|OPERATION_CLEANUP_ENABLED|操作のクリーンアップ SQL Server エージェント ジョブを実行することを示すには、このプロパティを True に設定します。 それ以外の場合は、このプロパティを False に設定します。|  
|保有期間 (日)|RETENTION_WINDOW|操作データの最大保有期間を日数で指定します。 指定された日数を経過したデータは、操作のクリーンアップ SQL エージェント ジョブによって削除されます。|  

## <a name="back-up-restore-and-move-the-ssis-catalog"></a>SSIS カタログのバックアップ、復元、および移動
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] には SSISDB データベースが用意されています。 **SSISDB** カタログに格納されているオブジェクト、設定、および業務データを検査するには、SSISDB データベースのビューに対してクエリを実行します。 このトピックでは、データベースのバックアップと復元の手順について説明します。  
  
 **SSISDB** カタログは、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置したパッケージを格納します。 カタログの詳細については、「 [SSIS カタログ](../../integration-services/catalog/ssis-catalog.md)」を参照してください。  
  
###  <a name="backup"></a> SSIS データベースをバックアップするには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開き、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続します。  
  
2.  BACKUP MASTER KEY Transact-SQL ステートメントを使用して、SSISDB データベースのマスター キーをバックアップします。 このキーは指定したファイルに格納されます。 ファイル内のマスター キーを暗号化するには、パスワードを使用します。  
  
     ステートメントの詳細については、「[BACKUP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-master-key-transact-sql.md)」を参照してください。  
  
     次の例では、マスター キーが `c:\temp directory\RCTestInstKey` ファイルにエクスポートされます。 マスター キーの暗号化には、 `LS2Setup!` というパスワードが使用されます。  
  
    ```  
    backup master key to file = 'c:\temp\RCTestInstKey'  
           encryption by password = 'LS2Setup!'  
  
    ```  
  
3.  **の** [データベースのバックアップ] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ダイアログ ボックスを使用して SSISDB データベースをバックアップします。 詳細については、[データベースをバックアップする方法 (SQL Server Management Studio)](https://go.microsoft.com/fwlink/?LinkId=231812) に関する記事をご覧ください。  
  
4.  次の手順を実行して、##MS_SSISServerCleanupJobLogin## の CREATE LOGIN スクリプトを生成します。 詳細については、「[CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)」を参照してください。  
  
    1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のオブジェクト エクスプローラーで、 **[セキュリティ]** ノードを展開し、 **[ログイン]** ノードを展開します。  
  
    2.  **[##MS_SSISServerCleanupJobLogin##]** を右クリックし、 **[ログインをスクリプト化]**  >  **[CREATE]**  >  **[新しいクエリ エディター ウィンドウ]** の順にクリックします。  
  
5.  SSISDB カタログが作成されていない [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに SSISDB データベースを復元する場合は、次の操作を行って、sp_ssis_startup の CREATE PROCEDURE スクリプトを生成します。 詳細については、「[CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)」を参照してください。  
  
    1.  オブジェクト エクスプローラーで、 **[データベース]** ノードを展開し、 **[master]**  >  **[プログラミング]**  >  **[ストアド プロシージャ]** ノードの順に展開します。  
  
    2.  **[dbo.sp_ssis_startup]** を右クリックし、 **[ストアド プロシージャをスクリプト化]**  >  **[CREATE]**  >  **[新しいクエリ エディター ウィンドウ]** の順にクリックします。  
  
6.  SQL Server エージェントが起動したことを確認します。  
  
7.  SSISDB カタログが作成されていない [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに SSISDB データベースを復元する場合は、次の操作を行って、SSIS サーバー メンテナンス ジョブのスクリプトを生成します。 SSISDB カタログが作成されると、スクリプトは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで自動的に作成されます。 このジョブは、保有期間外の操作ログのクリーンアップおよび古いバージョンのプロジェクトの削除に役立ちます。  
  
    1.  オブジェクト エクスプローラーで、 **[SQL Server エージェント]** ノードを展開し、 **[ジョブ]** ノードを展開します。  
  
    2.  SSIS サーバー メンテナンス ジョブを右クリックし、 **[ジョブをスクリプト化]**  >  **[CREATE]**  >  **[新しいクエリ エディター ウィンドウ]** の順にクリックします。  
  
### <a name="to-restore-the-ssis-database"></a>SSIS データベースを復元するには  
  
1.  SSISDB カタログが作成されていない [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに SSISDB データベースを復元する場合は、`sp_configure` ストアド プロシージャを実行して、共通言語ランタイム (CLR) を有効にします。 詳細については、「[sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)」と「[clr enabled サーバー構成オプション](https://go.microsoft.com/fwlink/?LinkId=231855)」を参照してください。  
  
    ```  
    use master   
           sp_configure 'clr enabled', 1  
           reconfigure  
  
    ```  
  
2.  SSISDB カタログが作成されていない [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに SSISDB データベースを復元する場合は、非対称キーと非対称キーからのログインを作成し、UNSAFE 権限をログインに付与します。  
  
    ```  
    Create Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey  
           FROM Executable File = 'C:\Program Files\Microsoft SQL Server\110\DTS\Binn\Microsoft.SqlServer.IntegrationServices.Server.dll'  
  
    ```  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ログインを行うには Microsoft Win32 API などの制限付きのリソースへの追加アクセスが必要であるため、CLR ストアド プロシージャでは、UNSAFE 権限をログインに付与する必要があります。 UNSAFE コード権限の要件の詳細については、「 [アセンブリの作成](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)」を参照してください。  
  
    ```  
    Create Login MS_SQLEnableSystemAssemblyLoadingUser  
           FROM Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey   
  
           Grant unsafe Assembly to MS_SQLEnableSystemAssemblyLoadingUser  
  
    ```  
  
3.  **の** [データベースの復元] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ダイアログ ボックスを使用して、バックアップから SSISDB データベースを復元します。 詳細については、次の各トピックを参照してください。  
  
    -   [[データベースの復元] &#40;[全般] ページ&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)  
  
    -   [[データベースの復元] &#40;[ファイル] ページ&#41;](../../relational-databases/backup-restore/restore-database-files-page.md)  
  
    -   [[データベースの復元] &#40;[オプション] ページ&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)  
  
4.  ##MS_SSISServerCleanupJobLogin##、sp_ssis_startup、および SSIS サーバー メンテナンス ジョブの「 [SSIS をバックアップするには](#backup) 」で作成したスクリプトを実行します。 SQL Server エージェントが起動したことを確認します。  
  
5.  次のステートメントを実行して、sp_ssis_startup プロシージャの自動実行を設定します。 詳細については、「[sp_procoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md)」を参照してください。  
  
    ```  
    EXEC sp_procoption N'sp_ssis_startup','startup','on'  
    ```  
  
6.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の **[ログインのプロパティ]** ダイアログ ボックスを使用して、SSISDB ユーザーの ##MS_SSISServerCleanupJobUser## (SSISDB database) を ##MS_SSISServerCleanupJobLogin## にマップします。  
  
7.  次のいずれかの方法を使用して、マスター キーを復元します。 暗号化の詳細については、「 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)」を参照してください。  
  
    -   **方法 1**  
  
         この方法は、データベース マスター キーのバックアップが実行済みで、マスター キーの暗号化に使用するパスワードがある場合に使用します。  
  
        ```  
               Restore master key from file = 'c:\temp\RCTestInstKey'  
               Decryption by password = 'LS2Setup!' -- 'Password used to encrypt the master key during SSISDB backup'  
               Encryption by password = 'LS3Setup!' -- 'New Password'  
               Force  
  
        ```  
  
        > [!NOTE]  
        >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントにバックアップ キー ファイルの読み取り権限があることを確認してください。  
  
        > [!NOTE]  
        >  データベース マスター キーがサービス マスター キーによって暗号化されていない場合、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] には次の警告メッセージが表示されます。 この警告メッセージは無視してください。  
        >   
        >  **現在のマスター キーは暗号化解除できません。FORCE オプションが指定されたので、エラーは無視されました。**  
        >   
        >  FORCE 引数は、現在のデータベース マスター キーが開いていない場合でも復元プロセスを続行するように指定します。 SSISDB カタログについては、データベースを復元するインスタンスでデータベース マスター キーが開いていないため、このメッセージが表示されます。  
  
    -   **方法 2**  
  
         この方法は、SSISDB の作成に使用した元のパスワードがある場合に使用します。  
  
        ```  
        open master key decryption by password = 'LS1Setup!' --'Password used when creating SSISDB'  
               Alter Master Key Add encryption by Service Master Key  
        ```  
  
8.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] catalog.check_schema_version [を実行して、SSISDB カタログ スキーマと](../../integration-services/system-stored-procedures/catalog-check-schema-version.md)バイナリ (ISServerExec および SQLCLR アセンブリ) に互換性があるかどうかを確認します。  
  
9. SSISDB データベースが正常に復元されたことを確認するには、SSISDB カタログに対して、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置したパッケージの実行などの操作を実行します。 詳細については、「[Integration Services (SSIS) パッケージの実行](../../integration-services/packages/run-integration-services-ssis-packages.md)」を参照してください。  
  
### <a name="to-move-the-ssis-database"></a>SSIS データベースを移動するには  
  
-   ユーザー データベースの移動の手順に従います。 詳細については、「 [ユーザー データベースの移動](../../relational-databases/databases/move-user-databases.md)」を参照してください。  
  
     SSISDB データベースのマスター キーをバックアップしてバックアップ ファイルを保護していることを確認します。 詳細については、「 [SSIS データベースをバックアップするには](#backup)」を参照してください。  
  
     Integration Services (SSIS) 関連のオブジェクトが、SSISDB カタログが作成されていない新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに作成されていることを確認します。  

## <a name="upgrade-the-ssis-catalog-ssisdb"></a>SSIS カタログ (SSISDB) のアップグレード
  データベースが SQL Server インスタンスの現在のバージョンよりも古い場合、SSISDB アップグレード ウィザードを実行して、SSIS カタログ データベース (SSISDB) をアップグレードしてください。 データベースは、次のいずれかの条件が該当した場合は古いものである可能性があります。  
  
-   古いバージョンの SQL Server からデータベースを復元した場合。  
  
-   SQL Server インスタンスをアップグレードする前に Always On 可用性グループからデータベースを削除しなかった場合。 このような状況では、データベースは自動アップグレードされません。 詳細については、「 [Upgrading SSISDB in an availability group](#Upgrade)」を参照してください。  
  
 このウィザードでは、ローカル サーバー インスタンス上のデータベースのみをアップグレードできます。  
  
### <a name="upgrade-the-ssis-catalog-ssisdb-by-running-the-ssisdb-upgrade-wizard"></a>SSISDB アップグレード ウィザードを実行して SSIS カタログ (SSISDB) をアップグレードする  
  
1.  SSIS カタログ データベース (SSISDB) をバックアップします。  
  
2.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でローカル サーバーを展開し、 **[Integration Services カタログ]** を展開します。  
  
3.  **[SSISDB]** を右クリックして **[データベースのアップグレード]** を選択し、SSISDB アップグレード ウィザードを起動します。 または、ローカル サーバーで管理者特権のアクセス許可を使用して `C:\Program Files\Microsoft SQL Server\140\DTS\Binn\ISDBUpgradeWizard.exe` を実行することにより、SSISDB アップグレード ウィザードを起動します。
  
     ![SSISDB アップグレード ウィザードを起動する](../../integration-services/service/media/ssisdb-upgrade-wizard-1.png)

4.  **[インスタンスの選択]** ページで、ローカル サーバー上の SQL Server インスタンスを選択します。  
  
    > [!IMPORTANT]  
    >  このウィザードでは、ローカル サーバー インスタンス上のデータベースのみをアップグレードできます。  
  
     ウィザードを実行する前に SSISDB データベースをバックアップしたことを示すために、チェック ボックスをオンにします。  
  
     ![SSISDB アップグレード ウィザードでサーバーを選択](../../integration-services/service/media/ssisdb-upgrade-wizard-2.png "SSISDB アップグレード ウィザードでサーバーを選択")  
  
5.  **[アップグレード]** を選択して SSIS カタログ データベースをアップグレードします。  
  
6.  **[結果]** ページで結果を確認します。  
  
     ![SSISDB アップグレード ウィザードで結果を確認](../../integration-services/service/media/ssisdb-upgrade-wizard-3.png "SSISDB アップグレード ウィザードで結果を確認")  

## <a name="always-on-for-ssis-catalog-ssisdb"></a>Always On for SSIS Catalog (SSISDB)
  Always On 可用性グループ機能は、データベース ミラーリングに代わる、高可用性と災害復旧のためのエンタープライズ レベルのソリューションです。 可用性グループは、可用性データベースというひとまとまりでフェールオーバーされる個別のユーザー データベースのセットのためのフェールオーバー環境をサポートします。 詳細については、「 [AlwaysOn 可用性グループ (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)」を参照してください。  
  
 SSIS カタログ (SSISDB) とそのコンテンツ (プロジェクト、パッケージ、実行ログなど) の高可用性を実現するには、(他のユーザー データベースと同様に) SSISDB データベースを Always On 可用性グループに追加できます。 フェールオーバーが発生すると、セカンダリ ノードのいずれかが自動的に新しいプライマリ ノードになります。  
 
 > [!IMPORTANT]
 > フェールオーバーが発生した場合、実行中のパッケージの再起動や再開は行われません。 
 
 **このセクションの内容:**  
  
1.  [前提条件](#prereq)  
  
2.  [Always On の SSIS サポートを構成する](#Firsttime)  
  
3.  [可用性グループの SSISDB をアップグレードする](#Upgrade)  
  
###  <a name="prereq"></a> 前提条件  
次の前提条件手順を実行してから、SSISDB データベースの Always On サポートを有効にする必要があります。  
  
1.  Windows フェールオーバー クラスターを設定します。 手順については、「 [Installing the Failover Cluster Feature and Tools for Windows Server 2012 (Windows Server 2012 のフェールオーバー クラスター機能とツールのインストール)](https://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) 」のブログ投稿を参照してください。 すべてのクラスター ノードに機能とツールをインストールします。  
  
2.  クラスターの各ノードに SQL Server 2016 with Integration Services (SSIS) 機能をインストールします。  
  
3.  SQL Server インスタンスごとに Always On 可用性グループを有効にします。 詳細については、「 [Always On 可用性グループの有効化と無効化 (SQL Server)](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md) 」を参照してください。  
  
###  <a name="Firsttime"></a> Always On の SSIS サポートを構成する  
  
-   [ステップ 1:Integration Services カタログを作成する](#Step1)  
  
-   [ステップ 2:SSISDB を Always On 可用性グループに追加する](#Step2)  
  
-   [ステップ 3:Always On の SSIS サポートを有効にする](#Step3)  
  
> [!IMPORTANT]  
> -   可用性グループの **プライマリ ノード** で、次の手順を実行する必要があります。
> -   SSISDB を Always On 可用性グループに追加した "*後に*"、**Always On の SSIS サポート**を有効にする必要があります。  

> [!NOTE]
> この手順の詳細については、データ プラットフォームの MVP である Marcos Freccia 氏による、スクリーン ショットが追加された次のチュートリアルをご覧ください:「[Adding SSISDB to AG for SQL Server 2016 (AG for SQL Server 2016 に SSISDB を追加する)](https://marcosfreccia.com/2017/04/28/adding-ssisdb-to-ag-for-sql-server-2016/)」。

####  <a name="Step1"></a> ステップ 1:Integration Services カタログを作成する  
  
1.  **SQL Server Management Studio** を起動し、SSISDB の Always On 高可用性グループの **プライマリ ノード** として設定するクラスターの SQL Server インスタンスに接続します。  
  
2.  オブジェクト エクスプローラーで、サーバー ノードを展開します。次に、 **[Integration Services カタログ]** ノードを右クリックし、 **[カタログの作成]** をクリックします。  
  
3.  **[CLR 統合を有効にする]** をクリックします。 カタログは CLR ストアド プロシージャを使用します。  
  
4.  SSIS サーバー インスタンスを再起動するたびに **catalog.startup** ストアド プロシージャが実行されるようにするには、 [[SQL Server のスタートアップ時に Integration Services ストアド プロシージャを自動実行できるようにする]](../system-stored-procedures/catalog-startup.md) をクリックします。 このストアド プロシージャは、SSISDB カタログに対する操作の状態のメンテナンスを実行します。 SSIS サーバー インスタンスがダウンした場合に、実行されていたパッケージの状態を修正します。  
  
5.  **パスワード**を入力し、 **[OK]** をクリックします。 カタログ データを暗号化するために使用されるデータベース マスター キーがパスワードで保護されます。 パスワードは安全な場所に保管してください。 データベース マスター キーをバックアップすることもお勧めします。 詳細については、「 [データベース マスター キーのバックアップ](../../relational-databases/security/encryption/back-up-a-database-master-key.md)」を参照してください。  
  
####  <a name="Step2"></a> ステップ 2:SSISDB を Always On 可用性グループに追加する  
SSISDB データベースを Always On 可用性グループに追加する手順は、他のユーザー データベースを可用性グループに追加する場合とほぼ同じです。 「 [可用性グループ ウィザードの使用](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)」を参照してください。  
  
**新しい可用性グループ** ウィザードの **[データベースの選択]** ページで SSIS カタログを作成するときに指定したパスワードを入力します。

![[データベースの選択]](../../integration-services/service/media/ssis-newavailabilitygroup.png "[データベースの選択]")  
  
####  <a name="Step3"></a> ステップ 3:Always On の SSIS サポートを有効にする  
 Integration Service カタログを作成した後に、 **[Integration Service カタログ]** ノードを右クリックし、 **[Always On サポートを有効にする]** をクリックします。 次の **[AlwaysOn のサポートを有効にする]** ダイアログ ボックスが表示されます。 このメニュー項目が無効な場合、すべての前提条件がインストールされていることを確認してから、 **[更新]** をクリックします。  
  
 ![Always On のサポートを有効にする](../../integration-services/service/media/ssis-enablesupportforalwayson.png)  
  
> [!WARNING]  
>  SSISDB データベースの自動フェールオーバーをサポートするには、Always On のSSIS のサポートを有効にする必要があります。  
  
 Always On 可用性グループから新しく追加したセカンダリ レプリカが一覧に表示されます。 一覧の各レプリカの **[接続]** をクリックし、認証資格情報を入力してレプリカに接続します。 Always On の SSIS サポートを有効にするには、ユーザー アカウントは、各レプリカの sysadmin グループのメンバーである必要があります。 各レプリカに正常に接続できたら、 **[OK]** をクリックして、Always On の SSIS のサポートを有効にします。  
 
他の前提条件を満足した後で、コンテキスト メニューの **[Enable Always On support]** \(Always On サポートの有効化\) が無効にオプションとして表示される場合は、次の操作を試してみてください。
1.  **[更新]** オプションをクリックして、コンテキスト メニューを更新します。
2.  プライマリ ノードに接続されていることを確認します。 プライマリ ノードでは Always On サポートを有効にする必要があります。
3.  SQL Server のバージョンが 13.0 以上であることを確認します。 SSIS は、SQL Server 2016 以降のバージョンでのみ Always On をサポートします。

###  <a name="Upgrade"></a> 可用性グループの SSISDB をアップグレードする  
 以前のバージョンから SQL Server をアップグレードするとき、SSISDB が Always On 可用性グループに含まれる場合、"Always On 可用性グループの SSISDB の確認" ルールでアップグレードがブロックされることがあります。 このブロックが発生するのは、可用性データベースがマルチユーザー データベースである必要があるにもかかわらず、アップグレードがシングル ユーザー モードで実行されたためです。 そのため、アップグレードまたは修正プログラムの適用中には、SSISDB を含むすべての可用性データベースがオフラインになり、アップグレードまたは修正プログラムの適用が行われません。 アップグレードを続行するには、まず可用性グループから SSISDB を削除し、次に各ノードのアップグレードまたは修正プログラムの適用を行い、さらに SSISDB を可用性グループに追加します。  
  
 "Always On 可用性グループ内の SSISDB の確認" ルールでブロックされる場合、次の手順に従って SQL Server をアップグレードします。  
  
1.  可用性グループから SSISDB を削除します。 詳細については、「[可用性グループからのセカンダリ データベースの削除 (SQL Server)](../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)」および「[可用性グループからのプライマリ データベースの削除 (SQL Server)](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)」を参照してください。  
  
2.  アップグレード ウィザードで **[再実行]** をクリックします。 "Always On 可用性グループ内の SSISDB の確認" ルールに合格します。  
  
3.  **[次へ]** をクリックしてアップグレードを続行します。  
  
4.  すべてのノードをアップグレードしたら、SSISDB データベースを Always On 可用性グループに追加します。 詳細については、「[可用性グループへのデータベースの追加 (SQL Server)](../../database-engine/availability-groups/windows/availability-group-add-a-database.md)」を参照してください。  
  
 SQL Server のアップグレード時にブロックされず、SSISDB が Always On 可用性グループに属している場合、SQL Server データベース エンジンをアップグレードした後に、別に SSISDB をアップグレードします。 次の手順で、SSIS アップグレード ウィザードを使用して SSISDB をアップグレードします。  
  
1.  可用性グループから SSISDB データベースを削除するか、SSISDB が可用性グループで唯一のデータベースの場合は可用性グループを削除します。 このタスクを実行するには、可用性グループの **プライマリ ノード**で **SQL Server Management Studio** を起動します。  
  
2.  すべての **レプリカ ノード**から SSISDB データベースを削除します。  
  
3.  **プライマリ ノード**の SSISDB データベースをアップグレードします。 SQL Server Management Studio の**オブジェクト エクスプローラー** で、 **[Integration Service カタログ]** を展開し、 **[SSISDB]** を右クリックし、 **[データベース アップグレード]** を選択します。 **SSISDB アップグレード ウィザード** の指示に従ってデータベースをアップグレードします。 **SSIDB アップグレード ウィザード** は、**プライマリ ノード**のローカルで起動します。  
  
4.  「[ステップ 2:SSISDB を Always On 可用性グループに追加する](#Step2)」の手順に従って、SSISDB を可用性グループに追加します。  
  
5.  「[ステップ 3:Always On の SSIS サポートを有効にする](#Step3)」の手順に従います。  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   blogs.msdn.com のブログ「 [SQL Server 2012 での SSIS と PowerShell](https://go.microsoft.com/fwlink/?LinkId=242539)」  
  
-   blogs.msdn.com のブログ エントリ「 [SSIS カタログのアクセス制御のヒント](https://go.microsoft.com/fwlink/?LinkId=246669)」  
  
-   blogs.msdn.com のブログ エントリ「 [SSIS カタログ マネージド オブジェクト モデルの概要](https://go.microsoft.com/fwlink/?LinkId=254267)」  
