---
title: トランスポート セキュリティ:可用性グループとデータベース ミラーリング
description: SQL Server でホストされている Always On 可用性グループまたはデータベース ミラーリング セッションに参加しているデータベース間で交換されるメッセージのトランスポートを、セキュリティで保護する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- sessions [SQL Server], database mirroring
- cryptography [SQL Server], database mirroring
- certificates [SQL Server], database mirroring
- encryption [SQL Server], database mirroring
- Windows authentication [SQL Server]
- authentication [SQL Server], database mirroring
- transport security
- database mirroring [SQL Server], security
ms.assetid: 49239d02-964e-47c0-9b7f-2b539151ee1b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 85ca560e24fac75897d0b65946121e3ca4251e20
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252750"
---
# <a name="transport-security---database-mirroring---always-on-availability"></a>トランスポート セキュリティ - データベース ミラーリング - AlwaysOn 可用性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  トランスポート セキュリティには認証が必要です。状況によっては、複数のデータベース間で交換されるメッセージの暗号化も必要になります。 データベース ミラーリングおよび [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]では、認証と暗号化はデータベース ミラーリング エンドポイントで構成します。 データベース ミラーリング エンドポイントの概要については、「 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   [認証](#Authentication)  
  
-   [データの暗号化](#DataEncryption)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="Authentication"></a> [認証]  
 認証とは、ユーザーが本人であるかどうかを検査するプロセスです。 データベース ミラーリング エンドポイント間の接続には、認証が必要になります。 パートナーまたはミラーリング監視サーバーから接続を要求された場合は、その接続要求を認証する必要があります。  
  
 サーバー インスタンスによりデータベース ミラーリングまたは [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] に使用される認証の種類は、データベース ミラーリング エンドポイントのプロパティで指定します。 データベース ミラーリング エンドポイントに使用できるトランスポート セキュリティには、次の 2 種類があります:Windows 認証 (セキュリティ サポート プロバイダー インターフェイス (SSPI)) と証明書ベース認証。  
  
### <a name="windows-authentication"></a>[Windows 認証]  
 Windows 認証では、各サーバー インスタンスが相手側のインスタンスにログインする際には、プロセスを実行している Windows ユーザー アカウントの Windows 資格情報が使用されます。 Windows 認証では、次のように、ログイン アカウントの手動による構成が必要になる場合があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが同じドメイン アカウントでサービスとして実行される場合、追加の構成は必要ありません。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが (同じドメインまたは信頼関係のあるドメインの) 異なるドメイン アカウントでサービスとして実行される場合、他の各サーバー インスタンス上の **master** に各アカウントのログインを作成する必要があります。また、そのログインには、エンドポイントに対する CONNECT 権限を与える必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスがネットワーク サービス アカウントとして実行される場合、他の各サーバー上の_master_ **\\** _に各ホスト コンピューター アカウント (_ DomainName **ComputerName$** ) のログインを作成する必要があります。また、そのログインには、エンドポイントに対する CONNECT 権限を与える必要があります。 これは、ネットワーク サービス アカウントで実行されているサーバー インスタンスではホスト コンピューターのドメイン アカウントを使用して認証を行うためです。  
  
> [!NOTE]  
>  Windows 認証を使用したデータベース ミラーリング セッションの設定例については、「[Windows 認証を使用したデータベース ミラーリングの設定の例 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-windows-authentication-transact-sql.md)」を参照してください。  
  
### <a name="certificates"></a>証明書  
 サーバー インスタンスが信頼されたドメインに存在しない場合や、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がローカル サービスとして実行されている場合など、一部の状況では Windows 認証を使用できません。 そのような場合には、接続要求を認証するときに、ユーザーの資格情報ではなく証明書が必要になります。 各サーバー インスタンスのミラーリング エンドポイントは、ローカルで作成された独自の証明書を使用して構成する必要があります。  
  
 暗号化方法は、証明書の作成時に設定されます。 詳細については、「 [データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)を使用します。 使用する証明書は慎重に管理してください。  
  
 接続を設定するときに、サーバー インスタンスにより、独自の証明書の秘密キーを使用して ID が作成されます。 接続要求を受け取るサーバー インスタンスでは、送信者の証明書の公開キーを使用して送信者の ID を認証します。 たとえば、Server_A と Server_B という 2 つのサーバー インスタンスを考えてみます。 Server_A では、Server_B に接続要求を送信する前に、秘密キーを使用して接続ヘッダーを暗号化します。 Server_B では、Server_A の証明書の公開キーを使用して接続ヘッダーの暗号化を解除します。 暗号化が解除されたヘッダーが正しい場合、Server_B は、そのヘッダーが Server_A によって暗号化されていたので、接続は認証されると認識します。 暗号化が解除されたヘッダーが正しくない場合、Server_B は、接続要求が認証されないため、接続が拒否されると認識します。  
  
##  <a name="DataEncryption"></a> データの暗号化  
 既定では、データベース ミラーリング エンドポイントは、ミラーリング接続経由で送信されるデータの暗号化を必要とします。 このようなエンドポイントの接続対象となるエンドポイントも暗号化を使用している必要があります。 ネットワークの安全性を保証できる場合を除いて、データベース ミラーリング接続に対して暗号化を使用することをお勧めします。 暗号化は、無効にしたり、必須ではない状態でサポートすることもできます。 暗号化が無効になっていると、データは暗号化されず、エンドポイントは暗号化を必要とするエンドポイントに接続できません。 暗号化がサポートされている場合は、相手側のエンドポイントによって暗号化がサポートまたは必要とされている場合にのみデータが暗号化されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で作成されるミラーリング エンドポイントは、暗号化が必須または無効の状態で作成されます。 暗号化の設定を SUPPORTED に変更するには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの ALTER ENDPOINT を使用します。 詳細については、「 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)」を参照してください。  
  
 必要に応じて、エンドポイントで使用可能な暗号化アルゴリズムを管理できます。それには、CREATE ENDPOINT ステートメントまたは ALTER ENDPOINT ステートメントの ALGORITHM オプションに、次のいずれかの値を指定します。  
  
|ALGORITHM の値|[説明]|  
|---------------------|-----------------|  
|RC4|エンドポイントで RC4 アルゴリズムを使用する必要があることを指定します。 これは既定値です。<br /><br /> <strong>\*\* 警告 \*\*</strong> RC4 アルゴリズムは推奨されません。 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] AES を使用することをお勧めします。|  
|AES|エンドポイントで AES アルゴリズムを使用する必要があることを指定します。|  
|AES RC4|2 つのエンドポイントが、AES アルゴリズムを優先するこのエンドポイントと暗号化アルゴリズムについてネゴシエートすることを指定します。|  
|RC4 AES|2 つのエンドポイントで暗号化アルゴリズムをネゴシエートし、このエンドポイントでは RC4 アルゴリズムを優先することを示します。|  
  
 接続するエンドポイントで 2 つのアルゴリズムが異なる順序で指定されている場合、接続を受け入れる側のエンドポイントの指定が優先されます。  
  
> [!NOTE]  
>  RC4 アルゴリズムは、旧バージョンとの互換性のためにのみサポートされています。 データベース互換性レベルが 90 または 100 の場合、新しい素材は RC4 または RC4_128 を使用してのみ暗号化できます (非推奨)。AES アルゴリズムのいずれかなど、新しいアルゴリズムを使用してください。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降のバージョンでは、どの互換性レベルでも、RC4 または RC4_128 を使用して暗号化された素材を暗号化解除できます。  
>   
>  RC4 は、AES よりもかなり高速ですが、比較的弱いアルゴリズムです。それに対して、AES は比較的強いアルゴリズムです。 したがって、AES アルゴリズムを使用することをお勧めします。  
  
 暗号化を指定する [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文の詳細については、「[CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **データベース ミラーリング エンドポイントのトランスポート セキュリティを構成するには**  
  
-   [Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
## <a name="see-also"></a>参照  
 [暗号化アルゴリズムの選択](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [DROP ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-endpoint-transact-sql.md)   
 [SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [データベースを別のサーバー インスタンスで使用できるようにするときのメタデータの管理 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)   
 [sys.dm_db_mirroring_connections &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-connections.md)   
 [データベース ミラーリング構成のトラブルシューティング &#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)   
 [AlwaysOn 可用性グループの構成のトラブルシューティング &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
