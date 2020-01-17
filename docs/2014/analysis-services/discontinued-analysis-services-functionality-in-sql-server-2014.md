---
title: SQL Server 2014 における Analysis Services 機能の廃止 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, backward compatibility
- SSAS, backward compatibility
- SQL Server Analysis Services, backward compatibility
- discontinued functionality [Analysis Services]
- unsupported features [Analysis Services]
ms.assetid: 39406be1-9819-4629-9c29-b32fb20bab2e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 616c39d03ff8081c209a80dcca912d831bcef1ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081683"
---
# <a name="discontinued-analysis-services-functionality-in-sql-server-2014"></a>SQL Server 2014 で提供が中止された Analysis Services の機能
  このトピックでは、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] で使用できなくなった [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]の機能について説明します。  
  
## <a name="discontinued-features-in-includesssql14includessssql14-mdmd"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
  
|カテゴリ|非推奨の機能|代替|  
|--------------|------------------------|-----------------|  
|ローカル キューブ|InsertInto 接続文字列プロパティ|ローカル キューブを設定するための元の接続文字列の構文は、CREATE GLOBAL CUBE ステートメントに置き換えられました。 詳細については、次を参照してください。[グローバル キューブの作成ステートメント&#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-global-cube)します。|  
|ローカル キューブ|CreateCube 接続文字列プロパティ|ローカル キューブを設定するための元の接続文字列の構文は、CREATE GLOBAL CUBE ステートメントに置き換えられました。 詳細については、次を参照してください。[グローバル キューブの作成ステートメント&#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-global-cube)します。|  
|データ マイニング|SQL Server 2000 PMML|SQL Server 2000 PMML 機能は、PMML 仕様では使用できなかったデータ マイニング アルゴリズムによって提供される独自の機能をサポートする専用の拡張機能がある PMML の形式を生成します。 SQL Server 2005 では、Analysis Services によって PMML 機能が新しい PMML 2. 1 標準に更新されました。 そのため、SQL Server 2000 で追加された専用の拡張機能は必要なくなりましたが、このリリースでもサポートされています。|  
|MDX ステートメント|CREATE ACTION ステートメント|このステートメントは、旧バージョンとの互換性のために用意されています。 このステートメントは、Action オブジェクトに置き換えられました。 最近のバージョンのアクションを作成する方法の詳細についての[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]を参照してください[アクション&#40;Analysis Services - 多次元データ&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md)します。|  
  
## <a name="discontinued-features-in-previous-releases"></a>以前のリリースで廃止された機能  
 SQL Server 2000 Analysis Services データベースを新しいバージョンに移行する際に使用された移行ウィザードは、SQL Server 2000 がサポートされなくなったため、提供が中止されました。  
  
 SQL Server 2000 Analysis Services データベースとの互換性を維持するための Decision Support オブジェクト (DSO) ライブラリも提供が中止され、SQL Server に付属しなくなりました。  
  
## <a name="see-also"></a>参照  
 [Analysis Services の旧バージョンとの互換性](analysis-services-backward-compatibility.md)  
  
  
