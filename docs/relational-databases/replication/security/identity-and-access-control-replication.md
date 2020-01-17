---
title: ID およびアクセス制御 (レプリケーション) | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- access controls [SQL Server replication]
- security [SQL Server replication], identity and access control
- authentication [SQL Server replication]
- identity [Replication]
ms.assetid: 4da0e793-1ee4-4f69-a80b-45c6732a238d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 2bb56fedd47434f865bc8121cd906a73528f5c1c
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769620"
---
# <a name="identity-and-access-control-replication"></a>ID およびアクセス制御 (レプリケーション)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  認証とは、あるエンティティ (ここでは、一般的にコンピューターを指します) によって、別のエンティティ ( *プリンシパル*とも呼ばれます。一般的に別のコンピューターまたはユーザーを指します) が自称するエンティティであるかどうかを確認するプロセスです。 承認とは、認証されたプリンシパルにリソース (ファイル システムのファイルやデータベースのテーブルなど) へのアクセスを認めるプロセスです。  
  
 レプリケーション セキュリティでは、認証と承認を使用して、レプリケートされたデータベース オブジェクトへのアクセスや、レプリケーション処理に関係するコンピューターやエージェントへのアクセスを制御します。 これは、以下の 3 つのメカニズムによって実現されます。  
  
-   エージェント セキュリティ  
  
     レプリケーション エージェントのセキュリティ モデルでは、レプリケーション エージェントの実行や接続に使用されるアカウントをきめ細かく制御できます。 エージェント セキュリティ モデルの詳細については、「 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)」を参照してください。 
  
-   管理ロール  
  
     レプリケーションのセットアップ、メンテナンス、および処理に対して適切なサーバー ロールやデータベース ロールが使用されていることを確認します。 詳細については、「 [Security Role Requirements for Replication](../../../relational-databases/replication/security/security-role-requirements-for-replication.md)」を参照してください。  
  
-   パブリケーション アクセス リスト (PAL)  
  
     パブリケーションへのアクセスは、PAL を通じて許可されます。 PAL は、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows のアクセス制御リストによく似た機能を備えています。 サブスクライバーがパブリッシャーやディストリビューターに接続し、パブリケーションへのアクセスを要求すると、エージェントによって渡された認証情報が PAL に対して確認されます。 PAL の詳細および推奨事項については、「[Secure the Publisher](../../../relational-databases/replication/security/secure-the-publisher.md)」(パブリッシャーのセキュリティ保護) を参照してください。  
  
## <a name="filtering-published-data"></a>パブリッシュされたデータのフィルター選択  
 レプリケーションでは、レプリケートされたデータやオブジェクトへのアクセスを認証と承認を使用して制御する以外に、列のフィルター選択と行のフィルター選択という 2 つのオプションを使用して、サブスクライバーで利用できるようにするデータを制御できます。 フィルター選択の詳細については、「[パブリッシュされたデータのフィルター選択](../../../relational-databases/replication/publish/filter-published-data.md)」を参照してください。  
  
 アーティクルを定義する際には、パブリケーションに必要な列のみをパブリッシュして、不要な列や機密データを含む列を除外することができます。 たとえば、Adventure Works データベースの **Customer** テーブルを現場の販売担当者にパブリッシュする際には、経営陣以外には関係のない **AnnualSales** 列を除外できます。  
  
 パブリッシュされたデータをフィルター選択することによって、データへのアクセスを制限し、サブスクライバーで使用できるデータを指定できます。 たとえば、 **Customer** テーブルをフィルター選択して、 **ShareInfo** 列の値が "yes" の顧客に関する情報のみをパートナー企業に提供することなどが可能です。 マージ レプリケーションにおいて HOST_NAME() を含むパラメーター化されたフィルターを使用する場合は、セキュリティ上の留意事項があります。 詳細については、「 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」の「HOST_NAME() によるフィルター選択」を参照してください。  

## <a name="manage-logins-and-passwords-in-replication"></a>レプリケーションのログインとパスワードの管理
レプリケーションを構成する際には、レプリケーション エージェントのログインとパスワードを指定します。 レプリケーションの構成後は、ログインとパスワードを変更できます。 詳細については、「 [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)」を参照してください。 レプリケーション エージェントで使用されるアカウントのパスワードを変更する場合は、[sp_changereplicationserverpasswords &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql.md) を実行します。  

グループのマネージド サービス アカウント (gMSA) の使用のサポートは、SQL Server 2014 で導入されました。 詳細については、ブログ「[Replication and group Managed Service Accounts](https://repltalk.com/2019/03/26/replication-and-group-managed-service-accounts/)」 (レプリケーションとグループのマネージド サービス アカウント) を参照してください。
  
## <a name="see-also"></a>参照  
 [脅威と脆弱性の対策 &#40;レプリケーション&#41;](../../../relational-databases/replication/security/threat-and-vulnerability-mitigation-replication.md) [レプリケーション エージェントのセキュリティ モデル](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [レプリケーション セキュリティの推奨事項](../../../relational-databases/replication/security/replication-security-best-practices.md)   

  
  
