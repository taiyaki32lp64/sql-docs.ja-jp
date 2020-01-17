---
title: clr enabled サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- assemblies [CLR integration], verifying can run
- clr enabled option
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 71392e537cb034976b3c47d819897356e3bb58cb
ms.sourcegitcommit: 445842da7c7d216b94a9576e382164c67f54e19a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71682088"
---
# <a name="clr-enabled-server-configuration-option"></a>clr enabled サーバー構成オプション
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でユーザー アセンブリを実行できるかどうかを指定するには、clr enabled オプションを使用します。 clr enabled オプションでは、次の値を指定します。 
  
|[値]|Description|  
|-----------|-----------------|  
|0|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でアセンブリを実行できません。|  
|1|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でアセンブリを実行できます。|  
  
WOW64 のみ。 WOW64 サーバーを再起動して設定の変更を有効にします。 他の種類のサーバーでは、再起動は不要です。  

RECONFIGURE を実行し、clr enabled オプションの実行値が 1 から 0 に変更されると、ユーザー アセンブリが含まれているすべてのアプリケーション ドメインが直ちにアンロードされます。  
  
>  **簡易プーリングでは、共通言語ランタイム (CLR) の実行はサポートされていません** "clr enabled" または "lightweight pooling" のいずれかのオプションを無効にしてください。 CLR に依存していてファイバー モードで正しく動作しない機能には、**hierarchyid** データ型、`FORMAT` 関数、レプリケーション、およびポリシー ベースの管理があります。  
> 
> [!WARNING]
>  CLR では、セキュリティ境界としてサポートされなくなった、.NET Framework のコード アクセス セキュリティ (CAS) が使用されます。 `PERMISSION_SET = SAFE` で作成された CLR アセンブリが、外部のシステム リソースにアクセスし、非管理対象コードを呼び出し、sysadmin 特権を取得できる場合があります。 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 以降、CLR アセンブリのセキュリティを強化するために `clr strict security` という `sp_configure` オプションが導入されました。 `clr strict security` は既定で有効になり、`SAFE` および `EXTERNAL_ACCESS` アセンブリを `UNSAFE` とマークされている場合と同様に扱います。 `clr strict security` オプションは、旧バージョンとの互換性のために無効にできますが、これは推奨されません。 Microsoft では、master データベースで `UNSAFE ASSEMBLY` アクセス許可が付与されている対応するログインを含む証明書または非対称キーで、すべてのアセンブリに署名することをお勧めします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者は、データベース エンジンが信頼するアセンブリのリストにアセンブリを追加することもできます。 詳細については、「[sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md)」を参照してください。
  
## <a name="example"></a>例  
 次の例では、最初に clr enabled オプションの現在の設定を表示し、その後、オプションの値を 1 に設定することで、このオプションを有効にします。 このオプションを無効にするには、値を 0 に設定します。  
  
```sql  
EXEC sp_configure 'clr enabled';  
EXEC sp_configure 'clr enabled' , '1';  
RECONFIGURE;    
```  
  
## <a name="see-also"></a>参照  
 [lightweight pooling サーバー構成オプション](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [lightweight pooling サーバー構成オプション](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
  
