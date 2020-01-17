---
title: SQL Server のインスタンス間での UCP の移動 (SQL Server ユーティリティ) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b402fd9e-0bea-4c38-a371-6ed7fea12e96
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bffc65e8586e8a158c58f7afb5cfb244835e8c86
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115389"
---
# <a name="move-a-ucp-from-one-instance-of-sql-server-to-another-sql-server-utility"></a>SQL Server のインスタンス間での UCP の移動 (SQL Server ユーティリティ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の 1 つのインスタンスから別のインスタンスにユーティリティ コントロール ポイント (UCP) を移動する方法について説明します。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="move-a-ucp-from-one-instance-of-sql-server-to-another"></a>SQL Server のインスタンス間での UCP の移動  
  
1.  UCP の新しいホスト インスタンスとなる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに新しい UCP を作成します。 詳細については、「[SQL Server ユーティリティ コントロール ポイントの作成 &#40;SQL Server ユーティリティ&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)」を参照してください。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティで、既定以外のポリシー設定が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに設定されている場合、ポリシーのしきい値を新しい UCP で再設定できるようにメモしておきます。 既定のポリシーは、インスタンスが新しい UCP に追加されるときに適用されます。 既定のポリシーが有効な場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのリスト ビューの **[ポリシーの種類]** 列に **[グローバル]** が表示されます。  
  
3.  古い UCP からすべてのマネージド インスタンスを削除します。 詳細については、「 [SQL Server ユーティリティからの SQL Server のインスタンスの削除](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md)」を参照してください。  
  
4.  古い UCP のユーティリティ管理データ ウェアハウス (UMDW) をバックアップします。 ファイル名は Sysutility_mdw_\<GUID>_DATA で、データベースの既定の場所は \<System drive>:\Program Files\Microsoft SQL Server\MSSQL10_50.<UCP_Name>\MSSQL\Data\\ です (通常、\<System drive> は C: ドライブ)。 詳細については、「 [バックアップと復元によるデータベースのコピー](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)」を参照してください。  
  
5.  UMDW のバックアップを新しい UCP に復元します。 詳細については、「 [バックアップと復元によるデータベースのコピー](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)」を参照してください。  
  
6.  インスタンスを新しい UCP に登録し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティで管理されるようにします。 詳細については、「 [SQL Server のインスタンスの登録 &#40;SQL Server ユーティリティ&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)の 1 つのインスタンスから別のインスタンスにユーティリティ コントロール ポイント (UCP) を移動する方法について説明します。  
  
7.  必要に応じて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のマネージド インスタンスにカスタムのポリシー定義を実装します。  
  
8.  データの収集と集計の操作が完了するまで約 1 時間待機します。  
  
9. データを更新するには、 **ユーティリティ エクスプローラー** で **[マネージド インスタンス]** ノードを右クリックし、 **[更新]** をクリックします。 リスト ビューのデータは、**ユーティリティ エクスプローラー**のコンテンツ ウィンドウに表示されます。 詳細については、「[リソース正常性ポリシーの結果の表示 &#40;SQL Server ユーティリティ&#41;](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server ユーティリティの機能とタスク](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [SQL Server のインスタンスの登録 &#40;SQL Server ユーティリティ&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)  
  
  
