---
title: リンク ディメンションの定義 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], linked
- linked dimensions [Analysis Services]
ms.assetid: d5ad5eae-5dde-46a6-91c3-c8766d016dec
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca4b3c0b2f2a6c63e62a44499d6e33e651ca9bae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075577"
---
# <a name="define-linked-dimensions"></a>リンク ディメンションの定義
  リンク ディメンションは、バージョンと互換性レベルが同じである別の Analysis Services データベース内で作成および保存されたディメンションに基づいています。 リンク ディメンションを使用すると、1 つのデータベースでディメンションを作成、保存、保守することができ、さらにそのディメンションを複数のデータベースで使用可能にすることができます。 ユーザーに対しては、リンク ディメンションは他のディメンションと同様に表示されます。  
  
 リンク ディメンションは読み取り専用です。 ディメンションを変更するか、新しいリレーションシップを作成するには、ソース ディメンションを変更し、次にリンク ディメンションとそのリレーションシップを削除して再作成する必要があります。 ソース オブジェクトから変更を取得する目的で、リンク ディメンションを更新することはできません。  
  
 関連するすべてのメジャー グループおよびディメンションは同じソース データベースから取得する必要があります。 キューブに追加したローカル メジャー グループとリンク ディメンションの間で新しいリレーションシップを作成することはできません。 リンク ディメンションおよびメジャー グループを現在のキューブに追加した後、両者間のリレーションシップがソース データベース内で維持される必要があります。  
  
> [!NOTE]  
>  更新機能が利用できないため、ほとんどの Analysis Services 開発者は、ディメンションをリンクする代わりにディメンションをコピーします。 同じソリューション内にある複数のプロジェクトに対してソリューションをコピーできます。 詳細については、「 [SSAS 内でのリンク ディメンションの更新](http://sqlblog.com/blogs/marco_russo/archive/2006/09/12/refresh-of-a-linked-dimension-in-ssas.aspx)」をご覧ください。  
  
## <a name="prerequisites"></a>前提条件  
 ディメンションを提供するソース データベースとそれを使用する現在のデータベースは、同じバージョンと互換性レベルとする必要があります。 詳細については、次を参照してください。[多次元データベースの互換性レベル設定&#40;Analysis Services&#41;](compatibility-level-of-a-multidimensional-database-analysis-services.md)します。  
  
 ソース データベースを配置してオンラインにする必要があります。 リンク オブジェクトをパブリッシュまたは使用するサーバーは、操作ができるように構成する必要があります (以下の説明を参照)。  
  
 使用するディメンション自体をリンク ディメンションにすることはできません。  
  
## <a name="configure-server-to-allow-linked-objects"></a>リンク オブジェクトを許可するサーバーの構成  
  
1.  SQL Server Management Studio で Analysis Services サーバーに接続します。 オブジェクト エクスプローラーでサーバー名を右クリックし、 **[ファセット]** をクリックします。  
  
2.  **LinkedObjectsLinksFromOtherInstancesEnabled** を **True** に設定し、他のインスタンスで実行されるデータベース内に格納されたリンク オブジェクトに対してサーバーで要求を発行できるようにします。  
  
3.  **LinkedObjectsLinksToOtherInstances** を **True** に設定し、他のインスタンスで実行されるデータベースのリンク オブジェクトに対してサーバーでデータを要求できるようにします。  
  
## <a name="create-a-linked-dimension-in-sql-server-data-tools"></a>SQL Server データ ツールでリンク ディメンションを作成するには  
  
1.  ウィザードを開始します。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、 **データベースまたはプロジェクトの** [ディメンション] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] フォルダーを右クリックし、 **[新しいリンク ディメンション]** をクリックします。  
  
2.  ディメンションを提供する Analysis Services データベースに接続します。 リンク オブジェクト ウィザードの **[データ ソースの選択]** ページで [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ ソースを選択するか、新しいデータ ソースを作成します。  
  
3.  ウィザードの **[オブジェクトの選択]** ページで、リモート データベース内でリンクするディメンションを選択します。  
  
4.  **[ウィザードの完了]** ページで、リンク オブジェクトをプレビューできます。 既に存在するディメンションと同じ名前のディメンションにリンクした場合は、序数 (最初の重複名の "1" から始まる数) が名前に追加されます。 ウィザードを完了すると、ディメンションが **[ディメンション]** フォルダーに追加されます。  
  
##  <a name="bkmk_CreateNew"></a> Analysis Services データベースへの新しいデータ ソース接続の作成  
 新しいデータ ソース ウィザードを使用して、ディメンションを提供する Analysis Services データベースに関するプロジェクト接続情報を追加します。 リンク オブジェクト ウィザードの [データ ソースの選択] ページにある **[新しいデータ ソース]** をクリックしてウィザードを起動できます。  
  
1.  データ ソース ウィザードの [接続の定義方法を選択します] ページで **[新規作成]** をクリックします。  
  
2.  接続マネージャーで、プロバイダーが **[ネイティブ OLE DB\Microsoft OLE DB Provider for Analysis Services 11.0]** に設定されていることを確認します。  
  
3.  サーバーの名前を入力します (使用*servername*\\*instancename*名前付きインスタンス)<sup>1</sup>または型**localhost**に同じコンピューターで実行されている Analysis Services サーバーに接続します。  
  
4.  接続には Windows 認証を使用します。  
  
5.  **[初期カタログ]** の下矢印をクリックしてこのサーバーのデータベースを選択します。  
  
6.  データ ソース ウィザードで **[次へ]** をクリックして次に進みます。  
  
7.  [権限借用情報] ページで、 **[サービス アカウントを使用する]** をクリックします。 **[次へ]** をクリックし、ウィザードを終了します。 リンク オブジェクト ウィザードでは、ここで定義した接続が選択されます。  
  
## <a name="next-steps"></a>次の手順  
 リンク ディメンションの構造は変更できないので、ディメンション デザイナーの **[ディメンション構造]** タブではリンク ディメンションの構造を表示できません。 リンク ディメンションの処理後に、 **[ブラウザー]** タブで表示できます。また、名前の変更や名前の翻訳の作成を行うことができます。  
  
## <a name="see-also"></a>参照  
 [互換性レベルの多次元データベースの設定&#40;Analysis Services&#41;](compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [リンク メジャー グループ](linked-measure-groups.md)   
 [ディメンション リレーションシップ](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)  
  
  
