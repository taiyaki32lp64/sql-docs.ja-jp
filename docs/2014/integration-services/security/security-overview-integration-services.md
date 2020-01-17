---
title: セキュリティの概要 (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b2e86fff86e24668e7fe6382545e024bed1a4025
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62927091"
---
# <a name="security-overview-integration-services"></a>セキュリティの概要 (Integration Services)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、豊富かつ柔軟なセキュリティ環境を提供できるように、複数の階層でセキュリティが構成されています。 このようなセキュリティの階層では、デジタル署名、パッケージのプロパティ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ロール、およびオペレーティング システム権限が使用されます。 こうしたセキュリティ機能のほとんどは、ID およびアクセス制御のカテゴリに分類されます。  
  
## <a name="identity-features"></a>ID に関する機能  
 アクセス制御に関する機能をパッケージに実装することにより、次の目的を達成できます。  
  
 **信頼できるソースのパッケージのみを開いて実行します**。  
  
 信頼できるソースのパッケージのみを開いて実行するには、まずパッケージのソースを特定する必要があります。 ソースは、証明書を使用してパッケージに署名することによって特定できます。 その後、パッケージを開いたり実行したりする際には、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で、デジタル署名が存在するかどうか、および有効かどうかを確認することができます。 詳細については、「 [デジタル署名を使用してパッケージのソースを特定する](identify-the-source-of-packages-with-digital-signatures.md)」を参照してください。  
  
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
  
 詳しくは、「 [Access Control for Sensitive Data in Packages](access-control-for-sensitive-data-in-packages.md)」をご覧ください。  
  
### <a name="controlling-access-to-packages"></a>パッケージへのアクセスの制御  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス内の msdb データベースに保存するか、.dtsx というファイル名拡張子の付いた XML ファイルとしてファイル システムに保存することができます。 詳細については、「 [パッケージを保存する](../save-packages.md)」を参照してください。  
  
#### <a name="saving-packages-to-the-msdb-database"></a>msdb データベースへのパッケージの保存  
 パッケージを msdb データベースに保存すると、サーバー レベル、データベース レベル、およびテーブル レベルのセキュリティを実現できます。 msdb データベースでは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは sysssispackages テーブルに格納されます。 パッケージは、msdb データベースの sysssispackages テーブルと sysdtspackages テーブルに保存されるため、msdb データベースのバックアップ時に自動的にバックアップされます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb データベースに格納されるパッケージは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデータベース レベルのロールを適用して保護することもできます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、パッケージへのアクセスを制御するための、db_ssisadmin、db_ssisltduser、および db_ssisoperator というデータベース レベルの 3 つの固定ロールがあります。 各パッケージにはリーダー ロールおよびライター ロールを関連付けることができます。 また、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージで使用する、データベース レベルのカスタム ロールを定義することもできます。 ロールは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内の msdb データベースに保存されるパッケージにのみ実装できます。 詳細については、「[Integration Services のロール &#40;SSIS サービス&#41;](integration-services-roles-ssis-service.md)」を参照してください。  
  
#### <a name="saving-packages-to-the-file-system"></a>ファイル システムへのパッケージの保存  
 パッケージを msdb データベースではなくファイル システムに格納する場合は、パッケージ ファイル、およびパッケージ ファイルが格納されるフォルダーをセキュリティで保護してください。  
  
### <a name="controlling-access-to-files-used-by-packages"></a>パッケージで使用するファイルへのアクセスの制御  
 構成、チェックポイント、およびログ記録を使用するように構成されているパッケージでは、パッケージの外部に格納される情報が生成されます。 この情報は重要な場合があるため、保護する必要があります。 チェックポイント ファイルはファイル システムにしか保存できませんが、構成とログはファイル システム、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのテーブルに保存できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に保存される構成とログは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセキュリティの対象ですが、ファイル システムに書き込まれる情報のセキュリティには別の方法が必要です。  
  
 詳細については、「 [パッケージで使用されるファイルへのアクセス](../access-to-files-used-by-packages.md)」を参照してください。  
  
#### <a name="storing-package-configurations-securely"></a>パッケージの構成の安全な格納  
 パッケージの構成は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのテーブル、またはファイル システムに保存できます。  
  
 構成は、msdb データベースだけでなく、すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに保存できます。 このため、パッケージ構成のリポジトリとして機能するデータベースを指定できます。 また、構成を格納するテーブルの名前を指定すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は正しい構造のテーブルを自動的に作成します。 構成をテーブルに保存すると、サーバー レベル、データベース レベル、およびテーブル レベルのセキュリティを実現できます。 さらに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に保存した構成は、データベースのバックアップ時に自動的にバックアップされます。  
  
 構成を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ではなくファイル システムに格納する場合は、パッケージ構成ファイルが格納されるフォルダーをセキュリティで保護してください。  
  
 構成の詳細については、「 [パッケージ構成](../package-configurations.md)」を参照してください。  
  
### <a name="controlling-access-to-the-integration-services-service"></a>Integration Services サービスへのアクセスの制御  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、格納されているパッケージの一覧を表示する際に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが使用されます。 権限のないユーザーが、ローカル コンピューターまたはリモート コンピューターに格納されているパッケージに関する情報を参照してプライベート情報を取得できないようにするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを実行するコンピューターへのアクセスを制限します。  
  
 詳細については、「 [Integration Services サービスへのアクセスの制御](../access-to-the-integration-services-service.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 セキュリティに関連する特定のタスクを実行する方法を示すトピックへのリンクを次に示します。  
  
-   [ユーザー定義ロールを作成する](../create-a-user-defined-role.md)  
  
-   [リーダー ロールおよびライター ロールをパッケージに割り当てる](../assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [レジストリ値を設定して署名ポリシーを実装する](../implement-a-signing-policy-by-setting-a-registry-value.md)  
  
-   [デジタル証明書を使用してパッケージに署名する](../sign-a-package-by-using-a-digital-certificate.md)  
  
-   [パッケージの保護レベルを設定または変更する](../set-or-change-the-protection-level-of-packages.md)  
  
## <a name="see-also"></a>参照  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
