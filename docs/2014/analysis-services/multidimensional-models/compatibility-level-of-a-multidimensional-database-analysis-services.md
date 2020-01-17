---
title: 互換性レベル (Analysis Services) の多次元データベースの設定 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 978279e6-a581-4184-af9d-8701b9826a89
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4c5eedfb396b33d33ceb9fbfad0245c4eb730997
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076689"
---
# <a name="set-the-compatibility-level-of-a-multidimensional-database-analysis-services"></a>多次元データベースの互換性レベルの設定 (Analysis Services)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]では、データベース互換性レベル プロパティによって、データベースの機能レベルが決定されます。 互換性レベルは、各モデルの種類に固有です。 たとえば、互換性レベルの`1100`データベースが多次元か表形式かによって異なる意味を持ちます。  
  
 このトピックでは、多次元データベースの互換性レベルについてのみ説明します。 表形式ソリューションの詳細については、次を参照してください。[互換性レベル&#40;SSAS テーブル SP1&#41;](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)します。  
  
> [!NOTE]  
>  表形式モデルには、多次元モデルに適用できないデータベース互換性レベルが存在します。 互換性レベル `1103` は、多次元モデルには存在しません。 参照してください[で SQL Server 2012 SP1 との互換性レベル表形式モデルの新](https://go.microsoft.com/fwlink/?LinkId=301727)の詳細については`1103`テーブル ソリューションの。  
  
 **多次元データベースの互換性レベル**  
  
 現在、機能レベルによって異なる多次元データベースの動作は、文字列ストレージ アーキテクチャのみです。 データベースの互換性レベルを高くすることで、メジャーとディメンションの文字列ストレージの上限である 4 GB をオーバーライドできます。  
  
 多次元データベースの `CompatibilityLevel` プロパティの有効値を以下に示します。  
  
|設定|説明|  
|-------------|-----------------|  
|`1050`|この値はスクリプトやツールには表示されませんが、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、または [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]で作成されたデータベースを表します。 `CompatibilityLevel` が明示的に設定されていないデータベースはすべて、暗黙的に `1050` レベルで実行されます。|  
|`1100`|これは、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] または [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]で作成した新しいデータベースの既定値です。 また、この値を以前のバージョンの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] で作成されたデータベースに指定すると、この互換性レベルでのみサポートされている機能 (つまり、文字列データを含むディメンション属性や個別のカウント メジャーの大きくなった文字列ストレージ) を使用できるようになります。<br /><br /> データベースを持つ、`CompatibilityLevel`に設定`1100`プロパティが追加`StringStoresCompatibilityLevel`、パーティションおよびディメンションの代替文字列ストレージを選択できます。|  
  
> [!WARNING]  
>  高いレベルに設定したデータベース互換性は元に戻せません。 互換性レベルを上げた後`1100`、新しいサーバー上で、データベースを実行し続ける必要があります。 ロールバックすることはできません`1050`します。 アタッチまたは復元することはできません、`1100`データベース サーバーのバージョンよりも前で[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]または[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]します。  
  
## <a name="prerequisites"></a>前提条件  
 データベース互換性レベルは、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]で導入されました。 データベース互換性レベルを表示または設定するには、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以降が必要です。  
  
 データベースをローカル キューブにすることはできません。 ローカル キューブでは、`CompatibilityLevel` プロパティがサポートされません。  
  
 データベースは、以前のリリース (SQL Server 2008 R2 以前) で作成され、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以降のサーバーにアタッチまたは復元されている必要があります。 SQL Server 2012 に配置されたデータベースは既に `1100` であり、ダウングレードして低いレベルで実行することはできません。  
  
## <a name="determine-the-existing-database-compatibility-level-for-a-multidimensional-database"></a>多次元データベースの既存のデータベース互換性レベルの確認  
 データベース互換性レベルを表示または変更するには、XMLA を使用するしかありません。 データベースを指定する XMLA スクリプトは、SQL Server Management Studio で表示または変更できます。  
  
 データベースの XMLA 定義で `CompatibilityLevel` プロパティを検索し、それが存在しなかった場合、データベースが `1050` レベルになっている可能性が高いと考えられます。  
  
 XMLA スクリプトの表示と変更の方法については、次のセクションで説明します。  
  
## <a name="set-the-database-compatibility-level-in-sql-server-management-studio"></a>SQL Server Management Studio でのデータベース互換性レベルの設定  
  
1.  互換性レベルを上げる前に、変更を元に戻すことができるように、データベースをバックアップします。  
  
2.  SQL Server Management Studio を使用して、データベースをホストする [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーに接続します。  
  
3.  データベース名を右クリックし、 **[データベースをスクリプト化]** をポイントして **[ALTER]** をポイントします。次に、 **[新しいクエリ エディター ウィンドウ]** をクリックします。 データベースの XMLA 表現が新しいウィンドウで開きます。  
  
4.  次の XML 要素をコピーします。  
  
    ```  
    <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
    ```  
  
5.  それを、 `</Annotations>` 終了要素の後、 `<Language>` 要素の前に貼り付けます。 XML は次の例のようになります。  
  
    ```  
    </Annotations>  
    <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
    <Language>1033</Language>  
    ```  
  
6.  ファイルを保存します。  
  
7.  スクリプトを実行するには、[クエリ] メニューの **[実行]** をクリックするか、F5 キーを押します。  
  
## <a name="supported-operations-that-require-the-same-compatibility-level"></a>同じ互換性レベルが必要なサポートされる操作  
 次の操作では、ソース データベースで同じ互換性レベルを共有している必要があります。  
  
1.  異なるデータベースのパーティションのマージは、両方のデータベースで同じ互換性レベルを共有している場合にのみサポートされます。  
  
2.  別のデータベースのリンク ディメンションを使用するには、同じ互換性レベルが必要です。 リンク ディメンションを使用する場合など、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]でデータベースを[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]移植する必要があります、データベース、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]データベースを[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]サーバーとの互換性レベルを`1100`します。  
  
3.  サーバーの同期は、サーバーで同じバージョンとデータベース互換性レベルを共有している場合にのみサポートされます。  
  
## <a name="next-steps"></a>次の手順  
 データベース互換性レベルを上げると、[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] で `StringStoresCompatibilityLevel` プロパティを設定できるようになります。 これにより、メジャーとディメンションの文字列ストレージが大きくなります。 この機能の詳細については、「 [ディメンションおよびパーティションの文字列ストレージの構成](configure-string-storage-for-dimensions-and-partitions.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データベースのバックアップ、復元、および同期 &#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
