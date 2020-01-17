---
title: セキュリティの概要 (Integration Services) | Microsoft Docs
ms.custom: security
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- Integration Services, security
- security [Integration Services], about security
- passwords [Integration Services]
- packages [Integration Services], security
- SQL Server Integration Services, security
- SSIS, security
- Integration Services packages, security
- SQL Server Integration Services packages, security
ms.assetid: 01aa0b88-d477-4581-9a3b-2efc3de2b133
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0bc268c2baea6e0e661fac123df9fe19ec60252c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71281949"
---
# <a name="security-overview-integration-services"></a>セキュリティの概要 (Integration Services)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、豊富かつ柔軟なセキュリティ環境を提供できるように、複数の階層でセキュリティが構成されています。 このようなセキュリティの階層では、デジタル署名、パッケージのプロパティ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ロール、およびオペレーティング システム権限が使用されます。 こうしたセキュリティ機能のほとんどは、ID およびアクセス制御のカテゴリに分類されます。  

## <a name="threat-and-vulnerability-mitigation"></a>脅威と脆弱性の対策
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] はさまざまなセキュリティ メカニズムを備えていますが、パッケージおよびそのパッケージで作成または使用されるファイルが悪用される可能性はあります。  
  
 次の表では、リスクの種類と、各リスクを軽減するために必要な予防的措置について説明します。  
  
|脅威または脆弱性|定義|対策|  
|-----------------------------|----------------|----------------|  
|[パッケージ ソース]|パッケージのソースは、パッケージを作成した個人または組織です。 不明なソースや信頼されていないソースのパッケージを実行することは危険な場合があります。|デジタル署名を使用してパッケージのソースを特定し、既知の信頼されているソースのパッケージだけを実行します。 詳細については、「 [デジタル署名を使用してパッケージのソースを特定する](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md)」を参照してください。|  
|パッケージの内容|パッケージの内容には、パッケージの要素とそのプロパティが含まれます。 プロパティには、パスワードなどの機密データや接続文字列を含めることができます。 SQL ステートメントなどのパッケージ要素によって、データベースの構造が明らかにされる場合があります。|次の手順を実行して、パッケージとその内容へのアクセスを制御します。<br /><br /> 1) パッケージ自体へのアクセスを制御するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの **msdb** データベースに保存されているパッケージに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のセキュリティ機能を適用します。 ファイル システムに保存されているパッケージには、アクセス制御リスト (ACL) など、ファイル システムのセキュリティ機能を適用します。<br /><br /> 2) パッケージの内容へのアクセスを制御するには、パッケージの保護レベルを設定します。<br /><br /> 詳細については、「[セキュリティの概要 (Integration Services)](../../integration-services/security/security-overview-integration-services.md)」と「[パッケージ内の機微なデータへのアクセス制御](../../integration-services/security/access-control-for-sensitive-data-in-packages.md)」を参照してください。|  
|パッケージ出力|構成、チェックポイント、およびログ記録を使用するようパッケージを構成すると、パッケージの外部にこの情報が格納されます。 パッケージに格納されない情報に機密データが含まれている場合があります。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース テーブルに保存される構成およびログを保護するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセキュリティ機能を使用します。<br /><br /> ファイルへのアクセスを制御するには、ファイル システムで使用可能なアクセス制御リスト (ACL) を使用します。<br /><br /> 詳細については、「 [パッケージで使用されるファイルへのアクセス](#files)|  
  
## <a name="identity-features"></a>ID に関する機能  
 アクセス制御に関する機能をパッケージに実装することにより、次の目的を達成できます。  
  
 **信頼できるソースのパッケージのみを開いて実行します**。  
  
 信頼できるソースのパッケージのみを開いて実行するには、まずパッケージのソースを特定する必要があります。 ソースは、証明書を使用してパッケージに署名することによって特定できます。 その後、パッケージを開いたり実行したりする際には、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で、デジタル署名が存在するかどうか、および有効かどうかを確認することができます。 詳細については、「 [デジタル署名を使用してパッケージのソースを特定する](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md)」を参照してください。  
  
## <a name="access-control-features"></a>アクセス制御に関する機能  
 アクセス制御に関する機能をパッケージに実装することにより、次の目的を達成できます。  
  
 **認証済みのユーザーのみがパッケージを開いて実行するようにします**。  
  
 認証済みのユーザーのみがパッケージを開いて実行するには、次の情報へのアクセスを制御する必要があります。  
  
-   パッケージの内容、特に機微なデータ  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に格納されているパッケージおよびパッケージの構成  
  
-   ファイル システムに格納されているパッケージおよび関連ファイル (構成ファイル、ログ、チェックポイント ファイルなど)  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービス、およびサービスによって [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]に表示されるパッケージに関する情報。  
  
### <a name="controlling-access-to-the-contents-of-packages"></a>パッケージの内容へのアクセスの制御  
 パッケージの内容へのアクセスを制限するために、パッケージの ProtectionLevel プロパティを設定してパッケージを暗号化できます。 このプロパティは、パッケージで必要な保護レベルに設定できます。 たとえば、チーム開発環境では、パッケージに関する作業を行っているチーム メンバーだけが知っているパスワードを使用して、パッケージを暗号化できます。  
  
 パッケージの ProtectionLevel プロパティを設定すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は機微なプロパティを自動的に検出し、指定されたパッケージ保護レベルに応じてこれらのプロパティを処理します。 たとえば、パッケージの ProtectionLevel プロパティを、機微な情報がパスワードで暗号化されるレベルに設定します。 このパッケージでは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によってすべての機微なプロパティの値が自動的に暗号化されます。正しいパスワードを指定しないと、対応するデータは表示されません。  
  
 通常、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、パスワードや接続文字列などの情報がプロパティに含まれている場合、またはタスクによって生成された XML ノードや変数にプロパティが対応する場合、このようなプロパティは機微なプロパティとして扱われます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] でプロパティが機微と見なされるかどうかは、接続マネージャーやタスクなど、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントの開発者がプロパティを機微として指定したかどうかによって決まります。 機微と見なされているプロパティの一覧では、ユーザーはプロパティを追加することも削除することもできません。カスタム タスク、接続マネージャー、またはデータ フロー コンポーネントを作成する場合は、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で機微なデータとして扱う必要のあるプロパティを指定できます。  
  
 詳しくは、「 [Access Control for Sensitive Data in Packages](../../integration-services/security/access-control-for-sensitive-data-in-packages.md)」をご覧ください。  
  
### <a name="controlling-access-to-packages"></a>パッケージへのアクセスの制御  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス内の msdb データベースに保存するか、.dtsx というファイル名拡張子の付いた XML ファイルとしてファイル システムに保存することができます。 詳細については、「 [パッケージを保存する](../../integration-services/save-packages.md)」を参照してください。  
  
#### <a name="saving-packages-to-the-msdb-database"></a>msdb データベースへのパッケージの保存  
 パッケージを msdb データベースに保存すると、サーバー レベル、データベース レベル、およびテーブル レベルのセキュリティを実現できます。 msdb データベースでは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは sysssispackages テーブルに格納されます。 パッケージは、msdb データベースの sysssispackages テーブルと sysdtspackages テーブルに保存されるため、msdb データベースのバックアップ時に自動的にバックアップされます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb データベースに格納されるパッケージは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデータベース レベルのロールを適用して保護することもできます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、パッケージへのアクセスを制御するための、db_ssisadmin、db_ssisltduser、および db_ssisoperator というデータベース レベルの 3 つの固定ロールがあります。 各パッケージにはリーダー ロールおよびライター ロールを関連付けることができます。 また、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージで使用する、データベース レベルのカスタム ロールを定義することもできます。 ロールは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内の msdb データベースに保存されるパッケージにのみ実装できます。 詳細については、「[Integration Services のロール &#40;SSIS サービス&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)」を参照してください。  
  
#### <a name="saving-packages-to-the-file-system"></a>ファイル システムへのパッケージの保存  
 パッケージを msdb データベースではなくファイル システムに格納する場合は、パッケージ ファイル、およびパッケージ ファイルが格納されるフォルダーをセキュリティで保護してください。  
  
### <a name="controlling-access-to-files-used-by-packages"></a>パッケージで使用するファイルへのアクセスの制御  
 構成、チェックポイント、およびログ記録を使用するように構成されているパッケージでは、パッケージの外部に格納される情報が生成されます。 この情報は重要な場合があるため、保護する必要があります。 チェックポイント ファイルはファイル システムにしか保存できませんが、構成とログはファイル システム、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのテーブルに保存できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に保存される構成とログは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセキュリティの対象ですが、ファイル システムに書き込まれる情報のセキュリティには別の方法が必要です。  
  
 詳細については、「 [パッケージで使用されるファイルへのアクセス](#files)」を参照してください。  
  
#### <a name="storing-package-configurations-securely"></a>パッケージの構成の安全な格納  
 パッケージの構成は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのテーブル、またはファイル システムに保存できます。  
  
 構成は、msdb データベースだけでなく、すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに保存できます。 このため、パッケージ構成のリポジトリとして機能するデータベースを指定できます。 また、構成を格納するテーブルの名前を指定すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は正しい構造のテーブルを自動的に作成します。 構成をテーブルに保存すると、サーバー レベル、データベース レベル、およびテーブル レベルのセキュリティを実現できます。 さらに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に保存した構成は、データベースのバックアップ時に自動的にバックアップされます。  
  
 構成を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ではなくファイル システムに格納する場合は、パッケージ構成ファイルが格納されるフォルダーをセキュリティで保護してください。  
  
 構成の詳細については、「 [パッケージ構成](../../integration-services/packages/package-configurations.md)」を参照してください。  
  
### <a name="controlling-access-to-the-integration-services-service"></a>Integration Services サービスへのアクセスの制御  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、格納されているパッケージの一覧を表示する際に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが使用されます。 権限のないユーザーが、ローカル コンピューターまたはリモート コンピューターに格納されているパッケージに関する情報を参照してプライベート情報を取得できないようにするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを実行するコンピューターへのアクセスを制限します。  
  
 詳細については、「 [Integration Services サービスへのアクセスの制御](#service)」を参照してください。  

## <a name="files"></a> パッケージで使用されるファイルへのアクセス
  パッケージに格納されないファイルは、パッケージ保護レベルでは保護されません。 このようなファイルには、次のファイルが含まれます。  
  
-   [構成ファイル]  
  
-   チェックポイント ファイル  
  
-   ログ ファイル  
  
 特に機密情報が含まれている場合、これらのファイルは個別に保護する必要があります。  
  
### <a name="configuration-files"></a>[構成ファイル]  
 ログイン情報やパスワード情報などの機密情報が構成に含まれている場合は、その構成を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に保存することを検討するか、アクセス制御リスト (ACL) を使用して、ファイルを保存する場所またはフォルダーへのアクセスを制限し、特定のアカウントにのみアクセスを許可する必要があります。 通常は、パッケージの実行を許可するアカウント、およびパッケージの管理とトラブルシューティング (構成の内容、チェックポイント、およびログ ファイルの確認) を行うアカウントにアクセス権を許可します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、サーバー レベルおよびデータベース レベルでの保護により、さらに堅牢なセキュリティが提供されます。 構成を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に保存するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成の種類を使用します。 ファイル システムに保存するには、XML 構成の種類を使用します。  
  
 詳細については、「 [パッケージ構成](../../integration-services/packages/package-configurations.md)」、「 [パッケージ構成を作成する](../../integration-services/packages/create-package-configurations.md)」、および「 [SQL Server インストールにおけるセキュリティの考慮事項](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)」を参照してください。  
  
### <a name="checkpoint-files"></a>チェックポイント ファイル  
 同様に、パッケージで使用するチェックポイント ファイルに機密情報が含まれている場合も、アクセス制御リスト (ACL) を使用して、ファイルが格納されている場所またはフォルダーを保護する必要があります。 チェックポイント ファイルは、パッケージの進行状況に関する現在の状態情報と変数の現在の値を格納します。 たとえば、電話番号を格納するカスタム変数がパッケージに含まれることがあります。 詳細については、「 [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md)」を参照してください。  
  
### <a name="log-files"></a>ログ ファイル  
 ファイル システムに書き込まれるログ エントリも、アクセス制御リスト (ACL) を使用して保護する必要があります。 ログ エントリは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに保存して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティで保護することもできます。 ログ エントリには機密情報が含まれることがあります。たとえば、パッケージに含まれる SQL 実行タスクによって、電話番号を参照する SQL ステートメントが構築される場合、SQL ステートメントのログ エントリにも電話番号が含まれています。 また、SQL ステートメントにより、データベース内のテーブル名や列名に関するプライベートな情報が明らかにされる場合もあります。 詳細については、「[Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」をご覧ください。  

## <a name="service"></a> Integration Services サービスへのアクセスの制御
  パッケージの保護レベルによって、パッケージを編集および実行できるユーザーを制限できます。 サーバーで現在実行中のパッケージの一覧を表示できるユーザー、および [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で現在実行中のパッケージを停止できるユーザーを制限するには、追加の保護が必要です。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、実行中のパッケージを一覧表示する際に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが使用されます。 Windows の Administrators グループのメンバーは、実行中のすべてのパッケージを表示および停止できます。 Administrators グループのメンバーではないユーザーは、本人が起動したパッケージのみを表示および停止できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス (特に、リモート フォルダーの列挙を行う可能性のある [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス) を実行するコンピューターへのアクセスを制限することは重要です。 認証を受けたユーザーであれば、パッケージの列挙を要求できます。 サービスが見つからない場合でも、サービスはフォルダーを列挙します。 これらのフォルダー名が、悪意あるユーザーに悪用される場合があります。 管理者がリモート コンピューターのフォルダーを列挙できるようにサービスを設定した場合、ユーザーも通常は参照できないフォルダー名を参照することができます。  

## <a name="related-tasks"></a>Related Tasks  
 セキュリティに関連する特定のタスクを実行する方法を示すトピックへのリンクを次に示します。  
  
-   [ユーザー定義ロールを作成する](../../integration-services/security/integration-services-roles-ssis-service.md#create)  
  
-   [リーダー ロールおよびライター ロールをパッケージに割り当てる](../../integration-services/security/integration-services-roles-ssis-service.md#assign)  
  
-   [レジストリ値を設定して署名ポリシーを実装する](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md#registry)  
  
-   [デジタル証明書を使用してパッケージに署名する](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md#cert)  
  
-   [パッケージの保護レベルを設定または変更する](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#set_protection)  
