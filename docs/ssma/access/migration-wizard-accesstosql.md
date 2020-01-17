---
title: 移行ウィザード (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migration Wizard dialog box
- Migration Wizard, adding Access databases
- Migration Wizard, Connect to SQL Azure
- Migration Wizard, Connect to SQL Server
- Migration Wizard, Link Tables
- Migration Wizard, Migration status
- Migration Wizard, New Project
- Migration Wizard, Selecting objects to migrate
ms.assetid: 5bab5914-b2ae-4795-8cf5-83e42d64bef2
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 658487186924fe5547edee70425524b2b4e3be6c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083591"
---
# <a name="migration-wizard-accesstosql"></a>移行ウィザード (AccessToSQL)
移行ウィザードを 1 つまたは複数のデータベースの移行へのアクセスを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 ウィザードを使用すると、するはプロジェクトを作成、データベース プロジェクトを追加、移行、およびに接続するオブジェクトの選択[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 変換、読み込み、および Access スキーマとデータを移行もされます。 アクセス テーブルをリンクする必要に応じて、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のテーブル。  
  
移行ウィザードのページのほとんどには、既存の SSMA ダイアログ ボックスと同じオプションが含まれます。 そのため、ウィザードのページが、ここで説明し、リンクも個別のオプションについて詳細を提供します。 ページに固有のオプションが含まれている場合、ここで説明されます。  
  
## <a name="starting-the-migration-wizard"></a>移行ウィザードの開始  
既定では、移行ウィザードは、SSMA を起動するときに表示されます。 ウィザードを開始することもできます、**ファイル**メニューを選択して**移行ウィザード**します。  
  
## <a name="welcome-page"></a>[ようこそ] ページ  
[ようこそ] ページでは、移行ウィザードを紹介し、ウィザードを開始するための次のオプションを提供します。  
  
**スタートアップ時に、このウィザードを起動します。**  
既定では、SSMA を起動すると、SSMA は、移行ウィザードを開始します。 ウィザードの自動開始を防ぐためには、このチェック ボックスをオフにします。  
  
## <a name="create-new-project-page"></a>新しいプロジェクト ページを作成します。  
新しいプロジェクトの作成ページには、プロジェクト ファイル名、場所、および移行プロジェクトの種類 (target の移行に使用される SQL Server のバージョン) を入力します。 詳細については、次を参照してください[新しいプロジェクト (SSMA)。](https://msdn.microsoft.com/ca294f6d-eeb5-42ca-9306-156281a3f0f3)  
  
## <a name="add-access-databases-page"></a>Access データベースのページを追加します。  
Access データベースの追加 ページでは、プロジェクトに 1 つ以上の Access データベースを追加します。 クリックして個々 のデータベースを追加する**データベースの追加**からデータベースを選択し、**オープン**ウィンドウ。 または、使用してデータベースを検索することができます、**検索データベース**ボタンをクリックします。 詳細については、次の各トピックを参照してください。  
  
-   [追加して、Access データベース ファイルを削除します。](adding-and-removing-access-database-files-accesstosql.md)  
  
-   [データベースのウィザード (場所の選択) を検索します。](https://msdn.microsoft.com/00b2d32a-998b-47a7-b25c-589b5bd6777a)  
  
-   [データベースのウィザード (ファイルの選択) を検索します。](https://msdn.microsoft.com/2f574a34-4bab-40a4-89a8-ad4907ffc3fd)  
  
-   [データベースのウィザードを検索 (選択の確認)](https://msdn.microsoft.com/62e20e03-50cc-4ac8-8072-524d194d2ec3)  
  
## <a name="select-objects-to-migrate-page"></a>オブジェクトの移行 ページを選択します  
移行のページにオブジェクトの選択、変換するオブジェクトを選択します。 すべてのオブジェクト、オブジェクト、または個々 のオブジェクトのグループを選択できます。  
  
**オブジェクトを選択するには**  
  
1.  展開**アクセス メタベース**、順に展開**データベース**します。  
  
2.  次の 1 つ以上の操作を行います。  
  
    -   すべてのデータベースを変換する場合は、横にチェック ボックスを選択します**データベース**します。  
  
    -   変換または個々 のデータベースの省略は、選択するか、データベース名の横にあるチェック ボックスをオフにします。  
  
    -   変換またはクエリの省略は、データベース、展開しし、オンまたはオフ、**クエリ**チェック ボックスをオンします。  
  
    -   変換または個々 のテーブルの省略は、データベースを展開し、**テーブル**、選択するか、テーブルの横にあるチェック ボックスをオフにします。  
  
オブジェクトの多くの場合を使用する可能性があります、**高度なオブジェクトの選択**データベース オブジェクトのアクセスをフィルター処理する右側のペインでオプションです。 たとえば、選択した場合**テーブル**内の文字列を入力して、左側のウィンドウでテーブルの一覧にフィルター処理できますしする、**フィルター**ボックス。 選択したり、ウィンドウの上部にあるボタンを使用して、フィルター選択されたテーブルの移行をオフにできます。  
  
フィルターの詳細については、の [オプション] セクションを参照してください。[高度なオブジェクトの選択 (SSMA 一般的)](https://msdn.microsoft.com/f53b0c79-5473-410a-a0dc-d8f544f7a63c)します。  
  
## <a name="connect-to-sql-server-page"></a>SQL Server のページへの接続します。  
接続[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ページで、接続のプロパティを指定しに接続する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 詳細については、次を参照してください。 [SQL サーバーへの接続](connect-to-sql-server-accesstosql.md)します。
  
> [!IMPORTANT]  
> 発生した接続に成功するとすぐに**リンク テーブル**ページ、テーブルのリンクのオプションがあります。 をクリックして**次**し、移行を開始します。  
  
## <a name="connect-to-sql-azure-page"></a>SQL Azure への接続 ページ  
SQL Azure のページへの接続は、接続のプロパティを指定し、SQL Azure に接続します。 新しい azure データベースを作成するには、これを行うを使用して**Azure データベースの作成**のクリックで表示されるオプション**参照**ボタンをクリックします。 詳細については、次を参照してください[SQL Azure への接続。](connect-to-azure-sql-db-accesstosql.md)  
  
> [!IMPORTANT]  
> 発生した接続に成功するとすぐに**リンク テーブル**ページ、テーブルのリンクのオプションがあります。 をクリックして**次**移行を開始するリンク ページ上のボタン。  
  
## <a name="link-tables-page"></a>リンク テーブル ページ  
リンク テーブル ページでは、移行後に、元の Access テーブルをリンクできます。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure テーブル。 クエリ、フォーム、レポート、およびデータ アクセス ページ内のデータを使用するように、Access データベースを変更するテーブルをリンクする、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Access データベース内のデータではなく SQL Azure データベース。  
  
**テーブルなリンク**  
選択、**テーブルをリンク**移行後にアクセス テーブルをリンクする チェック ボックス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure テーブル。 クリックする必要がありますの移行を開始する**次**ボタンをクリックします。  
  
## <a name="migration-status-page"></a>移行の状態 ページ  
移行の状態 ページにアクセス スキーマの変換の進行状況を表示する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のスキーマに変換されたスキーマを読み込む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のデータを移行します。  
  
このページの詳細については、次を参照してください[変換、読み込み、および移行。](https://msdn.microsoft.com/4ec83e96-88a5-4b7b-8d5a-f3429d9a936b)  
  
## <a name="see-also"></a>参照  
[SQL Server Migration Assistant for Access の概要&#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[SQL Server へのアクセス データベースの移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[ユーザー インターフェイスの Reference(Access)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
