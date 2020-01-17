---
title: SSMA プロジェクト (SybaseToSQL) での作業 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 11091d95-c488-48c3-891a-743cac94ac93
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: eb6f035b4d597e2b648134c195b698554dc78e12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072476"
---
# <a name="working-with-ssma-projects-sybasetosql"></a>SSMA プロジェクトでの作業 (SybaseToSQL)
Sybase Adaptive Server Enterprise (ASE) のデータベースを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL Azure では、まずプロジェクトを作成する SSMA またはします。 プロジェクトに移行する ASE のデータベースに関するメタデータを含むファイルは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure でのターゲット インスタンスに関するメタデータ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure 移行済みのオブジェクトとデータを受信する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure接続情報、およびプロジェクトの設定。  
  
切断されているプロジェクトを開くときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 これにより、オフラインで作業できます。 再接続できます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 詳細については、次を参照してください。 [SQL Server に接続する&#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) / [Azure SQL DB に接続する&#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)します。  
  
## <a name="reviewing-default-project-settings"></a>既定のプロジェクト設定を確認します。  
SSMA は、変換、およびデータベース オブジェクトの読み込み、データの移行し、ASE での SSMA を同期するためのいくつかのオプションを含むと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 これらのオプションの既定の設定は、多くのユーザーに適しています。 ただし、新しい SSMA プロジェクトを作成する前にする必要があります、オプションを確認し、する場合は、すべての新しいプロジェクトに使用される既定値を変更します。  
  
**既定のプロジェクト設定を確認するには**  
  
1.  **ツール**メニューの **プロジェクト設定の既定の**します。  
  
2.  プロジェクトの種類を選択します。**移行ターゲット バージョン**どの設定が表示または変更するために必要とクリックのドロップダウン**全般**タブ。  
  
3.  左側のウィンドウで次のようにクリックします。**変換**します。  
  
4.  右側のウィンドウで、必要に応じてオプションを変更するオプションを確認します。 これらのオプションの詳細については、次を参照してください。[プロジェクト設定&#40;変換&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)します。  
  
5.  移行、SQL Azure、オブジェクトの読み込み、GUI、およびマッピングの種類のページの手順 1. ~ 3. を繰り返します。  
  
    -   移行オプションについては、次を参照してください。[プロジェクト設定&#40;移行&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)します。  
  
    -   オブジェクトを読み込むためのオプションについては[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[プロジェクト設定&#40;同期&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)します。  
  
    -   GUI オプションの詳細については、次を参照してください。[プロジェクト設定&#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)します。  
  
    -   データ型マッピングの設定の詳細についてをクリックして[プロジェクト設定&#40;型マッピング&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)します。  
  
    -   SQL Azure のオプションの詳細については、次を参照してください。[プロジェクト設定&#40;Azure SQL DB &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)します。  
  
    > [!NOTE]  
    > SQL Azure の設定が選択した場合にのみ表示されます**SQL Azure への移行**してプロジェクトを作成します。  
  
## <a name="creating-new-projects"></a>新しいプロジェクトの作成  
ASE データベースからデータを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のプロジェクトを最初に作成する必要があります。  
  
**プロジェクトを作成するには**  
  
1.  **[ファイル]** メニューの **[新しいプロジェクト]** を選択します。  
  
    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
2.  **名前**ボックスに、プロジェクトの名前を入力します。  
  
3.  **場所**ボックスで、入力するか、プロジェクトのフォルダーを選択します。  
  
4.  **移行に**ドロップダウンで、ターゲットのバージョンを選択します。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移行に使用します。 使用可能なオプションがあります。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL DB  
  
クリックして**OK**します。  
  
## <a name="customizing-project-settings"></a>プロジェクト設定のカスタマイズ  
すべての新しい SSMA プロジェクトに適用される既定のプロジェクト設定を定義するだけでなく、各プロジェクトの設定をカスタマイズできます。 詳細については、次を参照してください。[プロジェクト オプションの設定&#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)します。  
  
ソースとターゲット データベース間のデータ型マッピングをカスタマイズするときに、プロジェクト、データベース、またはオブジェクト レベルでは、マッピングを定義できます。 型のマッピングの詳細については、次を参照してください。[マッピング Sybase ASE と SQL Server データ型&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)します。  
  
## <a name="saving-projects"></a>プロジェクトの保存  
プロジェクトを保存するときに、SSMA は、プロジェクトの設定と、必要に応じて、プロジェクト ファイルに、データベースのメタデータを保持します。  
  
**プロジェクトを保存するには**  
  
-   **ファイル**メニューの **プロジェクトの保存**します。  
  
    場合は、プロジェクト内のデータベースが変更されたか、変換されていない、SSMA は、プロジェクトにメタデータを保存することを求められます。 メタデータの保存と、オフラインで作業して、テクニカル サポート担当者など、他のユーザーに完全なプロジェクト ファイルを送信します。 メタデータを保存する場合は、次の操作を行います。  
  
    1.  状態を表示する各データベースに対して**メタデータが不足している**データベース名の横にあるチェック ボックスをオンにします。  
  
        メタデータの保存には数分かかる場合があります。 この時点でのメタデータを保存したくない場合は、チェック ボックスをオンされません。  
  
    2.  **[保存]** ボタンをクリックします。  
  
        SSMA は Sybase ASE スキーマを解析し、プロジェクト ファイルにメタデータを保存します。  
  
## <a name="opening-projects"></a>プロジェクトを開く  
ASE およびからは切断されて、プロジェクトを開いたときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 これにより、オフラインで作業できます。 メタデータを更新するにデータベース オブジェクトを読み込む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 データを移行する必要があります、ASE に再接続し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。  
  
**プロジェクトを開く**  
  
1.  次の手順のいずれかを使用します。  
  
    -   **ファイル**メニューで、**最近使ったプロジェクト**、開きたいプロジェクトを選択します。  
  
    -   **ファイル**メニューの **プロジェクトを開く**、.s2ssproj のプロジェクト ファイルの検索、ファイルを選択およびクリックして**オープン**します。  
  
2.  ASE に再接続するには、**ファイル**メニューの  **Sybase への再接続**します。  
  
3.  再接続する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure では、上、**ファイル**メニューの  **SQL Server に再接続** / **SQL Azure に再接続**。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順が、 [Sybase ASE への接続](connecting-to-sybase-ase-sybasetosql.md)します。  
  
## <a name="see-also"></a>参照  
[SQL Server - Azure SQL DB への Sybase ASE データベース移行&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Sybase ASE への接続&#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)  
[SQL Server に接続する&#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  
[Azure SQL DB に接続する&#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
