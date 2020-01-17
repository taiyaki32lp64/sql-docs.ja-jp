---
title: SQL Server の保護 | Microsoft Docs
ms.custom: ''
ms.date: 06/21/2019
ms.prod: sql
ms.prod_service: security
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
ms.openlocfilehash: 473c12211ada579c3ceb441792788a1e975a85e0
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892491"
---
# <a name="securing-sql-server"></a>SQL Server の保護

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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
| &nbsp; | &nbsp; |
  
### <a name="operating-system-security"></a>オペレーティング システムのセキュリティ  
 オペレーティング システムのサービス パックおよびアップグレードには、重要なセキュリティの強化が含まれています。 更新プログラムおよびアップグレードは、すべてデータベース アプリケーションでテストしてからオペレーティング システムに適用してください。  
  
 ファイアウォールも、セキュリティを実装する効果的な方法を提供します。 論理的には、組織のデータ セキュリティ ポリシーに従って、ネットワーク トラフィックを分離または制限する役割を果たすのがファイアウォールです。 ファイアウォールを使用する場合は、セキュリティ対策を特に強化するポイントを設けることで、オペレーティング システム レベルのセキュリティが向上します。 次の表に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でのファイアウォールの使用方法に関する詳細情報を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|ファイアウォールの構成: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[データベース エンジン アクセスを有効にするための Windows ファイアウォールを構成する](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)|  
|ファイアウォールの構成: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[Integration Services サービス (SSIS サービス)](../../integration-services/service/integration-services-service-ssis-service.md)|  
|ファイアウォールの構成: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|[Analysis Services のアクセスを許可するための Windows ファイアウォールの構成](https://docs.microsoft.com/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|  
|アクセスするためにファイアウォールの特定のポートを開く: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|  
|チャネル バインドとサービス バインドを使用して認証の拡張保護をサポートするように構成します。|[拡張保護を使用したデータベース エンジンへの接続](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)|  
| &nbsp; | &nbsp; |
  
 外部からのアクセスの縮小はセキュリティのための措置で、未使用のコンポーネントの停止または無効化などが含まれます。 外部からのアクセスを縮小すると、システムを攻撃する手段が限られるので、セキュリティの向上を図ることができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への外部からのアクセスを制限するために重要なことは、サービスとユーザーに適切な権限のみを付与して、必要なサービスを "最小の権限" で実行することです。 次の表に、サービスおよびシステム アクセスの詳細を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|次のために必要なサービス: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)|  
| &nbsp; | &nbsp; |
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システムがインターネット インフォメーション サービス (IIS) を使用する場合は、プラットフォームを外部のアクセスから保護するための追加の手順が必要です。 次の表に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および IIS に関する情報を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|IIS セキュリティ: [!INCLUDE[ssEW](../../includes/ssew-md.md)]|[!INCLUDE[ssEW](../../includes/ssew-md.md)] オンライン ブックの「IIS セキュリティ (IIS Security)」|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [認証]|[Reporting Services での認証](../../reporting-services/extensions/security-extension/authentication-in-reporting-services.md)|  
|[!INCLUDE[ssEW](../../includes/ssew-md.md)] と IIS アクセス|[!INCLUDE[ssEW](../../includes/ssew-md.md)] オンライン ブックの「インターネット インフォメーション サービス セキュリティ フローチャート」|  
| &nbsp; | &nbsp; |
  
### <a name="sql-server-operating-system-files-security"></a>SQL Server オペレーティング システム ファイルのセキュリティ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、操作やデータ保存にオペレーティング システム ファイルが使用されます。 ファイル セキュリティのベスト プラクティスでは、これらのファイルへのアクセスを制限する必要があります。 次の表に、これらのファイルに関する情報を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プログラム ファイル|[SQL Server の既定のインスタンスおよび名前付きインスタンスのファイルの場所](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)|  
| &nbsp; | &nbsp; |
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサービス パックおよびアップグレードは、強化されたセキュリティを提供します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用の利用可能な最新サービス パックを確認するには、 [SQL Server](https://go.microsoft.com/fwlink/?LinkID=31629) Web サイトを参照してください。  
  
 次のスクリプトを使用すると、システムにインストールされているサービス パックを確認できます。  
  
```sql
SELECT CONVERT(char(20), SERVERPROPERTY('productlevel'));  
```  
  
## <a name="principals-and-database-object-security"></a>プリンシパルとデータベース オブジェクト セキュリティ  
 プリンシパルは、個人、グループ、およびプロセスに与えられた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]へのアクセスです。 "セキュリティ保護可能なリソース" とは、サーバー、データベース、およびデータベースに含まれているオブジェクトを指します。 それぞれのリソースには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の外部からのアクセスを縮小するために構成できる一連の権限が設定されています。 次の表に、プリンシパルおよびセキュリティ保護可能なリソースに関する情報を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|サーバーとデータベースのユーザー、ロール、プロセス|[プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)|  
|サーバーとデータベース オブジェクトのセキュリティ|[セキュリティ保護可能](../../relational-databases/security/securables.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ階層|[権限の階層 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)|  
| &nbsp; | &nbsp; |
  
### <a name="encryption-and-certificates"></a>暗号化と証明書  
 暗号化では、アクセス コントロールの問題は解決されません。 ただし、暗号化を使用すると、アクセス コントロールがバイパスされるようなまれな状況においてもデータ損失のリスクが限定されるので、セキュリティが強化されます。 たとえば、データベース ホスト コンピューターの構成が適切でない場合に、クレジット カード番号などの機密データを悪意のあるユーザーが入手したとしても、盗まれた情報が暗号化されていれば悪用される可能性が小さくなります。 次の表に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]での暗号化の詳細を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|暗号化階層: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)|  
|安全な接続の実装|[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)|  
|暗号化関数|[暗号化関数 &#40;Transact-SQL&#41;](../../t-sql/functions/cryptographic-functions-transact-sql.md)|  
  
 証明書は、2 つのサーバー間で共有されているソフトウェアの "キー" であり、強力な認証による安全な通信を実現します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で証明書を作成して使用することで、オブジェクトおよび接続のセキュリティを向上させることができます。 次の表に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]での証明書の使用方法に関する情報を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|次のための証明書の作成: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)|  
|データベース ミラーリングでの証明書の使用|[データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)|  
| &nbsp; | &nbsp; |

## <a name="application-security"></a>アプリケーション セキュリティ

### <a name="client-programs"></a>クライアント プログラム

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティのベスト プラクティスには、安全なクライアント アプリケーションの作成が含まれています。 クライアント アプリケーションをネットワーク レイヤーで保護する方法の詳細については、「 [クライアント ネットワーク構成](../../database-engine/configure-windows/client-network-configuration.md)」を参照してください。

### <a name="windows-defender-application-control-wdac"></a>Windows Defender アプリケーション制御 (WDAC)

<!--
This next live paragraph, about Windows Defender Application Control (WDAC), was requested by Bella Brahm, 2019/06/20. (GeneMi)

WDAC can also prevent the kind of highly sophisticated 'Nansh0u' attacks described in 'https://www.guardicore.com/2019/05/nansh0u-campaign-hackers-arsenal-grows-stronger/'. That webpage recommends this present article.
-->

Windows Defender アプリケーション制御 (WDAC) により、未承認のコード実行を防ぐことができます。 WDAC は、実行可能ファイルベースのマルウェアの脅威を軽減する効果的な方法です。 詳細については、「[Windows Defender アプリケーション制御](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)」ドキュメントを参照してください。

## <a name="sql-server-security-tools-utilities-views-and-functions"></a>SQL Server のセキュリティ ツール、ユーティリティ、ビュー、関数  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、セキュリティの構成および管理に使用できるツール、ユーティリティ、ビュー、および関数が提供されています。  
  
### <a name="sql-server-security-tools-and-utilities"></a>SQL Server のセキュリティ ツールとユーティリティ  
 次の表に、セキュリティの構成と管理に使用できる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のツールとユーティリティに関する情報を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|接続、構成、制御: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[SQL Server Management Studio の使用 [SQL Server]](https://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)|  
|コマンド プロンプトでの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続とクエリの実行|[sqlcmd ユーティリティ](../../tools/sqlcmd-utility.md)|  
|ネットワーク構成および制御: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[SQL Server 構成マネージャー](../../relational-databases/sql-server-configuration-manager.md)|  
|ポリシー ベースの管理を使用した機能の有効化と無効化|[ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)|  
|レポート サーバーのための対称キーの操作|[rskeymgmt ユーティリティ &#40;SSRS&#41;](../../reporting-services/tools/rskeymgmt-utility-ssrs.md)|  
| &nbsp; | &nbsp; |

### <a name="sql-server-security-catalog-views-and-functions"></a>SQL Server セキュリティ カタログ ビューと関数  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では、パフォーマンスおよび実用性のために最適化されているいくつかのビューおよび関数でセキュリティ情報が公開されます。 次の表に、セキュリティ ビューおよびセキュリティ関数に関する情報を示します。  
  
|詳細|参照先|  
|---------------------------|---------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ カタログ ビューには、データベース レベルおよびサーバー レベルの権限、プリンシパル、ロールなどに関する情報が表示されます。 暗号化キーと証明書に関する情報や資格情報を表示するカタログ ビューもあります。|[セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ関数。現在のユーザー、権限、およびスキーマに関する情報を返します。|[セキュリティ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティの動的管理ビュー。|[セキュリティ関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)|  
| &nbsp; | &nbsp; |

## <a name="related-content"></a>関連コンテンツ  
 [SQL Server インストールにおけるセキュリティの考慮事項](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
 [SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
[SQL Server 2012 のセキュリティに関するベスト プラクティス - 運用作業と管理作業](https://download.microsoft.com/download/8/F/A/8FABACD7-803E-40FC-ADF8-355E7D218F4C/SQL_Server_2012_Security_Best_Practice_Whitepaper_Apr2012.docx)   
[SQL Server セキュリティ ブログ](https://blogs.msdn.microsoft.com/sqlsecurity/)  
[セキュリティのベスト プラクティスと Label Security のホワイト ペーパー](https://blogs.msdn.microsoft.com/sqlsecurity/2012/03/06/security-best-practice-and-label-security-whitepapers/)  
[行レベルのセキュリティ](../../relational-databases/security/row-level-security.md)   
[SQL Server の知的所有権の保護](../../relational-databases/security/protecting-your-sql-server-intellectual-property.md)   
  
