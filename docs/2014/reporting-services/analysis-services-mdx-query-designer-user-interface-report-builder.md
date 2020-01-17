---
title: Analysis Services MDX クエリデザイナーのユーザーインターフェイス (レポートビルダー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10012"
helpviewer_keywords:
- query designers, Analysis Services
ms.assetid: 7e288eee-2d37-485e-a6a0-dbba5e041e26
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b1d0a5738384a738c3e0882d16bbffb0f2a4d00a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891556"
---
# <a name="analysis-services-mdx-query-designer-user-interface-report-builder"></a>Analysis Services の MDX クエリ デザイナーのユーザー インターフェイス (レポート ビルダー)
  レポート ビルダーには、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データ ソースに対する多次元式 (MDX) クエリを作成するためのグラフィカル クエリ デザイナーが用意されています。 MDX のグラフィカル クエリ デザイナーには、デザイン モードとクエリ モードという 2 つのモードがあります。 どちらのモードにもメタデータ ペインが表示され、選択したキューブからメンバーをドラッグすることによって MDX クエリを作成できます。レポートの処理時には、このクエリに基づいてデータが取得されます。  
  
> [!IMPORTANT]  
>  ユーザーは、クエリを作成して実行する際にデータ ソースにアクセスします。 したがって、データ ソースに対する最小限の権限 (読み取り専用権限など) を付与する必要があります。  
  
 以下のセクションでは、グラフィカル クエリ デザイナーの各モードで表示される、ツール バーのボタンとクエリ デザイナーのペインについて説明します。  
  
## <a name="graphical-mdx-query-designer-in-design-mode"></a>グラフィカル MDX クエリ デザイナー (デザイン モード)  
 レポート データセットの MDX クエリを編集する場合、グラフィカル MDX クエリ デザイナーがデザイン モードで開きます。  
  
 次の図は、デザイン モードで表示される各ペインの名称を示しています。  
  
 ![Analysis Services MDX クエリ デザイナー、デザイン ビュー](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqd-dsawas-mdx-designmode.gif "Analysis Services MDX クエリ デザイナー、デザイン ビュー")  
  
 このモードのペインの一覧を次の表に示します。  
  
|ペイン|関数|  
|----------|--------------|  
|キューブの選択ボタン ( **[...]** )|現在選択されているキューブを表示します。|  
|メタデータ ペイン|選択されたキューブで定義されているメジャー、主要業績評価指標 (KPI)、およびディメンションの階層リストを表示します。|  
|計算されるメンバー ペイン|現在定義されている、クエリに使用することのできる計算されるメンバーを表示します。|  
|フィルター ペイン|ディメンションおよび関連する階層を選択することにより、ソースのデータをフィルター処理し、レポートに返されるデータを制限できます。|  
|データ ペイン|メタデータ ペインや計算されるメンバー ペインからアイテムをドラッグすると、結果セットの列見出しが表示されます。 **[自動実行]** ボタンが選択されている場合、結果セットは自動的に更新されます。 .|  
  
 データ ペインには、メタデータ ペインからディメンション、メジャー、KPI をドラッグしたり、計算されるメンバー ペインから計算されるメンバーをドラッグしたりできます。 フィルター ペインでは、ディメンションや関連する階層を選択し、フィルター式を設定することによって、クエリに利用可能なデータを制限できます。 **[自動実行]** (![クエリの自動実行](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-autoexecute.gif "クエリの自動実行")) 切り替えボタンがオンになっている場合、データ ペインにメタデータ オブジェクトをドロップするたびに、クエリが自動的に実行されます。 クエリを手動で実行するには、ツール バーの **[実行]** (![クエリの実行](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-run.gif "クエリの実行")) ボタンを使用します。  
  
 このモードで MDX クエリを作成すると、次のような追加のプロパティがクエリに自動的に追加されます。  
  
 **[メンバーのプロパティ]** MEMBER_CAPTION、MEMBER_UNIQUE_NAME  
  
 **[セルのプロパティ]** VALUE、BACK_COLOR、FORE_COLOR、FORMATTED_VALUE、FORMAT_STRING、FONT_NAME、FONT_SIZE、FONT_FLAGS  
  
 独自の追加プロパティを指定するには、クエリ モードで MDX クエリを手動で編集する必要があります。  
  
> [!NOTE]  
>  MDX の詳細および MDX クエリ デザイナーの一般的な情報については、 [SQL Server オンライン ブック](https://go.microsoft.com/fwlink/?linkid=98335)の「MDX クエリ エディター (Analysis Services - 多次元データ)」を参照してください。 ただし、レポートで MDX クエリからのデータを表示するには、レポート ビルダーに付属している MDX クエリ デザイナーを使用してクエリを作成する必要があります。 ファイルからの .mdx クエリのインポートはサポートされていません。  
  
### <a name="graphical-mdx-query-designer-toolbar-in-design-mode"></a>グラフィカル MDX クエリ デザイナーのツール バー (デザイン モード)  
 クエリ デザイナーのツール バーにある各種のボタンを使用すると、グラフィカル インターフェイスを使用して MDX クエリをデザインできます。 これらのボタンとその機能を次の表に示します。  
  
|ボタン|説明|  
|------------|-----------------|  
|**[テキストとして編集]**|このデータ ソースの種類では使用できません。|  
|**[インポート]**|ファイル システムのレポート定義 (.rdl) ファイルから既存のクエリをインポートします。|  
|![MDX クエリ ビューに変更](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-commandtypemdx.gif "MDX クエリのビューへの変更")|コマンドの種類を MDX に切り替えます。|  
|![結果データの更新](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-refresh.gif "結果データの更新")|データ ソースからメタデータを更新します。|  
|![Add calculated member](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-addcalculatedmember.gif "Add calculated member")|**[計算されるメンバー ビルダー]** ダイアログ ボックスを表示します。|  
|![空のセルの表示の切り替え](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-showemptycells.gif "空のセルの表示の切り替え")|データ ペインに空のセルを表示するかどうかを切り替えます。 これは、MDX で NON EMPTY 句を使用することに相当します。|  
|![クエリの自動実行](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-autoexecute.gif "クエリの自動実行")|クエリを自動的に実行し、変更が生じるたびに結果を表示します。 結果はデータ ペインに表示されます。|  
|![集計ボタンの表示](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-showaggregations.gif "集計ボタンの表示")|集計をデータ ペインに表示します。|  
|![[削除]](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-delete.gif "[削除]")|データ ペインで選択した列をクエリから削除します。|  
|![[クエリ パラメーター] ダイアログ ボックスのアイコン](https://docs.microsoft.com/analysis-services/analysis-services/media/iconqueryparameter.gif "[クエリ パラメーター] ダイアログ ボックスのアイコン")|**[クエリ パラメーター]** ダイアログ ボックスを表示します。 クエリ パラメーターの値を指定する場合、同じ名前のレポート パラメーターが自動的に作成されます。 クエリ パラメーターの値は、このレポート パラメーターを参照する式に設定されます。|  
|![[クエリの準備] ボタン](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-preparequery.gif "[クエリの準備] ボタン")|クエリを準備します。|  
|![クエリを実行する](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-run.gif "クエリを実行する")|クエリを実行し、結果をデータ ペインに表示します。|  
|![クエリを取り消す](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-cancel.gif "クエリを取り消す")|クエリを取り消します。|  
|![デザイン モードに切り替える](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-designmode.gif "デザイン モードに切り替える")|デザイン モードとクエリ モードを切り替えます。|  
  
## <a name="graphical-mdx-query-designer-in-query-mode"></a>グラフィカル MDX クエリ デザイナー (クエリ モード)  
 グラフィカル クエリ デザイナーを **クエリ** モードに変更するには、ツール バーの **[デザイン モード]** ボタンをクリックします。  
  
 次の図は、クエリ モードで表示される各ペインの名称を示しています。  
  
 ![Analysis Services MDX クエリ デザイナー、クエリ ビュー](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqd-dsawas-mdx-querymode.gif "Analysis Services MDX クエリ デザイナー、クエリ ビュー")  
  
 このモードのペインの一覧を次の表に示します。  
  
|ペイン|関数|  
|----------|--------------|  
|キューブの選択ボタン ( **[...]** )|現在選択されているキューブを表示します。|  
|メタデータ/関数/テンプレート ペイン|選択されたキューブで定義されているメジャー、KPI、およびディメンションの階層リストを表示します。|  
|クエリ ペイン|クエリ テキストを表示します。|  
|結果ペイン|クエリの実行結果を表示します。|  
  
 メタデータ ペインには、 **[メタデータ]** 、 **[関数]** 、 **[テンプレート]** の各タブが表示されます。 **[メタデータ]** タブからは、ディメンション、階層、KPI、およびメジャーを MDX クエリ ペインにドラッグできます。 **[関数]** タブからは、関数を MDX クエリ ペインにドラッグできます。 **[テンプレート]** タブからは、MDX テンプレートを MDX クエリ ペインに追加できます。 クエリを実行すると、結果ペインに MDX クエリの結果が表示されます。  
  
 デザイン モードで生成された既定の MDX クエリを拡張し、その他のメンバー プロパティおよびセル プロパティを追加できます。 このクエリを実行すると、その値は結果セットに表示されません。 ただし、値がデータセット フィールド コレクションと共に戻されるため、これらの値をレポートで使用できます。  
  
### <a name="graphical-query-designer-toolbar-in-query-mode"></a>グラフィカル クエリ デザイナーのツール バー (クエリ モード)  
 クエリ デザイナーのツール バーにある各種のボタンを使用すると、グラフィカル インターフェイスを使用して MDX クエリをデザインできます。  
  
 デザイン モードでもクエリ モードでも、表示されるツール バー ボタンは同じです。ただし、クエリ モードでは、次のボタンが無効になります。  
  
-   **[テキストとして編集]**  
  
-   **[計算されるメンバーの追加]** (![Add calculated member](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-addcalculatedmember.gif "Add calculated member"))  
  
-   **空のセルを表示する** (![空のセルの表示の切り替え](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-showemptycells.gif "空のセルの表示の切り替え"))  
  
-   **自動実行** (![クエリの自動実行](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-autoexecute.gif "クエリの自動実行"))  
  
-   **集計の表示** (![集計ボタンの表示](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-showaggregations.gif "集計ボタンの表示"))  
  
## <a name="see-also"></a>関連項目  
 [クエリ デザイナー &#40;レポート ビルダー&#41;](../../2014/reporting-services/query-designers-report-builder.md)  
  
  
