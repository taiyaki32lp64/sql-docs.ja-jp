---
title: 作成して、プロジェクト (AccessToSQL) の管理 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- creating projects
- new projects
- opening projects
- projects
- projects, creating and managing
- saving metadata
- saving projects
ms.assetid: f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: abbe0746193df3fe341b4f66086291dc1055e11b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006615"
---
# <a name="creating-and-managing-projects-accesstosql"></a>作成して、プロジェクト (AccessToSQL) の管理
Access データベースを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure では、SSMA プロジェクトを最初に作成する必要があります。 プロジェクトに移行する Access データベースに関するメタデータを含むファイルは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure でのターゲット インスタンスに関するメタデータ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure 移行済みのオブジェクトとデータを受信する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]接続情報、およびプロジェクトの設定。  
  
## <a name="reviewing-default-project-settings"></a>既定のプロジェクト設定を確認します。  
SSMA には、データを変換するために、いくつかのオプション変換すると、データベース オブジェクトの同期にはが含まれています。 これらのオプションの既定の設定は、多くのユーザーにとって適切です。 ただし、新しい SSMA プロジェクトを作成する前にする必要があります、オプションを確認し、する場合は、すべての新しいプロジェクトに使用される既定の設定を変更します。  
  
**既定のプロジェクト設定を確認するには**  
  
1.  **ツール**メニューの **プロジェクト設定の既定の**します。  
  
2.  プロジェクトの種類を選択します。**移行ターゲット バージョン**設定が表示/変更するには、クリックのドロップダウン**全般**タブ。  
  
3.  左側のウィンドウで次のようにクリックします。**変換**します。  
  
4.  右側のウィンドウで、オプションを確認します。 これらのオプションの詳細については、次を参照してください。[プロジェクトの設定 (変換)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)します。  
  
5.  必要に応じてオプションを変更します。  
  
6.  前の手順を繰り返して、**移行**、 **GUI**、および**型マッピングの**ページ。  
  
    -   移行オプションについては、次を参照してください。[プロジェクトの設定 (移行)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)します。  
  
    -   ユーザー インターフェイス オプションについては、次を参照してください。[プロジェクトの設定 (GUI)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)します。  
  
    -   データ型マッピングの設定の詳細については、次を参照してください。[プロジェクトの設定 (型のマッピング)](https://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)します。  
  
    -   SQL Azure の設定については、次を参照してください。[プロジェクトの設定 (SQL Azure)](https://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e)します。  
  
**注**プロジェクトを作成するときに SQL Azure への移行を選択する場合にのみに、SQL Azure の設定が使用できます。  
  
## <a name="creating-new-projects"></a>新しいプロジェクトの作成  
SSMA は、既定のプロジェクトを読み込むことがなく起動します。 Access データベースからデータを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のプロジェクトを作成する必要があります。  
  
**新しいプロジェクトを作成するには**  
  
1.  **[ファイル]** メニューの **[新しいプロジェクト]** を選択します。  
  
    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
2.  **名前**ボックスに、プロジェクトの名前を入力します。  
  
3.  **場所**ボックスで、入力するか、プロジェクトのフォルダーを選択します。  
  
4.  移行をドロップ ダウン、SQL Server 2005 のいずれかを選択/SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016 または Azure SQL DB、順にクリックします**OK**します。  
  
SSMA は、プロジェクト ファイルを作成します。 次の手順を実行できるようになりました[1 つ以上の Access データベースを追加する](adding-and-removing-access-database-files-accesstosql.md)します。  
  
## <a name="customizing-project-settings"></a>プロジェクト設定のカスタマイズ  
すべての新しい SSMA プロジェクトに適用するの既定のプロジェクト設定を定義するだけでなく、各プロジェクトの設定をカスタマイズすることもできます。 詳細については、次を参照してください。[設定の変換と移行オプション](setting-conversion-and-migration-options-accesstosql.md)します。  
  
ソースとターゲット データベース間のデータ型マッピングをカスタマイズするときに、プロジェクト、データベース、またはオブジェクト レベルでは、マッピングを定義できます。 型のマッピングの詳細については、次を参照してください。[マッピング ソースとターゲットのデータ型](mapping-source-and-target-data-types-accesstosql.md)します。  
  
## <a name="saving-projects"></a>プロジェクトの保存  
プロジェクトを保存するときに、SSMA は、プロジェクトの設定と、必要に応じて、プロジェクト ファイルに、データベースのメタデータを保持します。  
  
**プロジェクトを保存するには**  
  
-   **ファイル**メニューの **プロジェクトの保存**します。  
  
    場合は、プロジェクト内のデータベースが変更されたか、変換されていない、SSMA は、プロジェクトにメタデータを保存することを求められます。 メタデータの保存には、オフラインで作業することができます。 テクニカル サポート担当者など、他のユーザーに完全なプロジェクト ファイルを送信することもできます。 メタデータを保存する場合は、次の操作を行います。  
  
    1.  状態を表示する各データベースに対して**メタデータが不足している**データベース名の横にあるチェック ボックスをオンにします。  
  
        メタデータの保存には数分かかる場合があります。 この時点でのメタデータを保存したくない場合は、チェック ボックスをオンされません。  
  
    2.  **[保存]** をクリックします。  
  
        SSMA は Access スキーマを解析し、プロジェクト ファイルにメタデータを保存します。  
  
## <a name="opening-projects"></a>プロジェクトを開く  
切断されているプロジェクトを開くときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 これにより、オフラインで作業できます。 メタデータの読み込みデータベース オブジェクトを更新する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 データを移行するに再接続する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。  
  
**プロジェクトを開く**  
  
1.  次の手順のいずれかを使用します。  
  
    -   **ファイル**メニューで、**最近使ったプロジェクト**、開きたいプロジェクトを選択します。  
  
    -   **ファイル**メニューの **プロジェクトを開く**、.a2ssproj のプロジェクト ファイルの検索、ファイルを選択およびクリックして**オープン**します。  
  
2.  再接続する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の**ファイル**メニューの  **SQL Server に再接続**します。  
  
3.  上の SQL Azure に再接続する、**ファイル**メニューの  **SQL Azure に再接続します。**  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順が、 [1 つ以上の Access データベースの追加](adding-and-removing-access-database-files-accesstosql.md)します。  
  
## <a name="see-also"></a>参照  
[SQL Server へのアクセス データベースの移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[追加して、Access データベース ファイルを削除します。](adding-and-removing-access-database-files-accesstosql.md)  
  
