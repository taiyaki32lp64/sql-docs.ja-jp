---
title: Integration Services のロール (SSIS サービス) | Microsoft Docs
ms.custom: security
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.dtsserver.packageroles.f1
helpviewer_keywords:
- security [Integration Services], roles
- db_ssisoperator role
- db_ssisadmin role
- fixed database roles [Integration Services]
- packages [Integration Services], security
- roles [Integration Services]
- db_ssisltduser role
ms.assetid: 9702e90c-fada-4978-a473-1b1423017d80
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3290aa2297ca849ed175b7db109f6b200debc789
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295680"
---
# <a name="integration-services-roles-ssis-service"></a>Integration Services のロール (SSIS サービス)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に格納されたパッケージに安全にアクセスするための固定データベース レベルの特定のロールを提供します。 利用可能なロールは、パッケージを SSIS カタログ データベース (SSISDB) に保存するか、msdb データベースに保存するかどうかによって異なります。  
  
## <a name="roles-in-the-ssis-catalog-database-ssisdb"></a>SSIS カタログ データベース (SSISDB) のロール  
 SSIS カタログ データベース (SSISDB) は、パッケージやパッケージに関する情報に安全にアクセスするための、次の固定データベース レベルのロールを提供します。  
  
-   **ssis_admin**。 このロールは、SSIS カタログ データベースに対する完全な管理アクセスを提供します。  
  
-   **ssis_logreader** 。このロールは、ビュー関連のすべての SSISDB 運用ログにアクセスする権限を提供します。  
  
     ビューの一覧には、[catalog].[projects]、[catalog].[packages]、[catalog].[operations]、[catalog].[extended_operation_info]、[catalog].[operation_messages]、[catalog].[event_messages]、[catalog].[execution_data_statistics]、[catalog].[execution_component_phases]、[catalog].[execution_data_taps]、[catalog].[event_message_context]、[catalog].[executions]、[catalog].[executables]、[catalog].[executable_statistics]、[catalog].[validations]、[catalog].[execution_parameter_values] [catalog].[execution_property_override_values] が含まれます。  
  
## <a name="roles-in-the-msdb-database"></a>msdb データベースのロール  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、 **msdb**に保存されたパッケージへのアクセスを制御するために、 **db_ssisadmin**、 **db_ssisltduser**、 **db_ssisoperator** というデータベース レベルの 3 つの固定ロールがあります。 パッケージにロールを割り当てるには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用します。 ロールの割り当ては、 **msdb** データベースに保存されます。  
  
### <a name="read-and-write-actions"></a>読み取りアクションと書き込みアクション  
 次の表で、Windows の読み取りおよび書き込みアクションと、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]での固定データベース レベル ロールの読み取りおよび書き込みアクションについて説明します。  
  
|ロール|読み取りアクション|書き込みアクション|  
|----------|-----------------|------------------|  
|**msdb**<br /><br /> 内の複数の<br /><br /> **sysadmin**|独自のパッケージを列挙する。<br /><br /> すべてのパッケージを列挙する。<br /><br /> 独自のパッケージを表示する。<br /><br /> すべてのパッケージを表示する。<br /><br /> 独自のパッケージを実行する。<br /><br /> すべてのパッケージを実行する。<br /><br /> 独自のパッケージをエクスポートする。<br /><br /> すべてのパッケージをエクスポートする。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント内のすべてのパッケージを実行する。|パッケージをインポートする。<br /><br /> 独自のパッケージを削除する。<br /><br /> すべてのパッケージを削除する。<br /><br /> 独自のパッケージのロールを変更する。<br /><br /> すべてのパッケージのロールを変更する。<br /><br /> <br /><br /> **\*\* 警告 \*\*** db_ssisadmin ロールおよび dc_admin ロールのメンバーは、特権を sysadmin に昇格できる可能性があります。 このような特権の昇格が発生するのは、それらのロールが [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを変更でき、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] エージェントの sysadmin セキュリティ コンテキストを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パッケージを実行できるためです。 メンテナンス プラン、データ コレクション セット、およびその他の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの実行時にこの特権の昇格を防ぐには、特権が制限されたプロキシ アカウントを使用するようにパッケージを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを構成するか、db_ssisadmin ロールおよび dc_admin ロールには sysadmin メンバーのみを追加するようにします。|  
|**db_ssisadmin**|独自のパッケージを列挙する。<br /><br /> すべてのパッケージを列挙する。<br /><br /> 独自のパッケージを表示する。<br /><br /> 独自のパッケージを実行する。<br /><br /> 独自のパッケージをエクスポートする。|パッケージをインポートする。<br /><br /> 独自のパッケージを削除する。<br /><br /> 独自のパッケージのロールを変更する。|  
|**db_ssisltduser**|すべてのパッケージを列挙する。<br /><br /> すべてのパッケージを表示する。<br /><br /> すべてのパッケージを実行する。<br /><br /> すべてのパッケージをエクスポートする。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント内のすべてのパッケージを実行する。|なし|  
|**Windows 管理者**|実行中のすべてのパッケージの実行時の詳細を表示する。|現在実行中のパッケージをすべて停止する。|  
  
### <a name="sysssispackages-table"></a>sysssispackages テーブル  
 **msdb** の **sysssispackages** テーブルには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に保存されるパッケージが格納されています。 詳細については、「[sysssispackages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysssispackages-transact-sql.md)」を参照してください。  
  
 **sysssispackages** テーブルには、パッケージに割り当てられるロールに関する情報が含まれている列があります。  
  
-   **readerrole** 列は、パッケージへの読み取りアクセスが可能なロールを指定します。  
  
-   **writerrole** 列は、パッケージへの書き込みアクセスが可能なロールを指定します。  
  
-   **ownersid** 列には、パッケージを作成したユーザーの一意なセキュリティ識別子が格納されています。 この列により、パッケージの所有者が定義されます。  
  
### <a name="permissions"></a>アクセス許可  
 既定では、 **db_ssisadmin** および **db_ssisoperator** の各固定データベース レベル ロールの権限、およびパッケージを作成したユーザーの一意なセキュリティ識別子は、パッケージのリーダー ロールに適用されます。 **db_ssisadmin** ロールの権限およびパッケージを作成したユーザーの一意なセキュリティ識別子は、ライター ロールに適用されます。 ユーザーは、パッケージの読み取りアクセスを行うには **db_ssisadmin**、 **db_ssisltduser**、または **db_ssisoperator** ロールのメンバーである必要があります。 書き込みアクセスを行うには **db_ssisadmin** ロールのメンバーである必要があります。  
  
### <a name="access-to-packages"></a>パッケージへのアクセス  
 固定データベース レベル ロールは、ユーザー定義ロールと組み合わせて使用されます。 ユーザー定義ロールとは、ユーザーが [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で作成するロールのことで、権限をパッケージに割り当てるために使用します。 パッケージにアクセスするには、ユーザーは、ユーザー定義ロールおよび関連する [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 固定データベースレベル ロールのメンバーである必要があります。 たとえば、ユーザーがパッケージに割り当てられている **AuditUsers** ユーザー定義ロールのメンバーである場合、パッケージに対する読み取りアクセスを得るには、さらに **db_ssisadmin**、 **db_ssisltduser**、または **db_ssisoperator** ロールのメンバーでもある必要があります。  
  
 ユーザー定義ロールをパッケージに割り当てていない場合、パッケージへのアクセスは固定データベース レベル ロールによって決定されます。  
  
 ユーザー定義ロールを使用するには、パッケージに割り当てる前に、あらかじめ **msdb** データベースに追加しておく必要があります。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]では、新しいデータベース ロールを作成できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データベース レベルのロールは、msdb データベース内の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] システム テーブルに対する権限を付与します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER サービス) は、データベース エンジンに接続して **msdb** データベースにアクセスするためにあらかじめ起動されている必要があります。  
  
 パッケージにロールを割り当てるには、次のタスクを完了する必要があります。  
  
-   **オブジェクト エクスプローラーを開いて Integration Services に接続する**  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用してパッケージにロールを割り当てるには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のオブジェクト エクスプローラーを開き、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]に接続する必要があります。  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを起動してから、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]に接続します。  
  
-   **リーダー ロールおよびライター ロールをパッケージに割り当てる**  
  
     リーダー ロールおよびライター ロールをそれぞれのパッケージに割り当てることができます。  

## <a name="assign"></a> リーダー ロールおよびライター ロールをパッケージに割り当てる
  リーダー ロールおよびライター ロールをそれぞれのパッケージに割り当てることができます。  
  
### <a name="assign-a-reader-and-writer-role-to-a-package"></a>リーダー ロールおよびライター ロールをパッケージに割り当てる  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 接続を見つけます。  
  
2.  [格納されたパッケージ] フォルダーを展開し、ロールを割り当てるパッケージが格納されているサブフォルダーを展開します。  
  
3.  ロールを割り当てるパッケージを右クリックします。  
  
4.  **[パッケージのロール]** ダイアログ ボックスで、 **[リーダー ロール]** ボックスの一覧からリーダー ロールを選択し、 **[ライター ロール]** ボックスの一覧からライター ロールを選択します。  
  
5.  **[OK]** をクリックします。

## <a name="create"></a> ユーザー定義ロールを作成する
    
### <a name="to-create-a-user-defined-role"></a>ユーザー定義ロールを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を開きます。  
  
2.  **[表示]** メニューの **[オブジェクト エクスプローラー]** をクリックします。  
  
3.  オブジェクト エクスプローラー ツール バーで **[接続]** をクリックし、 **[データベース エンジン]** をクリックします。  
  
4.  **[サーバーへの接続]** ダイアログ ボックスで、サーバー名を指定し、認証モードを選択します。 ピリオド (.)、(local)、または **localhost** を使用すると、ローカル サーバーを指定できます。  
  
5.  **[接続]** をクリックします。  
  
6.  [データベース]、[システム データベース]、[msdb]、[セキュリティ]、[ロール] を順に展開します。  
  
7.  [ロール] ノードの [データベース ロール] を右クリックし、 **[新しいデータベース ロール]** をクリックします。  
  
8.  [全般] ページでロール名を指定します。必要に応じて、所有者および所有されているスキーマを指定し、ロール メンバーを追加します。  
  
9. 必要に応じて、 **[権限]** をクリックし、オブジェクトの権限を構成します。  
  
10. 必要に応じて、 **[拡張プロパティ]** をクリックし、任意の拡張プロパティを構成します。  
  
11. **[OK]** をクリックします。

## <a name="roles_dialog"></a> [パッケージのロール] ダイアログ ボックスの UI リファレンス
  **の** [パッケージのロール] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ダイアログ ボックスを使用すると、パッケージに対する読み取りアクセス権のあるデータベースレベル ロールおよびパッケージに対する書き込みアクセス権のあるデータベースレベル ロールを指定できます。 データベースレベル ロールは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb** データベースに格納されたパッケージにのみ適用されます。  
  
 ダイアログ ボックスに一覧表示されたロールは、 **msdb** システム データベースの現在のデータベース ロールです。 ロールが選択されていない場合は、既定の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ロールが適用されます。 リーダー ロールには、既定では、 **db_ssisadmin**および **db_ssisoperator**と、パッケージを作成したユーザーが含まれています。 ユーザーがこれらのロールのいずれかのメンバー、またはパッケージを作成したユーザーである場合は、パッケージの列挙、表示、エクスポート、および実行が可能です。 ライター ロールには、既定では、 **db_ssisadmin** と、パッケージを作成したユーザーが含まれています。 ユーザーがこのロールのメンバー、またはパッケージを作成したユーザーである場合は、パッケージのインポート、削除、変更を行うことができます。  
  
 **sysssispackages** テーブルの **ownersid** 列には、パッケージを作成したユーザーの一意なセキュリティ識別子が表示されます。  
  
### <a name="options"></a>オプション  
 **[パッケージ名]**  
 パッケージの名前を指定します。  
  
 **[リーダー ロール]**  
 ロールを一覧から選択します。  
  
 **[ライター ロール]**  
 ロールを一覧から選択します。  
