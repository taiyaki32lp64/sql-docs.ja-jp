---
title: contained database authentication サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- contained database, enabling
- contained database authentication option
ms.assetid: b80768d2-ac20-4035-a335-d9adb74b3f6e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f571690b4af27d4099e0750eeacedcafd943f1fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68012116"
---
# <a name="contained-database-authentication-server-configuration-option"></a>contained database authentication サーバー構成オプション
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **contained database authentication** オプションを使用して、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンス上で包含データベースを有効にします。  
  
 このサーバー オプションでは、 **contained database authentication**を制御できます。  
  
-   インスタンスで **contained database authentication** がオフ (0) の場合、包含データベースを作成したり [!INCLUDE[ssDE](../../includes/ssde-md.md)]にアタッチしたりすることはできません。  
  
-   インスタンスで **contained database authentication** がオン (1) の場合、包含データベースを作成したり [!INCLUDE[ssDE](../../includes/ssde-md.md)]にアタッチしたりすることができます。  
  
 包含データベースには、すべてのデータベース設定と、データベースを定義するために必要なメタデータが含まれており、データベースがインストールされている [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに対する構成上の依存関係がありません。 ユーザーは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] レベルでのログイン認証なしで包含データベースに接続できます。 データベース エンジンからデータベースを分離すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の他のインスタンスにデータベースを簡単に移動できるようになります。 すべてのデータベース設定をデータベースに含めることによって、データベース所有者はデータベースのすべての構成設定を管理できるようになります。 包含データベースの詳細については、「 [Contained Databases](../../relational-databases/databases/contained-databases.md)」をご覧ください。  

> [!NOTE]
> [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] と [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] の場合、包含データベースは常に有効であり、無効にすることはできません。
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに包含データベースが存在する場合、**contained database authentication** の設定は **RECONFIGURE WITH OVERRIDE** ステートメントを使用して 0 に設定できます。 **contained database authentication** を 0 に設定すると、包含データベースに対して contained database authentication が無効になります。  
  
> [!IMPORTANT]  
>  包含データベースを有効にすると、ALTER ANY USER 権限を持つデータベース ユーザー (db_owner ロールおよび db_accessadmin データベース ロールのメンバーなど) は、データベースへのアクセスが許可されます。そうすることで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへのアクセスが許可されます。 これは、サーバーへのアクセスの制御は sysadmin および securityadmin 固定サーバー ロールのメンバー、およびサーバー レベルでの管理 CONTROL SERVER および ALTER ANY LOGIN 権限によるログインに制限されなくなることを意味します。 包含データベースを許可する前に、包含データベースに関連するリスクを理解する必要があります。 詳しくは、「 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)」をご覧ください。  
  
## <a name="examples"></a>使用例  
 次の例では、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスで包含データベースを有効にします。  
  
```sql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
