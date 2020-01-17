---
title: クエリを実行する SQL Server にインストールされているストアド プロシージャを拡張 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], querying
ms.assetid: e02348e6-dba6-438a-98b6-684244bb034d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9f62c0dea02ee4c6f9bccda0dfaf7e7932c1dab7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62511935"
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>SQL Server にインストールされた拡張ストアド プロシージャの照会
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 A [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]拡張ストアド プロシージャを現在定義されている表示ユーザーを認証しを実行している各 DLL の名前が属している、 **sp_helpextendedproc**システム プロシージャ。 たとえば、次の例が DLL を返しますを**xp_hello**が属しています。  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 場合**sp_helpextendedproc**拡張ストアド プロシージャをすべての拡張ストアド プロシージャの Dll が表示されるかを指定せずに実行されます。  
  
> [!IMPORTANT]  
>  ログインしたユーザーが所有しているか、権限を持っている拡張ストアド プロシージャの情報だけが返されます。 メンバーのみ、 **sysadmin**固定サーバー ロールおよび**db_owner**、 **db_securityadmin**、および**db_ddladmin**固定データベースロールは、すべての拡張ストアド プロシージャの情報を表示できます。  
  
## <a name="see-also"></a>参照  
 [sp_helpextendedproc &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql)   
 [sp_addextendedproc &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
