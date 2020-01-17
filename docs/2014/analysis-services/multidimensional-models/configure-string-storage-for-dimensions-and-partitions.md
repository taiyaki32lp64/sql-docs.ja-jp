---
title: ディメンションおよびパーティションの文字列ストレージの構成 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 987f6cfc-da82-4b2e-96ef-a8af88339e5f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7fd9d9b293287d76b50c351b29b74df509793168
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076536"
---
# <a name="configure-string-storage-for-dimensions-and-partitions"></a>ディメンションおよびパーティションの文字列ストレージの構成
  文字列ストレージは、ディメンション属性またはパーティションの非常に大きな文字列 (文字列ストアの 4 GB のファイル サイズ制限を超えるもの) に対応するように再構成できます。 このサイズの文字列ストアがディメンションまたはパーティションに含まれている場合、ディメンション レベルまたはパーティション レベルで **[StringStoresCompatibilityLevel]** プロパティを変更することによって、ファイル サイズの制約を回避できます。これは、ローカル オブジェクトとリンクされている (ローカルまたはリモート) オブジェクトの両方に適用されます。  
  
 文字列ストレージは、追加容量が必要なそれらのオブジェクトに対してのみ増やすことができます。 多くの多次元モデルでは、文字列データはディメンションに関連付けられています。 ただし、文字列の上に個別のカウント メジャーが含まれているパーティションも、この設定の影響を受けます。 この設定は文字列のためであるため、数値データは影響を受けません。  
  
 このプロパティの有効値を以下に示します。  
  
|値|説明|  
|-----------|-----------------|  
|**1050**|既定の文字列ストレージ アーキテクチャを指定します。ストアごとの最大ファイル サイズが 4 GB に制限されます。|  
|**1100**|大きな文字列ストレージを指定します。ストアごとに最大 40 億個の一意な文字列がサポートされます。|  
  
> [!IMPORTANT]  
>  オブジェクトの文字列ストレージ設定を変更すると、そのオブジェクト自体と依存オブジェクトの再処理が必要になります。 手順を完了するには処理が必要です。  
  
 このトピックには、次のセクションが含まれます。  
  
-   [文字列ストアについて](#bkmk_background)  
  
-   [前提条件](#bkmk_prereq)  
  
-   [ステップ 1: SQL Server Data Tools で StringStoreCompatiblityLevel プロパティを設定します。](#bkmk_step1)  
  
-   [手順 2:オブジェクトを処理します。](#bkmk_step2)  
  
##  <a name="bkmk_background"></a> 文字列ストアについて  
 文字列ストレージの構成はオプションです。つまり、作成した新規データベースでも、既定の文字列ストア アーキテクチャが使用され、最大ファイル サイズが 4 GB に制限されます。 大きな文字列ストレージ アーキテクチャを使用すると、パフォーマンスにわずかながら明白な影響が生じます。 文字列ストレージ ファイルが最大 4 GB の制限に達しているか、それに近い場合にだけ使用してください。  
  
> [!NOTE]  
>  この設定はデータ マイニング モデルには適用されません。 現在、データ マイニング構造を含むモデルでは、GB 単位のファイル サイズの制限が引き続き発生する可能性があります。  
  
 Analysis Services 多次元データベースでは、データの特性に基づく最適化が実行できるように、文字列は数値データとは別に格納されます。 文字列データは、通常、名前や説明を表すディメンション属性で使用されます。 文字列データを個別のカウント メジャー内に置くこともできます。 文字列データはキーで使用することもできます。  
  
 文字列ストアは、そのファイル拡張子 (たとえば、asstore、.bstore、.ksstore、または .string) によって識別できます。 既定では、これらの各ファイルは、最大 4 GB に制限されます。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]では、必要に応じて文字列ストアを拡張できる別のストレージ方式を指定することにより、最大ファイル サイズをオーバーライドできます。  
  
 物理ファイルのサイズを制限する既定の文字列ストレージ アーキテクチャとは異なり、大きな文字列ストレージでは文字列の最大数を制限します。 大きな文字列ストレージの上限は、一意の文字列とレコードのどちらかの数が 40 億に達した時点となります。 大きな文字列ストレージでは均等なサイズのレコードが作成され、各レコードのサイズは 64 K ページに等しくなります。 1 つのレコードに収まらない非常に長い文字列がある場合、文字列数の実際の制限は 40 億よりも少なくなります。  
  
##  <a name="bkmk_prereq"></a> 前提条件  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]以上のバージョンが必要です。  
  
 ディメンションとパーティションは MOLAP ストレージを使用する必要があります。  
  
 データベース互換性レベルを 1100 に設定する必要があります。 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] と [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以上のバージョンの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]を使用してデータベースを作成または配置した場合、データベース互換性レベルはあらかじめ 1100 に設定されています。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の以前のバージョンで作成したデータベースを ssSQL11 以上に移動した場合、互換性レベルを更新する必要があります。 再配置ではなく、移動するデータベースには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して互換性レベルを設定できます。 詳細については、次を参照してください。[多次元データベースの互換性レベル設定&#40;Analysis Services&#41;](compatibility-level-of-a-multidimensional-database-analysis-services.md)します。  
  
##  <a name="bkmk_step1"></a> ステップ 1:SQL Server Data Tools で StringStoreCompatiblityLevel プロパティを設定します。  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]を使用して、変更するディメンションまたはパーティションが含まれているプロジェクトを開きます。  
  
2.  ディメンションの文字列ストレージを変更するには、ソリューション エクスプローラーを開きます。 文字列ストレージを変更するディメンションをダブルクリックします。  
  
3.  ディメンション デザイナーの [属性] ペインで、ディメンションの親ノードが選択されていることを確認します (たとえば、ディメンションが Customers の場合は、子属性のいずれかではなく、Customers を選択します)。  
  
4.  [プロパティ] ペインの [詳細設定] セクションで、 **[StringStoresCompatibilityLevel]** を **1100**に設定します。 大きなストレージを必要とする他のディメンションで同じ手順を繰り返すか、残りのディメンションの値を **1050** のままにします。  
  
5.  パーティションに対しては、ソリューション エクスプローラーから、キューブを開きます。  
  
6.  [パーティション] タブをクリックします。  
  
7.  パーティションを展開し、追加のストレージ容量を必要とするパーティションを選択して、 **StringStoresCompatibilityLevel** プロパティを変更します。  
  
8.  ファイルを保存します。  
  
##  <a name="bkmk_step2"></a> ステップ 2:オブジェクトを処理します。  
 オブジェクトを処理した後は、新しいストレージ アーキテクチャが使用されます。 オブジェクトを処理することで、以前は文字列ストアのオーバーフロー状態を報告していたエラーが発生しなくなるため、ストレージの制約の問題が正常に解決されたことも確認できます。  
  
-   ソリューション エクスプローラーで、変更したディメンションを右クリックし、 **[処理]** をクリックします。  
  
 新しい文字列ストア アーキテクチャを使用している各オブジェクトに、完全処理オプションを使用する必要があります。 処理の前に、ディメンションに対する影響分析を必ず実行して、依存オブジェクトも再処理が必要かどうかを確認してください。  
  
## <a name="see-also"></a>参照  
 [処理するためのツールと方法 &#40;Analysis Services&#41;](tools-and-approaches-for-processing-analysis-services.md)   
 [処理オプションと設定 &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md)   
 [パーティションのストレージ モードおよび処理](../multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)   
 [ディメンションのストレージ](../multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)  
  
  
