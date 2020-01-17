---
title: '[サーバーへの接続]([追加の接続パラメーター] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttoserver.options.registeredservers.f1
ms.assetid: ba34b01a-6289-4eb8-8341-fa3d9ec87b3f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e92fbb8bc29aed54e43925a0670d9a365388df62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62808680"
---
# <a name="connect-to-server-additional-connection-parameters-page"></a>[サーバーへの接続] \([追加の接続パラメーター] ページ)
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の **[接続先]** ダイアログ ボックスには、オプションとして最も一般的な接続文字列値が表示されます。 **[追加の接続パラメーター]** ページを使用すると、接続文字列に接続パラメーターをさらに追加できます。  
  
-   追加の接続パラメーターには、任意の ODBC 接続パラメーターを使用できます。  
  
-   追加の接続パラメーターは、 **;parameter1=value1;parameter2=value2**という形式で追加する必要があります。  
  
-   **[追加の接続パラメーター]** ページを使用して追加したパラメーターは、 **[接続先]** ダイアログ ボックスのオプションを使用して選択したパラメーターに追加されます。  
  
-   指定した各パラメーターの最後のインスタンスは、そのパラメーターの前のインスタンスをオーバーライドします。 **[追加の接続パラメーター]** ページを使用して追加したパラメーターは、 **[ログイン]** タブまたは **[接続プロパティ]** タブで指定したパラメーターより優先されます。 たとえば、 **[ログイン]** タブの **[サーバー名]** で「 **SERVER1**」と指定し、 **[追加の接続パラメーター]** ページで「 **;SERVER=SERVER2**」と指定した場合、 **SERVER2**に接続されます。  
  
-   **[追加の接続パラメーター]** ページで追加したパラメーターは、常にプレーン テキストとして渡されます。  
  
    > [!IMPORTANT]  
    >  **[追加の接続パラメーター]** ページにはログイン資格情報やパスワードを含めないでください。 このダイアログ ボックスで指定したパラメーターは、ネットワーク経由で渡されるときに暗号化されません。 代わりに **[ログイン]** タブを使用してください。  
  
## <a name="task-list"></a>タスク一覧  
  
### <a name="to-show-the-additional-connection-parameters-page"></a>[追加の接続パラメーター] ページを表示するには  
  
1.  [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]で、 **[クエリ]** メニューの **[接続]** をポイントし、 **[接続]** をクリックします。  
  
2.  **[接続先]** ダイアログ ボックスで、 **[オプション]** をクリックし、 **[追加の接続パラメーター]** タブをクリックします。  
  
## <a name="examples"></a>使用例  
  
### <a name="example-a-connecting-to-the-database-engine"></a>例 a:データベース エンジンへの接続  
 ACCOUNTING というサーバーの [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] データベースに接続するには、 **[追加の接続パラメーター]** ページに次のように入力します。  
  
```  
;SERVER=ACCOUNTING;DATABASE=AdventureWorks2012  
```  
  
### <a name="example-b-connecting-to-analysis-services"></a>例 b:Analysis Services への接続  
 分析サーバーに接続し、通知をリッスンするすべてのパーティションに対するクエリが (キャッシュをバイパスして) リアルタイムで実行されるようにして、書き戻しのタイムアウト値を 5 に設定するには、 **[追加の接続パラメーター]** ページに次のように入力します。  
  
```  
;Real Time Olap=TRUE;Writeback Timeout=5  
```  
  
  
