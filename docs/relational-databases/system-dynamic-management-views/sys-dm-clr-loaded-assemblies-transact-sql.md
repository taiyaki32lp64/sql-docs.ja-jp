---
title: sys.dm_clr_loaded_assemblies (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_clr_loaded_assemblies
- sys.dm_clr_loaded_assemblies_TSQL
- dm_clr_loaded_assemblies_TSQL
- sys.dm_clr_loaded_assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_loaded_assemblies dynamic management view
ms.assetid: 8523d8db-d8a0-4b1f-ae19-6705d633e0a6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1cd677e516048aa52badec7fc9875e5a5b13f25a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138657"
---
# <a name="sysdmclrloadedassemblies-transact-sql"></a>sys.dm_clr_loaded_assemblies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  サーバーのアドレス空間に読み込まれたマネージド ユーザー アセンブリごとに 1 行のデータを返します。 このビューを理解し、CLR 統合のトラブルシューティングを行うで実行されているデータベース オブジェクトが管理されている[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
 アセンブリは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド データベース オブジェクトの定義や配置のために使用されるマネージド コード DLL ファイルです。 これらのマネージ データベース オブジェクトのいずれかをユーザーが実行されるたびに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CLR がマネージ データベース オブジェクトが定義されているアセンブリ (とその参照) を読み込むとします。 アセンブリは、パフォーマンス向上のために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に読み込まれたままになるので、その後は、アセンブリを再度読み込まなくても、アセンブリに含まれているマネージド データベース オブジェクトを呼び出すことができます。 アセンブリがまでアンロードされません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メモリが不足します。 アセンブリと CLR 統合の詳細については、次を参照してください。 [CLR ホスト環境](../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)します。 マネージ データベース オブジェクトの詳細については、次を参照してください。[共通言語ランタイムによるデータベース オブジェクトの構築&#40;CLR&#41;統合](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)します。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|読み込まれたアセンブリの ID。 **Assembly_id**でアセンブリに関する詳細情報を確認するために使用できます、 [sys.assemblies &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)カタログ ビューです。 なお、 [!INCLUDE[tsql](../../includes/tsql-md.md)] [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)カタログは、現在のデータベースのみでアセンブリを示しています。 **Sqs.dm_clr_loaded_assemblies**サーバー上のすべての読み込まれたアセンブリを表示します。|  
|**appdomain_address**|**int**|アプリケーション ドメインのアドレス (**AppDomain**) で、アセンブリを読み込む。 1 人のユーザーによって所有されているすべてのアセンブリの読み込み、同じは常に**AppDomain**します。 **Appdomain_address**に関する詳細情報を参照に使用できる、 **AppDomain**で、 [sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md)ビュー。|  
|**load_time**|**datetime**|アセンブリが読み込まれた時刻。 アセンブリが、まで読み込まことに注意してください。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メモリが不足すると、アンロード、 **AppDomain**します。 監視することができます**load_time**頻度を理解する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メモリが不足して、アンロード、 **AppDomain**します。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="remarks"></a>コメント  
 **Dm_clr_loaded_assemblies.appdomain_address**ビューと多対一リレーションシップを持つ**dm_clr_appdomains.appdomain_address**します。 **Dm_clr_loaded_assemblies.assembly_id**ビューと一対多関係のある**sys.assemblies.assembly_id**します。  
  
## <a name="examples"></a>使用例  
 次の例は、現在読み込まれている現在のデータベースのすべてのアセンブリの詳細を表示する方法を示しています。  
  
```  
 SELECT a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
FROM sys.dm_clr_loaded_assemblies AS l   
INNER JOIN sys.assemblies AS a  
ON l.assembly_id = a.assembly_id;  
```  
  
 次の例の詳細を表示する方法を示しています、 **AppDomain**で、特定のアセンブリが読み込まれています。  
  
```  
SELECT appdomain_id, creation_time, db_id, user_id, state  
FROM sys.dm_clr_appdomains AS a  
WHERE appdomain_address =   
(SELECT appdomain_address   
 FROM sys.dm_clr_loaded_assemblies  
 WHERE assembly_id = 555);  
```  
  
## <a name="see-also"></a>参照  
 [共通言語ランタイム関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
