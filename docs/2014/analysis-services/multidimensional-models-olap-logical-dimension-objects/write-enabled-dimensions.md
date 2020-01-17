---
title: 書き込み許可ディメンション |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- write-enabled dimensions [Analysis Services]
- dimensions [Analysis Services], write-enabled
- dimension writeback [Analysis Services]
- write-enabled cubes [Analysis Services]
- writeback [Analysis Services], dimensions
ms.assetid: 0bac050d-cd3b-427b-884a-65a91be89500
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f76ba993508807e57e73d5e53ea25a4cbe382529
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62727447"
---
# <a name="write-enabled-dimensions"></a>書き込み許可ディメンション
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
 ディメンション内のデータは通常、読み取り専用です。 ただし、シナリオによってはディメンションに書き込み許可を設定する必要が生じます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、書き込み許可ディメンションにより、ビジネス ユーザーは、ディメンションの内容を変更し、ディメンションの階層の変更の直接的な影響を参照してください。 1 つのテーブルに基づいているすべてのディメンションへの書き込みを許可できます。 書き込み許可ディメンションでは、ビジネス ユーザーと管理者は、ディメンション内の属性メンバーの変更、移動、追加、および削除を行うことができます。 これらの更新プログラムと総称*ディメンションの書き戻し*します。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、すべてのディメンション属性に対するディメンションの書き戻しがサポートされており、ディメンションのすべてのメンバーを変更できます。 書き込み許可キューブや書き込み許可パーティションでは、更新はキューブのソース テーブルとは別に、書き戻しテーブルに格納されます。 ただし、書き込み許可ディメンションでは、更新はディメンションのテーブルに直接記録されます。 また、書き込み許可ディメンションが複数パーティションのキューブに含まれており、そのデータ ソースの一部またはすべてにディメンション テーブルのコピーがあると、書き戻しプロセスでは元のディメンション テーブルだけが更新されます。  
  
 書き込み許可ディメンションと書き込み許可キューブは、互いに異なりますが補完的な特徴を備えています。 書き込み許可ディメンションでは、ビジネス ユーザーはメンバーを更新できますが、書き込み許可キューブではセル値を更新できます。 これらの 2 つの機能は補完的なものですが、両方を組み合わせて使用する必要はありません。 ディメンションの書き戻しを行うために、ディメンションがキューブに含まれている必要はありません。 書き込み許可ディメンションは、書き込みが許可されていないキューブに含めることもできます。 ディメンションとキューブの書き込みを許可するときと、そのセキュリティをメンテナンスするときには、異なる手順を使用します。  
  
 ディメンションの書き戻しには次の制限が適用されます。  
  
-   新しいメンバーを作成するときは、ディメンションにすべての属性を含める必要があります。 ディメンションのキー属性値を指定せずにメンバーを挿入することはできません。 このため、メンバーの作成は、ディメンション テーブルに定義されている制約 (NULL 以外のキー値など) に拘束されます。  
  
-   ディメンションの書き戻しは、スター スキーマのみでサポートされています。 つまり、ディメンションはファクト テーブルに直接関連付けられている 1 つのディメンション テーブルに基づいている必要があります。 ディメンションの書き込みを許可すると、既存の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースに配置するか、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトを作成するときに、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によってこの要件が検証されます。  
  
 書き戻しディメンションの既存のすべてのメンバーを変更または削除できます。 メンバーを削除すると、子のメンバーもすべて連鎖的に削除されます。 たとえば、CountryRegion、Province、City、および Customer 属性を含む Customer ディメンションで、国または地域を削除すると、その国または地域に属する都道府県、市町村、および顧客もすべて削除されます。 国または地域に都道府県が 1 つしか含まれていない場合、その都道府県を削除すると、国または地域も削除されます。  
  
 書き戻しディメンションのメンバーは、同じレベル内でのみ移動できます。 たとえば、市町村は別の国または地域、あるいは都道府県の City レベルに移動できますが、Province レベルまたは CountryRegion レベルには移動できません。 親子階層では、すべてのメンバーはリーフ メンバーであるため、メンバーは `(All)` レベル以外のすべてのレベルに移動できます。  
  
 親子階層のメンバーを削除すると、メンバーの子はメンバーの親に移動します。 削除するメンバーに対してはリレーショナル テーブルの更新権限が必要ですが、移動するメンバーに対しては権限は必要ありません。 アプリケーションで親子階層内のメンバーを移動するときは、メンバーの子孫をメンバーと共に移動するか、メンバーの親に移動するかを UPDATE 操作で指定できます。 親子階層内のメンバーを再帰的に削除するには、そのメンバーとメンバーのすべての子孫に対するリレーショナル テーブルの更新権限が必要です。  
  
> [!NOTE]  
>  親子階層内の親属性を更新する場合、その他のプロパティまたは属性の更新は含めないでください。  
  
 ディメンションをすべて変更すると、そのディメンションの構造が変更されます。 ディメンションへの各変更は 1 つのトランザクションと見なされ、ディメンション構造を更新するための増分処理が必要になります。 書き込み許可ディメンションには、他のディメンションと同じ処理要件があります。  
  
> [!NOTE]  
>  ディメンションの書き戻しはリンク ディメンションではサポートされていません。  
  
## <a name="security"></a>セキュリティ  
 書き込み許可ディメンションを更新できるビジネス ユーザーは、そのディメンションへの読み取り/書き込みアクセスが許可されている [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース ロールに属するユーザーだけです。 ロールごとに、更新できるメンバーと更新できないメンバーを管理できます。 ビジネス ユーザーが書き込み許可ディメンションを更新するには、そのクライアント アプリケーションでこの機能がサポートされている必要があります。 このようなユーザーの場合、書き込み許可ディメンションを、その前回の変更以後に処理されたキューブに含める必要があります。 詳細については、「[オブジェクトと操作へのアクセスの承認 (Analysis Services)](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)」を参照してください。  
  
 管理者ロールに含まれているユーザーとグループは、書き込み許可ディメンションがキューブに含まれていなくても、その書き込み許可ディメンションの属性メンバーを更新できます。  
  
## <a name="see-also"></a>参照  
 [データベース ディメンション プロパティ](database-dimension-properties.md)   
 [書き込み許可パーティション](../multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [ディメンション &#40;Analysis Services - 多次元データ&#41;](dimensions-analysis-services-multidimensional-data.md)  
  
  
