---
title: Analysis Services プロジェクト (SSDT) のビルド |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- projects [Analysis Services], building
- Business Intelligence Development Studio, project building [Analysis Services]
ms.assetid: caac03cb-b2b4-4652-8913-3dd39c4b0127
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97e32b80d19675b3763101d1c226529a48e23e68
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076773"
---
# <a name="build-analysis-services-projects-ssdt"></a>Analysis Services プロジェクトのビルド (SSDT)
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]を使用した [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトの作成方法は、Visual Studio を使用したプログラミング プロジェクトの作成方法とほとんど同じです。 プロジェクトを作成する場合、出力ディレクトリ内に XML ファイルのセットが作成されます。 この XML ファイルは、Analysis Services Scripting Language (ASSL) を使用したファイルです。ASSL は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] や [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] などのクライアント アプリケーションが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスと接続して [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトの作成や変更に使用する XML 言語仕様です。 この XML ファイルを使用して [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクト内の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクト定義が、指定された [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスに配置されます。  
  
## <a name="building-a-project"></a>プロジェクトの作成  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトの作成時、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] は、プロジェクト内のすべての [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース オブジェクトを作成するために必要なすべての ASSL コマンドが含まれた完全な XML ファイル セットを出力フォルダー内に作成します。 そのプロジェクトが既に作成済みであり、その有効な構成について増分配置が指定されている場合、[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] は、配置されたオブジェクトの増分更新を実行する ASSL コマンドを含んでいる XML ファイルも作成します。 この XML ファイルは、プロジェクトの ..\obj\\< アクティブ構成\> フォルダーに書き込まれます。 プロジェクトを増分作成すると、大容量のプロジェクトやデータベースの配置および処理時間を短縮できます。  
  
> [!NOTE]  
>  Rebuild All コマンドを使用すると、増分配置設定を無視できます。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトを作成すると、プロジェクトのオブジェクト定義が検証されます。 検証の対象には、参照されるアセンブリが含まれます。 [タスク一覧] ウィンドウに、Analysis Management Objects (AMO) エラー テキストと共に作成エラーが表示されます。 エラーをクリックすると、エラーを修正するためのデザイナーを開くことができます。  
  
 検証が成功しても、配置の際に配置先サーバー上にオブジェクトが作成されたり、配置後にオブジェクトが正常に処理されたりすることが保証できるわけではありません。 次の問題によって、正常な配置や配置後の処理ができない場合があります。  
  
-   サーバーのセキュリティ チェックが行われず、ロック機能によってオブジェクトの配置ができない。  
  
-   サーバー上の物理的な場所が検証されない。  
  
-   データ ソース ビューの詳細情報が、配置先サーバー上の実際のデータ ソースと照らし合わせた検証が行われていない。  
  
 検証が成功すると、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] により XML ファイルが生成されます。 ファイルが作成されると、次の表に説明するファイルが出力フォルダー内に格納されます。  
  
|ファイル (bin フォルダー内)|説明|  
|-----------------------------|-----------------|  
|*Projectname*.asdatabase|配置スクリプト ファイル内で、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトのオブジェクトのメタデータを定義している ASSL 要素が格納されます。 このファイルは、配置エンジンがオブジェクトを [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースに配置するときに使用されます。|  
|*Projectname*.configsettings|配置の際に使用された構成設定値 (データ ソースの接続文字列など) が格納されます。この設定値は、直接変更したり、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の配置ウィザードを使用して変更したりできます。|  
|*Projectname*.deploymenttargets|配置の際に使用された配置先の設定 (サーバーおよびデータベース名) が格納されます。この設定は、直接変更したり、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の配置ウィザードを使用して変更したりできます。|  
|*Projectname*.deploymentoptions|配置の際に使用されたさまざまなオプション設定 (ストレージ場所など) が格納されます。この設定は、直接変更したり、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の配置ウィザードを使用したりして変更できます。|  
|*Assemblyname*/*dllname.* dll|参照されたアセンブリ別の個別のフォルダー。各フォルダーには、アセンブリの DLL、すべての参照されたアセンブリ、出力デバッグ情報が記録された関連 .pdb ファイルが格納されます。|  
  
|ファイル (obj フォルダー内)|説明|  
|-----------------------------|-----------------|  
|\<Configuration Name>\LastBuilt.xml|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトの最終作成時刻を表すタイム スタンプおよびハッシュ コードが含まれています。|  
  
 これらの XML ファイルに含まれていない\<Create > および\<Alter > タグで、展開時に作成されます。  
  
 参照されたアセンブリ (標準システムと [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] アセンブリを除く) も出力ディレクトリにコピーされます。 参照がソリューションの別のプロジェクト (複数) に対して行われる場合はまず、該当するプロジェクト構成を使用してそれらのプロジェクトが作成され、プロジェクト参照により確立された依存オブジェクトが作成され、その後、プロジェクトの出力フォルダーにコピーされます。  
  
## <a name="see-also"></a>参照  
 [Analysis Services スクリプト言語&#40;ASSL&#41;リファレンス](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [Analysis Services プロジェクトの配置 (SSDT)](deploy-analysis-services-projects-ssdt.md)  
  
  
