---
title: 拡張ストアドプロシージャの実行特性
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], executing
- executing extended stored procedures [SQL Server]
ms.assetid: 6fe1f7e8-cc02-49df-8a2a-d47a96ec3567
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 74ecd20f28e58e133b5710d3cbd9d18b27ca7756
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095986"
---
# <a name="execution-characteristics-of-extended-stored-procedures"></a>拡張ストアド プロシージャの実行における特性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに CLR Integration を使用してください。  
  
 拡張ストアド プロシージャの実行には次の 3 つの特性があります。  
  
-   拡張ストアドプロシージャ関数は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のセキュリティコンテキストで実行されます。  
  
-   拡張ストアド プロシージャ関数は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の処理領域で実行されます。  
  
-   拡張ストアド プロシージャの実行に関連付けられているスレッドは、クライアント接続に使用するスレッドと同じです。  
  
    > [!IMPORTANT]  
    >  システム管理者は、拡張ストアド プロシージャをサーバーに追加し、他のユーザーに実行権限を許可する前に、各拡張ストアド プロシージャに有害なコードや悪意のあるコードが含まれていないことを十分に確認する必要があります。  
  
-  
  
 拡張ストアドプロシージャ DLL が読み込まれると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が停止するか、管理者が DBCC *DLL_name* (FREE) を使用して dll を明示的にアンロードするまで、dll はサーバーのアドレス空間に読み込まれたままになります。  
  
 EXECUTE ステートメントを使用すると、拡張ストアド プロシージャをストアド プロシージャとして [!INCLUDE[tsql](../../includes/tsql-md.md)] から実行できます。  
  
```  
EXECUTE @retval = xp_extendedProcName @param1, @param2 OUTPUT  
```  
  
## <a name="parameters"></a>パラメーター  
 \@ *retval*  
 戻り値です。  
  
 \@ *param1*  
 入力パラメーターです。  
  
 \@ *param2*  
 入力/出力パラメーターです。  
  
> [!CAUTION]  
>  拡張ストアド プロシージャを使用すると、パフォーマンスの向上や、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能強化を図ることができます。 ただし、拡張ストアド プロシージャ DLL と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は同じアドレス領域を共有するため、問題のあるプロシージャにより [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能が影響を受けることがあります。 拡張ストアド プロシージャ DLL によってスローされる例外は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で処理されますが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ領域に損傷を与える可能性があります。 セキュリティ措置として、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に拡張ストアド プロシージャを組み込むことができるのは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者だけに限定されています。 これらのプロシージャは詳細にテストしてからインストールする必要があります。  
  
## <a name="see-also"></a>参照  
 [拡張ストアドプロシージャのプログラミング](../../relational-databases/extended-stored-procedures-programming/database-engine-extended-stored-procedures-programming.md)   
 [SQL Server にインストールされた拡張ストアド プロシージャの照会](../../relational-databases/extended-stored-procedures-programming/querying-extended-stored-procedures-installed-in-sql-server.md)  
  
  
