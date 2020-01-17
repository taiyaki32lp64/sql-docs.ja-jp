---
title: CLR の厳密なセキュリティ | Microsoft Docs
description: SQL Server で CLR の厳密なセキュリティを構成する方法
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- clr strict security
- clr_strict_security_TSQL
- clr strict security
- strict_security_TSQL
helpviewer_keywords:
- assemblies [CLR integration], strick security
- clr strict security option
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4c77d87f1ffe0083662f9f4fcfe643de3359ea59
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68012973"
---
# <a name="clr-strict-security"></a>CLR の厳密なセキュリティ   
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で `SAFE`、`EXTERNAL ACCESS`、`UNSAFE` のアクセス許可の解釈を制御します。   

|[値] |Description | 
|----- |----- | 
|0 |無効 - 旧バージョンとの互換性のために提供されています。 `Disabled` 値の使用はお勧めしません。 | 
|1 |有効 - [!INCLUDE[ssde-md](../../includes/ssde-md.md)]がアセンブリの `PERMISSION_SET` の情報を無視し、常に `UNSAFE` と解釈するようになります。  [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] の既定値は `Enabled` です。 | 

> [!WARNING]
>  CLR では、セキュリティ境界としてサポートされなくなった、.NET Framework のコード アクセス セキュリティ (CAS) が使用されます。 `PERMISSION_SET = SAFE` で作成された CLR アセンブリが、外部のシステム リソースにアクセスし、非管理対象コードを呼び出し、sysadmin 特権を取得できる場合があります。 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 以降、CLR アセンブリのセキュリティを強化するために `clr strict security` という `sp_configure` オプションが導入されました。 `clr strict security` は既定で有効になり、`SAFE` および `EXTERNAL_ACCESS` アセンブリを `UNSAFE` とマークされている場合と同様に扱います。 `clr strict security` オプションは、旧バージョンとの互換性のために無効にできますが、これは推奨されません。 Microsoft では、master データベースで `UNSAFE ASSEMBLY` アクセス許可が付与されている対応するログインを含む証明書または非対称キーで、すべてのアセンブリに署名することをお勧めします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者は、データベース エンジンが信頼するアセンブリのリストにアセンブリを追加することもできます。 詳細については、「[sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md)」を参照してください。

## <a name="remarks"></a>Remarks   

有効にすると、`CREATE ASSEMBLY` および `ALTER ASSEMBLY` のステートメントの `PERMISSION_SET` オプションが実行時に無視されますが、`PERMISSION_SET` オプションはメタデータに保持されます。 オプションを無視すると、既存のコード ステートメントの改変が最小限に抑えられます。

`CLR strict security` は `advanced option` です。  

> [!IMPORTANT]
>  厳密なセキュリティを有効にした場合、未署名のアセンブリの読み込みは失敗します。 各アセンブリを変更または削除して再作成して、サーバーでの `UNSAFE ASSEMBLY` アクセス許可のある対応するログインを含む証明書または非対称キーで署名されるようにする必要があります。

## <a name="permissions"></a>アクセス許可 

### <a name="to-change-this-option"></a>このオプションを変更するには  
`CONTROL SERVER` アクセス許可、または `sysadmin` 固定サーバー ロールのメンバーシップが必要です。

### <a name="to-create-an-clr-assembly"></a>CLR アセンブリを作成するには   
`CLR strict security` が有効になっている場合に CLR アセンブリを作成するには、次のアクセス許可が必要です。

- ユーザーには `CREATE ASSEMBLY` アクセス許可が必要です  
- さらに、次の条件のいずれかを満たす必要があります。  
  - サーバーでの `UNSAFE ASSEMBLY` アクセス許可のある対応するログインを含む証明書または非対称キーでアセンブリが署名されている。 アセンブリへの署名は推奨されます。  
  - データベースに `ON` に設定された `TRUSTWORTHY` プロパティが含まれ、そのデータベースがサーバーでの `UNSAFE ASSEMBLY` アクセス許可のあるログインによって所有されている。 このオプションは推奨されません。  

  
## <a name="see-also"></a>参照  
  
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [clr enabled サーバー構成オプション](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)
