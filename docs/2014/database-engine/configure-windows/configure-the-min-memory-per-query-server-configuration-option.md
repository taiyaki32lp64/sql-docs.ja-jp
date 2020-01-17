---
title: min memory per query サーバー構成オプションの構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- memory [SQL Server], queries
- minimum query memory
- queries [SQL Server], memory
- min memory per query option
ms.assetid: ecd3fb79-b4a6-432f-9ef5-530e0d42d5a6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: dfee7265529419aecf2b05831503ed134b93f525
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62787045"
---
# <a name="configure-the-min-memory-per-query-server-configuration-option"></a>min memory per query サーバー構成オプションの構成
  このトピックでは、構成する方法を説明します、`min memory per query`サーバー構成オプション[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]を使用して[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]または[!INCLUDE[tsql](../../includes/tsql-md.md)]します。 `min memory per query`オプション (単位: キロバイト) クエリを実行するために割り当てられるメモリの最小量を指定します。 たとえば場合、`min memory per query`設定されているを 2,048 KB は、少なくともそのメモリを取得するクエリは保証します。 既定値は 1,024 KB です。 最小値は 512 KB、最大値は 2,147,483,647 KB (2 GB) です。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **以下を使用して min memory per query オプションを構成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [Min memory per query オプションを構成した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   min memory per query オプションの値は、 [index create memory オプション](configure-the-index-create-memory-server-configuration-option.md)よりも優先順位が高くなります。 両方のオプションを変更し、index create memory の設定値を min memory per query より小さくした場合は、警告メッセージが表示されます。ただし、値はそのまま設定されます。 クエリ実行中にも同様の警告が表示されます。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   このオプションは詳細設定オプションであるため、熟練したデータベース管理者または認定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術者だけが変更するようにしてください。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ プロセッサは、クエリに割り当てる最適なメモリの量を決定しようとします。 min memory per query オプションを使用すると、管理者は、どの単一のクエリにも割り当てられるメモリ量の最小値を指定できます。 通常、クエリが大量のデータに対してハッシュおよび並べ替え操作を行う場合は、min memory per query オプションの設定よりも多くメモリがクエリに割り当てられます。 min memory per query の値を増やすと、小規模から中規模のクエリではパフォーマンスが向上する可能性があります。ただし、この値の増加によって、メモリ リソースでの競合も増加する可能性があります。 min memory per query オプションには、並べ替え用に割り当てられるメモリが含まれます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 パラメーターなしで、または最初のパラメーターだけを指定して **sp_configure** を実行する権限は、既定ですべてのユーザーに付与されます。 両方のパラメーターを指定して **sp_configure** を実行し構成オプションを変更したり RECONFIGURE ステートメントを実行したりするには、ALTER SETTINGS サーバーレベル権限がユーザーに付与されている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-configure-the-min-memory-per-query-option"></a>min memory per query オプションを構成するには  
  
1.  オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[メモリ]** ノードをクリックします。  
  
3.  **[クエリごとに使用する最小メモリ (KB 単位)]** ボックスで、クエリの実行用に割り当てる最小メモリ容量 (KB 単位) を指定します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-configure-the-min-memory-per-query-option"></a>min memory per query オプションを構成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) を使用して、 `min memory per query` オプションの値を `3500` KB に設定する方法を示します。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'min memory per query', 3500 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
##  <a name="FollowUp"></a>補足情報: Min memory per query オプションを構成した後  
 新しい設定は、サーバーを再起動しなくてもすぐに有効になります。  
  
## <a name="see-also"></a>関連項目  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [index create memory サーバー構成オプションの構成](configure-the-index-create-memory-server-configuration-option.md)  
  
  
