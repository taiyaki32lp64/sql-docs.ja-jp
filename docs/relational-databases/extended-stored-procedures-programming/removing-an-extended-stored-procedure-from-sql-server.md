---
title: 拡張ストアドプロシージャの削除
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- deleting extended stored procedures
- removing extended stored procedures
- extended stored procedures [SQL Server], removing
- dropping extended stored procedures
ms.assetid: 7827e574-3f59-4279-9a9b-532582e041cb
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: ec61cf630d606977689d3fb3763cce8bd8b705c8
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095436"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>SQL Server からの拡張ストアド プロシージャの削除
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに CLR Integration を使用してください。  
  
 ユーザー定義の拡張ストアドプロシージャ DLL 内の各拡張ストアドプロシージャ関数を削除するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者が、関数の名前とその関数が存在する DLL の名前を指定して、 **sp_dropextendedproc**システムストアドプロシージャを実行する必要があります。 たとえば、次のコマンドは、xp_hello という DLL にある関数**xp_hello**を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]から削除します。  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]以降では、 **sp_dropextendedproc**システム拡張ストアドプロシージャは削除されません。 代わりに、システム管理者は、拡張ストアドプロシージャに対する EXECUTE 権限を**public**ロールに対して拒否する必要があります。  
  
## <a name="see-also"></a>参照  
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
