---
title: SSMA プロジェクト (DB2ToSQL) での作業 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 07abef8a-28e8-4a66-927c-c9a5b8c938ef
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: d2c585764e5bb7fffa55624054aecc7a4c589bbe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086180"
---
# <a name="working-with-ssma-projects-db2tosql"></a>SSMA プロジェクト (DB2ToSQL) での作業
DB2 のデータベースを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、SSMA プロジェクトを作成します。 プロジェクトは、次の情報を含むファイルです。  
  
-   移行する DB2 データベースに関するメタデータ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
-   ターゲット インスタンスに関するメタデータ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移行済みのオブジェクトとデータを受信します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続情報です。  
  
-   プロジェクトの設定。  
  
DB2 から切断されているプロジェクトを開くときに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 オフラインで作業できます。 再接続する方法については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[SQL Server に接続する&#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)します。  
  
## <a name="reviewing-default-project-settings"></a>既定のプロジェクト設定を確認します。  
SSMA には、変換、データベース オブジェクトの読み込みとデータの移行、および DB2 での SSMA の同期のいくつかの設定が含まれていますと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 既定の設定は、多くのユーザーに適しています。 ただし、新しい SSMA プロジェクトを作成する前に、設定を確認する必要があります。 たい場合は、すべての新しいプロジェクトに使用される既定の設定を変更できます。  
  
**既定のプロジェクト設定を確認するには**  
  
1.  **ツール** メニューのをクリックして**プロジェクト設定の既定の**します。  
  
2.  プロジェクトの種類を選択します。**移行ターゲット バージョン**どの設定が表示または変更するために必要とクリックのドロップダウン**全般**タブ。  
  
3.  左側のウィンドウで次のようにクリックします。**変換**します。  
  
4.  右側のウィンドウで確認し、必要に応じて設定を変更します。 これらの設定の詳細については、次を参照してください。[プロジェクト設定&#40;変換&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)します。  
  
5.  移行、同期、システム オブジェクトの読み込み、GUI、およびマッピングの種類のページの手順 1. ~ 3. を繰り返します。  
  
    -   移行の設定については、次を参照してください。[プロジェクト設定&#40;移行&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-migration-db2tosql.md)します。  
  
    -   システム オブジェクトの設定については、次を参照してください。[プロジェクト設定&#40;システム オブジェクトの読み込み&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-loading-system-objects-db2tosql.md)します。  
  
    -   同期するための設定について[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[プロジェクト設定&#40;同期&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)します。  
  
    -   GUI の設定については、次を参照してください。[プロジェクト設定&#40;GUI&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-gui-db2tosql.md)します。  
  
    -   データ型マッピングの設定については、次を参照してください。[プロジェクト設定&#40;型マッピング&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md)します。  
  
## <a name="creating-new-projects"></a>新しいプロジェクトの作成  
DB2 データベースからデータを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、まずプロジェクトを作成する必要があります。  
  
**プロジェクトを作成するには**  
  
1.  **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。  
  
    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
2.  **名前**ボックスに、プロジェクトの名前を入力します。  
  
3.  **場所**ボックス、入力またはプロジェクトのフォルダーを選択し、クリックして**OK**します。  
  
4.  **移行に**ドロップダウンで、ターゲットのバージョンを選択します。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移行に使用します。 使用可能なオプションがあります。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL DB  
  
## <a name="customizing-project-settings"></a>プロジェクト設定のカスタマイズ  
すべての新しい SSMA プロジェクトに適用される既定のプロジェクト設定を定義するだけでなく、各プロジェクトの設定をカスタマイズできます。 詳細については、次を参照してください。[プロジェクト オプションの設定&#40;OracleToSQL&#41; ](../../ssma/oracle/setting-project-options-oracletosql.md)および関連するセクション。  
  
ソースとターゲット データベース間のデータ型マッピングをカスタマイズするときに、プロジェクト、データベース、またはオブジェクト レベルでは、マッピングを定義できます。 詳細については、次を参照してください。[マッピング DB2 と SQL Server データ型&#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)します。  
  
## <a name="saving-projects"></a>プロジェクトの保存  
プロジェクトを保存するときに、SSMA は、プロジェクトの設定と、必要に応じて、プロジェクト ファイルに、データベースのメタデータを保持します。  
  
**プロジェクトを保存するには**  
  
-   **ファイル** メニューのをクリックして**プロジェクトの保存**します。  
  
    場合は、プロジェクトのスキーマが変更されたか、変換されていない、SSMA は読み込みおよびメタデータを保存することを求められます。 オフライン作業を行う、読み込みとメタデータを保存します。 テクニカル サポート担当者などの他のユーザーに完全なプロジェクト ファイルを送信することもできます。 メタデータを保存する場合は、次の操作を行います。  
  
    1.  状態を表示する各スキーマの**メタデータが不足している**データベース名の横にあるチェック ボックスをオンにします。  
  
        メタデータの保存には数分かかる場合があります。 まだメタデータを保存したくない場合は、チェック ボックスをオンされません。  
  
    2.  **[保存]** ボタンをクリックします。  
  
        SSMA は DB2 スキーマを解析し、プロジェクト ファイルにメタデータを保存します。  
  
## <a name="opening-projects"></a>プロジェクトを開く  
DB2 およびからは切断されて、プロジェクトを開いたときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 オフラインで作業できます。 メタデータを更新するにデータベース オブジェクトを読み込む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 データを移行する必要があります、DB2 に再接続し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
**プロジェクトを開く**  
  
1.  次の手順のいずれかを使用します。  
  
    -   **ファイル**メニューで、**最近使ったプロジェクト**、開きたいプロジェクトをクリックします。  
  
    -   **ファイル**メニューの **プロジェクトを開く**、.o2ssproj のプロジェクト ファイルの検索、ファイルを選択およびクリックして**オープン**します。  
  
2.  DB2 に再接続するには、**ファイル** メニューのをクリックして**DB2 への再接続**します。  
  
3.  再接続する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の**ファイル** メニューのをクリックして**SQL Server に再接続**します。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順が、 [DB2 データベースに接続する](https://msdn.microsoft.com/5eb5801d-f0c3-4127-97c0-0b1ef49f4844)します。  
  
## <a name="see-also"></a>参照  
[SQL Server にデータベースを移行する DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
[DB2 データベースに接続する&#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
[SQL Server に接続する&#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
  
