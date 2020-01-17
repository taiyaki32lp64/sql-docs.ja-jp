---
title: 代替パイプ (SQL Server 構成マネージャー) でリッスンするようにサーバーの構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Named Pipes [SQL Server], configuring
- listening [SQL Server], pipes
- pipes [SQL Server], alternate
- alternate pipes [SQL Server]
ms.assetid: 914f7491-e2be-4b0d-b3aa-fe5409cdbafa
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 68b082d125650d150676d545cfdf6ab27bd25da2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62813525"
---
# <a name="configure-a-server-to-listen-on-an-alternate-pipe-sql-server-configuration-manager"></a>代替パイプをリッスンするサーバーの構成 (SQL Server 構成マネージャー)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で SQL Server 構成マネージャーを使用して、代替パイプをリッスンするようにサーバーを構成する方法について説明します。 既定では、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] の既定のインスタンスは、名前付きパイプ \\\\.\pipe\sql\query をリッスンします。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] および [!INCLUDE[ssEW](../../includes/ssew-md.md)] の名前付きインスタンスは、他のパイプをリッスンします。  
  
 クライアント アプリケーションを使用して特定の名前付きパイプに接続するには、次の 3 つの方法があります。  
  
-   サーバーで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスを実行します。  
  
-   クライアントで、名前付きパイプを指定して別名を作成します。  
  
-   クライアントで、カスタム接続文字列を使用して接続するように指定します。  
  
##  <a name="SSMSProcedure"></a> SQL Server 構成マネージャーの使用  
  
#### <a name="to-configure-the-named-pipe-used-by-the-sql-server-database-engine"></a>SQL Server データベース エンジンによって使用される名前付きパイプを構成するには  
  
1.  SQL Server 構成マネージャーのコンソール ペインで、 **[SQL Server ネットワークの構成]** を展開し、 **[\<*インスタンス名*> のプロトコル]** をクリックして展開します。  
  
2.  詳細ペインで **[名前付きパイプ]** を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[プロトコル]** タブで、 **[パイプ名]** ボックスに [!INCLUDE[ssDE](../../includes/ssde-md.md)] によってリッスンされるパイプを入力し、 **[OK]** をクリックします。  
  
4.  コンソール ペインで、 **[SQL Server のサービス]** をクリックします。  
  
5.  詳細ペインで **[SQL Server (** \<インスタンス名> **)]** を右クリックします。次に、 **[再起動]** をクリックして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を停止し、再起動します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が代替パイプをリッスンしている場合、クライアント アプリケーションを使用して特定の名前付きパイプに接続するには次の 3 つの方法があります。  
  
-   サーバーで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスを実行します。  
  
-   クライアントで、名前付きパイプを指定して別名を作成します。  
  
-   クライアントで、カスタム接続文字列を使用して接続するように指定します。  
  
## <a name="see-also"></a>参照  
 [クライアントが使用するサーバーの別名の作成または削除 &#40;SQL Server 構成マネージャー&#41;](create-or-delete-a-server-alias-for-use-by-a-client.md)   
 [サーバー ネットワークの構成](server-network-configuration.md)  
  
  
