---
title: 主要業績評価指標 (Kpi) では、多次元モデル |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- viewing Key Performance Indicators
- Key Performance Indicators [Analysis Services]
- KPIs [Analysis Services]
- OLAP objects [Analysis Services], performance indicators
- weights [Analysis Services]
- displaying Key Performance Indicators
- parent KPIs [Analysis Services]
- child KPIs
ms.assetid: 73aee2da-da30-44f1-829c-0a4c078a7768
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 35482dc6206f0ad8807cb0f9a3e46902d14061ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074798"
---
# <a name="key-performance-indicators-kpis-in-multidimensional-models"></a>多次元モデルの主要業績評価指標 (KPI)
  ビジネス用語では、主要業績評価指標 (KPI) とは、ビジネスの成功度を判断するための測定値のことです。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]における KPI は、キューブ内のメジャー グループに関連付けられた、ビジネスの成功の評価に使用される計算のコレクションです。 これらの計算は通常、多次元式 (MDX) または計算されるメンバーの組み合わせです。 KPI には、KPI の計算結果をクライアント アプリケーションでどのように表示するかについての情報を提供する追加のメタデータもあります。  
  
 KPI で扱う情報は、設定された目標、キューブに記録された実際の業績の公式、および業績の傾向と状態を示す測定値です。 公式の定義と、KPI の値に関するその他の定義には AMO を使用します。 クライアント アプリケーションによる KPI 値の取得およびエンド ユーザーへの公開には、ADOMD.NET などのクエリ インターフェイスが使用されます。 詳細については、「 [ADOMD.NET での開発](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net)」を参照してください。  
  
 簡単な <xref:Microsoft.AnalysisServices.Kpi> オブジェクトは、基本情報、目標、実際の達成値、状態値、傾向値、および KPI が表示されるフォルダーで構成されます。 基本情報には、KPI の名前および説明が含まれます。 目標は、数値に評価される MDX 式です。 実際の値は、数値に評価される MDX 式です。 状態と傾向の値は、数値に評価される MDX 式です。 フォルダーは、クライアントに表示される KPI の推奨される場所です。  
  
 ビジネス用語では、主要業績評価指標 (KPI) とは、ビジネスの成功度を判断するための測定値のことです。 KPI は一定期間中頻繁に評価されます。 たとえば、組織の営業部門では KPI として月間売上総利益を使用できます。一方、同じ組織の人事部門では、四半期単位の従業員離職率を使用できます。 これらはそれぞれ KPI の一例です。 企業幹部は、グループにまとめて事業のスコアカードに記録した KPI を頻繁に使用し、事業の成功度の履歴要約をすばやく正確に取得します。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]における KPI は、キューブ内のメジャー グループに関連付けられた、ビジネスの成功を評価するために使用する計算のコレクションです。 これらの計算は通常、多次元式 (MDX) および計算されるメンバーの組み合わせです。 KPI には、KPI の計算結果をクライアント アプリケーションでどのように表示するかについての情報を提供する追加のメタデータもあります。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] での KPI の主要な利点の 1 つは、別々のクライアント アプリケーションによって使用できる、サーバー ベースの KPI であることです。 サーバー ベースの KPI では、個別のクライアント アプリケーションで別々のバージョンのデータを管理するのではなく、単一の実稼働バージョンがサポートします。 さらに、複雑な計算を各クライアント コンピューターではなくサーバー上で実行するので、パフォーマンス上の利点も期待できます。  
  
## <a name="common-kpi-terms"></a>一般的な KPI 用語  
 次の表は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]の一般的な KPI 用語の定義を示しています。  
  
|項目|定義|  
|----------|----------------|  
|[目標]|KPI のターゲット値を返す MDX 数値式または計算。|  
|値|KPI の実際の値を返す MDX 数値式。|  
|状態|特定時点の KPI の状態を示す MDX 式。<br /><br /> 状態 MDX 式は、-1 ～ 1 の正規化された値を返します。 -1 以下の値は "不良" または "低" と解釈されます。 値 0 は "許容値" または "中" と解釈されます。 1 以上の値は、"良" または "高" と解釈されます。<br /><br /> 中間値は数の制限なく返すことができ、クライアント アプリケーションでサポートされていれば、それを使用して任意の数の状態情報を表示できます。|  
|傾向|一定期間にわたり、KPI の値を評価する MDX 式。 傾向は、特定のビジネス コンテキストで役に立つ任意の時間ベースの条件です。<br /><br /> 傾向 MDX 式を使用すると、ビジネス ユーザーは、一定期間内の KPI の上下を判断できるようになります。|  
|状態インジケーター|KPI の状態をわかりやすく示す視覚的要素。 要素の表示は、状態を評価する MDX 式の値によって決まります。|  
|傾向インジケーター|KPI の傾向をわかりやすく示す視覚的要素。 要素の表示は、傾向を評価する MDX 式の値によって決まります。|  
|[フォルダーの表示]|ユーザーがキューブを参照する際に KPI が表示されるフォルダー。|  
|[親 KPI]|親 KPI の計算の一部として子 KPI の値を使用する、既存の KPI への参照。 計算は、他の KPI の値で構成されている単一の KPI である場合もあります。 このプロパティにより、クライアント アプリケーションで親 KPI の下にある子 KPI が正しく表示されます。|  
|[現在の時間メンバー]|KPI の一時的なコンテキストを識別するメンバーを返す MDX 式。|  
|Weight|KPI に相対的な重要度を割り当てる MDX 数値式。 KPI が親 KPI に割り当てられている場合、親 KPI の値の計算時には、重みを使用して子 KPI の結果値が比例的に調整されます。|  
  
## <a name="parent-kpis"></a>親 KPI  
 組織は、異なるレベルの異なるビジネス基準を追跡することがあります。 たとえば、会社全体のビジネス上の成功を計測するために 2 ～ 3 の KPI を使用し、それらの KPI が、会社内のビジネス単位で追跡したその他 3 ～ 4 の KPI に基づいている場合があります。 また、会社内のビジネス単位は、同じ KPI の計算に異なる統計を使用する可能性があり、その結果が会社全体の KPI にロール アップされます。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、KPI 間に親子リレーションシップを定義できます。 この親子リレーションシップにより、子 KPI の結果を親 KPI の結果の計算に使用できます。 さらに、クライアント アプリケーションはこのリレーションシップを使用して、親子 KPI を正しく表示できます。  
  
## <a name="weights"></a>重み  
 重みは子 KPI にも割り当てることができます。 重みにより、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、親 KPI の値の計算時に子 KPI の結果を比例的に調整できます。  
  
## <a name="retrieving-and-displaying-kpis"></a>KPI の取得と表示  
 KPI の表示は、クライアント アプリケーションの実装に依存します。 たとえば、キューブ デザイナーの **[KPI]** タブのツール バーで **[ブラウザー ビュー]** を選択すると、有効なクライアント実装の 1 つが表示されます。このビューでは、状態インジケーターと傾向インジケーターの表示にグラフィックを使用し、KPI のグループ化に表示フォルダーを使用して、親 KPI の下に子 KPI を表示します。  
  
 MDX 式、ステートメント、スクリプトなどで使用する値または目標など、KPI の個々のセクションを取得するには、MDX 関数を使用できます。  
  
  
