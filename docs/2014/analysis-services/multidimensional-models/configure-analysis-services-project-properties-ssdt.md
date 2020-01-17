---
title: Analysis Services プロジェクトのプロパティ (SSDT) の構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- VS.TOOLSOPTIONSPAGES.BUSINESS_INTELLIGENCE_DESIGNERS.ANALYSIS_SERVICES_DESIGNERS.GENERAL
helpviewer_keywords:
- projects [Analysis Services], properties
ms.assetid: d9786c66-7d8c-48e3-950d-3f25044b4ce2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1eabb28250699305952d1d0746dc9487a1a25271
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076715"
---
# <a name="configure-analysis-services-project-properties-ssdt"></a>Analysis Services プロジェクトのプロパティの構成 (SSDT)
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトの構築と配置に影響する既定のプロパティで定義されています。  
  
 プロジェクト プロパティを変更するには、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクト オブジェクトを右クリックし、 **[プロパティ]** をクリックします。 または、[プロジェクト] メニューの **[プロパティ]** をクリックすることもできます。  
  
## <a name="property-description"></a>[プロパティの説明]  
 次の表に、プロジェクトの各プロパティの説明、それらの既定値、および値の変更に関する情報を示します。  
  
|プロパティ|既定の設定|説明|  
|--------------|---------------------|-----------------|  
|構築 / 配置サーバーのエディション|プロジェクトの開発に使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディション|最終的にプロジェクトを配置するサーバーのエディションを指定します。 1 つのプロジェクトに複数の開発者がいる場合、どの機能を [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトに組み込むかを知るには、開発者がサーバーのエディションを理解していることが必要です。|  
|構築 / 配置サーバーのエディション|プロジェクトの開発に使用するバージョン|最終的にプロジェクトを配置するサーバーのバージョンを指定します。|  
|構築 / 出力パス|/bin|プロジェクトのビルド プロセスの出力を示す相対パス|  
|構築 / パスワードの削除|True|ビルド中に出力ディレクトリに書き込まれる接続文字列から、既知のパスワードを削除するかどうかを指定します。 セキュリティを強化するにはパスワードを削除します。 削除した場合は、配置したプロジェクトを処理するときにパスワードを入力して、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] がソース データにアクセスできるようにする必要があります。|  
|デバッグ / 開始オブジェクト|\<現在アクティブなオブジェクト >|デバッグを開始するときに起動するオブジェクトを決定します。|  
|配置 / 配置モード|変更のみを配置|既定では、プロジェクトのオブジェクトの変更のみが配置されます (その他の変更がプロジェクト外で直接オブジェクトに加えられていない場合)。 また、配置のたびにプロジェクトのすべてのオブジェクトを配置することもできます。 最適なパフォーマンスを得るには、[変更のみを配置] を使用してください。|  
|配置 / 処理オプション|既定値|既定では、オブジェクトの変更を配置するときに [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] で必要な処理方法が決定されます。 通常は、これで配置時間が最速になりますが、 配置のたびに完全処理を実行するか処理を実行しないかを選択することもできます。|  
|配置 / トランザクション配置|False|既定では、変更されたオブジェクトまたはすべてのオブジェクトの配置は、それらを配置した後の処理とトランザクション関係がありません。 処理に失敗しても、配置は成功して持続できます。 この既定を変更して、配置と処理を 1 つのトランザクションに組み込むこともできます。|  
|配置 / ターゲット サーバー|localhost|既定では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクト内のデータベース オブジェクトは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] を使用しているローカル コンピューター上の [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] の既定のインスタンスに配置されます。 ローカル コンピューター上の特定のインスタンスを指定するか、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のオブジェクトを作成する権限のあるリモート コンピューター上の任意のインスタンスを指定するには、この既定を変更します。|  
|配置 / データベース|\<プロジェクト名 >|既定では、配置後に [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトのオブジェクトをインスタンス化する [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースの名前は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトを定義したときの名前です。 Server プロパティで指定されている [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンス上のデータベース名を変更するには、このプロパティを変更します。|  
  
## <a name="property-configurations"></a>プロパティの構成  
 プロパティは構成ごとに定義します。 プロジェクトを構成すると、開発者はビルド、デバッグ、配置設定などが異なる [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のプロジェクトを、基の XML プロジェクト ファイルを編集せずに操作できるようになります。  
  
 プロジェクトは、最初は "Development" という 1 つの構成で作成されます。 構成を追加作成し、構成マネージャーを使用して構成間の切り替えができます。  
  
 構成が追加されるまでは、全開発者がこの共通構成を使用します。 ただし、中に、さまざまなフェーズなど、初期の開発時にプロジェクトの開発 - とプロジェクトのさまざまな開発者のテストが可能性がありますさまざまなデータ ソースを使用して、さまざまな目的で異なるサーバーにプロジェクトを展開します。 構成を使用すると、このような異なる設定を別々の構成ファイルで維持できます。  
  
## <a name="see-also"></a>参照  
 [Analysis Services プロジェクトのビルド &#40;SSDT&#41;](build-analysis-services-projects-ssdt.md)   
 [Analysis Services プロジェクトの配置 &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
  
