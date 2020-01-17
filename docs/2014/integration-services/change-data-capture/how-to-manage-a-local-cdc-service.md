---
title: ローカルの CDC Service を管理する方法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7f9be649-cd93-40c1-bc48-0480106f207c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 27ec5fcac246c9907d38d8e0eff4e82befb0a04e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771308"
---
# <a name="how-to-manage-a-local-cdc-service"></a>ローカルの CDC Service を管理する方法
  この手順では、CDC Service 構成コンソールを使用して特定の CDC サービスを管理する方法について説明します。  
  
### <a name="to-manage-a-specific-cdc-service"></a>特定の CDC Service を管理するには  
  
1.  **[スタート]** メニューの **[CDC Service Configuration for Oracle]** をクリックします。  
  
2.  CDC Service 構成コンソールの左ペインで **[ローカルの CDC Service]** を展開します。  
  
3.  操作する CDC サービスを選択します。  
  
     操作する CDC サービスを右クリックして、目的のアクションをクリックすることもできます。  
  
     **または**  
  
     CDC Service 構成コンソールの左ペインで **[ローカルの CDC Service]** をクリックし、作業するサービスを CDC Service 構成コンソールの中央のセクションで選択します。  
  
     操作する CDC サービスを右クリックして、目的のアクションをクリックすることもできます。  
  
4.  CDC サービスの操作時には、以下のタスクを実行できます。  
  
    -   **サービスの削除**  
  
         サービスを削除するには、CDC Service 構成コンソールの右側にある **[アクション]** ペインで **[削除]** をクリックします。  
  
         または、削除する CDC サービスを右クリックして **[削除]** を選択します。  
  
         **注**:実行中のサービスを削除した場合、サービスは停止されてから削除されます。  
  
         Oracle CDC Windows Service の定義を削除するには、プログラムに、関連付けられている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内の MSXDBCDC データベースに対する更新アクセスが必要です。 **[OK]** をクリックしてサービスを削除すると、MSXDBCDC データベース内にある Oracle CDC Service 登録の削除が試みられます。 権限がないために削除できない場合、MSXDBCDC データベースに対する更新アクセスを持つ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを入力するためのダイアログ ボックスが表示されます。  
  
         [SQL Server への接続] ダイアログ ボックスに入力するデータについては、「 [Manage an Oracle CDC Service](manage-an-oracle-cdc-service.md) 」および「 [Connection to SQL Server for Delete](connection-to-sql-server-for-delete.md)」を参照してください。  
  
    -   **CDC Service のプロパティの編集**  
  
         CDC Service 構成コンソールの右側にある **[アクション]** ペインで **[プロパティ]** をクリックします。  
  
         または、プロパティを編集する CDC サービスを右クリックして **[プロパティ]** を選択します。  
  
## <a name="see-also"></a>関連項目  
 [Manage an Oracle CDC Service](manage-an-oracle-cdc-service.md)  
  
  
