---
title: データベース ミラーリング エンドポイントでの証明書の使用
descriptoin: Steps to configure the use of a certificate on both inbound and outbound connections for a SQL Server database mirroring endpoint.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- certificates [SQL Server], database mirroring
- authentication [SQL Server], database mirroring
- database mirroring [SQL Server], security
ms.assetid: f7c23cc2-48dc-4b78-b441-89ca29a0bd9e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d263276c392ef4fb40682b832cf94237694d94ac
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822327"
---
# <a name="use-certificates-for-a-database-mirroring-endpoint-transact-sql"></a>データベース ミラーリング エンドポイントでの証明書の使用 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  あるサーバー インスタンスのデータベース ミラーリングで証明書による認証を有効にするには、システム管理者は、各サーバー インスタンスが発信接続と着信接続の両方で証明書を使用するように構成する必要があります。 この場合、発信接続を最初に構成する必要があります。  
  
> [!NOTE]  
>  1 つのサーバー インスタンス上のすべてのミラーリング接続では、1 つのデータベース ミラーリング エンドポイントが使用されます。そのため、エンドポイントを作成する際にサーバー インスタンスの認証方法を指定する必要があります。 したがって、データベース ミラーリング用の認証は、サーバー インスタンスあたりに 1 つしか使用できません。  
  
## <a name="configuring-outbound-connections"></a>発信接続の構成  
 データベース ミラーリング用に構成する各サーバー インスタンスで、次の手順を実行します。  
  
1.  **master** データベースで、データベース マスター キーを作成します。  
  
2.  **master** データベースで、暗号化された証明書をサーバー インスタンスに作成します。  
  
3.  作成した証明書を使用して、サーバー インスタンスのエンドポイントを作成します。  
  
4.  証明書をファイルにバックアップし、そのファイルをセキュリティで保護された状態で他のシステムにコピーします。  
  
 パートナーおよびミラーリング監視サーバーがある場合は、それぞれで上記の手順を完了する必要があります。  
  
 詳細については、「 [データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)を使用します。  
  
## <a name="configuring-inbound-connections"></a>着信接続の構成  
 次に、データベース ミラーリング用に構成する各パートナーで、次の手順を実行します。 **master** データベースで、次の作業を行います。  
  
1.  他のシステムへのログインを作成します。  
  
2.  そのログインのユーザー名を作成します。  
  
3.  他のサーバー インスタンスのミラーリング エンドポイント用の証明書を入手します。  
  
4.  手順 2. で作成したユーザーに証明書を関連付けます。  
  
5.  ミラーリング エンドポイント用のログインに CONNECT 権限を許可します。  
  
 ミラーリング監視サーバーがある場合は、このサーバーでも着信接続の構成を行う必要があります。 この場合、どちらのパートナーのミラーリング監視サーバーでも、相手のログイン、ユーザー、証明書が必要です。  
  
 詳細については、「 [データベース ミラーリング エンドポイントで着信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)を使用します。  
  
## <a name="security"></a>Security  
 ネットワークがセキュリティで保護されていることを保証できる場合を除いて、データベース ミラーリング接続に対して暗号化を使用することをお勧めします。 詳細については、「 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)のインスタンスに AlwaysOn 可用性グループを作成する方法について説明します。  
  
 証明書を別のシステムにコピーする場合は、セキュリティで保護されたコピー方法を使用してください。 すべての証明書をセキュリティで保護された状態で保管するよう十分に注意してください。  
  
## <a name="see-also"></a>参照  
 [データベース マスター キーの作成](../../relational-databases/security/encryption/create-a-database-master-key.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [データベース ミラーリングと Always On 可用性グループのトランスポート セキュリティ &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
