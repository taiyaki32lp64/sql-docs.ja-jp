---
title: データベースに対するデータ ファイルまたはログ ファイルの追加 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], files
- adding data files
- adding files
- adding log files
- file additions [SQL Server], steps
- files [SQL Server], adding
- data additions [SQL Server]
ms.assetid: 8ead516a-1334-4f40-84b2-509d0a8ffa45
author: stevestein
ms.author: sstein
ms.openlocfilehash: 34e976dca163289450c3aa481d1f72bb46712046
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137404"
---
# <a name="add-data-or-log-files-to-a-database"></a>データベースに対するデータ ファイルまたはログ ファイルの追加
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]のデータベースにデータ ファイルまたはログ ファイルを追加する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **以下を使用してデータ ファイルまたはログ ファイルをデータベースに追加するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   BACKUP ステートメントの実行中にファイルを追加したり削除したりすることはできません。  
  
-   各データベースに、最大 32,767 のファイルと 32,767 のファイル グループを指定できます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 データベースに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-add-data-or-log-files-to-a-database"></a>データ ファイルまたはログ ファイルをデータベースに追加するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、ファイルを追加するデータベースを右クリックして、 **[プロパティ]** をクリックします。  
  
3.  **[データベースのプロパティ]** ダイアログ ボックスで、 **[ファイル]** ページをクリックします。  
  
4.  データ ファイルまたはトランザクション ログ ファイルを追加するには、 **[追加]** をクリックします。  
  
5.  **[データベース ファイル]** グリッドに、ファイルの論理名を入力します。 このファイル名は、データベース内で一意になる必要があります。  
  
6.  ファイルの種類 (データまたはログ) を選択します。  
  
7.  データ ファイルの場合、ファイルを含めるファイル グループを一覧から選択するか、 **[\<新しいファイル グループ>]** をクリックして新しいファイル グループを作成します。 トランザクション ログはファイル グループに追加できません。  
  
8.  ファイルの初期サイズを指定します。 データベースに格納するデータの予想最大量に基づいて、データ ファイルのサイズを可能な限り大きく設定しておきます。  
  
9. ファイルの拡張方法を指定するには、 **[自動拡張]** 列で参照ボタン ( **[...]** ) をクリックします。 次のオプションから選択します。  
  
    1.  データ領域の追加が必要になったときに、現在選択されているファイルを拡張できるようにするには、 **[自動拡張を有効にする]** チェック ボックスをオンにして、次のオプションから選択します。  
  
    2.  ファイルを一定の増加値で拡張することを指定するには、 **[MB 単位]** をクリックして、値を指定します。  
  
    3.  現在のファイル サイズとの比率でファイルを拡張することを指定するには、 **[比率]** をクリックして、値を指定します。  
  
10. 最大ファイル サイズの制限を指定するには、次のオプションから選択します。  
  
    1.  ファイルを拡張できる最大サイズを指定するには、 **[ファイル拡張の制限 (MB)]** をクリックして、値を指定します。  
  
    2.  必要なだけファイルを拡張できるようにするには、 **[ファイルを無制限に拡張]** をクリックします。  
  
    3.  ファイルの拡張を禁止するには、 **[自動拡張を有効にする]** チェック ボックスをオフにします。 このように設定しておくと、ファイルのサイズが、 **[初期サイズ (MB)]** 列に指定した値より大きくなることはありません。  
  
    > [!NOTE]  
    >  データベースの最大サイズは、使用できるディスクの空き領域、および使用中の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンによって決まるライセンス制限で決定されます。  
  
11. ファイルの場所のパスを指定します。 指定したパスは、ファイルを追加する前に存在していなければなりません。  
  
    > [!NOTE]  
    >  データ ファイルとトランザクション ログ ファイルは、既定では単一ディスクのシステムに適合するように、同じドライブおよびパスに配置されますが、実稼働環境ではこれが最適ではない場合があります。 詳細については、「 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)」を参照してください。  
  
12. **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-add-data-or-log-files-to-a-database"></a>データ ファイルまたはログ ファイルをデータベースに追加するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、2 つのファイルから成るファイル グループをデータベースに追加します。 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースに `Test1FG1` ファイル グループを作成し、そのファイル グループに 5 MB のファイルを 2 つ追加します。  
  
 [!code-sql[DatabaseDDL#AlterDatabase2](../../relational-databases/databases/codesnippet/tsql/add-data-or-log-files-to_1.sql)]  
  
 詳細については、「[ALTER DATABASE の File および Filegroup オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)   
 [データまたはログ ファイルのデータベースからの削除](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)   
 [データベースのサイズを大きくする](../../relational-databases/databases/increase-the-size-of-a-database.md)  
  
  
