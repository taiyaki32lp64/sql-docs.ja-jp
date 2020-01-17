---
title: SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- Security [SQL Server]
helpviewer_keywords:
- SQL Server, security
- security [SQL Server]
- database security [SQL Server]
- databases [SQL Server], security
ms.assetid: dfb39d16-722a-4734-94bb-98e61e014ee7
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: fc99b725f4c5895306d544df14bf2a9390189066
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244533"
---
# <a name="security-center-for-sql-server-database-engine-and-azure-sql-database"></a>SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター
  このページでは、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]および [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]でのセキュリティと保護に関して必要になる情報の検索に役立つリンクを示します。  
  
> [!NOTE]  
>  
  [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] の機能は向上し続けます。 
  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]に関する最新情報については、このトピックの最新バージョンをご覧ください。  
  
|認証: ユーザーはだれか|認証: 何を実行できるか|暗号化: 秘密データの格納|接続のセキュリティ: 制限とセキュリティ保護|監査: アクセスの記録|  
|----------------------------------|-------------------------------------|-------------------------------------|---------------------------------------------------|--------------------------------|  
|**だれが認証するか**<br /><br /> [![セキュリティ センター マップの Windows 認証](../../database-engine/media/security-center-map-windows-authenticaion.png "セキュリティ センター マップの Windows 認証")](https://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> <br /><br /> [![セキュリティ センター マップの SQL Server 認証](../../database-engine/media/security-center-map-sql-authenticaion.png "セキュリティ センター マップの SQL Server 認証")](https://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> **どこで認証されていますか?**<br /><br /> [![セキュリティ センター マップのログインとユーザー](../../database-engine/media/security-center-map-logins-users.png "セキュリティ センター マップのログインとユーザー")](https://msdn.microsoft.com/library/aa337562.aspx)<br /><br /> <br /><br /> [![セキュリティ センター マップの包含データベース ユーザー](../../database-engine/media/security-center-map-contained-users.png "セキュリティ センター マップの包含データベース ユーザー")](https://msdn.microsoft.com/library/ff929188.aspx)<br /><br /> **その他の Id の使用**<br /><br /> [![セキュリティ センター マップの資格情報](../../database-engine/media/security-center-map-credentials.png "セキュリティ センター マップの資格情報")](https://msdn.microsoft.com/library/ms161950.aspx)<br /><br /> [![セキュリティ センター マップの EXECUTE AS LOGIN](../../database-engine/media/security-center-map-exec-as-login.png "セキュリティ センター マップの EXECUTE AS LOGIN")](https://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> [![セキュリティ センター マップの EXECUTE AS USER](../../database-engine/media/security-center-map-exec-as-user.png "セキュリティ センター マップの EXECUTE AS USER")](https://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")|**権限の許可、取り消し、および拒否**<br /><br /> [![セキュリティ センター マップのセキュリティ保護可能なクラス](../../database-engine/media/security-center-map-securable-classes.png "セキュリティ センター マップのセキュリティ保護可能なクラス")](https://msdn.microsoft.com/library/ms190401.aspx)<br /><br /> [![セキュリティ センター マップのサーバーのアクセス許可](../../database-engine/media/security-center-map-srv-perms.png "セキュリティ センター マップのサーバーのアクセス許可")](https://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> [![セキュリティ センター マップのデータベース アクセス許可](../../database-engine/media/security-center-map-db-perms.png "セキュリティ センター マップのデータベース アクセス許可")](https://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> **ロールごとのセキュリティ**<br /><br /> [![セキュリティ センター マップのサーバー ロール](../../database-engine/media/security-center-map-srv-roles.png "セキュリティ センター マップのサーバー ロール")](https://msdn.microsoft.com/library/ms188659.aspx)<br /><br /> [![セキュリティ センター マップのデータベース ロール](../../database-engine/media/security-center-map-db-roles.png "セキュリティ センター マップのデータベース ロール")](https://msdn.microsoft.com/library/ms189121.aspx)<br /><br /> `Restricting Data Access to Selected Data Elements`<br /><br /> [![セキュリティ センター マップのビューとプロシージャ](../../database-engine/media/security-center-map-view-procs.png "セキュリティ センター マップのビューとプロシージャ")](https://msdn.microsoft.com/library/ms175503.aspx)<br /><br /> [![セキュリティ センター マップの行レベルのセキュリティ](../../database-engine/media/security-center-map-row-level-sec.png "セキュリティ センター マップの行レベルのセキュリティ")](https://msdn.microsoft.com/library/dn765131.aspx)<br /><br /> [![セキュリティ センター マップの動的なデータ マスキング](../../database-engine/media/security-center-map-data-masking.png "セキュリティ センター マップの動的なデータ マスキング")](https://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)<br /><br /> [![セキュリティ センター マップの署名済みオブジェクト](../../database-engine/media/security-center-map-signed-objects.png "セキュリティ センター マップの署名済みオブジェクト")](https://msdn.microsoft.com/library/ms181700.aspx)<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")|**ファイルの暗号化**<br /><br /> [![セキュリティ センター マップの BitLocker](../../database-engine/media/security-center-map-bitlocker.png "セキュリティ センター マップの BitLocker")](https://support.microsoft.com/kb/2855131)<br /><br /> [![セキュリティ センター マップの NTFS 暗号化](../../database-engine/media/security-center-map-ntfs-encryp.png "セキュリティ センター マップの NTFS 暗号化")](https://msdn.microsoft.com/library/dd163562.aspx)<br /><br /> [![セキュリティ センター マップの TDE](../../database-engine/media/security-center-map-tde.png "セキュリティ センター マップの TDE")](https://msdn.microsoft.com/library/bb934049.aspx)<br /><br /> [![セキュリティ センター マップのバックアップの暗号化](../../database-engine/media/security-center-map-backup-encryp.png "セキュリティ センター マップのバックアップの暗号化")](https://msdn.microsoft.com/library/dn449489.aspx)<br /><br /> **ソースの暗号化**<br /><br /> [![セキュリティ センター マップの EKM](../../database-engine/media/security-center-map-ekm.png "セキュリティ センター マップの EKM")](https://msdn.microsoft.com/library/bb895340.aspx)<br /><br /> [![セキュリティ センター マップの Azure Key Vault](../../database-engine/media/security-center-map-key-vault.png "セキュリティ センター マップの Azure Key Vault")](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)<br /><br /> **列、データ & キーの暗号化**<br /><br /> [![証明書による暗号化をマップ Security Center](../../database-engine/media/security-center-map-cert.png "証明書による暗号化をマップ Security Center")](https://msdn.microsoft.com/library/ms188061.aspx)<br /><br /> [![セキュリティ センター マップの対称キーによる暗号化](../../database-engine/media/security-center-map-sym-key.png "セキュリティ センター マップの対称キーによる暗号化")](https://msdn.microsoft.com/library/ms174361.aspx)<br /><br /> [![セキュリティ センター マップの非対称キーによる暗号化](../../database-engine/media/security-center-map-asym-key.png "セキュリティ センター マップの非対称キーによる暗号化")](https://msdn.microsoft.com/library/ms186950.aspx)<br /><br /> [![セキュリティ センター マップのパスフレーズによる暗号化](../../database-engine/media/security-center-map-passphrase.png "セキュリティ センター マップのパスフレーズによる暗号化")](https://msdn.microsoft.com/library/ms190357.aspx)|**ファイアウォールによる保護**<br /><br /> [![セキュリティ センター マップの Windows ファイアウォール](../../database-engine/media/security-center-map-windows-firewall.png "セキュリティ センター マップの Windows ファイアウォール")](https://msdn.microsoft.com/library/ms175043.aspx)<br /><br /> [![セキュリティ センター マップのサービス ファイアウォール](../../database-engine/media/security-center-map-service-firewall.png "セキュリティ センター マップのサービス ファイアウォール")](https://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> [![セキュリティ センター マップのデータベース ファイアウォール](../../database-engine/media/security-center-map-db-firewall.png "セキュリティ センター マップのデータベース ファイアウォール")](https://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> **転送中のデータの暗号化**<br /><br /> [![セキュリティ センター マップの強制 SSL](../../database-engine/media/security-center-map-forced-ssl.png "セキュリティ センター マップの強制 SSL")](https://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> [![セキュリティ センター マップのオプションの SSL](../../database-engine/media/security-center-map-opt-ssl.png "セキュリティ センター マップのオプションの SSL")](https://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")|**自動監査**<br /><br /> [![セキュリティ センター マップの SQL Server Audit](../../database-engine/media/security-center-map-sql-audit.png "セキュリティ センター マップの SQL Server Audit")](https://msdn.microsoft.com/library/cc280386.aspx)<br /><br /> [![セキュリティ センター マップの SQL Database Audit](../../database-engine/media/security-center-map-sqldb-audit.png "セキュリティ センター マップの SQL Database Audit")](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)<br /><br /> **カスタム監査**<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")<br /><br /> [![セキュリティ センター マップのトリガー](../../database-engine/media/security-center-map-triggers.png "セキュリティ センター マップのトリガー")](https://msdn.microsoft.com/library/ms175941.aspx)<br /><br /> **従っ**<br /><br /> [![SecCtrCompliance](../../database-engine/media/secctrcompliance.png "SecCtrCompliance")](https://azure.microsoft.com/support/trust-center/services/)<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")<br /><br /> ![Placeholder](../../database-engine/media/security-center-map-blankplaceholder.png "Placeholder")<br /><br /> ![セキュリティ センターの凡例](../../database-engine/media/security-center-map-legend.png "セキュリティ センターの凡例")|  
  
## <a name="links-to-specific-related-topics"></a>関連する特定のトピックへのリンク  
 ![小さいファイルフォルダーアイコン](../../integration-services/media/filefolder-small.gif "小さいファイル フォルダー アイコン")**認証: ユーザーはだれですか**。  
 **だれが認証するか(Windows また[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は)**  
  
-   [認証モードの選択](choose-an-authentication-mode.md)  
  
 **Master データベースでの認証**(ログインとデータベースユーザー)  
  
-   [SQL Server ログインの作成](authentication-access/create-a-login.md)  
  
-   [Azure SQL Database でのデータベースとログインの管理](https://msdn.microsoft.com/library/ee336235.aspx)  
  
-   [データベースユーザーの作成](authentication-access/create-a-database-user.md)  
  
 **ユーザー データベースでの認証**  
  
-   [包含データベースユーザー-データベースの移植性を高める](contained-database-users-making-your-database-portable.md)  
  
 **その他の Id の使用**  
  
-   [資格情報 &#40;データベースエンジン&#41;](authentication-access/credentials-database-engine.md)  
  
-   [別のログインとして実行](/sql/t-sql/statements/execute-as-transact-sql)  
  
-   [別のデータベースユーザーとして実行](/sql/t-sql/statements/execute-as-transact-sql)  
  
 ![小さいファイルフォルダーアイコン](../../integration-services/media/filefolder-small.gif "小さいファイル フォルダー アイコン")**暗号化: シークレットデータの格納**  
 **ファイルの暗号化**  
  
-   [BitLocker (ドライブレベル)](https://support.microsoft.com/kb/2855131)  
  
-   [NTFS 暗号化 (フォルダーレベル)](https://msdn.microsoft.com/library/dd163562.aspx)  
  
-   [Transparent Data Encryption (ファイルレベル)](encryption/transparent-data-encryption.md)  
  
-   [バックアップの暗号化 (ファイルレベル)](../backup-restore/backup-encryption.md)  
  
 **ソースの暗号化**  
  
-   [拡張キー管理モジュール](encryption/extensible-key-management-ekm.md)  
  
-   [Azure Key Vault に格納されているキー](encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
 **列、データ、キーの暗号化**  
  
-   [証明書による暗号化](/sql/t-sql/functions/encryptbycert-transact-sql)  
  
-   [非対称キーによる暗号化](/sql/t-sql/functions/encryptbyasymkey-transact-sql)  
  
-   [対称キーによる暗号化](/sql/t-sql/functions/encryptbykey-transact-sql)  
  
-   [パスフレーズによる暗号化](/sql/t-sql/functions/encryptbypassphrase-transact-sql)  
  
 ![小さいファイルフォルダーのアイコン](../../integration-services/media/filefolder-small.gif "小さいファイル フォルダー アイコン")**承認: 実行できる操作**  
 **権限の許可、取り消し、および拒否**  
  
-   [権限の階層 &#40;データベースエンジン&#41;](permissions-hierarchy-database-engine.md)  
  
-   [許可](permissions-database-engine.md)  
  
-   [[セキュリティ保護可能なリソース]](securables.md)  
  
 **ロールごとのセキュリティ**  
  
-   [サーバーレベルのロール](authentication-access/server-level-roles.md)  
  
-   [データベースレベルのロール](authentication-access/database-level-roles.md)  
  
 `Restricting Data Access to Selected Data Elements`  
  
-   
  [ビュー](../views/views.md) と [プロシージャ](../stored-procedures/stored-procedures-database-engine.md)を使用したデータ アクセスの制限  
  
-   [行レベルのセキュリティ](https://msdn.microsoft.com/library/azure/dn765131.aspx)  
  
-   [動的データ マスク](https://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)  
  
-   [署名されたオブジェクト](/sql/t-sql/statements/add-signature-transact-sql)  
  
 ![小さいファイルフォルダーアイコン](../../integration-services/media/filefolder-small.gif "小さいファイル フォルダー アイコン")**接続のセキュリティ: 制限とセキュリティ保護**  
 **ファイアウォールによる保護**  
  
-   [データベースエンジンアクセスできるように Windows ファイアウォールを構成する](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
-   [ファイアウォール設定の Azure SQL Database](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)  
  
-   [Azure サービスのファイアウォール設定](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)  
  
 **転送中のデータの暗号化**  
  
-   [データベースエンジンの Secure Sockets Layer](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)  
  
-   [SQL Database の Secure Sockets Layer](https://msdn.microsoft.com/library/azure/ff394108.aspx)  
  
 ![小さいファイルフォルダーアイコン](../../integration-services/media/filefolder-small.gif "小さいファイル フォルダー アイコン")の**監査: アクセスの記録**  
 **自動監査**  
  
-   [SQL Server 監査 &#40;データベースエンジン&#41;](auditing/sql-server-audit-database-engine.md)  
  
-   [SQL Database 監査](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)  
  
 **カスタム監査の実装**  
  
-   
  [DDL Triggers](../triggers/ddl-triggers.md) と [DML Triggers](../triggers/dml-triggers.md)の作成  
  
 ![小さいファイルフォルダーアイコン](../../integration-services/media/filefolder-small.gif "小さいファイル フォルダー アイコン")の**準拠**  
 **SQL Server**  
  
-   [一般的な条件](https://go.microsoft.com/fwlink/?LinkId=616319)  
  
 **SQL Database**  
  
-   [Microsoft Azure セキュリティセンター: 機能によるコンプライアンス](https://azure.microsoft.com/support/trust-center/services/)  
  
## <a name="see-also"></a>参照  
 [SQL Server のセキュリティ保護](securing-sql-server.md)   
 [プリンシパル &#40;データベースエンジン&#41;](authentication-access/principals-database-engine.md)   
 [証明書と非対称キーの SQL Server](sql-server-certificates-and-asymmetric-keys.md)   
 [SQL Server 暗号化](encryption/sql-server-encryption.md)   
 [セキュリティ構成](surface-area-configuration.md)   
 [強力なパスワード](strong-passwords.md)   
 [信頼可能データベースのプロパティ](trustworthy-database-property.md)   
 [データベースエンジンの機能とタスク](../../database-engine/database-engine-features-and-tasks.md)  
  
  
