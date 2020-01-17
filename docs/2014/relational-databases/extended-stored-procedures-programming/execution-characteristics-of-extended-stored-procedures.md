---
title: 拡張ストアド プロシージャの実行における特性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], executing
- executing extended stored procedures [SQL Server]
ms.assetid: 6fe1f7e8-cc02-49df-8a2a-d47a96ec3567
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d21f002ca6b7ea185df2e01f66abf0e1ef5cfd1b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62512220"
---
# <a name="execution-characteristics-of-extended-stored-procedures"></a>拡張ストアド プロシージャの実行における特性
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに CLR Integration を使用してください。  
  
 拡張ストアド プロシージャの実行には次の 3 つの特性があります。  
  
-   拡張ストアド プロシージャ関数は、のセキュリティ コンテキストで実行されます[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
-   拡張ストアド プロシージャ関数は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の処理領域で実行されます。  
  
-   拡張ストアド プロシージャの実行に関連付けられているスレッドは、クライアント接続に使用するスレッドと同じです。  
  
    > [!IMPORTANT]  
    >  システム管理者は、拡張ストアド プロシージャをサーバーに追加し、他のユーザーに実行権限を許可する前に、各拡張ストアド プロシージャに有害なコードや悪意のあるコードが含まれていないことを十分に確認する必要があります。  
  
-  
  
 DLL はまで、サーバーのアドレス空間に読み込まれた後、拡張のストアド プロシージャ DLL が読み込まれる、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が停止している管理者が DBCC を使用して DLL を明示的にアンロードまたは*DLL_name* (無料)。  
  
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
 [拡張ストアド プロシージャ プログラミング](database-engine-extended-stored-procedures-programming.md)   
 [SQL Server にインストールされた拡張ストアド プロシージャの照会](querying-extended-stored-procedures-installed-in-sql-server.md)  
  
  
