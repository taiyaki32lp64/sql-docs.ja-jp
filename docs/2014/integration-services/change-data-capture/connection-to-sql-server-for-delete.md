---
title: 削除用の SQLServer への接続 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 030b10c2-6b88-4c2c-bf67-22994be25a60
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: acb755f8cc1e425e38714013511948f7b5b4c580
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62836862"
---
# <a name="connection-to-sql-server-for-delete"></a>削除用の SQLServer への接続
  MSXDBCDC データベースに対する書き込み権限を含むデータベース ロール (**db_owner** ロールなど) を持たないログインが Oracle CDC インスタンスの削除を試みると、[SQL Server への接続] ダイアログ ボックスが表示されます。  
  
 Oracle CDC インスタンスを削除するには、このダイアログ ボックスに、 **db_owner** データベース ロールなど、MSXDBCDC データベースに対する書き込み権限を持つログインの資格情報を入力する必要があります。  
  
 [SQL Server への接続] ダイアログ ボックスに次の情報を入力します。  
  
 **[サーバー名]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が存在するサーバーの名前を入力します。  
  
 **[認証]**  
 次のいずれかを選択します。  
  
-   **[Windows 認証]**  
  
-   **[SQL Server 認証]**: このオプションを選択する場合、接続先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のユーザーの **[ログイン]** と **[パスワード]** を入力する必要があります。  
  
 **[オプション]**  
 矢印をクリックして、構成するオプションを表示します。 これらのオプションを既定値のままにすることもできます。 使用可能なオプションは次のとおりです。  
  
-   **[接続タイムアウト]**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続が確立されるまでプログラムが待機する時間 (秒単位) を入力します。この時間を超過するとタイムアウト エラーが発生します。 既定値は **15**です。  
  
-   **[実行タイムアウト]**: SQL コマンドの実行が完了するまでプログラムが待機する時間 (秒単位) を入力します。この時間を超過するとタイムアウト エラーが発生します。 既定値は、 **30**です。  
  
-   **[暗号化接続]**: 確立する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続を暗号化してプライバシーを確保するには、**[暗号化接続]** を選択します。  
  
-   **[詳細設定]**:必要に応じて、 **[詳細設定]** をクリックし、[高度な接続プロパティ] ダイアログ ボックスに追加の接続プロパティを入力します。  
  
## <a name="see-also"></a>参照  
 [CDC Service で使用する SQL Server 接続に必要な権限](sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  
