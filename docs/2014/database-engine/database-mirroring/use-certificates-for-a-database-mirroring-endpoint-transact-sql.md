---
title: データベース ミラーリング エンドポイントでの証明書の使用 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 116c5d900cf56d89c01bbf333d2d8bd3905aa371
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754024"
---
# <a name="use-certificates-for-a-database-mirroring-endpoint-transact-sql"></a>データベース ミラーリング エンドポイントでの証明書の使用 (Transact-SQL)
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
  
 詳細については、「 [データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md)を使用します。  
  
## <a name="configuring-inbound-connections"></a>着信接続の構成  
 次に、データベース ミラーリング用に構成する各パートナーで、次の手順を実行します。 **master** データベースで、次の作業を行います。  
  
1.  他のシステムへのログインを作成します。  
  
2.  そのログインのユーザー名を作成します。  
  
3.  他のサーバー インスタンスのミラーリング エンドポイント用の証明書を入手します。  
  
4.  手順 2. で作成したユーザーに証明書を関連付けます。  
  
5.  ミラーリング エンドポイント用のログインに CONNECT 権限を許可します。  
  
 ミラーリング監視サーバーがある場合は、このサーバーでも着信接続の構成を行う必要があります。 この場合、どちらのパートナーのミラーリング監視サーバーでも、相手のログイン、ユーザー、証明書が必要です。  
  
 詳細については、「 [データベース ミラーリング エンドポイントで着信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md)を使用します。  
  
## <a name="security"></a>セキュリティ  
 ネットワークがセキュリティで保護されていることを保証できる場合を除いて、データベース ミラーリング接続に対して暗号化を使用することをお勧めします。 詳細については、「 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)」を参照してください。  
  
 証明書を別のシステムにコピーする場合は、セキュリティで保護されたコピー方法を使用してください。 すべての証明書をセキュリティで保護された状態で保管するよう十分に注意してください。  
  
## <a name="see-also"></a>参照  
 [データベース マスター キーの作成](../../relational-databases/security/encryption/create-a-database-master-key.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)   
 [データベース ミラーリングと AlwaysOn 可用性グループのトランスポート セキュリティ&#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)   
 [SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)  
  
  
