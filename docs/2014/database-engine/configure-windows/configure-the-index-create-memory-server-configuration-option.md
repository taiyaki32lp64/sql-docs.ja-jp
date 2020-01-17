---
title: index create memory サーバー構成オプションの構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- index create memory option
ms.assetid: 3d722d9b-bada-4bf5-a9d7-bfc556bb4915
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 280d4edef062429304d5c6e1d6c65ea63fac2eee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62786946"
---
# <a name="configure-the-index-create-memory-server-configuration-option"></a>index create memory サーバー構成オプションの構成
  このトピックでは、 **で** または [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] index create memory [!INCLUDE[tsql](../../includes/tsql-md.md)]サーバー構成オプションを構成する方法について説明します。 **index create memory** オプションは、インデックス作成用として最初に割り当てられる最大メモリ容量を制御します。 このオプションの既定値は 0 (自己構成) です。 その後、インデックスを作成するためにより多くのメモリが必要になった場合、メモリ容量を確保できるのであれば、サーバーはそのメモリを使用します。したがって、使用メモリ容量がこのオプションの設定値を超えることになります。 追加メモリを確保できない場合は、既に割り当てられているメモリを使用してインデックス作成が続行されます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **以下を使用して index create memory オプションを構成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:**[index create memory オプションを構成した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   **min memory per query** オプションの設定は、 **index create memory** オプションよりも優先順位が高くなります。 両方のオプションを変更し、 **index create memory** の設定値を **min memory per query**より小さくした場合は、警告メッセージが表示されます。ただし、値はそのまま設定されます。 クエリ実行中にも同様の警告が表示されます。  
  
-   パーティション テーブルとパーティション インデックスを使用する場合、パーティション インデックスが未整理であったり、並列処理の頻度が高かったりすると、インデックスの作成に必要な最小メモリ容量が大幅に増加します。 このオプションを使用して、1 回のインデックス作成操作ですべてのインデックス パーティションに最初に割り当てられる合計メモリ容量を指定できるようになっています。 このオプションで指定したメモリ容量が、クエリの実行に必要となる最小メモリ容量より小さい場合は、クエリの実行が中止され、エラー メッセージが表示されます。  
  
-   このオプションの実行値は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているオペレーティング システムおよびハードウェア プラットフォームで実際に確保できるメモリ容量を超えることはありません。 32 ビット オペレーティング システムの場合、実行値は 3 GB より小さくなります。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   このオプションは詳細設定オプションであるため、熟練したデータベース管理者または認定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術者だけが変更するようにしてください。  
  
-   **index create memory** オプションは自動的に設定されるので、通常は調整する必要がありません。 ただし、インデックスを正常に作成できない場合は、必要に応じて、このオプションの値を実行値より大きくしてください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 パラメーターなしで、または最初のパラメーターだけを指定して **sp_configure** を実行する権限は、既定ですべてのユーザーに付与されます。 両方のパラメーターを指定して **sp_configure** を実行し構成オプションを変更したり RECONFIGURE ステートメントを実行したりするには、ALTER SETTINGS サーバーレベル権限がユーザーに付与されている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-configure-the-index-create-memory-option"></a>index create memory オプションを構成するには  
  
1.  オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[メモリ]** ノードをクリックします。  
  
3.  **[インデックス作成メモリ]** で、index create memory オプションの目的の値を入力または選択します。  
  
     **index create memory** オプションは、インデックス作成時の並べ替えに使用するメモリの量を制御する場合に使用します。 **index create memory** オプションは自動構成型で、ほとんどの場合、調整を行わなくても機能します。 ただし、インデックスを正常に作成できない場合は、必要に応じて、このオプションの値を実行値より大きくしてください。 クエリの並べ替えは、 **min memory per query** オプションを使用して制御します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-configure-the-index-create-memory-option"></a>index create memory オプションを構成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) を使用して、 `index create memory` オプションの値を `4096`に設定する方法を示します。  
  
```sql  
USE AdventureWorks2012 ;  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
EXEC sp_configure 'index create memory', 4096  
GO  
RECONFIGURE;  
GO  
```  
  
 詳細については、「 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)」を参照してください。  
  
##  <a name="FollowUp"></a>補足情報: index create memory オプションを構成した後  
 新しい設定は、サーバーを再起動しなくてもすぐに有効になります。  
  
## <a name="see-also"></a>参照  
 [sys.configurations &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-configurations-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [サーバー メモリに関するサーバー構成オプション](server-memory-server-configuration-options.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
