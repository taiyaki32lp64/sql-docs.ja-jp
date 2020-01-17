---
title: 共有データセット デザイン ビュー (レポート ビルダー) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 47c502da-d163-45d9-bf04-0849e5ba7929
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1589f171fd8d402572408186a10b3e6f4ac97982
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107584"
---
# <a name="shared-dataset-design-view-report-builder"></a>共有データセット デザイン ビュー (レポート ビルダー)
  共有データセット デザイン ウィンドウは、他のユーザーと共有できるデータセット クエリの作成に役立ちます。 このウィンドウで、共有データ ソースの選択、共有データセットのプロパティの指定、およびクエリ デザイナーによるクエリの作成を行います。  
  
 ![rs_SharedDatasetDesignMode](../media/rs-shareddatasetdesignmode.gif "rs_SharedDatasetDesignMode")  
  
 レポート内のデータの使用方法の詳細については、次を参照してください。[レポートへのデータの追加&#40;レポート ビルダーおよび SSRS&#41;](../report-data/report-datasets-ssrs.md)します。  
  
##  <a name="Ribbon"></a> リボン  
 リボンを使用すると、タスクの実行に必要なコマンドを簡単に見つけることができます。 コマンドは、接続、データセット、およびクエリ デザイナーの各論理グループに分類されています。  
  
### <a name="connection"></a>接続  
 レポートで共有データ ソースを選択するか、レポート サーバーで共有データ ソースを参照するには、接続グループの **[選択]** ボタンを使用します。  
  
> [!NOTE]  
>  共有データセットは共有データ ソースに基づく必要があります。 必要なデータ ソースを使用できない場合は、レポート サーバー上にデータ ソースを作成する必要があります。 詳細については、次を参照してください。[作成、削除、または共有データ ソースを変更&#40;レポート マネージャー&#41; ](../create-delete-or-modify-a-shared-data-source-report-manager.md)の Reporting Services のドキュメントで[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][オンライン ブックの「](https://go.microsoft.com/fwlink/?linkid=121312)します。  
  
 詳細については、「 [データ接続、データ ソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-report-builder.md)」を参照してください。  
  
### <a name="dataset"></a>データセット  
 共有データセット プロパティを設定するには、 **[オプションの設定]** ボタンを使用します。 その一部を次に示します。  
  
-   フィールド。 フィールド コレクションのフィールドを追加または編集できます。  
  
-   データ オプション。 大文字と小文字の区別や照合順序など、一致条件や並べ替え順序に影響を与えるオプションを設定できます。  
  
-   フィルター。 接続してデータを取得した後にレポート内のデータを制限するフィルターを定義できます。  
  
-   パラメーター。 パラメーターを追加したり、パラメーター オプションを編集したりできます。 たとえば、各パラメーターに既定値を指定すると、レポート サーバー上にこの共有データセットのキャッシュ更新計画を作成できます。  
  
 設定した値は、レポート サーバー上で共有データセット定義の一部となります。 レポート作成者がこの共有データセットをレポートに含めると、指定したオプションがそのデータセット インスタンスに適用されます。  
  
 共有データセットをレポートに追加した後に、レポート作成者がオーバーライドできるオプションは、照合順序、大文字と小文字の区別、アクセントの区別、かなの区別、文字幅の区別、および小計です。 追加のデータセット フィルターを作成して、レポート内のデータを制限することもできます。  
  
 詳細については、「 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)と呼ばれます。  
  
 キャッシュ更新計画の詳細については、次を参照してください。[共有データセットのキャッシュ&#40;SSRS&#41; ](../report-server/cache-shared-datasets-ssrs.md)の Reporting Services のドキュメントで[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][オンライン ブックの「](https://go.microsoft.com/fwlink/?linkid=121312)します。  
  
### <a name="query-designer"></a>[クエリ デザイナー]  
 クエリ デザイナー ツール バーを使用すると、データ接続から取得するデータを指定するクエリを作成できます。 データ接続のデータ ソースの種類に関連付けられているクエリ デザイナーによって、表示されるツール バーが異なります。  
  
 詳細については、データ ソースの種類に対応するトピックを参照してください[外部データ ソースからのデータの追加&#40;SSRS&#41; ](../report-data/add-data-from-external-data-sources-ssrs.md)と[クエリ デザイナー&#40;レポート ビルダー&#41; ](../query-designers-report-builder.md) .  
  

  
##  <a name="DesignSurface"></a> クエリ デザイナー画面  
 クエリ デザイナーを使用すると、外部データ ソースに対して必要な構文でクエリを作成できます。  
  
 一部のデータ ソースの種類ではグラフィカル クエリ デザイナーが提供されます。グラフィカル クエリ デザイナーを使用すると、外部データ ソースのメタデータを検索できます。 メタデータ ペインからクエリ デザイン画面に名前を対話的にドラッグすることも、使用する名前を対話的に選択することもできます。  
  
 一部のデータ ソースの種類では、テキスト ベースのクエリ デザイナーがサポートされています。テキスト ベースのクエリ デザイナーを使用すると、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]などの他のツールで作成したクエリを貼り付けることができます。  
  
 外部データ ソースに対して使用できるクエリに関しては、データ ソースの種類ごとに特定の要件があります。 詳細については、データ ソースの種類に対応するトピックを参照してください[外部データ ソースからのデータの追加&#40;SSRS&#41; ](../report-data/add-data-from-external-data-sources-ssrs.md)と[Reporting Services でサポートされるデータ ソース&#40;SSRS&#41; 。](../create-deploy-and-manage-mobile-and-paginated-reports.md)の Reporting Services のドキュメントで[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][オンライン ブックの「](https://go.microsoft.com/fwlink/?linkid=121312)します。  
  

  
##  <a name="Results"></a> クエリ結果の表示  
 レポートの処理時には、共有データセット デザイン ビューで作成したクエリに基づいて、データ接続からデータが取得されます。  
  
 クエリを実行してデータ接続からサンプル データを表示し、期待した種類のデータが返されることを確認します。 結果セットの列は、データ接続のデータ スキーマのメタデータに基づいています。 列名がデータセット フィールド コレクションになります。 クエリの結果セットに示されるデータ値は、デザイン時のデータです。 共有データセットを共有データセット定義としてレポート サーバーに保存した後は、クエリ テキストのみが保存されます。 クエリの結果セットのデータは保存されません。  
  
 レポート作成者がこの共有データセットをレポートに追加すると、レポート サーバー上のデータセット定義を指すポインターが追加されます。 レポートのレポート データ ペインには、データセット フィールド コレクションが表示されます。 クエリ テキストは使用できません。  
  
 クエリの実行に使用する資格情報は、レポートのプレビューやレポート サーバーからのレポートの実行に使用される資格情報とは異なります。 詳細については、「 [レポート ビルダーでの資格情報の指定](../specify-credentials-in-report-builder.md)」を参照してください。  
  
### <a name="running-a-report-with-parameters"></a>パラメーターを指定したレポートの実行  
 クエリにクエリ変数が含まれている場合、データセット パラメーターが自動的に作成されます。 また、データセット クエリの作成完了時には、データセット パラメーターに設定されるレポート パラメーターが自動的に作成されます。  
  
 レポートにパラメーターが含まれている場合は、すべてのパラメーターに既定値があるときにのみレポートを自動的に実行できます。 パラメーターに既定値がない場合にレポートを実行するときは、パラメーターの値を選択してから、 **[実行]** タブの **[レポートの表示]** をクリックする必要があります。  
  
 詳細については、「 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../report-design/report-parameters-report-builder-and-report-designer.md)」を参照してください。  
  

  
##  <a name="Save"></a> 共有データセットの保存  
 作成したクエリを保存するには、 **レポート ビルダー** のボタンの **[保存]** または **[名前を付けて保存]** をクリックします。 レポート サーバー上の適切なフォルダーに移動し、共有データセット定義を保存します。 レポート サーバーに保存しないと、共有データセットを他のユーザーが使用することはできません。  
  

  
## <a name="see-also"></a>参照  
 [レポートにデータを追加&#40;レポート ビルダーおよび SSRS&#41;](../report-data/report-datasets-ssrs.md)   
 [データのフィルター、グループ化、および並べ替え &#40;レポート ビルダーおよび SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../report-design/report-parameters-report-builder-and-report-designer.md)  
  
  
