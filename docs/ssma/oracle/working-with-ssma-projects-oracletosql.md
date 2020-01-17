---
title: SSMA プロジェクト (OracleToSQL) での作業 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Customizing Project Settings
ms.assetid: ee5d94c0-c7a6-4779-bd32-729bdaf61e1b
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: b96aba990231225516a7ba8ccf1523b91cb56c86
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266361"
---
# <a name="working-with-ssma-projects-oracletosql"></a>SSMA プロジェクトの操作 (OracleToSQL)
Oracle データベースを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、SSMA プロジェクトを作成します。 プロジェクトは、次の情報を含むファイルです。  
  
-   移行する Oracle データベースに関するメタデータ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
-   ターゲット インスタンスに関するメタデータ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移行済みのオブジェクトとデータを受信します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続情報です。  
  
-   プロジェクトの設定。  
  
Oracle から切断されているプロジェクトを開くときに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 オフラインで作業できます。 再接続する方法については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[SQL Server に接続する&#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)します。  
  
## <a name="reviewing-default-project-settings"></a>既定のプロジェクト設定を確認します。  
SSMA には、変換、およびデータベース オブジェクトの読み込み、データの移行し、Oracle との SSMA の同期のいくつかの設定が含まれていますと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 既定の設定は、多くのユーザーに適しています。 ただし、新しい SSMA プロジェクトを作成する前に、設定を確認する必要があります。 たい場合は、すべての新しいプロジェクトに使用される既定の設定を変更できます。  
  
**既定のプロジェクト設定を確認するには**  
  
1.  **ツール** メニューのをクリックして**プロジェクト設定の既定の**します。  
  
2.  プロジェクトの種類を選択します。**移行ターゲット バージョン**どの設定が表示または変更するために必要とクリックのドロップダウン**全般**タブ。  
  
3.  左側のウィンドウで次のようにクリックします。**変換**します。  
  
4.  右側のウィンドウで確認し、必要に応じて設定を変更します。 これらの設定の詳細については、次を参照してください。[プロジェクト設定&#40;変換&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)します。  
  
5.  移行、同期、システム オブジェクトの読み込み、GUI、およびマッピングの種類のページの手順 1. ~ 3. を繰り返します。  
  
    -   移行の設定については、次を参照してください。[プロジェクト設定&#40;移行&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md)します。  
  
    -   システム オブジェクトの設定については、次を参照してください。[プロジェクト設定&#40;システム オブジェクトの読み込み&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-loading-system-objects-oracletosql.md)します。  
  
    -   同期するための設定について[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[プロジェクト設定&#40;同期&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)します。  
  
    -   GUI の設定については、次を参照してください。[プロジェクト設定&#40;GUI&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md)します。  
  
    -   データ型マッピングの設定については、次を参照してください。[プロジェクト設定&#40;型マッピング&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)します。  
  
## <a name="creating-new-projects"></a>新しいプロジェクトの作成  
Oracle データベースからデータを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、まずプロジェクトを作成する必要があります。  
  
**プロジェクトを作成するには**  
  
1.  **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。  
  
    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
2.  **名前**ボックスに、プロジェクトの名前を入力します。  
  
3.  **場所**ボックス、入力またはプロジェクトのフォルダーを選択し、クリックして**OK**します。  
  
4.  **移行に**ドロップダウンで、ターゲットのバージョンを選択します。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移行に使用します。 使用可能なオプションがあります。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL DB  
  
## <a name="customizing-project-settings"></a>プロジェクト設定のカスタマイズ  
すべての新しい SSMA プロジェクトに適用される既定のプロジェクト設定を定義するだけでなく、各プロジェクトの設定をカスタマイズできます。 詳細については、次を参照してください。[プロジェクト オプションの設定&#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md)します。  
  
ソースとターゲット データベース間のデータ型マッピングをカスタマイズするときに、プロジェクト、データベース、またはオブジェクト レベルでは、マッピングを定義できます。 詳細については、次を参照してください。[マッピング Oracle および SQL Server データ型&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)します。  
  
## <a name="saving-projects"></a>プロジェクトの保存  
プロジェクトを保存するときに、SSMA は、プロジェクトの設定と、必要に応じて、プロジェクト ファイルに、データベースのメタデータを保持します。  
  
**プロジェクトを保存するには**  
  
-   **ファイル** メニューのをクリックして**プロジェクトの保存**します。  
  
    場合は、プロジェクトのスキーマが変更されたか、変換されていない、SSMA は読み込みおよびメタデータを保存することを求められます。 オフライン作業を行う、読み込みとメタデータを保存します。 テクニカル サポート担当者などの他のユーザーに完全なプロジェクト ファイルを送信することもできます。 メタデータを保存する場合は、次の操作を行います。  
  
    1.  状態を表示する各スキーマの**メタデータが不足している**データベース名の横にあるチェック ボックスをオンにします。  
  
        メタデータの保存には数分かかる場合があります。 まだメタデータを保存したくない場合は、チェック ボックスをオンされません。  
  
    2.  **[保存]** ボタンをクリックします。  
  
        SSMA は Oracle スキーマを解析し、プロジェクト ファイルにメタデータを保存します。  
  
## <a name="opening-projects"></a>プロジェクトを開く  
Oracle およびからは切断されて、プロジェクトを開いたときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 オフラインで作業できます。 メタデータを更新するにデータベース オブジェクトを読み込む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 データを移行する必要があります、Oracle に再接続し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
**プロジェクトを開く**  
  
1.  次の手順のいずれかを使用します。  
  
    -   **ファイル**メニューで、**最近使ったプロジェクト**、開きたいプロジェクトをクリックします。  
  
    -   **ファイル**メニューの **プロジェクトを開く**、.o2ssproj のプロジェクト ファイルの検索、ファイルを選択およびクリックして**オープン**します。  
  
2.  Oracle に再接続するには、**ファイル** メニューのをクリックして**Oracle への再接続**します。  
  
3.  再接続する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の**ファイル** メニューのをクリックして**SQL Server に再接続**します。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順が、 [Oracle データベース (OracleToSQL) に接続する](https://msdn.microsoft.com/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6)します。  
  
## <a name="see-also"></a>参照  
[SQL Server にデータベースを移行する Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
[Oracle データベースに接続する&#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)  
[SQL Server に接続する&#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
  
