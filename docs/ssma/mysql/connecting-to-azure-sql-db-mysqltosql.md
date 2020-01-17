---
title: Azure SQL DB (MySQLToSQL) への接続 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Azure, SQL Azure permissions
- Connecting to SQL Azure, synchronization
ms.assetid: d0b6f16a-1880-459d-a0c7-28b7ef15c56a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7fb6740681c08cb915755b3362352f139e078c4c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103189"
---
# <a name="connecting-to-azure-sql-db-mysqltosql"></a>Azure SQL DB への接続 (MySQLToSQL)
MySQL データベースを SQL Azure に移行するには、SQL Azure のターゲット インスタンスに接続する必要があります。 接続するときに、SSMA は SQL Azure のインスタンスのすべてのデータベースに関するメタデータを取得し、SQL Azure メタデータ エクスプ ローラーでデータベースのメタデータを表示します。 SSMA は、パスワードは保存されませんに接続している SQL Azure のインスタンスの情報を格納します。  
  
プロジェクトを閉じるまで SQL Azure への接続をアクティブに保ちます。 プロジェクトを再度開くと、アクティブなサーバーに接続する場合 SQL Azure に再接続する必要があります。 SQL Azure にデータベース オブジェクトを読み込むし、データを移行するまで、オフライン使用できます。  
  
SQL Azure のインスタンスに関するメタデータは、自動的に同期されません。 代わりに、SQL Azure メタデータ エクスプ ローラー内のメタデータを更新するには、SQL Azure メタデータを手動で更新する必要があります。 詳細については、このトピックの後半の「SQL Azure メタデータの同期」セクションを参照してください。  
  
## <a name="required-sql-azure-permissions"></a>SQL Azure に必要なアクセス許可  
SQL Azure への接続に使用されるアカウントには、アカウントで実行された操作に応じてさまざまなアクセス許可が必要です。  
  
-   MySQL のオブジェクトに変換する[!INCLUDE[tsql](../../includes/tsql-md.md)]スクリプトの構文は、SQL Azure からメタデータを更新するかに変換された構文を保存する、アカウントは SQL Azure のインスタンスにログオンする権限が必要です。  
  
-   を SQL Azure にデータベース オブジェクトを読み込むにはアクセス許可の最小要件、メンバーシップ、 **db_owner**ターゲット データベースのデータベース ロール。  
  
## <a name="establishing-a-sql-azure-connection"></a>SQL Azure を確立する接続  
MySQL データベースのオブジェクトを SQL Azure の構文に変換する前に、または複数の MySQL データベースを移行する SQL Azure のインスタンスへの接続を確立する必要があります。  
  
接続のプロパティを定義するときに、オブジェクトとデータを移行するデータベースを指定します。 SQL Azure に接続した後は、MySQL スキーマ レベルでは、このマッピングをカスタマイズできます。 詳細については、次を参照してください[MySQL データベースを SQL Server スキーマへのマッピング&#40;MySQLToSQL。&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> SQL Azure に接続する前に、SQL Azure のインスタンスが実行されていて、接続を受け入れることを確認します。  
  
**SQL Azure に接続するには**  
  
1.  **ファイル**メニューの  **SQL Azure への接続**(このオプションは、プロジェクトの作成後に有効です)。  
  
    SQL Azure に以前接続した場合、コマンド名になります**SQL Azure に再接続**します。  
  
2.  接続ダイアログ ボックスで入力するか、SQL Azure のサーバー名を選択します。  
  
3.  入力を選択または**参照**データベース名。  
  
4.  入力または選択**UserName**します。  
  
5.  入力、**パスワード**します。  
  
6.  SSMA では、SQL Azure に暗号化された接続をお勧めします。  
  
7.  **[接続]** をクリックします。  
  
> [!IMPORTANT]  
> SSMA for MySQL はへの接続をサポートしていません**マスター** SQL Azure データベース。  
  
## <a name="synchronizing-sql-azure-metadata"></a>SQL Azure の同期メタデータ  
SQL Azure データベースに関するメタデータは、自動的に更新されません。 SQL Azure メタデータ エクスプ ローラー内のメタデータは、SQL Azure に最初に接続すると、最後を手動でメタデータのスナップショットには、メタデータが更新されました。 すべてのデータベースまたは任意の 1 つのデータベースまたはデータベース オブジェクトのメタデータを手動で更新することができます。  
  
**メタデータを同期するには**  
  
1.  SQL Azure に接続していることを確認します。  
  
2.  SQL Azure メタデータ エクスプ ローラーで、データベースまたはデータベースのスキーマを更新する横のチェック ボックスを選択します。  
  
    たとえば、すべてのデータベースのメタデータを更新するには、データベースの横にあるボックスを選択します。  
  
3.  データベース、または個々 のデータベースまたはデータベースのスキーマを右クリックし、**データベースと同期する**します。  
  
## <a name="next-step"></a>次の手順  
移行の次の手順は、プロジェクトのニーズによって異なります。  
  
-   MySQL スキーマと SQL Azure データベースとスキーマの間のマッピングをカスタマイズするを参照してください[SQL Server スキーマへのマッピングの MySQL データベース&#40;MySQLToSQL。&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   プロジェクトの構成オプションをカスタマイズするを参照してください[プロジェクト オプションの設定&#40;MySQLToSQL。&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   ソースとターゲットのデータ型のマッピングをカスタマイズするを参照してください[マッピング MySQL および SQL Server データ型&#40;MySQLToSQL。&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   これらのタスクを実行する必要はありません場合、MySQL データベースのオブジェクトの定義を SQL Azure のオブジェクトの定義に変換できます。 詳細については、次を参照してください[MySQL データベースを変換する&#40;MySQLToSQL。&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>関連項目  
[SQL Server - Azure SQL DB への移行 MySQL データベース&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
