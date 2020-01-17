---
title: リレーショナル クエリ デザイナーでのクエリの作成 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 28b25861-f3b4-4c3e-a9b0-03d6e4cfea26
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 901abf5be70f0b3c70b89b0415c59f19a9327b29
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107434"
---
# <a name="build-a-query-in-the-relational-query-designer-report-builder-and-ssrs"></a>リレーショナル クエリ デザイナーでのクエリの作成 (レポート ビルダーおよび SSRS)
  クエリ デザイナーでは、レポート データセットの外部データ ソースから取得するデータを指定できます。 クエリ デザイナーは、ウィザードでクエリを構築するときや、データセット クエリを作成するときに使用します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 データセットはデータ ソースに基づきます。 データセット クエリを定義するときに開くクエリ デザイナーは、データ ソースの種類と作成環境によって決まります。 クエリ デザイナーの機能は、基になるデータ ソースによって異なります。 データ層の詳細については、次を参照してください[データ接続、データ ソース、およびレポート ビルダーでの接続文字列](../data-connections-data-sources-and-connection-strings-in-report-builder.md)または[データ接続、データ ソース、および Reporting Services の接続文字列](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 クエリ デザイナーでは、次のタスクを実行できます。  
  
-   外部データ ソースの複数のスキーマについてメタデータを検索する  
  
-   データセット用に取得するフィールドを指定する  
  
-   テーブルなどの 2 つのオブジェクト間のリレーションシップを指定する  
  
-   レポート データとして取得する前にデータを制限するフィルターを指定する  
  
-   パラメーターを作成するかどうかを指定する  
  
-   外部データ ソースに対して計算を実行する集計を指定する  
  
 クエリ デザイナーを開いた後、埋め込みデータセットと共有データセットのどちらについても、同じ方法でクエリを作成します。 次の手順では、埋め込みデータセット クエリを使用します。  
  
 詳細については、「[リレーショナル クエリ デザイナーのユーザー インターフェイス &#40;レポート ビルダー&#41;](relational-query-designer-user-interface-report-builder.md)」を参照してください。  
  
### <a name="to-build-a-query-for-an-embedded-dataset-in-report-design-view"></a>レポート デザイン ビューで埋め込みデータセットに対するクエリを作成するには  
  
1.  クエリ デザイナーを開きます。 レポート データ ペインでデータセットを右クリックし、 **[クエリ]** をクリックします。  
  
     データ ソースに関連付けられているクエリ デザイナーが開きます。  
  
2.  データベース ビュー ペインで、テーブル、ビュー、ストアド プロシージャなどのデータベース スキーマ オブジェクトの階層ビューを表示するフォルダーを展開します。 選択ボックスをクリックしてオブジェクトのすべてのフィールドを選択するか、ノードを展開して個々のフィールドを選択します。  
  
     データベース ビュー ペインでフィールドを選択すると、 **[フィールドの選択]** ペインに選択内容が表示されます。  
  
     複数の関連するデータベース テーブルからフィールドを選択する場合に、データベース スキーマから検出されたテーブルのリレーションシップを表示するには、リレーションシップ ペインを使用します。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     データセット フィールドの一覧がレポート データ ペインに表示されます。  
  
### <a name="to-specify-limits-for-a-query"></a>クエリに対する制限を指定するには  
  
1.  リレーショナル クエリ デザイナーで、フィールドを選択しており、それらのフィールドが **[選択されたフィールド]** ペインに表示されることを確認します。  
  
2.  適用されたフィルター ペインのツール バーで、 **[フィルターの追加]** をクリックします。 新しいフィルター行が表示されます。  
  
3.  **[フィールド名]** で、クリックしてフィールドのドロップダウン リストを表示し、フィルター処理の基準にするフィールドの名前をクリックします。 たとえば、数量を基準にフィルター処理を行うには、アイテムの数を格納するフィールドをクリックします。  
  
4.  **[演算子]** で、クリックして演算子のドロップダウン リストを表示し、フィルターで使用する比較演算子を選択します。  
  
5.  **[値]** に、フィルター処理の基準にする値を入力します。 たとえば、100 よりも大きい数量をフィルター処理の対象とするには、「100」と入力します。  
  
6.  ユーザーがフィルター値を指定できるようにデータセット パラメーターを作成する場合は、この行のパラメーター オプションを選択します。 データセット パラメーターに対応するレポート パラメーターが自動的に生成されます。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 データセット フィールドの一覧がレポート データ ペインに表示されます。  
  
### <a name="to-view-a-query-result-set"></a>クエリの結果セットを表示するには  
  
1.  クエリ デザイナーのツール バーで、 **[クエリの実行]\(!)** をクリックします。  
  
    > [!NOTE]  
    >  クエリ デザイナーでは、デザイン時の資格情報を使用してクエリを実行し、結果セットを取得します。 詳細については、「 [レポート ビルダーでの資格情報の指定](../specify-credentials-in-report-builder.md)」を参照してください。  
  
 データ ソースに対してクエリが実行され、サンプル データがクエリ結果ペインに表示されます。  
  
## <a name="see-also"></a>関連項目  
 [レポートにデータを追加&#40;レポート ビルダーおよび SSRS&#41;](report-datasets-ssrs.md)   
 [外部データ ソースのデータを追加する &#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md)   
 [クエリ デザイナー &#40;レポート ビルダー&#41;](../query-designers-report-builder.md)   
 [共有データセットまたは埋め込みデータセットの作成 &#40;レポート ビルダーおよび SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [レポート デザイン ビュー (レポート ビルダー)](../report-builder/report-design-view-report-builder.md)   
 [共有データセット デザイン ビュー (レポート ビルダー)](../report-builder/shared-dataset-design-view-report-builder.md)   
 [Reporting Services クエリ デザイナー](../reporting-services-query-designers.md)  
  
  
