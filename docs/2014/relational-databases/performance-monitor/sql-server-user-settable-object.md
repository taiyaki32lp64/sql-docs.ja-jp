---
title: 'SQL Server: User Settable オブジェクト | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- User Settable object
- SQLServer:User Settable
ms.assetid: 633de3ef-533c-4f0c-9c7b-c105129d8e94
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5ac802569356979f3a01da4c204a80272c2be43a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151088"
---
# <a name="sql-server-user-settable-object"></a>SQL Server: User Settable オブジェクト
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **User Settable** オブジェクトを使用すると、カスタムのカウンター インスタンスを作成できます。 カスタムのカウンター インスタンスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのユーザー独自のコンポーネントなど、既存のカウンターでは監視されないサーバーの特性を監視するために使用します。たとえば、ログに記録された顧客注文数や製品在庫数などを監視できます。  
  
 **User Settable** オブジェクトには、**ユーザー カウンター 1** から **ユーザー カウンター 10** まで、クエリ カウンターの 10 個のインスタンスが含まれています。 これらのカウンターは、 **sp_user_counter1** から **sp_user_counter10** までの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャに対応します。 ユーザー アプリケーションからこれらのストアド プロシージャが実行されると、ストアド プロシージャによって設定された値がシステム モニターに表示されます。 1 つのカウンターは、1 日に発生した特定製品の注文件数を数えるストアド プロシージャなど、任意の整数値を 1 つ監視できます。  
  
> [!NOTE]  
>  ユーザー カウンターのストアド プロシージャは、システム モニターから自動的にポーリングされることはありません。 カウンター値を更新するには、ユーザー アプリケーションから明示的にストアド プロシージャを実行する必要があります。 カウンター値を自動的に更新するには、トリガーを使用します。 たとえば、テーブルの行数を監視するカウンターを作成するには、テーブルに対する INSERT と DELETE のトリガーを作成し、 `SELECT COUNT(*) FROM table`というステートメントが実行されるようにします。 テーブルに対する INSERT 操作か DELETE 操作が発生するとトリガーが起動され、システム モニター カウンターが自動的に更新されます。  
  
 次の表では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **User Settable** オブジェクトについて説明します。  
  
|SQL Server User Settable カウンター|説明|  
|---------------------------------------|-----------------|  
|**クエリ**|**User Settable** オブジェクトには、Query カウンターが含まれています。 ユーザーは、クエリ オブジェクト内の **ユーザー カウンター** を構成します。|  
  
 次の表では、 **Query** カウンターの **インスタンス** について説明します。  
  
|Query カウンターのインスタンス|説明|  
|-----------------------------|-----------------|  
|**ユーザー カウンター 1**|**sp_user_counter1**を使用して定義します。|  
|**ユーザー カウンター 2**|**sp_user_counter2**を使用して定義します。|  
|**ユーザー カウンター 3**|**sp_user_counter3**を使用して定義します。|  
|[...]||  
|**ユーザー カウンター 10**|**sp_user_counter10**を使用して定義します。|  
  
 ユーザー カウンターのストアド プロシージャを使用するには、カウンターの新しい値を示す 1 つの整数パラメーターを指定して、独自のアプリケーションからそのストアド プロシージャを実行します。 たとえば、 **ユーザー カウンター 1** の値を 10 に設定するには、次の Transact-SQL ステートメントを実行します。  
  
```  
EXECUTE sp_user_counter1 10  
```  
  
 ユーザー カウンターのストアド プロシージャは、独自のストアド プロシージャなど他のストアド プロシージャを呼び出せる場所なら、どこからでも呼び出すことができます。 たとえば、次のストアド プロシージャを作成して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが起動されてから行われた接続と接続試行の数を数えることができます。  
  
```  
DROP PROC My_Proc  
GO  
CREATE PROC My_Proc  
AS   
   EXECUTE sp_user_counter1 @@CONNECTIONS  
GO  
```  
  
 @@CONNECTIONS 関数は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが起動されてから行われた接続または接続試行の数を返します。 返された値が、パラメーターとして **sp_user_counter1** ストアド プロシージャに渡されます。  
  
> [!IMPORTANT]  
>  ユーザー カウンターのストアド プロシージャで定義するクエリは、できるだけ単純なものにしてください。 大量の並べ替え操作やハッシュ操作を実行するクエリや大量の I/O を実行するクエリは、メモリを集中的に消費するので、パフォーマンスに影響する可能性があります。  
  
## <a name="permissions"></a>アクセス許可  
 **sp_user_counter** はすべてのユーザーが使用できますが、任意のクエリ カウンターに制限することもできます。  
  
## <a name="see-also"></a>参照  
 [リソースの利用状況の監視 &#40;システム モニター&#41;](monitor-resource-usage-system-monitor.md)  
  
  
