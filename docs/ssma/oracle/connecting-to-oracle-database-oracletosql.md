---
title: Oracle データベース (OracleToSQL) に接続する |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Refreshing Oracle Metadata
ms.assetid: e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: fc25c36a0d0133975414f4c7270da2974b552f40
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266186"
---
# <a name="connecting-to-oracle-database-oracletosql"></a>Oracle データベースへの接続 (OracleToSQL)
Oracle データベースを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、移行する Oracle データベースに接続する必要があります。 接続すると、SSMA は、すべての Oracle スキーマに関するメタデータを取得し、Oracle メタデータ エクスプ ローラー ペインに表示します。 SSMA は、データベース サーバーに関する情報を格納しますが、パスワードは保存されません。  
  
プロジェクトを閉じるまで、データベースへの接続をアクティブに保ちます。 プロジェクトを再度開くとする場合は、データベースにアクティブな接続を再接続する必要があります。  
  
Oracle データベースについてのメタデータは、自動的に更新されません。 代わりに、Oracle メタデータ エクスプ ローラーでメタデータを更新する場合は、手動で更新してください。 詳細については、このトピックの後半の「Oracle メタデータを更新」セクションを参照してください。  
  
## <a name="required-oracle-permissions"></a>必要な Oracle の権限  
Oracle データベースへの接続に使用されるアカウントが少なくとも必要**CONNECT**アクセス許可。 これにより、SSMA を接続するユーザーが所有するスキーマからメタデータを取得できます。 他のスキーマ内のオブジェクトのメタデータを取得し、それらのスキーマ内のオブジェクトを変換は、次のアクセス許可がアカウントに必要です。  
  
-   すべてのプロシージャを作成します。  
  
-   すべてのプロシージャを実行します。  
  
-   任意のテーブルを選択します。  
  
-   任意のシーケンスを選択します。  
  
-   任意の型を作成します。  
  
-   CREATE ANY TRIGGER  
  
-   すべてのディクショナリを選択します。  
  
## <a name="establishing-a-connection-to-oracle"></a>Oracle への接続を確立します。  
データベースに接続するときに SSMA は、データベースのメタデータを読み取るし、プロジェクト ファイルにこのメタデータを追加します。 このメタデータは、オブジェクトを変換するとき、SSMA によって使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]構文へのデータを移行する場合と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 Oracle メタデータ エクスプ ローラー ウィンドウでこのメタデータを参照して、個々 のデータベース オブジェクトのプロパティを確認できます。  
  
> [!IMPORTANT]  
> 接続しようとすると、前に、データベース サーバーを実行しているし、接続を受け入れることを確認します。  
  
**Oracle に接続するには**  
  
1.  **ファイル**メニューの  **Connect to Oracle**します。  
  
    Oracle に接続されていた場合、コマンド名になります**Oracle への再接続**します。  
  
2.  **プロバイダー**ボックスで、 **Oracle Client プロバイダー**または**OLE DB Provider**にプロバイダーがインストールされている依存します。 既定値は、Oracle クライアントです。  
  
3.  **モード**ボックスで、いずれかを選択**標準モード**、 **TNSNAME モード**、または**接続文字列モード**します。  
  
    標準モードを使用すると、サーバー名とポートを指定します。 Oracle サービス名を手動で指定するのにには、サービス名のモードを使用します。 完全な接続文字列を指定するのにには、接続文字列モードを使用します。  
  
4.  選択した場合**標準モード**、次の値を指定します。  
  
    1.  **サーバー名**ボックスで、入力するか、またはデータベース サーバーの IP アドレスを選択します。  
  
    2.  既定値が (1521) のポートでの Oracle の接続に使用されるポート番号を入力の接続を受け入れるように、データベース サーバーが構成されていない場合、**サーバー ポート**ボックス。  
  
    3.  **Oracle SID**ボックスに、システム識別子を入力します。  
  
    4.  **ユーザー名**ボックスに、必要なアクセス許可のある Oracle アカウントを入力します。  
  
    5.  **パスワード**ボックスに、指定されたユーザー名のパスワードを入力します。  
  
5.  選択した場合**TNSNAME モード**、次の値を指定します。  
  
    1.  **接続識別子**入力ボックスに、データベースの識別子 (TNS 別名) を接続します。  
  
    2.  **ユーザー名**ボックスに、必要なアクセス許可のある Oracle アカウントを入力します。  
  
    3.  **パスワード**ボックスに、指定されたユーザー名のパスワードを入力します。  
  
6.  選択した場合**接続文字列モード**での接続文字列を指定、**接続文字列**ボックス。  
  
    次の例では、OLE DB 接続文字列を示しています。  
  
    `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`  
  
    次の例は、統合セキュリティを使用する Oracle クライアント接続文字列を示しています。  
  
    `Data Source=MyOracleDB;Integrated Security=yes;`  
  
    詳細については、次を参照してください。 [Oracle に接続する&#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)します。  
  
## <a name="reconnecting-to-oracle"></a>Oracle への再接続  
プロジェクトを閉じるまで、データベース サーバーへの接続をアクティブに保ちます。 プロジェクトを再度開くとする場合は、データベースにアクティブな接続を再接続する必要があります。 メタデータを更新するには、データベース オブジェクトに読み込む必要になるまでオフラインで作業できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データを移行します。  
  
## <a name="refreshing-oracle-metadata"></a>Oracle のメタデータの更新  
Oracle データベースについてのメタデータは、自動的に更新されません。 Oracle メタデータ エクスプ ローラー内のメタデータは、初めて接続されたときのメタデータまたはメタデータを手動で更新された前回のスナップショットです。 すべてのスキーマ、1 つのスキーマ、または個々 のデータベース オブジェクトのメタデータを手動で更新することができます。  
  
**メタデータを更新するには**  
  
1.  データベースに接続していることを確認します。  
  
2.  Oracle メタデータ エクスプ ローラーでは、更新する各スキーマまたはデータベース オブジェクトの横にあるチェック ボックスを選択します。  
  
3.  右クリック**スキーマ**、個々 のスキーマまたはデータベース オブジェクトをクリックし **データベースからの更新**します。  
  
    アクティブな接続がない、SSMA が表示されます、 **Connect to Oracle**ダイアログ ボックスを接続することができます。  
  
4.  [データベース] ダイアログ ボックスから、更新、更新するには、どのオブジェクトを指定します。  
  
    -   オブジェクトを更新する をクリックして、 **Active**矢印が表示されるまでオブジェクトの横にあるフィールドです。  
  
    -   オブジェクトが更新されていることを防ぐためにをクリックして、 **Active**までオブジェクトの横にあるフィールド、 **X**が表示されます。  
  
    -   更新頻度や、オブジェクトのカテゴリを拒否する をクリックして、 **Active**カテゴリ フォルダーの横にあるフィールドです。  
  
    色の設定の定義を表示する をクリックして、**凡例**ボタンをクリックします。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-step"></a>次の手順  
  
-   移行プロセスの次の手順が、 [SQL Server のインスタンスへの接続](connecting-to-sql-server-oracletosql.md)します。  
  
## <a name="see-also"></a>参照  
[SQL Server にデータベースを移行する Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
