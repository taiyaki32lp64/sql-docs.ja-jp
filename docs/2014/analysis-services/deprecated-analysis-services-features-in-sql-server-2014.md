---
title: 非推奨の Analysis Services の SQL Server 2014 の機能 |Microsoft Docs
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
- deprecated features [Analysis Services]
ms.assetid: 2c96ecfe-a170-41d0-bee3-74503f880197
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 04d12aab677e38d17d4e869e6885eb470854d824
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081916"
---
# <a name="deprecated-analysis-services-features-in-sql-server-2014"></a>SQL Server 2014 に含まれている非推奨の Analysis Services 機能
  このトピックでは、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] でまだ使用できるものの、非推奨とされた [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]の機能について説明します。 これらの機能は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の今後のリリースで削除される予定です。 非推奨の機能を新しいアプリケーションで使用しないでください。  
  
## <a name="features-not-supported-in-the-next-version-of-sql-server"></a>SQL Server の次のバージョンでサポートされない機能  
 以下の [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 機能は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の次のバージョンではサポートされません。 新規の開発作業ではこれらの機能を使用しないようにし、現在これらの機能を使用しているアプリケーションはできるだけ早く修正してください。  
  
|カテゴリ|非推奨の機能|代替|  
|--------------|------------------------|-----------------|  
|MDX 関数|CalculationPassValue 関数|[なし] : OLAP エンジンは計算パスを管理します。 この関数は必要ではなくなりました。|  
|MDX 関数|CalculationCurrentPass 関数|[なし] : OLAP エンジンは計算パスを管理します。 この関数は必要ではなくなりました。|  
|多次元式 (MDX) (Multidimensional Expressions (MDX))|NON_EMPTY_BEHAVIOR クエリ オプティマイザー ヒントが既定で有効になっていました。|NON_EMPTY_BEHAVIOR クエリ オプティマイザー ヒントは、将来のリリースでは既定で無効にされる予定です。 MDX 最適化ヒントは、適切に使用しないと正しくない結果が生じる可能性があります。|  
|その他|CELL_EVALUATION_LIST intrinsic セル プロパティ|以前は、セルに適用する評価された数式の一覧を提供していました。 このリリースの Analysis Services では、このプロパティは空白です。  解決順序は MDX スクリプトで指定されるようになりました。 詳細については、次を参照してください[理解パス順序と解決順序&#40;MDX。&#41;](multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md)|  
|オブジェクト|COM アセンブリ|COM アセンブリにより、セキュリティ上のリスクが生じる可能性があります。 COM アセンブリのサポートは、将来のリリースでは削除される予定です。|  
  
## <a name="features-not-supported-in-a-future-version-of-sql-server"></a>SQL Server の今後のバージョンでサポートされない機能  
 以下の [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 機能は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の次のバージョンではサポートされますが、その後のバージョンでは削除されます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のどのバージョンであるかは決定していません。  
  
|カテゴリ|非推奨の機能|代替|  
|--------------|------------------------|-----------------|  
|多次元モデル|リモート パーティション|[なし] : 代わりにローカル パーティションを使用します。 参照してください[を作成およびローカル パーティションの管理&#40;Analysis Services&#41; ](multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)詳細についてはします。|  
|多次元モデル|リモート リンク メジャー グループ|リモート リンク メジャー グループは、リモート サーバー上のデータ ソースを使用するリンク メジャー グループです。 リンク メジャー グループに対してリモート データ ソースを使用する機能は、非推奨にするスケジュールが設定されています。<br /><br /> この機能に代わる機能はありません。 代わりに、ローカル リンク メジャー グループを使用することをお勧めします。 詳細については、「 [Linked Measure Groups](multidimensional-models/linked-measure-groups.md) 」をご覧ください。|  
|多次元モデル|ディメンションの書き戻し|[なし] : 書き戻し機能が必要な場合はパーティションの書き戻しを使用します。 参照してください[パーティションの書き戻しの設定](multidimensional-models/set-partition-writeback.md)詳細についてはします。|  
|多次元モデル|リンク ディメンション|[なし] : 別のモデル内にあるディメンションにリンクする代わりに、追加のモデルにディメンションをコピーすることを検討してください。|  
|MDX (MDX)|Non_Empty_Behavior プロパティ|[なし] : 計算されるメンバーを作成するときにこのプロパティを設定すると、無効な結果を返す可能性が大きくなります。 OLAP エンジンへの最近の最適化により、スパース データセットに対する操作が改善され、このプロパティの関連性は低くなりました。|  
  
## <a name="see-also"></a>関連項目  
 [Analysis Services の旧バージョンとの互換性](analysis-services-backward-compatibility.md)   
 [SQL Server 2014 で提供が中止された Analysis Services の機能](discontinued-analysis-services-functionality-in-sql-server-2014.md)  
  
  
