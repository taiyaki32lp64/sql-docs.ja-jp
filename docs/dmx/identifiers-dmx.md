---
title: 識別子 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1f72832fd684dd59e27ce58576a7f65fa8796347
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074809"
---
# <a name="identifiers-dmx"></a>識別子 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  すべてのオブジェクトで[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]に識別子を設定する必要があります。 オブジェクトの名前が識別子となります。 サーバー、データベース、およびデータベース オブジェクト (データ ソース、データ ソース ビュー、キューブ、ディメンション、マイニング モデルなど) は識別子を持っています。  
  
 データ マイニング拡張機能 (DMX) には 2 つのクラスの識別子があります。  
  
-   [標準識別子](#RegularIdentifiers)  
  
-   [区切られた識別子](#DelimitedIdentifiers)  
  
 オブジェクト識別子は、オブジェクトの定義時に作成されます。 オブジェクトを参照するには、この作成された識別子を使用します。 識別子は 100 文字以下である必要があります。  
  
##  <a name="RegularIdentifiers"></a> 標準識別子  
 DMX の標準識別子は、識別子の形式に関する [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] の規則に準拠しています。 DMX の標準識別子には区切り記号は必要ありません。 通常、区切られていない識別子を使用する DMX ステートメントの例を次に示します。  
  
```  
SELECT * FROM Clustering.CONTENT;  
```  
  
### <a name="rules-for-regular-identifiers"></a>標準識別子に関する規則  
 標準識別子の形式に関する規則は、次のとおりです。  
  
1.  標準識別子の最初の文字は、次のうちのいずれかである必要があります。  
  
    -   Unicode 規格 &#xa0;2.0 で定義されている文字。 これには、ラテン文字 a ~ z、a ~ Z、およびその他の言語の文字が含まれます。  
  
    -   アンダースコア (_)。  
  
2.  名前の先頭以外では、次の文字を使用できます。  
  
    -   Unicode 規格 &#xa0;2.0 で定義されているようになりました。  
  
    -   Basic Latin スクリプトまたはその他の各国スクリプトの 10 進数  
  
    -   アンダースコア (_)。  
  
3.  DMX 予約語を識別子として使用することはできません。 DMX では、予約語の大文字と小文字は区別されません。 詳細については、次を参照してください。[予約済みキーワード&#40;DMX&#41;](../dmx/reserved-keywords-dmx.md)します。  
  
4.  埋め込まれたスペースや特殊文字を識別子に含めることはできません。  
  
 これらの規則に準拠していない識別子を DMX ステートメントで使用する場合は、その識別子をかっこで区切る必要があります。  
  
##  <a name="DelimitedIdentifiers"></a> 区切られた識別子  
 区切られた識別子はかっこ ([ ]) で囲みます。  これらの規則に準拠した区切られた識別子を使用した DMX ステートメントの例は、次のとおりです。  
  
```  
SELECT * FROM [Marketing_Clusters].CONTENT;  
```  
  
 標準識別子の形式に関する規則に準拠していない識別子は、必ず区切り記号で区切る必要があります。 スペースを含んでいる区切られた識別子を使用した DMX ステートメントの例は、次のとおりです。  
  
```  
SELECT * FROM [Targeted Mailing].CONTENT;  
```  
  
 区切られた識別子を使用するのは、次のような場合です。  
  
-   予約語をオブジェクト名やオブジェクト名の一部に使用する場合。  
  
     予約キーワードはオブジェクト名に使用しないことをお勧めします。 以前のバージョンからアップグレードしたデータベースに[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]の以前のバージョンで予約されていなかった単語を含む識別子が含まれている可能性があります[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]の予約語であるが、[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]します。 オブジェクト名の変更が可能になるまで、このようなオブジェクトを参照するには、区切られた識別子を使用します。  
  
-   修飾された識別子として示されていない文字を使用する場合。  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、現在のコード ページ内の文字はすべて区切られた識別子に使用することができますが、特殊文字を区別しないでオブジェクト名に使用すると、DMX ステートメントの読み取りおよびメンテナンスが難しくなる場合があります。  
  
### <a name="rules-for-delimited-identifiers"></a>区切られた識別子に関する規則  
 区切られた識別子の形式に関する規則は、次のとおりです。  
  
1.  区切られた識別子は、標準識別子の場合と同じ文字数、つまり、区切り記号を除いた 1 ～ 100 文字で構成されます。  
  
2.  識別子の本体は、区切り記号を含め、現在のコード ページ内で使用される文字の任意の組み合わせで構成されます。 識別子の本体に区切り記号が含まれている場合は、特別な処理が必要になります。  
  
    -   識別子の本体に左かっこ ([) が含まれている場合は、処理を行う必要はありません。  
  
    -   識別子の本体に右かっこ (]) が含まれている場合は、コード ページ内で表現するために右かっこを 2 つ (]]) 指定する必要があります。  
  
### <a name="delimiting-identifiers-with-multiple-parts"></a>複数の部分に区切られた識別子  
 修飾されたオブジェクト名を使用する際、場合によってはオブジェクト名を構成している複数の識別子を区切る必要があります。 各識別子は個々に区切ってください。  
  
## <a name="see-also"></a>参照  
 [データ マイニング拡張機能 &#40;DMX&#41; リファレンス](../dmx/data-mining-extensions-dmx-reference.md)   
 [データ マイニング拡張機能&#40;DMX&#41;構文要素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [データ マイニング拡張機能&#40;DMX&#41;関数リファレンス](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [データ マイニング拡張機能&#40;DMX&#41;演算子リファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [データ マイニング拡張機能&#40;DMX&#41;ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)   
 [データ マイニング拡張機能&#40;DMX&#41;構文表記規則](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [一般的な予測関数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
