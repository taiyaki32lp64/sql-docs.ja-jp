---
title: 多次元モデルの翻訳 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.deletelanguagefirm.f1
ms.assetid: 5521f8ef-b10a-4861-9df7-1e43e0a1fb3f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a80c7950ec4079021bbcf03d9ccee6970d68786b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072743"
---
# <a name="translations-in-multidimensional-models"></a>多次元モデルの翻訳
  複数の言語のサポートで[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]翻訳を使用して行われます。 翻訳には、複数の言語で表示可能な [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトのプロパティの言語識別子およびバインドが含まれます。 たとえば、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースの翻訳を、指定した言語でそのデータベースのキャプションと説明が表示されるように定義できます。 翻訳の詳細については、次を参照してください。[キューブの翻訳](../multidimensional-models-olap-logical-cube-objects/cube-translations.md)します。  
  
## <a name="defining-translations"></a>翻訳の定義  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] で翻訳を定義するには、翻訳対象の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトに適したデザイナーを使用します。 翻訳を定義すると、該当する [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトに関連付けられた `Translation` オブジェクトが作成されます。この Translation オブジェクトには、関連付けられた [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトのプロパティに対応する、指定した言語の明示的なリテラル値が含まれています。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、次のオブジェクトおよびプロパティに翻訳を関連付けることができます。  
  
|オブジェクト|[プロパティ]|デザイナー|  
|------------|----------------|--------------|  
|[データベース]|`Caption`, `Description`|[一般的な&#40;データベース デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](../general-database-designer-analysis-services-multidimensional-data.md)|  
|Cube|`Caption`, `Description`|[翻訳&#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|[メジャー グループ]|`Caption`|[翻訳&#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|[メジャー]|`Caption`, `DisplayFolder`|[翻訳&#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|キューブ ディメンション|`Caption`|[翻訳&#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Perspective|`Caption`|[翻訳&#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|主要業績評価指標 (KPI)|`Caption`、 `Description`、 `DisplayFolder`|[翻訳&#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|操作|`Caption`|[翻訳&#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|名前付きセット|`Caption`|[翻訳&#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|計算されるメンバー|`Caption`|[翻訳&#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|データベース ディメンション|`Caption`, `AttributeAllMember`|[翻訳&#40;ディメンション デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|属性|`Caption`, `CaptionColumn`<sup>1</sup>, `AttributeHierarchyDisplayFolder`, `NamingTemplate`, `MembersWithDataCaption`|[翻訳&#40;ディメンション デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|Hieararchy|`Caption`, `AllMemberName`|[翻訳&#40;ディメンション デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|Level|`Caption`|[翻訳&#40;ディメンション デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
  
 <sup>1</sup> 、`CaptionColumn`属性のプロパティのデータ ソース ビュー内の列にバインドできるし、他の翻訳とは異なり、インスタンスの指定されている以外の Windows 照合順序を使用することができます。  
  
### <a name="defining-attribute-translations"></a>属性翻訳の定義  
 データベース ディメンション内の属性に関連付けられている翻訳は、他の翻訳とは異なり、次のように処理されます。  
  
-   `CaptionColumn` プロパティには、明示的なリテラル値ではなく列バインドを関連付けることができ、その属性のメンバーのメンバー名を翻訳できます。  
  
-   インスタンスについて指定されている照合順序以外の Windows 照合順序を使用して、翻訳で指定されている言語に合わせて、属性のメンバーを適切に並べ替えることができます。  
  
 使用することができます、**属性データの翻訳** ダイアログ ボックスで[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]データベース ディメンションの属性の翻訳を定義します。 詳細については、**属性データの翻訳**ダイアログ ボックスを参照してください[属性データの翻訳 ダイアログ ボックス&#40;Analysis Services - 多次元データ&#41;](../attribute-data-translation-dialog-box-analysis-services-multidimensional-data.md)します。  
  
## <a name="resolving-translations"></a>翻訳の解決  
 クライアント アプリケーションが、指定された言語識別子内の情報を要求すると、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトのデータおよびメタデータを、最も近い言語識別子に解決しようとします。 クライアント アプリケーションで既定の言語が指定されていない場合、ニュートラルなロケール識別子 (0) が指定されている場合、または既定の言語識別子 (1024) が処理される場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] はインスタンスの既定の言語を使用して [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトのデータおよびメタデータを返します。  
  
 クライアント アプリケーションで既定の言語識別子以外の言語識別子が指定されている場合、インスタンスはすべての使用可能なオブジェクトに対して、可能なすべての翻訳を反復処理します。 指定された言語識別子が翻訳の言語識別子と一致した場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] はその翻訳を返します。 一致する言語識別子が見つからない場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は次のいずれかの方法を使用して、指定された言語識別子に最も近い言語識別子を持つ翻訳を返します。  
  
-   次の言語識別子については、指定された言語識別子の翻訳が定義されていない場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は代替言語識別子の使用を試みます。  
  
    |指定された言語識別子|代替言語識別子|  
    |-----------------------------------|-----------------------------------|  
    |3076 - 中国語 (中華人民共和国香港特別行政区)|1028 - 中国語 (台湾)|  
    |5124 - 中国語 (中華人民共和国マカオ特別行政区)|1028 - 中国語 (台湾)|  
    |1028 - 中国語 (台湾)|既定の言語|  
    |4100 - 中国語 (シンガポール)|2052 - 中国語 (中華人民共和国)|  
    |2074 - クロアチア語|既定の言語|  
    |3098 - クロアチア語 (キリル文字)|既定の言語|  
  
-   他のすべての言語識別子の場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、指定された言語識別子の第一言語を抽出し、Windows によって指示された言語識別子を第一言語に最適なものとして取得します。 最適な言語識別子の翻訳が見つからない場合や、指定された言語識別子が第一言語に最適なものである場合は、既定の言語が使用されます。  
  
## <a name="deleting-translation-objects"></a>翻訳オブジェクトの削除  
 ディメンションまたはキューブ デザイナーで、完全に削除する翻訳オブジェクトを右クリックします。 削除したオブジェクトは復元および再利用ができないので、続行する前に、影響を受けるオブジェクトの一覧を確認してください。  
  
## <a name="see-also"></a>参照  
 [Analysis Services 多次元のグローバリゼーションのシナリオ](../globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [言語および照合順序 &#40;Analysis Services&#41;](../languages-and-collations-analysis-services.md)  
  
  
