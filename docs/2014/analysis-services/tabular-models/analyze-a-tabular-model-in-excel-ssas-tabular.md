---
title: Excel (SSAS テーブル) で表形式モデルの分析 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.chooseperspect.f1
ms.assetid: 47fa45fc-60ab-41a1-bde3-5781c8462889
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 17d2b9fee3c4e733ed46f9b975e69f84f05b93f2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067758"
---
# <a name="analyze-a-tabular-model-in-excel-ssas-tabular"></a>Excel でのテーブル モデルの分析 (SSAS テーブル)
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] の [Excel で分析] 機能によって Microsoft Excel が開き、モデル ワークスペース データベースへのデータ ソース接続が作成され、ピボットテーブルがワークシートに追加されます。 モデル オブジェクト (テーブル、列、メジャー、階層、および KPI) は、ピボットテーブルのフィールドの一覧にフィールドとして含まれています。  
  
> [!NOTE]  
>  [Excel で分析] 機能を使用するには、レポート デザイナーがインストールされているコンピューターに Microsoft Office 2003 以降が [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]と同じコンピューターにインストールされている必要があります。 Office が同じコンピューターにインストールされていない場合は、別のコンピューターの Excel を使用して、データ ソースとしてモデル ワークスペース データベースに接続できます。 これにより、ピボットテーブルをワークシートに手動で追加することができます。 モデル オブジェクト (テーブル、列、メジャー、および KPI) は、ピボットテーブルのフィールドの一覧にフィールドとして含まれています。  
  
## <a name="tasks"></a>処理手順  
  
#### <a name="to-analyze-a-tabular-model-project-by-using-the-analyze-in-excel-feature"></a>[Excel で分析] 機能を使用してテーブル モデル プロジェクトを分析するには  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で、 **[モデル]** メニューの **[Excel で分析]** をクリックします。  
  
2.  **[資格情報とパースペクティブの選択]** ダイアログ ボックスで、モデル ワークスペース データ ソースに接続するための次のいずれかの資格情報オプションを選択します。  
  
    -   現在のユーザー アカウントを使用するには、 **[現在の Windows ユーザー]** を選択します。  
  
    -   別のユーザー アカウントを使用するには、 **[別の Windows ユーザー]** を選択します。  
  
         通常、このユーザー アカウントはロールのメンバーになります。 パスワードは必要ありません。 このアカウントを使用できるのは、ワークスペース データベースに Excel で接続している場合のみです。  
  
    -   セキュリティ ロールを使用するには、 **[ロール]** を選択して、一覧から 1 つ以上のロールを選択します。  
  
         セキュリティ ロールはロール マネージャーを使用して定義する必要があります。 詳細については、「[ロールの作成および管理 (SSAS テーブル)](roles-ssas-tabular.md)」を参照してください。  
  
3.  パースペクティブを使用するには、 **[パースペクティブ]** ボックスの一覧からパースペクティブを選択します。  
  
     パースペクティブ (既定値以外) は [パースペクティブ] ダイアログ ボックスを使用して定義する必要があります。 詳細については、「[パースペクティブの作成と管理 (SSAS テーブル)](perspectives-ssas-tabular.md)」を参照してください。  
  
> [!NOTE]  
>  Excel のピボットテーブルのフィールドの一覧は、モデル デザイナーでモデル プロジェクトに変更を加えても自動的に更新されません。 ピボットテーブルのフィールドの一覧を更新するには、Excel の **[オプション]** リボンで **[更新]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Excel で分析 &#40;SSAS テーブル&#41;](analyze-in-excel-ssas-tabular.md)  
  
  
