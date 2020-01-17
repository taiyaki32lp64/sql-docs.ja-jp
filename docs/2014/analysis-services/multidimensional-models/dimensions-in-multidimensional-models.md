---
title: 多次元モデル内のディメンション |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- OLAP [Analysis Services], dimensions
- dimensions [Analysis Services], about dimensions
- OLAP objects [Analysis Services], dimensions
ms.assetid: 2b62b05c-00fd-4e60-b77f-f707ba83a19b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 520d6f11e5a472d5337a3747cc73c1d3656171c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075175"
---
# <a name="dimensions-in-multidimensional-models"></a>多次元モデル内のディメンション
  データベース ディメンションとは、ファクト データに関する情報を 1 つまたは複数のキューブで提供するための、属性と呼ばれる関連オブジェクトが集まったものです。 たとえば、Product ディメンションの一般的な属性としては、製品名、製品カテゴリ、製品ライン、製品サイズ、製品価格などがあります。 これらのオブジェクトは、データ ソース ビューのテーブル内の列にバインドされており、 既定では、これらの属性は、属性階層として表示され、キューブ内のファクト データを理解する際に使用できます。 属性はユーザー定義階層にまとめることができます。これらの階層には、ユーザーがキューブ内のデータを参照する際に使用できるナビゲーション パスが含まれています。  
  
 キューブには、ユーザーがファクト データの分析の基準として使用する、すべてのディメンションが含まれています。 キューブ内のデータベース ディメンションのインスタンスは、キューブ ディメンションと呼ばれ、キューブ内の 1 つ以上のメジャー グループに関連しています。 データベース ディメンションは、キューブで何度も使用できます。 たとえば、ファクト テーブルに時間関連のファクトが複数含まれている場合は、時間関連の各ファクトを分析するために別々のキューブ ディメンションを定義できます。 ただし、時間関連のデータベース ディメンションは 1 つしか必要ありません。つまり、時間に基づく複数のキューブ ディメンションをサポートするために、時間関連のリレーショナル データベースも 1 つしか必要となりません。  
  
> [!NOTE]  
>  ディメンション デザインに関連するパフォーマンスの問題については、「 [SQL Server 2008 R2 Analysis Services パフォーマンス ガイド](https://go.microsoft.com/fwlink/?LinkId=306717)」を参照してください。  
  
## <a name="defining-dimensions-attributes-and-hierarchies"></a>ディメンション、属性、および階層の定義  
 データベースとキューブのディメンション、属性、および階層を定義するための最も簡単な方法は、キューブ ウィザードを使用して、キューブの定義と同時にディメンションを作成することです。 キューブ ウィザードでは、データ ソース ビューのディメンション テーブルに基づいてディメンションを作成します。このディメンション テーブルは、キューブで使用するために、ウィザードで指定されたり、ユーザーが指定したりします。 その後、データベース ディメンションを作成して新しいキューブに追加すると、キューブ ディメンションが作成されます。  
  
 キューブを作成するときは、データベースに既に存在するディメンションを新しいキューブに追加することもできます。 これらのディメンションは、別のキューブやディメンション ウィザードで以前に定義されている場合があります。 データベース ディメンションは、定義した後に、ディメンション デザイナーで変更および構成できます。 またキューブ ディメンションは、キューブ デザイナーで、限られた範囲内でカスタマイズできます。  
  
> [!NOTE]  
>  XMLA または分析管理オブジェクト (AMO) のいずれかを使用すると、ディメンション、属性、および階層をプログラムによってデザインおよび構成することもできます。 詳細については、次を参照してください。 [Analysis Services スクリプト言語&#40;ASSL&#41;参照](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)と[Analysis Management Objects を使用した開発&#40;AMO&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 このトピックでは、次の内容について紹介します。  
  
 [データベース ディメンションの定義](define-database-dimensions.md)  
 ディメンション デザイナーを使用して、データベース ディメンションを変更および構成する方法について説明します。  
  
 [ディメンションの属性のプロパティの参照](dimension-attribute-properties-reference.md)  
 ディメンション デザイナーを使用して、データベース ディメンションの属性を定義、変更、および構成する方法について説明します。  
  
 [属性リレーションシップの定義](attribute-relationships-define.md)  
 ディメンション デザイナーを使用して、属性リレーションシップを定義、変更、および構成する方法について説明します。  
  
 [ユーザー定義階層の作成](user-defined-hierarchies-create.md)  
 ディメンション デザイナーを使用してユーザー定義階層のディメンション属性を定義、変更、および構成する方法について説明します。  
  
 [ビジネス インテリジェンス ウィザードを使用したディメンションの拡張](../use-the-business-intelligence-wizard-to-enhance-dimensions.md)  
 ビジネス インテリジェンス ウィザードを使用して、データベース ディメンションを拡張する方法について説明します。  
  
## <a name="see-also"></a>参照  
 [多次元モデルのキューブ](cubes-in-multidimensional-models.md)  
  
  
