---
title: network packet size サーバー構成オプションの構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default packet size
- size [SQL Server], packets
- packets [SQL Server], size
- network packet size option
ms.assetid: 236985bf-fc4a-4a57-98f7-a71ef977fd7b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: be854d2002692611289d401b4ad98cb63cf4a27b
ms.sourcegitcommit: 0d89bcaebdf87db3bd26db2ca263be9c671b0220
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2019
ms.locfileid: "68731108"
---
# <a name="configure-the-network-packet-size-server-configuration-option"></a>network packet size サーバー構成オプションの構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックでは、 **で** または [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] network packet size [!INCLUDE[tsql](../../includes/tsql-md.md)]サーバー構成オプションを構成する方法について説明します。 **network packet size** オプションは、ネットワーク全体で使用するパケット サイズ (バイト単位) を設定します。 パケットとは、固定サイズのデータのチャンクで、クライアントとサーバー間で要求および結果を転送します。 既定のパケット サイズは 4,096 バイトです。  
  
> [!NOTE]  
>  パフォーマンスの向上が明確でない限り、パケット サイズは変更しないでください。 多くのアプリケーションでは、既定のパケット サイズが最適です。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
     [セキュリティ](#Security)  
  
-   **以下を使用して network packet size オプションを構成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [network packet size オプションを構成した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   暗号化された接続の最大ネットワーク パケット サイズは 16,383 バイトです。  
  
> [!NOTE]  
> MARS が有効な場合、SMUX プロバイダーによって SSL 暗号化の前に 16 バイトのヘッダーがパケットに追加され、最大ネットワーク パケット サイズは 16,368 バイトに減ります。
   
###  <a name="Recommendations"></a> 推奨事項  
  
-   このオプションは詳細設定オプションであるため、熟練したデータベース管理者または認定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロフェッショナルだけが変更するようにしてください。  
  
-   アプリケーションで一括コピー操作を行ったり、大量の text 型または image 型のデータを送受信する場合は、パケット サイズを既定値より大きくすると、ネットワークの読み取りと書き込みの操作が少なくなるので効率が向上することがあります。 アプリケーションで送受信する情報量が少ない場合は、パケット サイズを 512 バイトに設定できます。これは、ほとんどのデータ転送に十分なサイズです。  
  
-   異なるネットワーク プロトコルを使用しているシステムでは、最も一般的に使用されるプロトコル向けのサイズに network packet size を設定します。 ネットワーク プロトコルで大きなパケットがサポートされるときは、network packet size オプションを設定することでネットワーク パフォーマンスを向上できます。 クライアント アプリケーションはこの値をオーバーライドできます。  
  
-   OLE DB 関数、ODBC (Open Database Connectivity) 関数、および DB-Library 関数を呼び出して、パケット サイズの変更を要求することもできます。 要求されたパケット サイズにサーバーが対応できない場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] からクライアントに警告メッセージが送信されます。 環境によっては、パケット サイズを変更すると、次のような通信リンク エラーが発生することがあります。  
  
     `Native Error: 233, no process is on the other end of the pipe.`  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 パラメーターなしで、または最初のパラメーターだけを指定して **sp_configure** を実行する権限は、既定ですべてのユーザーに付与されます。 両方のパラメーターを指定して **sp_configure** を実行し構成オプションを変更したり RECONFIGURE ステートメントを実行したりするには、ALTER SETTINGS サーバーレベル権限がユーザーに付与されている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-configure-the-network-packet-size-option"></a>network packet size オプションを構成するには  
  
1.  オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[詳細設定]** ノードをクリックします。  
  
3.  **[ネットワーク]** の **[ネットワーク パケット サイズ]** ボックスに値を指定します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-configure-the-network-packet-size-option"></a>network packet size オプションを構成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) を使用して、 `network packet size` オプションの値を `6500` バイトに設定する方法を示します。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'network packet size', 6500 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 詳細については、「 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)」を参照してください。  
  
##  <a name="FollowUp"></a>補足情報: network packet size オプションを構成した後  
 新しい設定は、サーバーを再起動しなくてもすぐに有効になります。  
  
## <a name="see-also"></a>参照  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
