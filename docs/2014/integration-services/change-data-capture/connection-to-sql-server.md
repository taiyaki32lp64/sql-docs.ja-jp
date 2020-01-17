---
title: SQL Server への接続 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5bb582f9-68d3-4c1e-ab02-6fc16807f1a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 09d597cb7776362c44ca53e8d544f66608d8d37c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62837002"
---
# <a name="connection-to-sql-server"></a>SQL Server への接続
  MSXDBCDC データベースに対する書き込み権限を含むデータベース ロール (**db_owner** ロールなど) を持たないログインが Oracle CDC インスタンスの作成を試みると、[SQL Server への接続] ダイアログ ボックスが表示されます。  
  
 新しい Oracle CDC インスタンスを作成するには、このダイアログ ボックスに、 **db_owner** データベース ロールなど、MSXDBCDC データベースに対する書き込み権限を持つログインの資格情報を入力する必要があります。  
  
 [SQL Server への接続] ダイアログ ボックスに次の情報を入力します。  
  
### <a name="server-name"></a>[サーバー名]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が存在するサーバーの名前を入力します。  
  
### <a name="authentication"></a>認証  
 次のいずれかを選択します。  
  
-   [Windows 認証]  
  
-   **[SQL Server 認証]**: このオプションを選択する場合、接続先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のユーザーの **[ログイン]** と **[パスワード]** を入力する必要があります。  
  
### <a name="options"></a>および  
 矢印をクリックして、構成するオプションを表示します。 これらのオプションを既定値のままにすることもできます。 使用可能なオプションは次のとおりです。  
  
-   **[接続タイムアウト]**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続が確立されるまでプログラムが待機する時間 (秒単位) を入力します。この時間を超過するとタイムアウト エラーが発生します。 既定値は **15**です。  
  
-   **[実行タイムアウト]**: SQL コマンドの実行が完了するまでプログラムが待機する時間 (秒単位) を入力します。この時間を超過するとタイムアウト エラーが発生します。 既定値は、 **30**です。  
  
-   **[暗号化接続]**: 確立する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続を暗号化してプライバシーを確保するには、**[暗号化接続]** を選択します。  
  
-   **[詳細設定]**:必要に応じて、 **[詳細設定]** をクリックし、[高度な接続プロパティ] ダイアログ ボックスに追加の接続プロパティを入力します。  
  
## <a name="see-also"></a>関連項目  
 [CDC Service で使用する SQL Server 接続に必要な権限](sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  
