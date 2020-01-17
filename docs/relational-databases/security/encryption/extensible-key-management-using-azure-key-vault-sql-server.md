---
title: Azure Key Vault を使用した拡張キー管理
description: 拡張キー管理用の SQL Server コネクタと SQL Server 用の Azure Key Vault を使用します。
ms.custom: seo-lt-2019
ms.date: 07/22/2016
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Extensible Key Management with key vault
- Transparent Data Encryption, using EKM and key vault
- EKM, with key vault
- TDE, EKM and key vault
- Key Management with key vault
- SQL Server Connector, about
ms.assetid: 3efdc48a-8064-4ea6-a828-3fbf758ef97c
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: df42a2d0f7dea2e32df61670aff88374a6fcff54
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558066"
---
# <a name="extensible-key-management-using-azure-key-vault-sql-server"></a>Azure Key Vault を使用する拡張キー管理 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 用の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタを使用すると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の暗号化において、Azure Key Vault サービスを[拡張キー管理 &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md) プロバイダーに使用して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の暗号化キーを保護することができます。  
  
 このトピックでは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタについて説明します。 その他の情報については、「 [Azure Key Vault を使用した拡張キー管理のセットアップ手順](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)」、「 [SQL 暗号化機能への SQL Server コネクタの使用](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)」、「 [SQL Server コネクタのメンテナンスとトラブルシューティング](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)」を参照してください。  
  
##  <a name="Uses"></a> 拡張キー管理 (EKM) の概要と用途  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、[Transparent Data Encryption &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)、[列レベルの暗号化 (CLE)](../../../t-sql/functions/cryptographic-functions-transact-sql.md)、[バックアップの暗号化](../../../relational-databases/backup-restore/backup-encryption.md)など、機密データの保護に有効ないくつかの種類の暗号化が用意されています。 いずれのケースも、この従来のキー階層では、対称データ暗号化キー (DEK) を使用してデータが暗号化されます。 対称なデータ暗号化キーは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に格納されたキーの階層で暗号化することにより、さらに保護されます。 このモデルに代わるのが、EKM プロバイダー モデルです。 EKM プロバイダーのアーキテクチャでは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の外側にある外部暗号化サービス プロバイダーに格納された非対称キーを使用して、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でデータの暗号化キーを保護することができます。 このモデルによって、セキュリティの層が拡充され、キーとデータの管理が分離されます。  
   
 次の図は、従来のサービスにおけるキー管理階層と Azure Key Vault システムとを比較したものです。  
  
 ![ekm-key-hierarchy-traditional](../../../relational-databases/security/encryption/media/ekm-key-hierarchy-traditional.png "ekm-key-hierarchy-traditional")  
  
   
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタが、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と Azure Key Vault の橋渡し的役割を担うことで、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、Azure Key Vault サービスのスケーラビリティ、高パフォーマンス、高可用性を活かすことができます。 以下の図は、EKM プロバイダー アーキテクチャにおけるキーの階層が、Azure Key Vault および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コネクタと連動するようすを表しています。  
  
  Azure Key Vault は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Azure Virtual Machines 上の [!INCLUDE[msCoName](../../../includes/msconame-md.md)] インストール環境で使用したり、オンプレミス サーバー用に使用したりすることが可能です。 また、資格情報コンテナー サービスでは、厳密な管理および監視下にあるハードウェア セキュリティ モジュール (HSM) を使用し、非対称暗号化キーをより高いレベルで保護するオプションも提供します。 資格情報コンテナーの詳細については、「 [Azure Key Vault](https://go.microsoft.com/fwlink/?LinkId=521401)」を参照してください。  
  
 次の図は、Key Vault を使用した EKM のプロセス フローについてまとためものです。 (図の中にプロセス手順番号が示されていますが、図の後に示す設定手順の番号と対応しているわけではありません。)  
  
 ![Azure Key Vault を使用した SQL Server EKM](../../../relational-databases/security/encryption/media/ekm-using-azure-key-vault.png "Azure Key Vault を使用した SQL Server EKM")  

> [!NOTE]  
>  1\.0.0.440 以前のバージョンは置き換えられ、実稼働環境ではサポートされなくなりました。 [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=45344)にアクセスし、[[SQL Server コネクタのメンテナンスとトラブルシューティング]](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) ページの "SQL Server コネクタのアップグレード" に示されている手順を使用して、バージョン 1.0.1.0 以降にアップグレードしてください。
  
 次の手順については、「 [Azure Key Vault を使用した拡張キー管理のセットアップ手順](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)」を参照してください。  
  
 使用シナリオについては、「 [SQL 暗号化機能への SQL Server コネクタの使用](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server コネクタのメンテナンスとトラブルシューティング](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  
