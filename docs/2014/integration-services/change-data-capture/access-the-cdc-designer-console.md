---
title: CDC デザイナー コンソールへのアクセス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- accMsDes
ms.assetid: b168c64e-c1b5-42d4-a92a-84de1dd0324e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c552ef16cc2f9502a365ba09c7f8868eccd53396
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62836084"
---
# <a name="access-the-cdc-designer-console"></a>CDC デザイナー コンソールへのアクセス
  CDC デザイナー コンソールには、コンソールをインストールしたコンピューターからアクセスすることができます。 インストールの詳細については、インストールを参照してください。  
  
 CDC デザイナー コンソールを開くと、[SQL Server への接続] ダイアログ ボックスが表示されます。  
  
 CDC デザイナーにアクセスする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインには、MSXDBCDC データベースに対する UPDATE 権限が必要です。 また、新しい Oracle CDC インスタンスを作成するには、ログインが `dbcreator` 固定サーバー ロールを持っている必要もあります。 また、使用する CDC データベースへの SELECT アクセス権がログインに含まれていることも推奨されます。このアクセス権が含まれていない場合、ユーザーはそれらのデータベースの状態を表示できません。  
  
 [SQL Server への接続] ダイアログ ボックスに次の情報を入力します。  
  
### <a name="server-name"></a>[サーバー名]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が存在するサーバーの名前を入力します。  
  
### <a name="authentication"></a>認証  
 次のいずれかを選択します。  
  
-   **[Windows 認証]**  
  
-   **[SQL Server 認証]** : このオプションを選択する場合、接続先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のユーザーの **[ログイン]** と **[パスワード]** を入力する必要があります。  
  
 ログインには、MSXCDCDB データベースへのアクセスを許可するデータベース ロールが必要です。 また、使用する追加のデータベースへのアクセスがログインに含まれていることも推奨されます。このアクセスが含まれていない場合、ユーザーはそれらのデータベース内のデータを表示できません。  
  
### <a name="options"></a>および  
 矢印をクリックして、構成するオプションを表示します。 これらのオプションを既定値のままにすることもできます。 使用可能なオプションは次のとおりです。  
  
 **[接続タイムアウト]**  
 CDC Service for Oracle が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続を待機する時間 (秒単位) を入力します。この時間を超過するとタイムアウトとなります。既定値は **15**です。  
  
 **[実行タイムアウト]**  
 Oracle CDC Windows Service がコマンドの実行を待機する時間 (秒単位) を入力します。この時間を超過するとタイムアウトとなります。既定値は、 **30**です。  
  
 **[暗号化接続]**  
 Oracle CDC Service とターゲットの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの間の暗号化された接続を使用した通信に対しては、 **[暗号化接続]** を選択します。 **[詳細設定]** : 必要に応じて、 **[詳細設定]** をクリックし、[高度な接続プロパティ] ダイアログ ボックスに追加の接続プロパティを入力します。  
  
 **詳細設定**  
 必要に応じて、 **[詳細設定]** をクリックし、[高度な接続プロパティ] ダイアログ ボックスに追加の接続プロパティを入力します。  
  
 [高度な接続プロパティ] ダイアログ ボックスの詳細については、「 [高度な接続プロパティ](advanced-connection-properties.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [CDC デザイナーで使用する SQL Server 接続に必要な権限](sql-server-connection-required-permissions-for-the-cdc-designer.md)  
  
  
