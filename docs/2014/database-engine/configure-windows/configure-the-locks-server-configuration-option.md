---
title: locks サーバー構成オプションの構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- locks option [SQL Server]
ms.assetid: b0cf0f86-7652-4574-a9fb-908e10d03973
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 22f47a80a73efc8d462ef8f26f2e6b0fb5b3f3c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62787394"
---
# <a name="configure-the-locks-server-configuration-option"></a>locks サーバー構成オプションの構成
  このトピックでは、 **または** を使用して、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] locks [!INCLUDE[tsql](../../includes/tsql-md.md)]サーバー構成オプションを構成する方法について説明します。 **locks** オプションは、使用できるロックの最大数を設定することによって、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] がそのために使用するメモリの量を制限します。 既定値は 0 です。0 の場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] はシステム要件の変更に基づいてロック構造を動的に割り当てたり、割り当てを解除したりできます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **以下を使用して locks オプションを構成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [Locks オプションを構成した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   このオプションは詳細設定オプションであるため、熟練したデータベース管理者または認定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術者だけが変更するようにしてください。  
  
-   **locks** を 0 に設定してサーバーを起動すると、ロック マネージャーは 2,500 個のロック構造の初期プール用に [!INCLUDE[ssDE](../../includes/ssde-md.md)] から十分なメモリを取得します。 ロック プールがなくなると、プール用のメモリが追加取得されます。  
  
     通常、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のメモリ プールから取得できるメモリよりも多くのメモリがロック プールに必要であり、より多くのコンピューター メモリが使用できる ( **max server memory** のしきい値に達していない) 場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] はメモリを動的に割り当ててロック要求に応じます。 ただし、そのメモリを割り当てることによって、オペレーティング システム レベルでページングが発生する場合、たとえば、別のアプリケーションが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスと同じコンピューター上で実行されていて、そのメモリを使用している場合は、ロック用に割り当てを増やすことはできません。 動的なロック プールは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]に割り当てられたメモリのうち最大 60% まで取得できます。 ロック プールが [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスによって取得されたメモリの 60% に達した場合、またはコンピューターで使用できるメモリがなくなった場合、さらにロック要求があるとエラーが発生します。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が動的にロックを割り当てるように構成することをお勧めします。 ただし、**locks** を設定し、ロック リソースを動的に割り当てる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能をオーバーライドすることができます。 **locks** が 0 以外の値に設定されている場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] は **locks**に指定された値よりも多くのロックを割り当てることができません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に使用可能なロック数を超えたことを示すメッセージが表示された場合は、この値を大きくします。 各ロックはそれぞれ 96 バイトのメモリを消費するため、この値を大きくした場合、状況によってはサーバー専用のメモリも増やす必要があります。  
  
-   **locks** オプションも、ロックのエスカレートがいつ行われるかに影響を与えます。 **locks** を 0 に設定すると、現在のロック構造で使用されるメモリが [!INCLUDE[ssDE](../../includes/ssde-md.md)] のメモリ プールの 40% に達したときに、ロックのエスカレートが行われます。 **locks** が 0 に設定されていない場合は、ロック数が **locks**に指定された値の 40% に達したときに、ロックのエスカレートが行われます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 パラメーターなしで、または最初のパラメーターだけを指定して **sp_configure** を実行する権限は、既定ですべてのユーザーに付与されます。 両方のパラメーターを指定して **sp_configure** を実行し構成オプションを変更したり RECONFIGURE ステートメントを実行したりするには、ALTER SETTINGS サーバーレベル権限がユーザーに付与されている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-configure-the-locks-option"></a>locks オプションを構成するには  
  
1.  オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[詳細設定]** ノードをクリックします。  
  
3.  **[並列処理]** で、 **locks** オプションの目的の値を入力します。  
  
     **locks** オプションは、使用可能なロックの最大数を設定して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってロックに使用されるメモリの量を制限するために使用します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-configure-the-locks-option"></a>locks オプションを構成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) を使用して `locks` オプションの値を設定する方法を示します。使用できるロックの数をユーザー全体で `20000`に設定します。  
  
```sql  
Use AdventureWorks2012 ;  
GO  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'locks', 20000;  
GO  
RECONFIGURE;  
GO  
```  
  
 詳細については、「 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)」を参照してください。  
  
##  <a name="FollowUp"></a>補足情報: Locks オプションを構成した後  
 設定を有効にするには、サーバーを再起動する必要があります。  
  
## <a name="see-also"></a>関連項目  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
