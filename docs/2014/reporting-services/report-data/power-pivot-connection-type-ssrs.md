---
title: PowerPivot の接続の種類 (SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a104c3c7-f118-4d02-9a0f-6859f1469d11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e9b8fb98082fb3509acf50e6546673e86962893c
ms.sourcegitcommit: 381595e990f2294dbf324ef31071e2dd2318b8dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74200420"
---
# <a name="powerpivot-connection-type-ssrs"></a>PowerPivot の接続の種類 (SSRS)
  SQL Server Analysis Services データ処理拡張機能を使用すると、SharePoint の PowerPivot ギャラリーにパブリッシュされた PowerPivot ブックからデータを取得することができます。  
  
 このトピックの情報を使用して、データ ソースを構築してください。 詳細な手順については、「[データ接続またはデータソース &#40;レポートビルダーと SSRS&#41;の追加と検証](add-and-verify-a-data-connection-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="prerequisites"></a>前提条件  
 PowerPivot データ ソースは、SharePoint サイトの PowerPivot ギャラリーにパブリッシュされている必要があります。  
  
 レポート ビルダーから PowerPivot ブックへの接続をサポートするには、ワークステーション コンピューターに SQL Server 2008 R2 ADOMD.NET が必要です。 このクライアントライブラリは PowerPivot for Excel と共にインストールされますが、このアプリケーションがインストールされていないコンピューターを使用している場合は、 [SQL Server 2008 R2 Feature Pack](https://www.microsoft.com/download/details.aspx?id=16978)から ADOMD.NET をダウンロードしてインストールする必要があります。  
  
## <a name="data-source-type"></a>データ ソースの種類  
 使用するレポート データ ソースの種類は **Microsoft SQL Server Analysis Services**です。  
  
## <a name="connection-string"></a>接続文字列  
 接続文字列は、PowerPivot ギャラリーまたはその他のライブラリ (など) の SharePoint でパブリッシュされた PowerPivot http://contoso-srv/subsite/PowerPivotLibrary/ContosoSales.xlsxブックの URL です。  
  
## <a name="credentials"></a>資格情報  
 PowerPivot ブックおよび SharePoint サイトへのアクセスに必要な資格情報を指定します (Windows 認証 (統合セキュリティ) など)。 詳細については、「 [Reporting Services のデータ接続、データソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)」または「[レポートビルダーで資格情報を指定する](../specify-credentials-in-report-builder.md)」を参照してください。  
  
## <a name="queries"></a>クエリ  
 PowerPivot データ ソースに接続した後、MDX グラフィカル クエリを使用して、基となるデータ構造を参照および選択してクエリを作成します。 クエリを作成したら、それを実行して結果ペインにサンプル データを表示します。  
  
 クエリ デザイナーにより、クエリを分析してデータセット フィールドが決定されます。 また、 **レポート データ** ペインでデータセット フィールド コレクションを手動で編集することもできます。 詳細については、「[レポート データ ペインでのフィールドの追加、編集、更新 &#40;レポート ビルダーおよび SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="filters"></a>フィルター  
 フィルター ペインで、クエリ結果から除外するか、クエリ結果に追加するディメンションおよびメンバーを指定します。  
  
## <a name="parameters"></a>パラメーター  
 フィルター ペインで、フィルターの **[パラメーター]** オプションを選択して、フィルターの選択に対応する使用可能な値を持つレポート パラメーターが自動的に作成されるようにします。  
  
## <a name="remarks"></a>コメント  
 PowerPivot ギャラリーの PowerPivot ブックからレポート ビルダーを開いた場合、PowerPivot ブックのピボットテーブル、ピボットグラフ、スライサー、およびその他のレイアウト機能や分析機能は、レポートで再作成されません。 代わりに、PowerPivot ブック内のデータを参照する、あらかじめ構成されたデータ ソースが空のレポートに含まれます。 PowerPivot ブックに基づくレポートをデザインする場合、レポートで再作成するスライサー、フィルター、およびテーブルやグラフの数によっては、手間と時間がかかることがあります。 そのため、レポートでのデータの表示方法については、PowerPivot のデザインとは切り離して考えることをお勧めします。  
  
 PowerPivot ブック内のデータは大幅に圧縮されていますが、PowerPivot ブックから取得されたレポートのデータは圧縮されません。 クエリ デザイナーを使用してフィルターとパラメーターを指定し、レポートに必要なデータだけに制限します。  
  
 Analysis Services キューブへの接続とは異なり、PowerPivot モデルには階層はありません。 ブック内の関連するスライサーに同様の機能を提供するには、レポートでカスケード型パラメーターを作成する必要があります。 詳細については、「 [カスケード型パラメーターのレポートへの追加 (レポート ビルダーおよび SSRS)](../report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)で作成するモバイル レポートで使用できます。  
  
 PowerPivot モデルの基になるデータ値に対応するように、式を調整しなければならない場合があります。 式を変更してデータを適切なデータ型に変換したり、集計関数を追加または削除したりすることが必要になります。 たとえば、データ型を文字列型から整数型に変換するには、 `=CInt`を使用します。 レポートをパブリッシュする前に、PowerPivot モデルのデータから意図した値が表示されることを必ず確認してください。  
  
 PowerPivot ギャラリーのレポートのプレビュー イメージは、以下の条件を満たしている場合にのみ生成されます。  
  
-   データを提供するレポートおよび PowerPivot ブックは、同じ PowerPivot ギャラリーに一緒に保存する必要があります。  
  
-   レポートには、PowerPivot データ ソースからの PowerPivot データのみが格納されます。  
  
## <a name="see-also"></a>参照  
 [Analysis Services MDX クエリデザイナーのユーザーインターフェイス &#40;レポートビルダー&#41;](../analysis-services-mdx-query-designer-user-interface-report-builder.md)   
 [式 &#40;レポートビルダーと SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
