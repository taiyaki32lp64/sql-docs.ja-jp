---
title: sp_add_trusted_assembly (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_trusted_assembly_TSQL
- sp_add_trusted_assembly
- sys.sp_add_trusted_assembly_TSQL
- sys.sp_add_trusted_assembly
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_add_trusted_assembly
ms.assetid: ''
author: VanMSFT
ms.author: vanto
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb34a814780a46c12c65948bd0b552effaacda4d
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452873"
---
# <a name="syssp_add_trusted_assembly-transact-sql"></a>sp_add_trusted_assembly (Transact-sql)  
[!INCLUDE[tsql-appliesto-ss2017-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdbmi-xxxx-xxx-md.md)]

サーバーの信頼されたアセンブリの一覧にアセンブリを追加します。

 ![トピックリンクアイコン](../../database-engine/configure-windows/media/topic-link.gif "トピックリンクアイコン") [Transact-sql 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>構文
```  
sp_add_trusted_assembly 
    [ @hash = ] 'value'
    [ , [ @description = ] 'description' ]
```  

## <a name="remarks"></a>備考  

この手順では、 [trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)にアセンブリを追加します。

## <a name="arguments"></a>[引数]

[@hash =]'*value*'  
サーバーの信頼されたアセンブリの一覧に追加するアセンブリの SHA2_512 ハッシュ値。 アセンブリが署名されていないか、データベースが信頼できるものとしてマークされていない場合でも、 [CLR strict security](../../database-engine/configure-windows/clr-strict-security.md)が有効になっていると、信頼されたアセンブリが読み込まれる

[@description =]'*description*'  
アセンブリに関するオプションのユーザー定義の説明。 信頼するアセンブリの簡易名、バージョン番号、カルチャ、公開キー、およびアーキテクチャをエンコードする正規名を使用することをお勧めします。 この値は、共通言語ランタイム (CLR) 側でアセンブリを一意に識別し、clr_name の値と同じです。 

## <a name="permissions"></a>Permissions

@No__t-0 固定サーバーロールまたは `CONTROL SERVER` 権限のメンバーシップが必要です。

## <a name="examples"></a>使用例  

次の例では、サーバーの信頼されたアセンブリの一覧に `pointudt` という名前のアセンブリを追加します。 これらの値は、 [sys. アセンブリ](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)から入手できます。     

```  
EXEC sp_add_trusted_assembly 0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC, 
N'pointudt, version=0.0.0.0, culture=neutral, publickeytoken=null, processorarchitecture=msil';
```  

## <a name="see-also"></a>「  
  [sp_drop_trusted_assembly](sys-sp-drop-trusted-assembly-transact-sql.md)  
  [trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)  
  [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  [CLR strict security](../../database-engine/configure-windows/clr-strict-security.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

