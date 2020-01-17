---
title: 書き込み許可パーティション |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], partitions
- write-enabled partitions [Analysis Services]
- partitions [Analysis Services], write-enabled
- partitions [Analysis Services], storage
- writeback [Analysis Services], partitions
- storing data [Analysis Services], partitions
ms.assetid: 46e7683f-03ce-4af2-bd99-a5203733d723
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 13864dba5cac0274204050a8c78730de29f3321e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62727176"
---
# <a name="write-enabled-partitions"></a>書き込み許可パーティション
  キューブ内のデータは通常、読み取り専用です。 ただし、シナリオによっては、パーティションに書き込み許可を設定する必要が生じます。 書き込み許可パーティションを使用すると、ビジネス ユーザーは、セル値を変更し、その変更がキューブ データに与える影響を分析して、シナリオを調べることができます。 パーティションを書き込み許可にすると、クライアント アプリケーションは、パーティションのデータへの変更内容を記録できます。 これらの変更内容は、書き戻しデータとして知られており、個別のテーブルに格納され、メジャー グループの既存のデータは上書きされません。 ただし、キューブ データの一部のように、クエリ結果に組み込まれます。  
  
 キューブ全体を書き込み許可にすることも、キューブ内の特定のパーティションのみを書き込み許可にすることもできます。 書き込み許可ディメンションは、互いに異なりますが補完的です。 書き込み許可パーティションではパーティション セルを更新でき、書き込み許可ディメンションではディメンション メンバーを更新できます。 また、これらの 2 つの機能を組み合わせて使用することもできます。 たとえば、書き込み許可キューブまたは書き込み可能パーティションには、書き込み許可ディメンションを含める必要はありません。 **関連トピック:**[Write-Enabled ディメンション](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)します。  
  
> [!NOTE]  
>  データ ソースとして Microsoft Access データベースを持つキューブを書き込み許可にするときは、キューブ、パーティション、またはディメンションのデータ ソース定義に Microsoft OLE DB Provider for ODBC Drivers を使用しないでください。 代わりに、Microsoft Jet 4.0 OLE DB Provider、または Jet 4.0 OLE を含む任意のバージョンの Jet Service Pack を使用できます。 詳細については、マイクロソフト サポート技術情報の記事を参照してください。 [Microsoft Jet 4.0 データベース エンジンの service pack の入手方法](https://support.microsoft.com/?kbid=239114)します。  
  
 キューブを書き込み許可にできるのは、そのすべてのメジャーに `Sum` 集計関数が使用されている場合だけです。 リンク メジャー グループとローカル キューブは書き込み許可にできません。  
  
## <a name="writeback-storage"></a>書き戻しストレージ  
 ビジネス ユーザーによるすべての変更は、現在表示中の値との差分として書き戻しテーブルに格納されます。 たとえば、エンド ユーザーがあるセル値を 90 から 100 に変更した場合、書き戻しテーブルには値 `+10` が格納されます。このとき、変更時刻および変更を行ったビジネス ユーザーに関する情報も格納されます。 クライアント アプリケーションには、蓄積された変更の最終結果が表示されます。 キューブにある元の値はそのまま維持され、変更の監査記録は書き戻しテーブルに記録されます。  
  
 リーフ セルおよび非リーフ セルへの変更の処理は異なります。 リーフ セルは、メジャー グループによって参照されるすべてのディメンションのメジャーとリーフ メンバーの交差部分を表します。 リーフ セルの値は、ファクト テーブルから直接取得されるものであり、ドリル ダウンでそれ以上分割することはできません。 キューブまたはいずれかのパーティションが書き込み可能であれば、リーフ セルに変更を加えることができます。 非リーフ セルに変更を加えることができるのは、その非リーフ セルを構成するリーフ セル間で変更を配布する方法がクライアント アプリケーションに用意されている場合だけです。 このプロセスは、"割り当て" と呼ばれ、多元式 (MDX) の UPDATE CUBE ステートメントを介して管理されます。 ビジネス インテリジェンスの開発者は、UPDATE CUBE ステートメントを使用して、割り当て機能を含めることができます。 詳細については、次を参照してください。 [UPDATE CUBE ステートメント&#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-update-cube)します。  
  
> [!IMPORTANT]  
>  更新されるセルが重ならない場合は、`Update Isolation Level` 接続文字列プロパティを使用して、UPDATE CUBE のパフォーマンスを向上させることができます。 詳細については、「 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 」を参照してください。  
  
 非リーフ セルに加えられた変更がクライアント アプリケーションによって配布されるかどうかに関係なく、クエリが評価されるときは必ず、書き戻しテーブル内の変更がリーフ セルと非リーフ セルの両方に適用されるため、ビジネス ユーザーは変更がキューブ全体に与える影響を調べることができます。  
  
 ビジネス ユーザーが行った変更は、独立した書き戻しテーブルに保持されます。このテーブルを使用して、次の操作を実行できます。  
  
-   パーティションに変換して、変更を永続的にキューブに組み込む。 このアクションはメジャー グループを読み取り専用にします。 フィルター式を指定して、変換する変更を選択できます。  
  
-   破棄して、パーティションを元の状態に戻す。 このアクションはパーティションを読み取り専用にします。  
  
## <a name="security"></a>セキュリティ  
 ビジネス ユーザーは、属しているロールにキューブのセルへの読み取り/書き込み権限が割り当てられている場合にのみキューブの書き戻しテーブルに変更内容を記録できます。 ロールごとに、更新できるキューブ セルと更新できないキューブ セルを管理できます。 詳細については、次を参照してください。[キューブまたはモデル アクセス許可を付与&#40;Analysis Services&#41;](../multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)します。  
  
## <a name="see-also"></a>参照  
 [書き込み許可ディメンション](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)   
 [集計と集計デザイン](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)   
 [パーティション &#40;Analysis Services - 多次元データ&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [書き込み許可ディメンション](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
