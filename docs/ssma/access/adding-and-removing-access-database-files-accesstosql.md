---
title: データベース ファイル (AccessToSQL) の追加と削除のアクセス |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- adding Access files
- adding and removing Access databases
- browsing Access metadata
- browsing metadata, Access databases
- connecting, Access databases
- databases
- files, adding and removing
- finding Access databases
- finding database files
- locating database files
- metadata
- metadata, browsing
- metadata, refreshing
- refreshing metadata
- removing Access files
- scanning for database files
- searching for database files
ms.assetid: e944c740-4c8a-4bc1-b0ed-be57bc06dced
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 39df13a3cab2d842a313ca37fc4a98d0c331ba83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104213"
---
# <a name="adding-and-removing-access-database-files-accesstosql"></a>追加および Access データベース ファイル (AccessToSQL) を削除します。
アクセス データを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure では、SSMA プロジェクトに 1 つ以上の Access データベースを追加する必要があります。 これらのデータベースは、Access 97 または以降のバージョンである必要があります。 アクセスの以前のバージョンからのデータベースがある場合より新しいバージョンにデータベースを変換する必要があります。 これには開くして SSMA に追加する前に、Access 97 以降のバージョンでデータベースを保存します。  
  
## <a name="what-happens-when-you-add-access-database-files"></a>Access データベース ファイルを追加するとどうなりますか。  
SSMA プロジェクトに Access データベースを追加して SSMA は、データベースのメタデータを読み取るし、このメタデータをプロジェクト ファイルを追加します。 このメタデータには、データベースとそのオブジェクトについて説明します。 SSMA は、オブジェクトを変換するときに、メタデータを使用して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure の構文にデータを移行するときと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 アクセス メタデータ エクスプ ローラーでこのメタデータを参照して、個々 のデータベース オブジェクトのプロパティを確認できます。  
  
> [!NOTE]  
> Access データベースは、複数のファイルに分割することができます。 テーブルを含むバックエンド データベースとクエリ、フォーム、レポート、マクロ、モジュール、およびショートカットが含まれているフロント エンドのデータベース。 分割データベースを移行する場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure、SSMA をフロント エンドのデータベースを追加します。  
  
## <a name="permissions-that-are-required-by-ssma"></a>SSMA で必要なアクセス許可  
Access データベースを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure、ユーザー グループと管理者のユーザーには、管理のアクセス許可が必要です。 ワークグループの保護を持つデータベースを移行する方法については、次を参照してください。 [Access データベースを移行の準備](preparing-access-databases-for-migration-accesstosql.md)します。  
  
## <a name="selecting-databases-to-add"></a>追加するデータベースの選択  
SSMA プロジェクトでは、1 つまたは複数のデータベースを追加して、ファイルはすべて 1 つの既知の場所に場合、は、次の手順を使用して、ファイルを追加できます。  
  
**個々 のデータベース ファイルを追加するには**  
  
1.  **ファイル** メニューのをクリックして**データベースの追加**します。  
  
2.  **オープン** ダイアログ ボックスで、データベース ファイルまたはファイルが含まれているフォルダーに移動します。  
  
3.  ファイルを追加するをクリックする選択**オープン**します。  
  
## <a name="finding-databases-to-add"></a>追加するデータベースの検索  
SSMA プロジェクトでは、別のフォルダーから複数の Access データベースを追加する、またはファイルを検索することが 1 つのファイルを追加する、する次の手順を見つけてファイルの 1 つのプロジェクトに追加します。  
  
**検索データベースを追加するには**  
  
1.  **ファイル** メニューのをクリックして**検索データベース**します。  
  
2.  検索データベースのウィザードでは、ドライブ、ファイルのパスまたは UNC パスを検索したいの名前を入力します。 またはをクリックして**参照**ドライブまたはネットワーク フォルダーを指定します。  
  
3.  クリックして**追加**場所を一覧に追加します。  
  
    複数の検索場所を追加する前の 2 つの手順を繰り返します。  
  
4.  必要に応じて、返されるデータベースの一覧を絞り込む検索条件を追加します。  
  
    > [!IMPORTANT]  
    > **ファイル名の全部または一部**テキスト ボックスでは、ワイルドカード文字はサポートされません。  
  
5.  クリックして**スキャン**します。  
  
    スキャン ページが表示されます。 これには、検出されたデータベースと、検索の進行状況が表示されます。 検索を停止する をクリックして**停止**します。  
  
6.  ファイルの選択 ページで、プロジェクトに追加するデータベースを選択します。  
  
    使用することができます、**すべて選択**と**すべてクリア**を選択するか、すべてのデータベースをクリアするリストの上部にあるボタン。 CTRL キーを押しながら複数のデータベースを選択するか、SHIFT キーをデータベースの範囲を選択するようにできます。  
  
7.  **[次へ]** をクリックします。  
  
8.  確認してください ページで、次のようにクリックします。**完了**します。  
  
## <a name="browsing-access-metadata"></a>参照メタデータにアクセス  
Access データベースをプロジェクトに追加すると、アクセス メタデータ エクスプ ローラーでプロジェクトのメタデータが表示されます。 データベースと、エクスプ ローラーでデータベース オブジェクトの階層を参照することができます。  
  
**メタデータを参照するには**  
  
1.  メタデータ エクスプ ローラーでのアクセス、**アクセス メタベース**、順に展開**データベース**します。  
  
2.  確認するには、順に展開するデータベースを展開**クエリ**します。  
  
    クエリの一覧に注目してください。 クエリを選択する場合、 **SQL**  タブと**プロパティ**右側のウィンドウでタブが表示されます。  
  
3.  展開**テーブル**し、テーブルを選択します。  
  
    4 つのタブが表示されることに注意してください。**テーブル**、**の種類のマッピング**、**プロパティ**、および**データ**します。  
  
4.  テーブルを展開し、**キー**、キーを選択します。  
  
    右側のウィンドウで、キーのプロパティが表示されます。  
  
5.  展開**インデックス**、インデックスを選択します。  
  
    インデックスのプロパティは、右側のウィンドウに表示されます。  
  
## <a name="refreshing-databases"></a>データベースを更新します。  
そのファイルを追加した後に、Access データベースが変更された場合は、Access データベースからメタデータを更新できます。  
  
**アクセスのメタデータを更新するには**  
  
-   アクセス メタデータ エクスプ ローラーで、データベースを右クリックし、**データベースからの更新**します。  
  
## <a name="removing-databases"></a>データベースの削除  
Access データベースは、次の手順に従って、プロジェクトから削除できます。  
  
**プロジェクトからデータベースを削除するには**  
  
1.  メタデータ エクスプ ローラーでのアクセス、**アクセス メタベース**、順に展開**データベース**します。  
  
2.  データベースを右クリックし、**データベースの削除**します。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順が、 [SQL Server に接続](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)します。  
  
## <a name="see-also"></a>参照  
[SQL Server へのアクセス データベースの移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[作成して、プロジェクトの管理](creating-and-managing-projects-accesstosql.md)  
  
