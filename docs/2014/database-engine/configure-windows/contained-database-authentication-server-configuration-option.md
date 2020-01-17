---
title: contained database authentication サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- contained_database_authentication_TSQL
- contained database authentication
helpviewer_keywords:
- contained database, enabling
- contained database authentication option
ms.assetid: b80768d2-ac20-4035-a335-d9adb74b3f6e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d4efcddfb4c8cb53603614f3ffbdc3cb088990ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62782909"
---
# <a name="contained-database-authentication-server-configuration-option"></a>contained database authentication サーバー構成オプション
  **contained database authentication** オプションを使用して、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンス上で包含データベースを有効にします。  
  
 このサーバー オプションでは、 **contained database authentication**を制御できます。  
  
-   インスタンスで **contained database authentication** がオフ (0) の場合、包含データベースを作成したり [!INCLUDE[ssDE](../../includes/ssde-md.md)]にアタッチしたりすることはできません。  
  
-   インスタンスで **contained database authentication** がオン (1) の場合、包含データベースを作成したり [!INCLUDE[ssDE](../../includes/ssde-md.md)]にアタッチしたりすることができます。  
  
 包含データベースには、すべてのデータベース設定と、データベースを定義するために必要なメタデータが含まれており、データベースがインストールされている [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに対する構成上の依存関係がありません。 ユーザーは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] レベルでのログイン認証なしで包含データベースに接続できます。 データベース エンジンからデータベースを分離すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の他のインスタンスにデータベースを簡単に移動できるようになります。 すべてのデータベース設定をデータベースに含めることによって、データベース所有者はデータベースのすべての構成設定を管理できるようになります。 包含データベースの詳細については、「 [Contained Databases](../../relational-databases/databases/contained-databases.md)」をご覧ください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに包含データベースが存在する場合、**contained database authentication** の設定は **RECONFIGURE WITH OVERRIDE** ステートメントを使用して 0 に設定できます。 **contained database authentication** を 0 に設定すると、包含データベースに対して contained database authentication が無効になります。  
  
> [!IMPORTANT]  
>  包含データベースを有効にすると、ALTER ANY USER 権限を持つデータベース ユーザー (db_owner ロールおよび db_accessadmin データベース ロールのメンバーなど) は、データベースへのアクセスが許可されます。そうすることで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへのアクセスが許可されます。 これは、サーバーへのアクセスの制御は sysadmin および securityadmin 固定サーバー ロールのメンバー、およびサーバー レベルでの管理 CONTROL SERVER および ALTER ANY LOGIN 権限によるログインに制限されなくなることを意味します。 包含データベースを許可する前に、包含データベースに関連するリスクを理解する必要があります。 詳細については、「 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスで包含データベースを有効にします。  
  
```sql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
