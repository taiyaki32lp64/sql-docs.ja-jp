---
title: 'レッスン 8: アクションの定義 |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 15459396-83c9-48a0-b10a-99ae38768c79
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8293bb8d1f0465d09b296cbd18702b569f073766
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078227"
---
# <a name="lesson-8-defining-actions"></a>レッスン 8: アクションの定義
  このレッスンでは、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] プロジェクトでアクションを定義する方法を学習します。 アクションは [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] に格納される多次元式 (MDX) ステートメントです。アクションはクライアント アプリケーションに統合することができ、ユーザーによって開始可能です。  
  
> [!NOTE]  
>  このチュートリアルの各レッスンの操作内容が反映されたプロジェクトを、オンラインで入手できます。 途中のレッスンから開始する場合は、前のレッスンの操作内容が反映されたプロジェクトを作業の開始点として使用できます。 このチュートリアルのサンプル プロジェクトをダウンロードするには、[ここ](https://go.microsoft.com/fwlink/?LinkID=221866) をクリックしてください。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は、次の表に示されている種類のアクションをサポートします。  
  
|||  
|-|-|  
|CommandLine|コマンド プロンプトでコマンドを実行します。|  
|データセット|データセットをクライアント アプリケーションに返します。|  
|ドリルスルー|ドリルスルー ステートメントを式として返します。この式は、行セットを返すときにクライアントによって実行されます。|  
|Html|インターネット ブラウザーで HTML スクリプトを実行します。|  
|[専用]|この一覧に表示されていないインターフェイスを使用して操作を実行します。|  
|レポート|パラメーター化された URL ベースの要求をレポート サーバーに送信して、レポートをクライアント アプリケーションに返します。|  
|[行セット]|行セットをクライアント アプリケーションに返します。|  
|ステートメントから削除してください。|OLE DB コマンドを実行します。|  
|[URL]|インターネット ブラウザーで動的 Web ページを表示します。|  
  
 アクションを使用すると、アプリケーションを起動したり、選択したアイテムのコンテキスト内で他のステップを実行することができます。 詳細については、[「アクション (Analysis Services - 多次元データ)」](multidimensional-models/actions-analysis-services-multidimensional-data.md) および [「多次元モデルのアクション」](multidimensional-models/actions-in-multidimensional-models.md) を参照してください。  
  
> [!NOTE]  
>  アクション例については、[計算ツール] ペインの [テンプレート] タブか、 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW サンプル データ ウェアハウスのアクション例を参照してください。 このデータベースのインストールの詳細については、「 [Analysis Services 多次元モデリング チュートリアル用のサンプル データおよびプロジェクトのインストール](install-sample-data-and-projects.md)」 を参照してください。  
  
 このレッスンの内容は次のとおりです。  
  
 [ドリルスルー アクションの定義と使用](lesson-8-1-defining-and-using-a-drillthrough-action.md)  
 この作業では、このチュートリアルで以前に定義したファクト ディメンションのリレーションシップによって、ドリルスルー アクションの定義、使用、変更を行います。  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 9:パースペクティブと翻訳の定義](lesson-9-defining-perspectives-and-translations.md)  
  
## <a name="see-also"></a>参照  
 [Analysis Services のチュートリアル シナリオ](analysis-services-tutorial-scenario.md)   
 [多次元モデリング&#40;Adventure Works チュートリアル&#41;](multidimensional-modeling-adventure-works-tutorial.md)   
 [アクション&#40;Analysis Services - 多次元データ&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md)   
 [「多次元モデルのアクション」](multidimensional-models/actions-in-multidimensional-models.md)  
  
  
