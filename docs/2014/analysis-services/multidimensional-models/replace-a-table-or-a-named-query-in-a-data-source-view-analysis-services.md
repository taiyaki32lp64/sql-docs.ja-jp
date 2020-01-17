---
title: テーブルまたはデータ ソース ビュー (Analysis Services) の名前付きクエリの置換 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- replacing tables
- data source views [Analysis Services], tables
- named queries [Analysis Services], replacing tables
- tables [Analysis Services], data source views
- partitions [Analysis Services], named queries
ms.assetid: 60c2a018-1299-4915-b60e-e73316524def
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b9f1863fc3d707614b7c957dc5ef49561272d6e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073128"
---
# <a name="replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services"></a>データ ソース ビュー内のテーブルまたは名前付きクエリの置換 (Analysis Services)
  データ ソース ビュー デザイナーでは、データ ソース ビュー (DSV) 内のテーブル、ビュー、または名前付きクエリを、同じデータ ソースまたは異なるデータ ソースの別のテーブルやビュー、あるいは DSV で定義されている名前付きクエリに置換できます。 テーブルを置換した場合、DSV 内のテーブルのオブジェクト ID は変更されないので、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースまたはプロジェクト内でそのテーブルを参照している他のすべてのオブジェクトは、引き続きそのテーブルを参照します。 名前や列の型の一致に基づいて、引き続き関連のあるリレーションシップは維持されます。 これに対して、テーブルを削除して追加した場合、参照とリレーションシップは失われるので、再作成する必要があります。  
  
 テーブルを別のテーブルに置換するには、プロジェクト モードのデータ ソース ビュー デザイナー内のソース データに対するアクティブな接続が必要です。  
  
 データ ソース ビュー内のテーブルをデータ ソース内の別のテーブルに置換することが最も頻繁に行われます。 ただし、名前付きクエリをテーブルに置換することもできます。 たとえば、以前にテーブルを名前付きクエリに置換し、今回はテーブルに戻す場合があります。  
  
> [!IMPORTANT]  
>  データ ソース内のテーブルの名前を変更した場合は、DSV を更新する前に、テーブルの置換手順を実行し、名前を変更したテーブルを DSV 内の対応するテーブルのソースとして指定します。 置換および名前変更の手順を行うと、DSV 内のテーブル、テーブルの参照、およびテーブルのリレーションシップは維持されます。 この手順を実行しないと、DSV を更新したときに、データ ソース内の名前を変更したテーブルは削除されたと見なされます。 詳細については、「[データ ソース ビューでのスキーマの更新 (Analysis Services)](refresh-the-schema-in-a-data-source-view-analysis-services.md)」を参照してください。  
  
##  <a name="bkmk_nq"></a> テーブルを名前付きクエリで置換する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でプロジェクトを開くか、テーブルまたは名前付きクエリを置換するデータ ソース ビューが含まれているデータベースに接続します。  
  
2.  ソリューション エクスプローラーで、 **[データ ソース ビュー]** フォルダーを展開して、データ ソース ビューをダブルクリックします。  
  
3.  **[名前付きクエリの作成]** ダイアログ ボックスを開きます。 **[テーブル]** または **ダイアグラム** ペインで、置換するテーブルを右クリックし、 **[テーブルの置換]** をポイントして **[新しい名前付きクエリの使用]** をクリックします。  
  
4.  **[名前付きクエリの作成]** ダイアログ ボックスで名前付きクエリを定義し、 **[OK]** をクリックします。  
  
5.  変更したデータ ソース ビューを保存します。  
  
## <a name="replace-a-table-or-named-query-with-a-table"></a>テーブルまたは名前付きクエリを別のテーブルで置換する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でプロジェクトを開くか、テーブルまたは名前付きクエリを置換するデータ ソース ビューが含まれているデータベースに接続します。  
  
2.  ソリューション エクスプローラーで、 **[データ ソース ビュー]** フォルダーを展開して、データ ソース ビューをダブルクリックします。  
  
3.  **[テーブルと他のテーブルとの置換]** ダイアログ ボックスを開きます。 **[テーブル]** または **ダイアグラム** ペインで、置換するテーブルまたは名前付きクエリを右クリックし、 **[テーブルの置換]** をポイントして **[他のテーブルを使用]** をクリックします。  
  
4.  **[テーブルと他のテーブルとの置換]** ダイアログ ボックスで、次の操作を実行します。  
  
    1.  **[データソース]** ボックスの一覧で、使用するデータ ソースを選択します。  
  
    2.  テーブルまたは名前付きクエリを置換するテーブルを選択します。  
  
5.  **[OK]** をクリックします。  
  
6.  変更したデータ ソース ビューを保存します。  
  
## <a name="see-also"></a>参照  
 [「多次元モデルのデータ ソース ビュー」](data-source-views-in-multidimensional-models.md)  
  
  
