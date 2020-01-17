---
title: 権限借用と接続の資格情報 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- impersonation [CLR integration]
- security [CLR integration]
- database objects [CLR integration], connections
- connections [CLR integration]
- authentication [CLR integration]
- user impersonation [CLR integration]
- credentials [CLR integration]
- database objects [CLR integration], security
ms.assetid: 293dce7d-1db2-4657-992f-8c583d6e9ebb
author: rothja
ms.author: jroth
ms.openlocfilehash: d83ee1d69e7083931a2f6e6befb89912abec43f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138681"
---
# <a name="impersonation-and-credentials-for-connections"></a>接続の権限借用と資格情報
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR (共通言語ランタイム) 統合では、複雑な Windows 認証を使用する方が、SQL Server 認証を使用するよりもセキュリティが向上します。 Windows 認証を使用する場合には、次の点を考慮してください。  
  
 Windows に接続する SQL Server プロセスは、SQL Server Windows サービス アカウントのセキュリティ コンテキストを既定で取得します。 ただし、CLR 関数をプロキシ ID にマッピングすることにより、その発信接続に対し、Windows サービス アカウントとは異なるセキュリティ コンテキストを設定することができます。  
  
 場合によってを使用して、呼び出し元を偽装する可能性があります、 **SqlContext.WindowsIdentity**サービス アカウントとして実行しているのではなくプロパティ。 **WindowsIdentity**インスタンスは、呼び出し元のコードを呼び出すし、クライアントが Windows 認証を使用する場合にのみ使用するクライアントの id を表します。 取得した後、 **WindowsIdentity**呼び出すことができますのインスタンス、 **Impersonate**スレッドのセキュリティ トークンを変更し、クライアントの代わりに ADO.NET 接続を開きます。  
  
 SQLContext.WindowsIdentity.Impersonate を呼び出した後は、ローカル データにアクセスすることはできませんし、システム データにアクセスすることはできません。 ここでも、データにアクセスするには、WindowsImpersonationContext.Undo を呼び出す必要があります。  
  
 次の例を使用して、呼び出し元を偽装する方法を示しています、 **SqlContext.WindowsIdentity**プロパティ。  
  
 Visual C#  
  
```  
WindowsIdentity clientId = null;  
WindowsImpersonationContext impersonatedUser = null;  
  
clientId = SqlContext.WindowsIdentity;  
  
// This outer try block is used to protect from   
// exception filter attacks which would prevent  
// the inner finally block from executing and   
// resetting the impersonation.  
try  
{  
   try  
   {  
      impersonatedUser = clientId.Impersonate();  
      if (impersonatedUser != null)  
         return GetFileDetails(directoryPath);  
         else return null;  
   }  
   finally  
   {  
      if (impersonatedUser != null)  
         impersonatedUser.Undo();  
   }  
}  
catch  
{  
   throw;  
}  
```  
  
> [!NOTE]  
>  権限借用の動作の変更については、次を参照してください。 [SQL Server 2016 におけるデータベース エンジン機能の重大な変更](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)します。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows ID インスタンスを取得した場合、既定では、そのインスタンスを別のコンピューターに反映できません。既定では、Windows セキュリティ インフラストラクチャによりこの操作が制限されます。 ただし、"委任" というメカニズムを使用すると、信頼関係のある複数のコンピューターに Windows ID を反映できるようになります。 TechNet 記事では、委任の詳細については、"[Kerberos プロトコル遷移および制約付き委任](https://go.microsoft.com/fwlink/?LinkId=50419)"。  
  
## <a name="see-also"></a>参照  
 [SqlContext オブジェクト](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
  
