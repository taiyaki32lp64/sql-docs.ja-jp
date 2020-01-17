---
title: 属性
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- free-form attributes [Master Data Services]
- attributes [Master Data Services], about attributes
- attributes [Master Data Services], file attributes
- file attributes [Master Data Services]
- attributes [Master Data Services], free-form attributes
- attributes [Master Data Services]
ms.assetid: 95ecb75f-c559-41c3-933c-40ae60a4c2fd
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 19cbf51a9ac022674e9dfec7b287a38d16af00cf
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728754"
---
# <a name="attributes-master-data-services"></a>属性 (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  属性とは、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] エンティティに含まれるオブジェクトです。 属性値はエンティティのメンバーを表します。 属性を使用してリーフ メンバー、統合メンバー、またはコレクションを表すことができます。  
  
## <a name="how-attributes-relate-to-other-model-objects"></a>属性と他のモデル オブジェクトとの関連付け  
 属性は、エンティティ テーブルの列と考えることができます。 属性値は、特定のメンバーを表すために使用される値です。  
  
 ![テーブルとして表されるマスターデータサービスエンティティ](../master-data-services/media/mds-conc-entity-table.gif "テーブルとして表されるマスターデータサービスエンティティ")  
  
 多数の属性を含むエンティティを作成するときは、属性を属性グループに整理できます。 詳細については、「[属性グループ (マスター データ サービス)](../master-data-services/attribute-groups-master-data-services.md)」を参照してください。  
  
## <a name="required-attributes"></a>必須の属性  
 エンティティを作成すると、Name 属性と Code 属性が自動的に作成されます。 Code 属性には値が必要であり、Code 属性はエンティティ内で一意であることが必要です。 Name 属性と Code 属性を削除することはできません。  
  
## <a name="attribute-types"></a>属性の種類  
 属性には、次の 3 種類があります。  
  
-   自由形式属性。テキスト、数値、日付、またはリンクを自由形式で入力できます。  
  
-   ドメイン ベースの属性。エンティティによって設定されます。 詳細については、「[ドメインベースの属性 (マスター データ サービス)](../master-data-services/domain-based-attributes-master-data-services.md)」を参照してください。  
  
-   ファイル属性。ファイル、ドキュメント、または画像を格納するために使用されます。 ファイル属性は、ファイルに特定の拡張子を付けることによって、データの一貫性を確保するためのものです。 悪意のあるユーザーによる異なる種類のファイルのアップロードを防ぐことを保証するものではありません。  
  
### <a name="numeric-free-form-attributes"></a>数値自由形式属性  
 数値自由形式属性値は **SqlDouble** 値型に限定されるため、この属性には特別な処理が必要です。  
  
 既定では、 **SqlDouble** 値には有効桁数 15 桁の 10 進数が含まれますが、内部的には最大 17 桁が保持されています。 浮動小数点数の有効桁数により、複数の結果が得られます。  
  
-   特定の有効桁数で等しく見える 2 つの浮動小数点数が、最小有効数字が異なっているために等しくない場合があります。  
  
-   浮動小数点数を使用する数学的演算または比較演算で小数が使用された場合は、浮動小数点数がその小数に正確に近似していない場合があるため、同じ結果が生成されないことがあります。  
  
-   浮動小数点数が含まれていると、値が " *ラウンド トリップ* " されない場合があります。 値のラウンド トリップとは、演算で元の浮動小数点数が別の形式に変換され、逆の演算で変換後の形式から浮動小数点数に戻されて、最終の浮動小数点数が元の浮動小数点数に等しくなる場合をいいます。 変換で最小有効数字が 1 桁以上失われるか、または変更された場合は、ラウンド トリップが失敗します。  
  
## <a name="attribute-examples"></a>属性の例  
 次の例では、エンティティに Name、Code、Subcategory、StandardCost、ListPrice、および FilePhoto という属性があります。 これらの属性はメンバーを表します。 各メンバーは、属性値の 1 行で表されます。  
  
 ![自転車製品エンティティテーブル](../master-data-services/media/mds-conc-entity-table-w-data.gif "自転車製品エンティティテーブル")  
  
 次の例では、Product エンティティに次の属性が含まれます。  
  
-   自由形式属性 Name、Code、StandardCost、および ListPrice  
  
-   ドメイン ベースの属性 Subcategory  
  
-   ファイル属性 FilePhoto  
  
 Subcategory は、Product のドメイン ベースの属性として使用されるエンティティです。 Category は、Subcategory のドメイン ベースの属性として使用されるエンティティです。 Product エンティティと同様に、Category エンティティと Subcategory エンティティにはそれぞれ、既定の Name 属性と Code 属性が含まれています。  
  
 ![製品エンティティツリー構造](../master-data-services/media/mds-conc-entity-ui.gif "製品エンティティツリー構造")  
  
## <a name="related-tasks"></a>関連タスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|新しい自由形式のテキスト属性を作成する。|[テキスト属性を作成する (マスター データ サービス)](../master-data-services/create-a-text-attribute-master-data-services.md)|  
|新しい自由形式の数値属性を作成する。|[数値属性を作成する (マスター データ サービス)](../master-data-services/create-a-numeric-attribute-master-data-services.md)|  
|新しい自由形式のリンク属性を作成する。|[リンク属性を作成する (マスター データ サービス)](../master-data-services/create-a-link-attribute-master-data-services.md)|  
|新しいファイル属性を作成する。|[ファイル属性を作成する (マスター データ サービス)](../master-data-services/create-a-file-attribute-master-data-services.md)|  
|新しいドメインベース属性を作成する。|[ドメイン ベースの属性を作成する (マスター データ サービス)](../master-data-services/create-a-domain-based-attribute-master-data-services.md)|  
|既存の属性の名前を変更する。|[属性名とデータ型を変更する (マスター データ サービス)](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)|  
|変更の追跡グループに既存の属性を追加する。|[変更の追跡グループに属性を追加する (マスター データ サービス)](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)|  
|既存の属性を削除する。|[属性を削除する (マスター データ サービス)](../master-data-services/delete-an-attribute-master-data-services.md)|  
|属性の順序を変更する。|[属性の順序の変更](../master-data-services/change-the-order-of-attributes.md)|  
|日付属性を作成する|[日付属性を作成する (マスター データ サービス)](../master-data-services/create-a-date-attribute-master-data-services.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [ドメインベースの属性 (マスター データ サービス)](../master-data-services/domain-based-attributes-master-data-services.md)  
  
-   [属性グループ (マスター データ サービス)](../master-data-services/attribute-groups-master-data-services.md)  
  
-   [メンバー (マスター データ サービス)](../master-data-services/members-master-data-services.md)  
  
-   [リーフ権限 (マスター データ サービス)](../master-data-services/leaf-permissions-master-data-services.md)
  
