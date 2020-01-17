---
title: SQL Server の保護 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- Security [SQL Server]
helpviewer_keywords:
- database objects [SQL Server], security
- SQL Server, security
- operating systems [SQL Server], security
- security [SQL Server], planning
- applications [SQL Server], security
ms.assetid: 4d93489e-e9bb-45b3-8354-21f58209965d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: c1a701f1e63877c807964a8d81a829afdc9f7b81
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891614"
---
# <a name="securing-sql-server"></a>SQL Server の保護
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の保護は、プラットフォーム、認証、オブジェクト (データを含む)、およびシステムにアクセスするアプリケーションの 4 つの領域が関係する一連の手順としてとらえることができます。 以下の各トピックでは、効果的なセキュリティ計画を作成および実装する方法について、順を追って説明します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティの詳細については、 [SQL Server](https://go.microsoft.com/fwlink/?LinkID=31629) Web サイトを参照してください。 このサイトには、推奨事項やセキュリティ チェックリストが掲載されています。 このサイトには、最新のサービス パックの情報およびダウンロードも含まれています。  
  
## <a name="platform-and-network-security"></a>プラットフォームとネットワーク セキュリティ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のプラットフォームは、クライアントをデータベース サーバーに接続する物理的なハードウェアおよびネットワーク システムと、データベース要求の処理に使用するバイナリ ファイルで構成されます。  
  
### <a name="physical-security"></a>物理的なセキュリティ  
 物理的なセキュリティのベスト プラクティスは、物理的なサーバーおよびハードウェア コンポーネントへのアクセスを制限することです。 たとえば、鍵のかかる部屋を使用し、データベース サーバー ハードウェアおよびネットワーク デバイスへのアクセスを制限します。 さらに、バックアップ メディアをオフサイトの安全な場所で保管することにより、バックアップ メディアへのアクセスも制限します。  
  
 物理的なネットワーク セキュリティを実装する第一歩は、承認されていないユーザーがネットワークにアクセスできないようにすることです。 次の表に、ネットワーク セキュリティ情報の詳細を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|[!INCLUDE[ssEW](../../includes/ssew-md.md)] および他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エディションへのネットワーク アクセス|[!INCLUDE[ssEW](../../includes/ssew-md.md)] オンライン ブックの「サーバー環境の構成とセキュリティ設定」|  
  
### <a name="operating-system-security"></a>オペレーティング システムのセキュリティ  
 オペレーティング システムのサービス パックおよびアップグレードには、重要なセキュリティの強化が含まれています。 更新プログラムおよびアップグレードは、すべてデータベース アプリケーションでテストしてからオペレーティング システムに適用してください。  
  
 ファイアウォールも、セキュリティを実装する効果的な方法を提供します。 論理的には、組織のデータ セキュリティ ポリシーに従って、ネットワーク トラフィックを分離または制限する役割を果たすのがファイアウォールです。 ファイアウォールを使用する場合は、セキュリティ対策を特に強化するポイントを設けることで、オペレーティング システム レベルのセキュリティが向上します。 次の表に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でのファイアウォールの使用方法に関する詳細情報を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|ファイアウォールの構成: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[データベース エンジン アクセスを有効にするための Windows ファイアウォールを構成する](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)|  
|ファイアウォールの構成: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[SSIS サービスにアクセスするように Windows ファイアウォールを構成する](../../integration-services/configure-a-windows-firewall-for-access-to-the-ssis-service.md)|  
|ファイアウォールの構成: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|[Analysis Services のアクセスを許可するための Windows ファイアウォールの構成](https://docs.microsoft.com/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|  
|アクセスするためにファイアウォールの特定のポートを開く: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|  
|チャネル バインドとサービス バインドを使用して認証の拡張保護をサポートするように構成します。|[拡張保護を使用したデータベース エンジンへの接続](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)|  
  
 外部からのアクセスの縮小はセキュリティのための措置で、未使用のコンポーネントの停止または無効化などが含まれます。 外部からのアクセスを縮小すると、システムを攻撃する手段が限られるので、セキュリティの向上を図ることができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への外部からのアクセスを制限するために重要なことは、サービスとユーザーに適切な権限のみを付与して、必要なサービスを "最小の権限" で実行することです。 次の表に、サービスおよびシステム アクセスの詳細を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|次のために必要なサービス: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システムがインターネット インフォメーション サービス (IIS) を使用する場合は、プラットフォームを外部のアクセスから保護するための追加の手順が必要です。 次の表に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および IIS に関する情報を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|IIS セキュリティ: [!INCLUDE[ssEW](../../includes/ssew-md.md)]|[!INCLUDE[ssEW](../../includes/ssew-md.md)] オンライン ブックの「IIS セキュリティ (IIS Security)」|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [認証]|[Reporting Services での認証](../../reporting-services/extensions/security-extension/authentication-in-reporting-services.md)|  
|[!INCLUDE[ssEW](../../includes/ssew-md.md)] と IIS アクセス|[!INCLUDE[ssEW](../../includes/ssew-md.md)] オンライン ブックの「インターネット インフォメーション サービス セキュリティ フローチャート」|  
  
### <a name="sql-server-operating-system-files-security"></a>SQL Server オペレーティング システム ファイルのセキュリティ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、操作やデータ保存にオペレーティング システム ファイルが使用されます。 ファイル セキュリティのベスト プラクティスでは、これらのファイルへのアクセスを制限する必要があります。 次の表に、これらのファイルに関する情報を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プログラム ファイル|[SQL Server の既定のインスタンスおよび名前付きインスタンスのファイルの場所](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサービス パックおよびアップグレードは、強化されたセキュリティを提供します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用の利用可能な最新サービス パックを確認するには、 [SQL Server](https://go.microsoft.com/fwlink/?LinkID=31629) Web サイトを参照してください。  
  
 次のスクリプトを使用すると、システムにインストールされているサービス パックを確認できます。  
  
```  
SELECT CONVERT(char(20), SERVERPROPERTY('productlevel'));  
GO  
```  
  
## <a name="principals-and-database-object-security"></a>プリンシパルとデータベース オブジェクト セキュリティ  
 プリンシパルは、個人、グループ、およびプロセスに与えられた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]へのアクセスです。 "セキュリティ保護可能なリソース" とは、サーバー、データベース、およびデータベースに含まれているオブジェクトを指します。 それぞれのリソースには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の外部からのアクセスを縮小するために構成できる一連の権限が設定されています。 次の表に、プリンシパルおよびセキュリティ保護可能なリソースに関する情報を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|サーバーとデータベースのユーザー、ロール、プロセス|[プリンシパル &#40;データベース エンジン&#41;](authentication-access/principals-database-engine.md)|  
|サーバーとデータベース オブジェクトのセキュリティ|[セキュリティ保護可能](securables.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ階層|[権限の階層 &#40;データベース エンジン&#41;](permissions-hierarchy-database-engine.md)|  
  
### <a name="encryption-and-certificates"></a>暗号化と証明書  
 暗号化では、アクセス コントロールの問題は解決されません。 ただし、暗号化を使用すると、アクセス コントロールがバイパスされるようなまれな状況においてもデータ損失のリスクが限定されるので、セキュリティが強化されます。 たとえば、データベース ホスト コンピューターの構成が適切でない場合に、クレジット カード番号などの機密データを悪意のあるユーザーが入手したとしても、盗まれた情報が暗号化されていれば悪用される可能性が小さくなります。 次の表に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]での暗号化の詳細を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|暗号化階層: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[暗号化階層](encryption/encryption-hierarchy.md)|  
|安全な接続の実装|[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)|  
|暗号化関数|[暗号化関数 &#40;Transact-SQL&#41;](/sql/t-sql/functions/cryptographic-functions-transact-sql)|  
  
 証明書は、2 つのサーバー間で共有されているソフトウェアの "キー" であり、強力な認証による安全な通信を実現します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で証明書を作成して使用することで、オブジェクトおよび接続のセキュリティを向上させることができます。 次の表に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]での証明書の使用方法に関する情報を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|次のための証明書の作成: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)|  
|データベース ミラーリングでの証明書の使用|[データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)|  
  
## <a name="application-security"></a>アプリケーション セキュリティ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティのベスト プラクティスには、安全なクライアント アプリケーションの作成が含まれています。  
  
 クライアント アプリケーションをネットワーク レイヤーで保護する方法の詳細については、「 [クライアント ネットワーク構成](../../database-engine/configure-windows/client-network-configuration.md)」を参照してください。  
  
## <a name="sql-server-security-tools-utilities-views-and-functions"></a>SQL Server のセキュリティ ツール、ユーティリティ、ビュー、関数  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、セキュリティの構成および管理に使用できるツール、ユーティリティ、ビュー、および関数が提供されています。  
  
### <a name="sql-server-security-tools-and-utilities"></a>SQL Server のセキュリティ ツールとユーティリティ  
 次の表に、セキュリティの構成と管理に使用できる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のツールとユーティリティに関する情報を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|接続、構成、制御: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[SQL Server Management Studio の使用 [SQL Server]](../../database-engine/use-sql-server-management-studio.md)|  
|コマンド プロンプトでの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続とクエリの実行|[sqlcmd ユーティリティ](../../tools/sqlcmd-utility.md)|  
|ネットワーク構成および制御: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[SQL Server 構成マネージャー](../sql-server-configuration-manager.md)|  
|ポリシー ベースの管理を使用した機能の有効化と無効化|[ポリシー ベースの管理を使用したサーバーの管理](../policy-based-management/administer-servers-by-using-policy-based-management.md)|  
|レポート サーバーのための対称キーの操作|[rskeymgmt ユーティリティ &#40;SSRS&#41;](../../reporting-services/tools/rskeymgmt-utility-ssrs.md)|  
  
### <a name="sql-server-security-catalog-views-and-functions"></a>SQL Server セキュリティ カタログ ビューと関数  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では、パフォーマンスおよび実用性のために最適化されているいくつかのビューおよび関数でセキュリティ情報が公開されます。 次の表に、セキュリティ ビューおよびセキュリティ関数に関する情報を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ カタログ ビューには、データベース レベルおよびサーバー レベルの権限、プリンシパル、ロールなどに関する情報が表示されます。 暗号化キーと証明書に関する情報や資格情報を表示するカタログ ビューもあります。|[セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/security-catalog-views-transact-sql)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ関数。現在のユーザー、権限、およびスキーマに関する情報を返します。|[セキュリティ関数 &#40;Transact-SQL&#41;](/sql/t-sql/functions/security-functions-transact-sql)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティの動的管理ビュー。|[セキュリティ関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql)|  
  
## <a name="related-content"></a>関連コンテンツ  
 [SQL Server インストールにおけるセキュリティの考慮事項](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
 [SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
