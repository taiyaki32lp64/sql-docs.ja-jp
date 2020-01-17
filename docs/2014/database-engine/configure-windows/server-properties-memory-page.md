---
title: サーバーのプロパティ ([メモリ] ページ) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.serverproperties.memory.f1
ms.assetid: 46a77d4e-ab92-49d3-a14b-423462e50715
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6950199a5da1f4aa773eaa12fee80edb98aba04f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62809419"
---
# <a name="server-properties-memory-page"></a>[サーバーのプロパティ] ([メモリ] ページ)
  このページを使用すると、サーバーのメモリ オプションを表示または変更できます。 **[最小サーバー メモリ]** を 0 に、 **[最大サーバー メモリ]** を 2,147,483,647 MB に設定しておくと、オペレーティング システムおよび他のアプリケーションによって現在どれだけの量のメモリが使用されているかに応じて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は常に最適な量のメモリを利用できます。 コンピューターと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の負荷が変化すると、割り当てメモリも変化します。 この動的メモリ割り当ては、次に示す最小値および最大値に制限できます。  
  
## <a name="options"></a>および  
 **[最小サーバー メモリ (MB)]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が最小割り当てメモリ以上で起動されること、およびこの値を下回ってメモリを解放しないことを指定します。 この値は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスのサイズおよび動作に基づいて設定します。 オペレーティング システムが要求する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用のメモリが多くなりすぎて Windows パフォーマンスが低下することのないように、このオプションは常に妥当な値に設定しておきます。  
  
 **[最大サーバー メモリ (MB)]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が起動時および実行時に割り当てることができる最大メモリ量を指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と同時に複数のアプリケーションを実行し、これらのアプリケーションの実行に十分なメモリを確保する場合、この構成オプションを特定の値に設定できます。 他のアプリケーション (Web サーバー、電子メール サーバーなど) からは、必要なときにのみメモリを要求する場合には、このオプションを設定しないでください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はそれらのアプリケーションに対し、必要に応じてメモリを解放します。 ただし、多くのアプリケーションでは起動時に利用可能なメモリをできるだけ確保し、その後必要に応じてさらに要求することはありません。 このように動作するアプリケーションが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と同時に同じコンピューター上で実行されている場合、アプリケーションの要求するメモリが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に割り当てられないようにするために、このオプションを適切な値に設定します。 指定できるメモリの最小容量**サーバー メモリの最大**64 メガバイト (MB) は、32 ビット システムと 128 MB の 64 ビット システム。  
  
 **[インデックス作成メモリ (KB 単位、0 = 動的メモリ)]**  
 インデックス作成時の並べ替え操作中に使用するメモリの量を KB 単位で指定します。 既定値の 0 は動的割り当てを有効にするもので、特別な調整を必要とすることなくほとんどのケースで使用できます。ユーザーは、704 ～ 2,147,483,647 の範囲内で値を指定できます。  
  
> [!NOTE]  
>  1 ～ 703 の値は許可されません。 この範囲内の値を入力した場合、入力された値は値 704 でオーバーライドされます。  
  
 **[クエリごとに使用する最小メモリ (KB 単位)]**  
 クエリを実行するために割り当てるメモリの量を (KB 単位で) 指定します。 ユーザーは、512 ～ 2,147,483,647 KB の範囲内で値を指定できます。 既定値は 1024 KB です。  
  
 **[構成した値]**  
 このペインの各オプションに構成されている値を表示します。 これらの値を変更した場合は、 **[実行中の値]** をクリックして、変更後の値が反映されているかどうかを確認してください。 値が反映されていない場合は、最初に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを再起動する必要があります。  
  
 **[実行中の値]**  
 このペイン上のオプションの、現在実行中の値を表示します。 これらの値は読み取り専用です。  
  
## <a name="see-also"></a>参照  
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [サーバー メモリに関するサーバー構成オプション](server-memory-server-configuration-options.md)  
  
  
