---
title: SQL Server の暗号化 | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], about encryption
- security [SQL Server], encryption
- cryptography [SQL Server], about cryptography
ms.assetid: ead0150e-4943-4ad5-84c8-36f85c7278f4
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e3fea2c9fdd532385378e2c66af08eefd4804442
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957316"
---
# <a name="sql-server-encryption"></a>SQL Server の暗号化
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  暗号化は、キーまたはパスワードを使用してデータを難読化するプロセスです。 暗号化によって、データは対応する暗号化解除キーまたはパスワードがないと使用できなくなります。 暗号化では、アクセス コントロールの問題は解決されません。 ただし、暗号化を使用すると、アクセス コントロールがバイパスされる場合でもデータ損失のリスクが限定されるので、セキュリティが強化されます。 たとえば、データベース ホスト コンピューターの構成が適切でない場合に、機密データをハッカーが入手したとしても、その情報が暗号化されていれば、ハッカーはその情報を使用できません。  
  

> [!IMPORTANT]  
>  暗号化は、セキュリティの強化に役立つ便利なツールですが、すべてのデータまたは接続に対して考慮すべきものではありません。 暗号化を実装するかどうかを検討する際は、ユーザーがデータにどのようにアクセスするかを考慮する必要があります。 ユーザーがパブリック ネットワーク経由でデータにアクセスする場合は、セキュリティを強化するためにデータの暗号化が必要になると考えられます。 一方、すべてのアクセスにセキュリティで保護されたイントラネット構成が使用される場合には、暗号化は必ずしも必要ありません。 暗号化を使用する場合は、それに伴ってパスワード、キー、および証明書のメンテナンス計画が必要になります。  
  
> [!NOTE]  
>  トランスポート層セキュリティ (TLS1.2) に関する最新情報は、「[Microsoft SQL Server 用の TLS 1.2 のサポート](https://support.microsoft.com/kb/3135244)」から入手できます。  

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、接続、データ、およびストアド プロシージャに対して暗号化を使用できます。 次のトピックでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] での暗号化の詳細が説明されています。  

 [暗号化階層](../../../relational-databases/security/encryption/encryption-hierarchy.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の暗号化階層について説明します。  
  
 [暗号化アルゴリズムの選択](../../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
 効果的な暗号化アルゴリズムを選択する方法について説明します。  
  
 [透過的なデータ暗号化 &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
 データを透過的に暗号化する方法に関する一般情報を提供します。  
  
 [SQL Server とデータベースの暗号化キー &#40;データベース エンジン&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の暗号化キーでは、公開キー、秘密キー、対称キーを組み合わせて機密データの保護に使用します。 このセクションでは、暗号化キーを実装および管理する方法について説明します。  
  
 [Always Encrypted &#40;データベース エンジン&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
 オンプレミスのデータベース管理者、クラウド データベース オペレーターなどを含む、高い特権を持つものの無許可のユーザーが暗号化データにアクセスできないようにします。  
  
 [動的なデータ マスキング](../../../relational-databases/security/dynamic-data-masking.md)  
 特権のないユーザーに対してデリケートなデータをマスクし、データの公開を制限します。  
  
 [SQL Server の証明書と非対称キー](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)  
 公開キー暗号化の使用に関する情報。  
  
## <a name="related-content"></a>関連コンテンツ  
 [SQL Server の保護](../../../relational-databases/security/securing-sql-server.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] プラットフォームを保護する方法、およびユーザーとセキュリティ保護可能なオブジェクトを操作する方法の概要を説明します。  

[Azure SQL Database のセキュリティ機能の概要](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview)
</br>データの保護、アクセスの制御、プロアクティブな監視に関する Azure SQL Database のセキュリティの概要を説明します。
  
 [暗号化関数 &#40;Transact-SQL&#41;](../../../t-sql/functions/cryptographic-functions-transact-sql.md)  
 暗号化機能を実装する方法について説明します。  
  
 [ENCRYPTBYPASSPHRASE &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbypassphrase-transact-sql.md)  
 パスワードを使用してデータを暗号化する方法について説明します。  
  
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)  
 対称キーを使用してデータを暗号化する方法について説明します。  
  
 [ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbyasymkey-transact-sql.md)  
 非対称キーを使用してデータを暗号化する方法について説明します。  
  
 [ENCRYPTBYCERT &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbycert-transact-sql.md)  
 証明書を使用してデータを暗号化する方法について説明します。  
  
## <a name="external-resources"></a>外部リソース  
 [Microsoft TechNet:SQL Server TechCenter:SQL Server 2012 - セキュリティと保護](https://download.microsoft.com/download/8/F/A/8FABACD7-803E-40FC-ADF8-355E7D218F4C/SQL_Server_2012_Security_Best_Practice_Whitepaper_Apr2012.docx)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のセキュリティに関する最新情報が掲載されています。  
  
## <a name="see-also"></a>参照  
 [sys.key_encryptions &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)   
 [SQL Server とデータベースの暗号化キー &#40;データベース エンジン&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [Reporting Services の暗号化キーのバックアップと復元](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)     
 [データベース エンジンへの暗号化接続の有効化](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)    
  
  
