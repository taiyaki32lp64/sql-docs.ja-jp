---
title: サブジェクト領域データベース スキーマのオプション (スキーマ生成ウィザード) (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.schemagenwizard.subjectareaschemaopts.f1
ms.assetid: 4c109bb8-e19d-412b-908f-bfdd7f872439
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2173255654b9ef02c269ec34bd21f93f8bf629a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067974"
---
# <a name="subject-area-database-schema-options-schema-generation-wizard-analysis-services---multidimensional-data"></a>[サブジェクト領域データベース スキーマのオプション] (スキーマ生成ウィザード) (Analysis Services - 多次元データ)
  **[サブジェクト領域データベース スキーマのオプション]** ページを使用すると、スキーマの生成方法を制御したり、データの保存方法を定義したりできます。  
  
## <a name="options"></a>および  
 **スキーマを所有しています。**  
 新しいサブジェクト領域データベース内のスキーマの名前を指定します。  
  
 **ディメンション テーブルに主キーを作成します。**  
 生成されたスキーマのディメンション テーブルに主キーを作成します。 このオプションを選択しない場合、インデックスは作成されません。  
  
> [!NOTE]  
>  このオプションを選択しない場合は、参照整合性が適用されます。  
  
 **インデックスを作成します。**  
 生成されたスキーマの外部キー列にインデックスを作成します。  
  
 **参照整合性を適用します。**  
 生成されたスキーマで参照整合性を適用します。 このオプションを選択しない場合、リレーションシップは作成されますが適用されません。  
  
 **再生時にデータを保持します。**  
 ウィザードの完了時にサブジェクト領域データベースのデータを保持します。 このオプションを選択しない場合、サブジェクト領域データベースのすべてのデータは警告なしに消去されます。  
  
 **Time テーブルを設定します。**  
 ウィザードで Time テーブルにデータを設定する方法を指定します。 このオプションで使用できる値を次の表に示します。  
  
> [!NOTE]  
>  このオプションは、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] をプロジェクト モードで使用して [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] からスキーマ生成ウィザードが呼び出された場合だけ有効になります。  
  
|値|説明|  
|-----------|-----------------|  
|[設定]|サブジェクト領域の Time テーブルにデータが設定されます。|  
|[設定しない]|サブジェクト領域の Time テーブルにデータは設定されません。|  
|[空の場合のみ設定]|サブジェクト領域の Time テーブルは、空の場合にだけデータが設定されます。|  
  
## <a name="see-also"></a>関連項目  
 [スキーマ生成ウィザードの F1 ヘルプ&#40;Analysis Services - 多次元データ&#41;](schema-generation-wizard-f1-help-analysis-services-multidimensional-data.md)  
  
  
