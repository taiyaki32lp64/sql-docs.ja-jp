---
title: SQL Server の暗号化 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], about encryption
- security [SQL Server], encryption
- cryptography [SQL Server], about cryptography
ms.assetid: ead0150e-4943-4ad5-84c8-36f85c7278f4
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: f2aa6c25f8e8741308ff8f8b5df93cb2af67ad91
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957097"
---
# <a name="sql-server-encryption"></a>SQL Server の暗号化
  暗号化は、キーまたはパスワードを使用してデータを難読化するプロセスです。 暗号化によって、データは対応する暗号化解除キーまたはパスワードがないと使用できなくなります。 暗号化では、アクセス コントロールの問題は解決されません。 ただし、暗号化を使用すると、アクセス コントロールがバイパスされる場合でもデータ損失のリスクが限定されるので、セキュリティが強化されます。 たとえば、データベース ホスト コンピューターの構成が適切でない場合に、機密データをハッカーが入手したとしても、その情報が暗号化されていれば、ハッカーはその情報を使用できません。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、接続、データ、およびストアド プロシージャに対して暗号化を使用できます。 次の表に、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]での暗号化の詳細を示します。  
  
> [!IMPORTANT]  
>  暗号化は、セキュリティの強化に役立つ便利なツールですが、すべてのデータまたは接続に対して考慮すべきものではありません。 暗号化を実装するかどうかを検討する際は、ユーザーがデータにどのようにアクセスするかを考慮する必要があります。 ユーザーがパブリック ネットワーク経由でデータにアクセスする場合は、セキュリティを強化するためにデータの暗号化が必要になると考えられます。 一方、すべてのアクセスにセキュリティで保護されたイントラネット構成が使用される場合には、暗号化は必ずしも必要ありません。 暗号化を使用する場合は、それに伴ってパスワード、キー、および証明書のメンテナンス計画が必要になります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [暗号化階層](encryption-hierarchy.md)  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の暗号化階層について説明します。  
  
 [暗号化アルゴリズムの選択](choose-an-encryption-algorithm.md)  
 効果的な暗号化アルゴリズムを選択する方法について説明します。  
  
 [Transparent Data Encryption &#40;TDE&#41;](transparent-data-encryption.md)  
 データを透過的に暗号化する方法に関する一般情報を提供します。  
  
 [SQL Server とデータベースの暗号化キー &#40;データベースエンジン&#41;](sql-server-and-database-encryption-keys-database-engine.md)  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の暗号化キーでは、公開キー、秘密キー、対称キーを組み合わせて機密データの保護に使用します。 このセクションでは、暗号化キーを実装および管理する方法について説明します。  
  
## <a name="related-content"></a>関連コンテンツ  
 [SQL Server のセキュリティ保護](../securing-sql-server.md)  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] プラットフォームを保護する方法、およびユーザーとセキュリティ保護可能なオブジェクトを操作する方法の概要を説明します。  
  
 [暗号化関数 &#40;Transact-sql&#41;](/sql/t-sql/functions/cryptographic-functions-transact-sql)  
 暗号化機能を実装する方法について説明します。  
  
 [ENCRYPTBYPASSPHRASE &#40;Transact-sql&#41;](/sql/t-sql/functions/encryptbypassphrase-transact-sql)  
 パスワードを使用してデータを暗号化する方法について説明します。  
  
 [ENCRYPTBYKEY &#40;Transact-sql&#41;](/sql/t-sql/functions/encryptbykey-transact-sql)  
 対称キーを使用してデータを暗号化する方法について説明します。  
  
 [ENCRYPTBYASYMKEY &#40;Transact-sql&#41;](/sql/t-sql/functions/encryptbyasymkey-transact-sql)  
 非対称キーを使用してデータを暗号化する方法について説明します。  
  
 [ENCRYPTBYCERT &#40;Transact-sql&#41;](/sql/t-sql/functions/encryptbycert-transact-sql)  
 証明書を使用してデータを暗号化する方法について説明します。  
  
## <a name="external-resources"></a>外部リソース  
 [2005セキュリティを SQL Server するための10の手順](https://www.itprotoday.com/sql-server/10-steps-sql-server-2005-security)  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のセキュリティに関する最新情報が掲載されています。  
  
## <a name="see-also"></a>参照  
 [key_encryptions &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-key-encryptions-transact-sql)   
 [SQL Server とデータベースの暗号化キー &#40;データベースエンジン&#41;](sql-server-and-database-encryption-keys-database-engine.md)   
 [暗号化キーのバックアップと復元 Reporting Services](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
  
  
