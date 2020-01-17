---
title: 拡張ストアドプロシージャのクエリ
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], querying
ms.assetid: e02348e6-dba6-438a-98b6-684244bb034d
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 875d4f252058d442c91915eb69784507c39b2e94
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095944"
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>SQL Server にインストールされた拡張ストアド プロシージャの照会
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証されたユーザーは、 **sp_helpextendedproc**システムプロシージャを実行することによって、現在定義されている拡張ストアドプロシージャと、それぞれが属している DLL の名前を表示できます。 たとえば、次の例では、 **xp_hello**が属している DLL が返されます。  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 拡張ストアドプロシージャを指定せずに**sp_helpextendedproc**を実行すると、すべての拡張ストアドプロシージャとその dll が表示されます。  
  
> [!IMPORTANT]  
>  ログインしたユーザーが所有しているか、権限を持っている拡張ストアド プロシージャの情報だけが返されます。 すべての拡張ストアドプロシージャの情報を表示できるのは、 **sysadmin**固定サーバーロールのメンバーと、 **db_owner**、 **db_securityadmin**、および**db_ddladmin**の固定データベースロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [transact-sql &#40;  の&#41; sp_helpextendedproc](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_addextendedproc](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)  
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
