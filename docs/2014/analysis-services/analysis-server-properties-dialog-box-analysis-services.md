---
title: 分析サーバーのプロパティ ダイアログ ボックス (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- SQL12.ASVS.SSMSIMBI.SERVERPROPERTIES.F1
- SQL12.ASVS.SQLSERVERSTUDIO.SERVERPROPERTIES.F1
helpviewer_keywords:
- Analysis Server Properties dialog box
ms.assetid: b01ec658-c191-49c9-a6cb-549b21a368ab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b32b0fa678df98494f91c1026adebe701d807342
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062620"
---
# <a name="analysis-server-properties-dialog-box-analysis-services"></a>[分析サーバーのプロパティ] ダイアログ ボックス (Analysis Services)
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の **[分析サーバーのプロパティ]** ダイアログ ボックスを使用すると、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のインスタンスの全般的な設定、言語と照合順序の設定、およびセキュリティ設定を行うことができます。 **オブジェクト エクスプローラー**の [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスを右クリックし、ショートカット メニューの **[プロパティ]** を選択することによって、 **[分析サーバーのプロパティ]** ダイアログ ボックスを表示できます。 **[分析サーバーのプロパティ]** ダイアログ ボックスには、次のプロパティが含まれます。  
  
## <a name="information-properties"></a>情報プロパティ  
 このページを使用すると、サーバーのモード、バージョン、互換性レベルを表示できます。 各インスタンスは、テーブル サーバー モードまたは多次元サーバー モードでインストールされ、テーブル モデルまたは多次元モデルを読み込むことができます。 両方のモードをサポートする場合は、インスタンスを 2 つインストールする必要があります。  
  
 **サポートされる互換性レベル**と同じですが、 `DefaultCompatibilityLevel` AMO 内のプロパティ。 このプロパティは読み取り専用であり、インストール時に指定したサーバー配置モードに基づいています。 サーバーのモードやバージョンによって異なる操作 (テーブル サーバー インスタンスにテーブル データベースのバックアップを復元する操作など) を実行するときに、サーバーでこのプロパティが確認されます。 テーブル モデルや多次元モデルのデータベース互換性モードと混同しないでください。名前と値が類似しているため注意が必要です。 このサーバー プロパティの有効値は次のとおりです。  
  
-   **1100** は、配置モード 0 に対する既定の互換性レベルです (多次元モードとデータ マイニング モードの場合)。  
  
-   **1103** は、配置モード 1 または 2 に対する既定の互換性レベルです (テーブル モードや [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]をサポートするインストールの場合)。  
  
 サーバーは、クライアントが名前空間の要求 DISCOVER_XML_METADATA をサポートしている場合に、この値を返します。 詳細については、「[DISCOVER_XML_METADATA 行セット](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-xml-metadata-rowset)」を参照してください。  
  
## <a name="general-properties"></a>全般プロパティ  
 このページを使用して、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスのフォルダーの場所、ネットワークの設定など、基本および詳細な全般的プロパティを設定します。  
  
 サーバーのプロパティ ページには、管理者が変更する可能性が高いプロパティのみが表示されます。こうしたプロパティには、サーバーをチューニングして構成するためのメモリ プールやスレッド プールのプロパティなどがあります。 主要なプロパティ グループへのリンクを次に示します。  
  
-   [全般プロパティ](server-properties/general-properties.md)  
  
-   [データ マイニング プロパティ](server-properties/data-mining-properties.md)  
  
-   [機能プロパティ](server-properties/feature-properties.md)  
  
-   [Filestore プロパティ](server-properties/filestore-properties.md)  
  
-   [ロック マネージャーのプロパティ](server-properties/lock-manager-properties.md)  
  
-   [ログのプロパティ](server-properties/log-properties.md)  
  
-   [メモリのプロパティ](server-properties/memory-properties.md)  
  
-   [ネットワーク プロパティ](server-properties/network-properties.md)  
  
-   [OLAP のプロパティ](server-properties/olap-properties.md)  
  
-   [セキュリティのプロパティ](server-properties/security-properties.md)  
  
-   [スレッド プール プロパティ](server-properties/thread-pool-properties.md)  
  
## <a name="language-collation-properties"></a>言語/照合順序プロパティ  
 このページを使用して、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]の既定の言語および照合順序のオプションを設定します。 次に、各オプションの簡単な説明を示します。 詳細な説明については、「[言語および照合順序 &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)」を参照してください。  
  
-   **[バイナリ]** 。このオプションを使用すると、文字ごとに定義されたビット パターンに基づいてデータの並べ替えと比較を行います。 バイナリの並べ替え順では大文字と小文字が区別されるため、小文字は大文字より前に配置されます。また、アクセントも区別されます。 これは、最速の並べ替え順です。  
  
     このオプションが選択されていない場合、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] には関連する言語またはアルファベットの辞書で定義されている並べ替えおよび比較ルールが使用されます。  
  
    > [!NOTE]  
    >  このオプションが選択されている場合、 **[大文字と小文字を区別する]** 、 **[アクセントを区別する]** 、 **[かなを区別する]** 、および **[文字幅を区別する]** オプションは無効になります。  
  
-   **[バイナリ 2]** 。このオプションを使用すると、文字ごとに定義されたビット パターンに基づいて Unicode データの並べ替えと比較を行います。 バイナリの並べ替え順では大文字と小文字が区別されるため、小文字は大文字より前に配置されます。また、アクセントも区別されます。 これは、最速の並べ替え順です。  
  
-   **[大文字と小文字を区別する]** を使用すると、関連する言語またはアルファベットに適用される辞書のルールに基づいてデータの並べ替えと比較を行い、大文字と小文字による区別を行います。  
  
     このオプションが選択されていない場合、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は大文字と小文字を区別しません。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] かどうか小文字を大文字より下位または並べ替える上位ときに定義しません**大文字**が選択されていません。  
  
-   **[アクセントを区別する]** を使用すると、関連する言語またはアルファベットに適用される辞書のルールに基づいてデータの並べ替えと比較を行い、アクセント符号が付いた文字と付いていない文字を区別します。 たとえば、'a' と '&#xE1;' は等しくありません。  
  
     このオプションが選択されていない場合、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] はアクセント符号の付いた文字と付いていない文字を同じものと見なします。  
  
-   **かなを区別する**を使用して、関連する言語またはアルファベットでは、2 つの種類の日本語のかな文字を区別する、指定された辞書のルールに基づいてデータを比較します。ひらがなとカタカナ。  
  
     このオプションが選択されていない場合、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] はひらがなとカタカナを同じものと見なします。  
  
-   **[文字幅を区別する]** を使用すると、関連する言語またはアルファベットに適用される辞書のルールに基づいてデータの並べ替えと比較を行い、1 バイト文字 (半角文字) と同じ文字の 2 バイト表現 (全角文字) とを区別します。  
  
     このオプションが選択されていない場合、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は同じ文字の 1 バイト表現と 2 バイト表現を同じものと見なします。  
  
## <a name="security-properties"></a>セキュリティのプロパティ  
 このページを使用して、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスのサーバー管理者ロールに所属する Windows ユーザー アカウントとグループ アカウントを指定します。 このロールのメンバーシップによって、サーバー全体のタスク (データベースの作成や処理、サーバーのプロパティの変更、このロールの他のメンバーシップの追加や削除、トレースの起動など) を実行するための権限が付与されます。 参照してください[サーバーの管理者アクセス許可の付与&#40;Analysis Services&#41; ](instances/grant-server-admin-rights-to-an-analysis-services-instance.md)詳細についてはします。  
  
## <a name="see-also"></a>参照  
 [Analysis Services インスタンスのサーバー モードの決定](instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Analysis services サーバーのプロパティを構成します。](server-properties/server-properties-in-analysis-services.md)   
 [Analysis Services でサポートされる認証方法](instances/authentication-methodologies-supported-by-analysis-services.md)   
 [ロールと権限 &#40;Analysis Services&#41;](multidimensional-models/roles-and-permissions-analysis-services.md)   
 [言語および照合順序 &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)  
  
  
