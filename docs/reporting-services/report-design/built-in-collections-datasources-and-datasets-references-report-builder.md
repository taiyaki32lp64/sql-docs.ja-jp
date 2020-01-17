---
title: DataSources コレクションと DataSets コレクションの参照 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: f951a4aa-da55-4e43-8579-4a5d4480d11f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 930dfe2773b72723c2b8dc8571272847bb0d62d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581802"
---
# <a name="built-in-collections---datasources-and-datasets-references-report-builder"></a>組み込みコレクション - DataSources と DataSets の参照 (レポート ビルダー)
  **DataSources** コレクションは、レポートで使用されているすべてのデータ ソースを表します。 同様に、 **DataSets** コレクションは、レポート内のすべてのデータ ソースのデータセットすべてを表します。 参照するデータ ソース別に構成されているレポート データセットの階層ビューを表示するには、 **[レポート データ]** ペインを使用します。 これらのコレクションへの参照を含めても、レポートをプレビューしたときには値が表示されません。 このコレクションを使用できるのは、レポートがレポート サーバーにパブリッシュされた後だけです。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="datasources"></a>DataSources  
 **DataSources** コレクションは、パブリッシュ済みレポート定義で参照されるデータ ソースを表します。 この情報をレポートに含め、レポート データのソースを説明することもできます。 このコレクションは、 **プレビュー** モードでは使用できません。 次の表では、 **DataSources** コレクション内の変数について説明します。  
  
|**変数**|**型**|**[説明]**|  
|------------------|--------------|---------------------|  
|**DataSourceReference**|**String**|レポート サーバー上のデータ ソース定義の完全パスです。 たとえば、レポートでレポート履歴の一部として使用されたすべてのデータ ソースの一覧を含める場合があります。 次の例では、AdventureWorks2012 という名前のデータ ソースの完全パスを示します。<br /><br /> `/DataSources/AdventureWorks2012`」を参照してください。|  
|**型**|**String**|データ ソースのデータ プロバイダーの種類です。 たとえば、 `SQL`のようにします。|  
  
## <a name="datasets"></a>DataSets  
 **DataSets** コレクションは、レポート定義で参照されるデータセットを表します。 レポートのクエリをテキスト ボックスに含めて、レポート内のデータに関心を持っているユーザーが元のコマンド テキストを参照できるようにすることもできます。 このコレクションは、 **プレビュー** モードでは使用できません。 次の表では、 **DataSets** コレクションのメンバーについて説明します。  
  
|**メンバー**|**型**|**[説明]**|  
|----------------|--------------|---------------------|  
|**CommandText**|**String**|データベース データ ソースの場合、これはデータ ソースからデータを取得するために使用するクエリです。 クエリが式の場合は、評価済みの式になります。|  
|**RewrittenCommandText**|**String**|データ プロバイダーの展開された CommandText 値。 これは通常、レポート パラメーターにマップされたクエリ パラメーターと共にレポートに使用されます。 コマンド テキスト パラメーター参照を、マップされたレポート パラメーターに対して選択された定数値に展開する場合、データ プロバイダーがこのプロパティを設定します。|  
  
### <a name="using-query-expressions"></a>クエリ式の使用  
 式を使用して、データセットに含まれているクエリを定義できます。 この機能を使用して、ユーザーからの入力や他のデータセットのデータ、その他の変数によりクエリが変化するようにレポートをデザインできます。 クエリについては、「[レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [式 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [式の例 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
