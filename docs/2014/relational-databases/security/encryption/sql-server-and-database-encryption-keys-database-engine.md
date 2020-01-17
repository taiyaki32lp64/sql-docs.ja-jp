---
title: SQL Server とデータベースの暗号化キー (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- keys [SQL Server], database encryption
ms.assetid: 15c0a5e8-9177-484c-ae75-8c552dc0dac0
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: e9ddec585f530cf57481c56477d5be4aeaedb44a
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957126"
---
# <a name="sql-server-and-database-encryption-keys-database-engine"></a>SQL Server とデータベースの暗号化キー (データベース エンジン)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]では、暗号化キーを使用して、サーバーデータベースに格納されているデータ、資格情報、および接続情報をセキュリティで保護します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]には、*対称*と*非対称*の2種類のキーがあります。 対称キーでは、データの暗号化と暗号化解除に同じパスワードが使用されます。 非対称キーでは、データを暗号化するパスワード ( *公開* キー) とデータの暗号化を解除するパスワード ( *秘密* キー) が使い分けられます。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の暗号化キーでは、公開キー、秘密キー、対称キーを組み合わせて機密データの保護に使用します。 対称キーは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを最初に起動するときの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 初期化時に作成されます。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、このキーを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に格納されている機密データを暗号化します。 公開キーと秘密キーはオペレーティング システムによって作成され、これらのキーを使用して対称キーが保護されます。 公開キーと秘密キーのペアは、データベースに機密データを格納する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスごとに作成されます。  
  
## <a name="applications-for-sql-server-and-database-keys"></a>SQL Server およびデータベース キーの用途  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]では、キーに2つの主要なアプリケーションがあります。1つは[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンスに対して生成される*サービスマスターキー* (SMK)、もう1つはデータベースに使用される*データベースマスターキー* (DMK) です。  
  
 SMK は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの初回起動時に自動的に生成され、リンク サーバーのパスワード、資格情報、およびデータベース マスター キーの暗号化に使用されます。 SMK は、Windows データ保護 API (DPAPI) を使用するローカル コンピューター キーを使用して暗号化されます。 DPAPI では、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントの Windows 資格情報およびコンピューターの資格情報から派生するキーが使用されます。 サービス マスター キーの暗号化を解除できるのは、作成元のサービス アカウント、またはコンピューターの資格情報にアクセスできるプリンシパルに限られています。  
  
 データベース マスター キーは対称キーで、証明書の秘密キーやデータベース内にある非対称キーを保護するときに使用されます。 このキーはデータの暗号化にも使用できますが、長さに制限があるため、対称キーに比べるとデータに対する実用性は低くなります。  
  
 このマスター キーは、その作成時に、トリプル DES アルゴリズムとユーザー指定のパスワードを使用して暗号化されます。 マスター キーの暗号化を自動的に解除できるように、SMK を使用してこのキーのコピーが暗号化されます。 暗号化されたコピーは、使用先のデータベースおよび `master` システム データベースの両方に格納されます。  
  
 
  `master` システム データベースに格納された DMK のコピーは、DMK が変更されるたびに自動的に更新されます。 ただし、この既定の動作は `DROP ENCRYPTION BY SERVICE MASTER KEY` ステートメントの `ALTER MASTER KEY` オプションを使用して変更できます。 サービス マスター キーで暗号化されていない DMK を開くには、`OPEN MASTER KEY` ステートメントとパスワードを使用する必要があります。  
  
## <a name="managing-sql-server-and-database-keys"></a>SQL Server およびデータベースのキーの管理  
 暗号化キーの管理は、新しいデータベース キーの作成、サーバーおよびデータベースのキーのバックアップ作成、およびキーの復元、削除、変更のタイミングと方法を把握することによって行われます。  
  
 対称キーを管理するには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 付属のツールを使用して以下の作業を行います。  
  
-   サーバーを復旧させるため、または計画的な移行の一環として使用できるように、サーバーおよびデータベースのキーのコピーをバックアップします。  
  
-   以前に保存したキーをデータベースに復元します。 これにより、新しいサーバー インスタンスは、そのインスタンスで暗号化していない既存のデータにアクセスできるようになります。  
  
-   暗号化されたデータにアクセスできなくなった場合は、データベース内の暗号化されたデータを削除します。  
  
-   キーに障害が起きた場合は、そのキーを再作成し、データを再暗号化します。 セキュリティを高めるには、キーを定期的 (たとえば数か月ごと) に再作成して、キーを解読しようとする攻撃からサーバーを保護する必要があります。  
  
-   複数のサーバーが 1 つのデータベースとそのデータベースの暗号化を解除するキーの両方を共有する場合は、サーバー スケールアウト配置に対してサーバー インスタンスを追加または削除します。  
  
## <a name="important-security-information"></a>重要なセキュリティ情報  
 サービス マスター キーで保護されているオブジェクトにアクセスするには、そのキーの作成に使用された [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウント、またはコンピューター アカウントのいずれかが必要です。 つまり、コンピューターはキーが作成されたシステムに関連付けられています。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウント *または* コンピューター アカウントを変更しても、キーにアクセスできなくなることはありません。 ただし、両方を変更するとサービス マスター キーにはアクセスできなくなります。 この 2 つのアカウントが一方しかない状態でサービス マスター キーにアクセスできなくなると、元のキーで暗号化されたデータとオブジェクトは暗号化解除できなくなります。  
  
 サービス マスター キーで保護されている接続は、サービス マスター キーがないと復元できません。  
  
 データベース マスター キーで保護されたオブジェクトとデータにアクセスする場合は、そのキーを保護する際に使用されたパスワードのみが必要です。  
  
> [!CAUTION]  
>  上記のキーすべてにアクセスできなくなると、それらのキーで保護されているオブジェクト、接続、およびデータにもアクセスできなくなります。 ここで示したリンクの説明に従ってサービス マスター キーを復元するか、または元の暗号化システムに戻ってアクセスを復旧します。 アクセスを復旧するための "抜け道" はありません。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [サービスマスターキー](service-master-key.md)  
 サービス マスター キーとその推奨事項について簡単に説明します。  
  
 [拡張キー管理 &#40;EKM&#41;](extensible-key-management-ekm.md)  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]でサード パーティのキー管理システムを使用する方法について説明します。  
  
## <a name="related-tasks"></a>Related Tasks  
 [サービスマスターキーのバックアップ](back-up-the-service-master-key.md)  
  
 [サービスマスターキーの復元](restore-the-service-master-key.md)  
  
 [データベースマスターキーの作成](create-a-database-master-key.md)  
  
 [データベースマスターキーのバックアップ](back-up-a-database-master-key.md)  
  
 [データベースマスターキーの復元](restore-a-database-master-key.md)  
  
 [2つのサーバーに同一の対称キーを作成する](create-identical-symmetric-keys-on-two-servers.md)  
  
 [Azure Key Vault &#40;SQL Server を使用した拡張キー管理&#41;](extensible-key-management-using-azure-key-vault-sql-server.md)  
  
 [EKM を使用して TDE を有効にする](enable-tde-on-sql-server-using-ekm.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 [CREATE MASTER KEY &#40;Transact-sql&#41;](/sql/t-sql/statements/create-master-key-transact-sql)  
  
 [ALTER SERVICE MASTER KEY &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-service-master-key-transact-sql)  
  
 [データベースマスターキーの復元](restore-a-database-master-key.md)  
  
## <a name="see-also"></a>参照  
 [暗号化キーのバックアップと復元 Reporting Services](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [SSRS Configuration Manager&#41;&#40;暗号化キーを削除して再作成します](../../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [SSRS Configuration Manager &#40;のスケールアウト配置に対する暗号化キーの追加と削除&#41;](../../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
 [Transparent Data Encryption &#40;TDE&#41;](transparent-data-encryption.md)  
  
  
