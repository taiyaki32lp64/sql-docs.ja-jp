---
title: リンク メジャー グループ |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- linked measure groups [Analysis Services]
- referencing measure groups
- Linked Measure Group Wizard
- measure groups [Analysis Services], linked
- linked dimensions [Analysis Services]
ms.assetid: 7f838452-8669-4194-8e15-7afdc7f15251
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ec38404a32751330d7fefd974fafe3d571d3b11b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074779"
---
# <a name="linked-measure-groups"></a>リンク メジャー グループ
  リンク メジャー グループは、同じデータベースまたは別の Analysis Services データベースにある別のキューブ内の別のメジャー グループに基づいています。 複数のキューブ内にある一連のメジャー、および対応するデータ値を再使用する場合は、リンク メジャー グループを使用することができます。  
  
 同じサーバー上で実行されるソリューションに、元のメジャー グループとリンク メジャー グループが存在することをお勧めします。 リモート サーバー上のメジャー グループへのリンクは、将来のリリースで廃止予定が (を参照してください[SQL Server 2014 で非推奨の Analysis Services 機能](../deprecated-analysis-services-features-in-sql-server-2014.md))。  
  
> [!IMPORTANT]  
>  リンク メジャー グループは読み取り専用です。 最新の変更内容を取得するには、すべてのリンク メジャー グループを削除し、変更後のソース オブジェクトに基づいてリンク メジャー グループを再作成する必要があります。 したがって、メジャー グループに対して今後変更を加える必要がある場合は、プロジェクト間でメジャー グループのコピーと貼り付けを行うことを、代わりのアプローチとして検討する必要があります。  
  
## <a name="usage-limitations"></a>使用法の制限  
 前に説明したように、リンク メジャーを使用する場合の重要な制約は、リンク メジャーを直接カスタマイズできないことです。 メジャー グループ自体の中にあるアイテムのデータ型、形式、データ バインド、可視性、およびメンバーシップに対する変更は、いずれも元のメジャー グループに加える必要のある変更です。  
  
 操作上、リンク メジャー グループは、クライアント アプリケーションからアクセスする場合はその他のメジャー グループとまったく同じであり、クエリもその他のメジャー グループと同様に行われます。  
  
 リンク メジャー グループを含むキューブでクエリを実行する場合、対象のキューブの最初の計算パスでリンクが確立され解決されます。 このため、リンク メジャー グループに格納されている計算は、クエリが評価されるまで解決できません。 つまり、計算されるメジャーと計算されるセルは、ソース キューブから継承されるのではなく、対象のキューブで再作成される必要があります。  
  
 使用法の制限を次に示します。  
  
-   リンク メジャー グループを別のリンク メジャー グループから作成することはできません。  
  
-   リンク メジャー グループ内のメジャーを追加または削除することはできません。 メンバーシップは、元のメジャー グループ内でのみ定義されます。  
  
-   リンク メジャー グループでは、書き戻しがサポートされていません。  
  
-   複数の多対多リレーションシップで、リンク メジャー グループを使用することはできません。特に、これらのリレーションシップが異なるキューブ内に存在する場合です。 このような方法で使用すると、あいまいな集計になります。 詳細については、「 [多対多リレーションシップを含むキューブでリンク メジャーの値が不適切](https://social.technet.microsoft.com/wiki/contents/articles/22911.incorrect-amounts-for-linked-measures-in-cubes-containing-many-to-many-relationships-ssas-troubleshooting.aspx)」を参照してください。  
  
 リンク メジャー グループに含まれるメジャーは、同一の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースから取得したリンク ディメンションに従ってのみ直接編成できます。 ただし、計算されるメンバーを使用すると、リンク メジャー グループから、キューブ内の他のリンクされていないディメンションに情報を関連付けることができます。 さらに、参照リレーションシップや多対多リレーションシップなどの間接リレーションシップを使用して、他のリンクされていないディメンションをリンク メジャー グループに関連付けることもできます。  
  
## <a name="create-or-modify-a-linked-measure"></a>リンク メジャーの作成または削除  
 リンク メジャー グループを作成するには、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] を使用します。  
  
1.  後続のキューブ内でリンク メジャー グループを後から再作成する必要が生じないように、この時点で、ソース キューブ内にある元のメジャー グループに対するすべての変更を最終的に確定します。 リンク オブジェクトの名前を変更することはできますが、他のどのプロパティも変更できません。  
  
2.  ソリューション エクスプローラーで、リンク メジャー グループを追加するキューブをダブルクリックします。 この手順により、キューブ デザイナーでキューブが開かれます。  
  
3.  キューブ デザイナーの [メジャー] ペインまたは [ディメンション] ペインで、どちらかのペインの任意の場所を右クリックし、 **[新しいリンク オブジェクト]** をクリックします。 この結果、リンク オブジェクト ウィザードが開始されます。  
  
4.  最初のページで、データ ソースを指定します。 この結果、元のメジャー グループの場所が確立されます。 既定値は、現在のデータベース内にある現在のキューブですが、別の Analysis Services データベースを選択することもできます。  
  
5.  次のページで、リンクするメジャー グループまたはディメンションを選択します。 メジャー グループなど、ディメンションとキューブ オブジェクトが個別に一覧表示されます。 現在のキューブ内にまだ存在していないオブジェクトのみが使用できます。  
  
6.  リンク オブジェクトを作成するには、 **[完了]** をクリックします。 [メジャー] ペインと [ディメンション] ペインで、リンク オブジェクトがリンク アイコン付きで表示されます。  
  
## <a name="secure-a-linked-measure"></a>リンク メジャーをセキュリティで保護  
 リンクが定義されると、リンク メジャー グループのメジャーへのアクセスは、他のメジャー グループへのアクセスと同じように管理されます。 リンク オブジェクトは、ロール デザイナー内で、リンクされていない対応オブジェクトの横に表示されます。 メジャー グループのセキュリティの管理の詳細については、「[キューブ権限またはモデル権限の付与 &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)」を参照してください。  
  
 リンク メジャー グループを定義または使用するには、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスの Windows サービス アカウントが、ソース [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスでソース キューブおよびメジャー グループに対する `ReadDefinition` アクセス権および `Read` アクセス権を持つ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース ロールに属しているか、またはソース [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Administrators ロールに属している必要があります。  
  
## <a name="see-also"></a>参照  
 [リンク ディメンションの定義](define-linked-dimensions.md)  
  
  
