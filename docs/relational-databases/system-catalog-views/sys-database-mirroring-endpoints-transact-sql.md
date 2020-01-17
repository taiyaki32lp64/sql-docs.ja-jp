---
title: sys.database_mirroring_endpoints (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring_endpoints_TSQL
- database_mirroring_endpoints
- sys.database_mirroring_endpoints
- database_mirroring_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], endpoint
- HADR [SQL Server], endpoint
- database mirroring [SQL Server], catalog views
- sys.database_mirroring_endpoints catalog view
ms.assetid: f2285199-97ad-473c-a52d-270044dd862b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bcbe9d23bab18e47b69f82812f604a94d4c5ce9c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022770"
---
# <a name="sysdatabasemirroringendpoints-transact-sql"></a>sys.database_mirroring_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベースのインスタンスのミラーリング エンドポイントの 1 つの行を含む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
> [!NOTE]  
>  データベース ミラーリング エンドポイントには、ミラーリング監視サーバーとデータベース ミラーリング パートナー間のセッションと Always On 可用性グループのプライマリ レプリカとセカンダリ レプリカ間のセッションの両方がサポートしています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<列を継承 >**|-|列を継承**sys.endpoints** (詳細については、次を参照してください。 [sys.endpoints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md))。|  
|**role**|**tinyint**|ミラーリング ロール。次のいずれかになります。<br /><br /> **0** = なし<br /><br /> **1**パートナーを =<br /><br /> **2** = ミラーリング監視サーバー<br /><br /> **3** = all<br /><br /> 注:この値は、データベース ミラーリングのみ関連します。|  
|**role_desc**|**nvarchar(60)**|ミラーリング ロールの説明。次のいずれかになります。<br /><br /> **NONE**<br /><br /> **パートナー**<br /><br /> **ミラーリング監視サーバー**<br /><br /> **ALL**<br /><br /> 注:この値は、データベース ミラーリングのみ関連します。|  
|**is_encryption_enabled**|**bit**|**1**その暗号化が有効になっていることを意味します。<br /><br /> **0**その暗号化が無効になっていることを意味します。|  
|**connection_auth**|**tinyint**|エンドポイントへの接続に必要な接続認証の種類。次のいずれかになります。<br /><br /> **1** - NTLM<br /><br /> **2** -KERBEROS<br /><br /> **3** -ネゴシエート<br /><br /> **4** -証明書<br /><br /> **5** -NTLM、CERTIFICATE<br /><br /> **6** -KERBEROS、CERTIFICATE<br /><br /> **7** -NEGOTIATE、CERTIFICATE<br /><br /> **8** -CERTIFICATE、NTLM<br /><br /> **9** -証明書、KERBEROS<br /><br /> **10** -CERTIFICATE、NEGOTIATE|  
|**connection_auth_desc**|**Nvarchar (60)**|このエンドポイントは、のいずれかへの接続に必要な認証の種類の説明です。<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> ネゴシエート<br /><br /> CERTIFICATE<br /><br /> NTLM、CERTIFICATE<br /><br /> KERBEROS、CERTIFICATE<br /><br /> NEGOTIATE、CERTIFICATE<br /><br /> CERTIFICATE、NTLM<br /><br /> CERTIFICATE、KERBEROS<br /><br /> CERTIFICATE、NEGOTIATE|  
|**certificate_id**|**int**|認証で使用される証明書の ID (存在する場合)。<br /><br /> 0 = Windows 認証が使用されます。|  
|**encryption_algorithm**|**tinyint**|暗号化アルゴリズム。次のいずれかになります。<br /><br /> **0** -なし<br /><br /> **1** -RC4<br /><br /> **2** -AES<br /><br /> **3** -NONE、RC4<br /><br /> **4** -NONE、AES<br /><br /> **5** -RC4、AES<br /><br /> **6** -AES、RC4<br /><br /> **7** -NONE、RC4、AES<br /><br /> **8** -NONE、AES、RC4|  
|**encryption_algorithm_desc**|**nvarchar(60)**|いずれかの暗号化アルゴリズムの説明です。<br /><br /> なし<br /><br /> RC4<br /><br /> AES<br /><br /> NONE、RC4<br /><br /> NONE、AES<br /><br /> RC4、AES<br /><br /> AES、RC4<br /><br /> NONE、RC4、AES<br /><br /> NONE、AES、RC4|  
  
## <a name="remarks"></a>コメント  
  
> [!NOTE]  
>  RC4 アルゴリズムは、旧バージョンとの互換性のためにのみサポートされています。 データベース互換性レベルが 90 または 100 の場合、新しい素材は RC4 または RC4_128 を使用してのみ暗号化できます (非推奨)。AES アルゴリズムのいずれかなど、新しいアルゴリズムを使用してください。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]以降では、どの互換性レベルでも、RC4 または RC4_128 を使用して暗号化された素材を解除できます。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [追加または可用性レプリカを変更する場合は、エンドポイント URL の指定&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)   
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [sys.database_mirroring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [SQL Server システム カタログに対するクエリに関してよくあるご質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
