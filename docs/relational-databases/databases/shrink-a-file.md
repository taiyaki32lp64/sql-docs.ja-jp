---
title: ファイルの圧縮 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.shrinkfile.f1
helpviewer_keywords:
- shrinking files
- decreasing file size
- databases [SQL Server], shrinking
- reducing file size
- size [SQL Server], files
- file size [SQL Server]
ms.assetid: ce5c8798-c039-4ab2-81e7-90a8d688b893
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3adf38c1908e17dbac530cab0cc47658e9241559
ms.sourcegitcommit: 5d9ce5c98c23301c5914f142671516b2195f9018
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71961930"
---
# <a name="shrink-a-file"></a>ファイルの圧縮
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]のデータ ファイルまたはログ ファイルを圧縮する方法について説明します。  
  
 ファイルの末尾にあるデータのページを、ファイルの先頭に近い占有されていない領域に移動することにより、データ ファイルが圧縮され、領域が回復されます。 ファイル末尾に十分な空き領域が作成された場合は、ファイル末尾のデータ ページの割り当てを解除して、ファイル システムに戻すことができます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
     [セキュリティ](#Security)  
  
-   **以下を使用してデータ ファイルまたはログ ファイルを圧縮するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   プライマリ データ ファイルは、model データベースのプライマリ ファイルのサイズより小さくすることはできません。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   ファイルを圧縮するために移動されたデータは、ファイル内のあらゆる使用可能な場所に分散される場合があります。 これにより、インデックスの断片化が発生し、広範なインデックスを検索するクエリのパフォーマンスが低下する場合があります。 断片化を解消するには、圧縮後にファイルのインデックスを再構築することを検討してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 **sysadmin** 固定サーバー ロールまたは **db_owner** 固定データベース ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-shrink-a-data-or-log-file"></a>データ ファイルまたはログ ファイルを圧縮するには  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、圧縮するデータベースを右クリックします。  
  
3.  **[タスク]** 、 **[圧縮]** の順にポイントし、 **[ファイル]** をクリックします。  
  
     **[データベース]**  
     選択しているデータベースの名前が表示されます。  
  
     **ファイルの種類**  
     ファイルの種類を選択します。 選択できるファイルの種類は **[データ]** および **[ログ]** です。 既定の選択は **[データ]** です。 別のファイル グループの種類を選択すると、その選択に応じて他のフィールドの選択が変更されます。  
  
     **ファイル グループ**  
     上記で選択した **[ファイルの種類]** に関連付けられたファイル グループの一覧から、ファイル グループを選択します。 別のファイル グループを選択すると、その選択に応じて他のフィールドの選択が変更されます。  
  
     **[ファイル名]**  
     選択したファイル グループおよびファイルの種類で利用可能なファイルの一覧からファイルを選択します。  
  
     **場所**  
     現在選択されているファイルへの完全なパスを表示します。 このパスは編集できませんが、クリップボードにコピーできます。  
  
     **[現在割り当てられている領域]**  
     データ ファイルの場合は、現在割り当てられている領域が表示されます。 ログ ファイルの場合は、DBCC SQLPERF(LOGSPACE) の出力から計算された、現在割り当てられている領域が表示されます。  
  
     **[使用可能な空き領域]**  
     データ ファイルの場合は、DBCC SHOWFILESTATS(fileid) の出力から計算された、現在使用できる空き領域が表示されます。 ログ ファイルの場合は、DBCC SQLPERF(LOGSPACE) の出力から計算された、現在使用できるスペースが表示されます。  
  
     **[未使用領域を解放する]**  
     ファイル内のすべての未使用領域をオペレーティング システムに渡し、ファイルを最後に割り当てられたエクステントにまで圧縮して、データをまったく移動せずにファイル サイズを小さくします。 割り当てられていないページへの行の再割り当て処理は行われません。  
  
     **[未使用領域の解放前にページを再構成する]**  
     対象ファイルのサイズを指定して DBCC SHRINKFILE を実行することと同じです。 このオプションがオンになっている場合は、 **[圧縮先のファイル]** ボックスで対象ファイルのサイズを指定する必要があります。  
  
     **[圧縮先のファイル]**  
     圧縮操作の対象ファイルのサイズを指定します。 サイズは、現在割り当てられている領域より大きく、ファイルに割り当てられた合計エクステントよりも小さくする必要があります。 最小値または最大値の範囲外の値を入力した場合、フォーカスを変更したり、ツール バーのボタンをクリックしたりしたときに、入力した値が最小値または最大値に戻ります。  
  
     **[データを同じファイル グループの他のファイルに移行してファイルを空にする]**  
     指定したファイルからすべてのデータを移行します。 このオプションを使用すると、ALTER DATABASE ステートメントを使用してファイルを削除することができます。 このオプションは、EMPTYFILE オプションを指定して DBCC SHRINKFILE を実行することと同じです。  
  
4.  ファイルの種類とファイル名を選択します。  
  
5.  必要に応じて、 **[未使用領域を解放する]** をオンにします。  
  
     このオプションをオンにすると、ファイル内の未使用領域がオペレーティング システムに解放され、最後に割り当てられたエクステントにファイルが圧縮されます。 これにより、データを移動しなくてもファイル サイズが減少します。  
  
6.  必要に応じて、 **[未使用領域の解放前にファイルを再構成する]** をオンにします。 このオプションをオンにする場合は、 **[圧縮先のファイル]** の値を指定する必要があります。 既定では、このオプションはオフになっています。  
  
     このオプションをオンにすると、ファイル内の未使用領域がオペレーティング システムに解放され、未割り当てページに行の再割り当てを試みます。  
  
7.  必要に応じて、データベースを圧縮した後に、データベース ファイル内に残す空き領域の最大のパーセンテージを入力します。 0 ～ 99 の値を指定できます。 このオプションは、 **[未使用領域の解放前にファイルを再構成する]** がオンになっている場合にのみ使用できます。  
  
8.  必要に応じて、 **[データを同じファイル グループの他のファイルに移行してファイルを空にする]** をオンにします。  
  
     このオプションをオンにすると、指定したファイルのすべてのデータが同じファイル グループの他のファイルに移動されます。 その後、空になったファイルを削除できます。 このオプションは、EMPTYFILE オプションを指定して DBCC SHRINKFILE を実行するのと同じ効果があります。  
  
9. **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-shrink-a-data-or-log-file"></a>データ ファイルまたはログ ファイルを圧縮するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) を使用して、 `UserDB` データベースに存在する `DataFile1` という名前のデータ ファイルのサイズを 7 MB に圧縮します。  
  
 [!code-sql[DBCC#DBCC_SHRINKFILE1](../../relational-databases/databases/codesnippet/tsql/shrink-a-file_1.sql)]  
  
## <a name="see-also"></a>参照  
 [DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)   
 [データベースの圧縮](../../relational-databases/databases/shrink-a-database.md)   
 [データまたはログ ファイルのデータベースからの削除](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
  
  
