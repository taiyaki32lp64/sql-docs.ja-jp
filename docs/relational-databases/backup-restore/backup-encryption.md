---
title: バックアップの暗号化 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 334b95a8-6061-4fe0-9e34-b32c9f1706ce
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 19a8597136f073d609c7a9cc77ce8e2b73c72004
ms.sourcegitcommit: 36c3ead6f2a3628f58040acf47f049f0b0957b8a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71688291"
---
# <a name="backup-encryption"></a>バックアップの暗号化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップの暗号化オプションについて概説します。 バックアップ時の暗号化の使用、利点、および推奨される操作の詳細が含まれています。  

## <a name="Overview"></a> 概要  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]以降では、バックアップの作成時に SQL Server がデータを暗号化する機能があります。 バックアップの作成時に暗号化アルゴリズムと暗号化機能 (証明書または非対称キー) を指定することにより、暗号化されたバックアップ ファイルを作成することができます。 あらゆるバックアップ先ストレージ、つまり内部設置型のストレージも Window Azure ストレージもサポートされます。 また、暗号化オプションは、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] で導入された新機能である [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]の操作用に構成できます。  
  
 バックアップ時に暗号化を行うには、暗号化アルゴリズムを指定し、暗号化キーを保護するための暗号化機能を指定する必要があります。 サポートされている暗号化オプションは次のとおりです。  
  
- **暗号化アルゴリズム:** サポートされている暗号化アルゴリズムは、AES 128、AES 192、AES 256、および Triple DES です  
  
- **暗号化機能:** 証明書キーまたは非対称キー  
  
> [!CAUTION]  
> 証明書または非対称キーをバックアップすることが非常に重要であり、これらを使用して暗号化したバックアップ ファイルとは別の場所に保存することをお勧めします。 証明書または非対称キーがないと、バックアップ ファイルが使用不可能になり、バックアップを復元することができません。  
  
 **暗号化されたバックアップの復元:** SQL Server の復元では、復元時に暗号化パラメーターを指定する必要はありません。 ただし、バックアップ ファイルの暗号化に使用された証明書または非対称キーを復元先のインスタンスで使用できる必要があります。 復元を実行するユーザー アカウントには、証明書またはキーに対する **VIEW DEFINITION** 権限が必要です。 暗号化されたバックアップを別のインスタンスに復元する場合は、そのインスタンスで証明書を使用できるようにする必要があります。  
  
 TDE で暗号化されたデータベースからバックアップを復元する場合、復元先のインスタンスで TDE の証明書を使用できる必要があります。  
  
##  <a name="Benefits"></a> 利点  
  
1. データベースのバックアップを暗号化することは、データの保護に役立ちます。SQL Server では、バックアップの作成時にバックアップ データを暗号化するためのオプションが提供されます。  
  
1. 暗号化は、TDE を使用して暗号化されたデータベースにも使用できます。  
  
1. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]によって実行されたバックアップでも暗号化がサポートされるため、オフサイト バックアップのセキュリティを強化できます。  
  
1. この機能では、AES 256 ビットまでの複数の暗号化アルゴリズムがサポートされます。 このため、要件に合うアルゴリズムを選択できます。  
  
1. 暗号化キーは拡張キー管理 (EKM) プロバイダーと統合できます。  
 
##  <a name="Prerequisites"></a> 前提条件  
 バックアップを暗号化するための前提条件は次のとおりです。  
  
1. **master データベースのデータベース マスター キーの作成:** データベース マスター キーは対称キーで、証明書の秘密キーやデータベース内にある非対称キーを保護するときに使用されます。 詳細については、「[SQL Server とデータベースの暗号化キー &#40;データベース エンジン&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)」を参照してください。  
  
1. バックアップの暗号化に使用する証明書または非対称キーを作成します。 証明書の作成の詳細については、「[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)」を参照してください。 証明書の作成の詳細については、「[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)」を参照してください。  
  
    > [!IMPORTANT]  
    >  サポートされるのは、拡張キー管理 (EKM) に存在する非対称キーのみです。  
  
##  <a name="Restrictions"></a> 制限  
 暗号化オプションに適用される制限事項は次のとおりです。  
  
- バックアップ データの暗号化に非対称キーを使用する場合は、EKM プロバイダーに存在する非対称キーのみがサポートされます。  
  
- SQL Server Express および SQL Server Web では、バックアップ時の暗号化がサポートされません。 ただし、暗号化されたバックアップから SQL Server Express インスタンスまたは SQL Server Web インスタンスへの復旧は、サポートされます。  
  
- 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、暗号化されたバックアップを読み取ることができません。  
  
- [既存のバックアップ セットに追加する] オプションは、暗号化されたバックアップに対してはサポートされません。  

##  <a name="Permissions"></a> Permissions  

バックアップの暗号化または暗号化されたバックアップからの復元を行うには、データベース バックアップの暗号化に使用する証明書または非対称キーに対する**VIEW DEFINITION** 権限を使用します。  
  
> [!NOTE]  
> TDE で保護されたデータベースをバックアップまたは復元する場合、TDE 証明書へのアクセスは必要ありません。  
  
## <a name="Methods"></a> バックアップの暗号化方法  
 以下のセクションでは、バックアップ時にデータを暗号化する手順の概要を説明します。 Transact-SQL を使用して既存のバックアップを暗号化するためのさまざまな手順を示した完全なチュートリアルについては、「 [暗号化されたバックアップの作成](../../relational-databases/backup-restore/create-an-encrypted-backup.md)」を参照してください。  
  
### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio の使用  
 次のいずれかのダイアログ ボックスを使用して、データベース バックアップの作成時にバックアップを暗号化することができます。  
  
1. [データベースのバックアップ &#40;[バックアップ オプション] ページ&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md): **[バックアップ オプション]** ページで、 **[暗号化]** を選択し、暗号化に使用する暗号化アルゴリズムと証明書または非対称キーを指定します。  
  
1. [メンテナンス プラン ウィザードの使用](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md#SSMSProcedure) : **[データベースのバックアップ () タスクの定義]** ページの **[オプション]** タブでバックアップ タスクを選択する場合は、 **[バックアップの暗号化]** を選択し、暗号化に使用する暗号化アルゴリズムと証明書またはキーを指定することができます。  
  
### <a name="using-transact-sql"></a>Transact-SQL の使用  
 バックアップ ファイルを暗号化するためのサンプル TSQL ステートメントを次に示します。  
  
```sql  
BACKUP DATABASE [MYTestDB]  
TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
WITH  
  COMPRESSION,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ),  
  STATS = 10  
GO  
```  
  
 Transact-SQL ステートメントの完全な構文については、「[BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)」を参照してください。  
  
### <a name="using-powershell"></a>PowerShell の使用  
 この例では、暗号化オプションを作成し、それを **Backup-SqlDatabase** コマンドレットのパラメーター値として使用して暗号化されたバックアップを作成します。  
  
```powershell
$encryptionOption = New-SqlBackupEncryptionOption -Algorithm Aes256 -EncryptorType ServerCertificate -EncryptorName "BackupCert"  

Backup-SqlDatabase -ServerInstance . -Database "<myDatabase>" -BackupFile "<myDatabase>.bak" -CompressionOption On -EncryptionOption $encryptionOption  
```  
  
##  <a name="RecommendedPractices"></a> 推奨される操作  
 インスタンスがインストールされているローカル コンピューター以外の場所に暗号化証明書とキーのバックアップを作成します。 ディザスター リカバリー シナリオに対応するには、証明書またはキーのバックアップをオフサイトに保管することを検討します。 バックアップの暗号化に使用された証明書がないと、暗号化されたバックアップを復元することはできません。  
  
 暗号化されたバックアップを復元するには、復元先のインスタンスで、バックアップの作成時に使用された元の証明書および対応する拇印を使用できるようにしておく必要があります。 このため証明書には、有効期限切れによる更新またはその他の変更を行わないでください。 更新すると証明書が更新され拇印の変更が発生するため、バックアップ ファイルに対して証明書が無効になることがあります。 復元を実行するアカウントには、バックアップ時に暗号化に使用される証明書または非対称キーに対する VIEW DEFINITION 権限が必要です。  
  
 可用性グループ データベースのバックアップは、通常は優先されるバックアップ レプリカで実施します。  バックアップを実施したのとは異なるレプリカでバックアップを復元する場合は、バックアップに使用した元の証明書が、復元先のレプリカで利用できることを確認してください。  
  
 データベースが TDE 対応の場合は、データベースの暗号化とバックアップに別々の証明書または非対象キーを選択することにより、セキュリティを強化します。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
|トピック/タスク|[説明]|  
|-----------------|-----------------|  
|[暗号化されたバックアップの作成](../../relational-databases/backup-restore/create-an-encrypted-backup.md)|暗号化されたバックアップを作成するために必要な基本手順について説明します。|  
|[Azure Key Vault を使用する拡張キー管理 &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)|Azure Key Vault のキーで保護される暗号化されたバックアップを作成する例を示します。|  
  
## <a name="see-also"></a>参照  
 [バックアップの概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)  
