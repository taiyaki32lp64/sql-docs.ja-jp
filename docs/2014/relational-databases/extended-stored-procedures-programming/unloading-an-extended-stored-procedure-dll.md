---
title: ストアド プロシージャ DLL のアンロードの拡張 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2772c8d6470f9ad6eb5e8b7cadb6dedd136bd48b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63137583"
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>拡張ストアド プロシージャ DLL のアンロード
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに CLR Integration を使用してください。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DLL の関数のいずれかに呼び出しが行われるとすぐには、拡張ストアド プロシージャ DLL を読み込みます。 DLL がロードされた状態は、サーバーがシャットダウンするか、DBCC ステートメントを使用してシステム管理者によってアンロードされるまで、維持されます。 たとえば、このコマンドのアンロード、 **xp_hello.dll**、システム管理者は、サーバーをシャット ダウンせずに、このファイルの新しいバージョンをディレクトリにコピーすることができます。  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>関連項目  
 [DBCC dllname &#40;FREE&#41; &#40;TRANSACT-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dllname-free-transact-sql)  
  
  
