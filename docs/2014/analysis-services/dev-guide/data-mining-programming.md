---
title: データ マイニングのプログラミング |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- data mining [Analysis Services], developer's guide
ms.assetid: 9fd77b16-0b89-44ce-bcf1-7c04b62499da
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9d18e97a60bf1c6108b3672f40747e8b612ad6e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62732268"
---
# <a name="data-mining-programming"></a>データ マイニングのプログラミング
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の組み込みのツールやビューアーが要件を満たしていない場合は、独自の拡張機能をコーディングすることによって [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の機能を拡張できます。 この方法では、2 つのオプションがあります。  
  
-   **XMLA**  
  
     [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] クライアント アプリケーションとの通信用プロトコルとして XML for Analysis (XMLA) をサポートします。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、XML for Analysis 仕様を拡張する追加のコマンドをサポートしています。  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ではデータ定義、データ操作、およびデータ制御サポートに XMLA を使用するため、[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] に用意されているビジュアル ツールを使用してマイニング構造とマイニング モデルを作成し、データ マイニング拡張機能 (DMX) と Analysis Services スクリプト言語 (ASSL) のスクリプトを使用して作成したデータ マイニング オブジェクトを拡張できます。  
  
     データ マイニング オブジェクトを XMLA スクリプトだけで作成および変更できます。また、プログラムを使用して、独自のアプリケーションからモデルに対して予測クエリを実行できます。  
  
-   **分析管理オブジェクト (AMO)**  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] には、サード パーティのデータ マイニング プロバイダーがデータ マイニング オブジェクトを [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] に統合できるようにする完全なフレームワークも用意されています。  
  
     AMO を使用して、マイニング構造とマイニング モデルを作成できます。 CodePlex の次のサンプルを参照してください。  
  
    -   [AMO ブラウザー]  
  
         指定した SSAS インスタンスに接続し、マイニング構造とマイニング モデルを含め、すべてのサーバー オブジェクトとそれらのプロパティを一覧表示します。  
  
    -   AMO の簡単な例  
  
         AS Simple サンプルは、ほとんどの主要なオブジェクトに対するプログラムによるアクセスを取り扱い、メタデータの参照方法やオブジェクト内の値へのアクセス方法を示します。  
  
         このサンプルでは、データ マイニング構造とモデルを作成して操作する方法や、既存のデータ マイニング モデルを参照する方法も示します。  
  
-   **DMX**  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーへの接続を作成したことを前提とすると、DMX を使用して、コマンド ステートメント、予測クエリ、およびメタデータ クエリをカプセル化し、表形式で結果を返すことができます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [OLE DB for Data Mining](../../../2014/analysis-services/dev-guide/ole-db-for-data-mining.md)  
 データ マイニングと多次元データをサポートするための仕様への追加項目として、新しいスキーマ行セットと列、およびマイニング構造の作成と管理のためのデータ マイニング拡張機能 (DMX) 言語について説明します。  
  
## <a name="related-reference"></a>関連リファレンス  
 [ADOMD.NET での開発](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net)  
 ADOMD.NET クライアントおよびサーバー プログラミング オブジェクトについて説明します。  
  
 [分析管理オブジェクト &#40;AMO&#41; による開発](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)  
 AMO プログラミング ライブラリについて説明します。  
  
 [Analysis Services スクリプト言語 (ASSL) での開発](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)  
 XML for Analysis (XMLA) とその拡張機能について説明します。  
  
## <a name="see-also"></a>参照  
 [Developer's Guide &#40;Analysis Services&#41;](../analysis-services-developer-documentation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; リファレンス](/sql/dmx/data-mining-extensions-dmx-reference)  
  
  
