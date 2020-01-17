---
title: 組み込み Globals および Users 参照 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 5f5e1149-c967-454d-9a63-18ec4a33d985
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3b39bf6a3a7c04d5d8ca457bb199229fdaebae76
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581845"
---
# <a name="built-in-collections---built-in-globals-and-users-references-report-builder"></a>組み込みコレクション - 組み込み Globals および Users 参照 (レポート ビルダー)
  組み込みフィールドのコレクションには、レポートの処理時に Reporting Services によって提供されるグローバルな値を表す **Globals** コレクションと **User** コレクションの両方が含まれています。 **Globals** コレクションでは、レポート名、レポート処理の開始時刻、レポート ヘッダーまたはレポート フッターの現在のページ番号などの値が提供されます。 **User** コレクションでは、ユーザー ID と言語設定が提供されます。 これらの値は、レポート内の結果をフィルター処理する際に式で使用できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-the-globals-collection"></a>Globals コレクションの使用  
 **Globals** コレクションには、レポートのグローバル変数が保持されます。 デザイン画面では、これらの変数は、`[&ReportName]` など、先頭に & (アンパサンド) が付いた状態で表示されます。 次の表では、 **Globals** コレクションのメンバーについて説明します。  
  
|**メンバー**|**型**|**[説明]**|  
|----------------|--------------|---------------------|  
|ExecutionTime|**DateTime**|レポートの実行を開始した日付と時刻です。|  
|PageNumber|**Integer**|ページ番号をリセットした改ページを基準とする現在のページ番号です。 レポート処理の開始時、初期値は 1 に設定されています。 ページ番号は、表示されるページごとに増えます。<br /><br /> 四角形、データ領域、データ領域グループ、マップの改ページ内でページ番号を付けるには、PageBreak プロパティで、ResetPageNumber プロパティを **True**に設定します。 Tablix 列階層グループではサポートされていません。<br /><br /> PageNumber は、ページ ヘッダーまたはページ フッターの式でのみ使用できます。|  
|ReportFolder|**String**|レポートを含んでいるフォルダーへの完全なパスです。 これには、レポート サーバーの URL は含まれません。|  
|ReportName|**String**|レポート サーバー データベースに格納されているとおりのレポートの名前です。|  
|ReportServerUrl|**String**|レポートが実行されるレポート サーバーの URL です。|  
|TotalPages|**Integer**|PageNumber をリセットした改ページを基準とする合計ページ数です。 改ページを設定しない場合、この値は OverallTotalPages と同じです。<br /><br /> TotalPages は、ページ ヘッダーまたはページ フッターの式でのみ使用できます。|  
|PageName|**String**|ページの名前です。 レポート処理の開始時、初期値はレポート プロパティの InitialPageName から設定されます。 各レポート アイテムが処理されると、この値は四角形、データ領域、データ領域グループ、またはマップの PageName の対応する値に置き換えられます。 Tablix 列階層グループではサポートされていません。<br /><br /> PageName は、ページ ヘッダーまたはページ フッターの式でのみ使用できます。|  
|OverallPageNumber|**Integer**|レポート全体に対する現在のページのページ番号です。 この値は ResetPageNumber の影響を受けません。<br /><br /> OverallPageNumber は、ページ ヘッダーまたはページ フッターの式でのみ使用できます。|  
|OverallTotalPages|**Integer**|レポート全体の合計ページ数です。 この値は ResetPageNumber の影響を受けません。<br /><br /> OverallTotalPages は、ページ ヘッダーまたはページ フッターの式でのみ使用できます。|  
|RenderFormat|**RenderFormat**|現在の表示要求に関する情報です。<br /><br /> 詳細については、次のセクションの「RenderFormat」を参照してください。|  
  
 **Globals** コレクションのメンバーからは、Variant 値が返されます。 特定のデータ型を必要とする、このコレクションのメンバーを式で使用する場合は、先に変数をキャストする必要があります。 たとえば、バリアント型の実行時間を Date 形式に変換するには、 `=CDate(Globals!ExecutionTime)`を使用します。 詳細については、「 [式で使用されるデータ型 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)など、先頭に &amp; (アンパサンド) が付いた状態で表示されます。  
  
### <a name="renderformat"></a>RenderFormat  
 次の表では、 **RenderFormat**のメンバーについて説明します。  
  
|メンバー|型|[説明]|  
|------------|----------|-----------------|  
|[オブジェクト名]|**String**|RSReportServer 構成ファイルに登録されているレンダラーの名前です。<br /><br /> レポート処理または表示サイクルの特定の部分で使用できます。|  
|IsInteractive|**ブール値**|現在の表示要求で対話型の表示形式を使用するかどうかを示します。|  
|DeviceInfo|読み取り専用の名前/値のコレクションです。|現在の表示要求の deviceinfo パラメーターのキーと値のペアです。<br /><br /> キーまたはインデックスを使用して、コレクションに文字列値を指定できます。|  
  
### <a name="examples"></a>使用例  
 **Globals** コレクションへの参照を式で使用する方法を次の例に示します。  
  
-   レポートのフッター内のテキスト ボックスで次の式を使用すると、ページ番号およびレポートの総ページ数が返されます。  
  
     `=Globals.PageNumber & " of " & Globals.TotalPages`  
  
-   次の式は、レポート名およびレポートが実行された時間を返します。 時間の書式は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の短い日付用の書式設定の文字列を使用して設定されます。  
  
     `=Globals.ReportName & ", dated " & Format(Globals.ExecutionTime, "d")`  
  
-   選択した列の **[列表示]** ダイアログ ボックスで次の式を使用すると、レポートが Excel にエクスポートされているときにのみ列が表示されます。 それ以外の場合、列は非表示になります。  
  
     `EXCELOPENXML` は、Office 2007 に含まれる Excel 形式を参照します。 `EXCEL` は、Office 2003 に含まれる Excel 形式を参照します。  
  
     `=IIF(Globals!RenderFormat.Name = "EXCELOPENXML" OR Globals!RenderFormat.Name = "EXCEL", false, true)`  
  
## <a name="using-the-user-collection"></a>User コレクションの使用  
 **User** コレクションには、レポートを実行しているユーザーのデータが保持されます。 このコレクションを使用すると、現在のユーザーのデータのみを表示するなど、レポートに表示されるデータをフィルター選択することも、レポート タイトルなどに UserID を表示することもできます。 デザイン画面では、これらの変数は、`[&UserID]` など、先頭に & (アンパサンド) が付いた状態で表示されます。  
  
 次の表では、 **User** コレクションのメンバーについて説明します。  
  
|**メンバー**|**型**|**[説明]**|  
|----------------|--------------|---------------------|  
|**言語**|**文字列**|レポートを実行しているユーザーの言語です。 たとえば、 `en-US`のようにします。|  
|**UserID**|**String**|レポートを実行しているユーザーの ID です。 Windows 認証を使用している場合、この値は現在のユーザーのドメイン アカウントです。 値は、Windows 認証またはカスタム認証を使用できる [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] セキュリティ拡張機能によって決まります。|  
 
### <a name="using-locale-settings"></a>ロケール設定の使用  
 式を使用し、 **User.Language** 値でクライアント コンピューターのロケール設定を参照して、ユーザーに対してどのようにレポートを表示するかを指定できます。 たとえば、ロケール値に基づいて異なるクエリ式を使用するレポートを作成できます。 クエリは、返された言語に応じて異なる列からローカライズされた情報を取得するように変更できます。 また、この変数を基にしてレポートまたはレポート アイテムの言語設定に式を使用することもできます。  
  
> [!NOTE]  
>  レポートの言語設定は変更できますが、言語設定の変更により、表示に関する問題が発生する可能性があることに注意してください。 たとえば、レポートのロケール設定を変更すると、レポートの日付の書式が変更されますが、通貨の書式も変更される可能性があります。 通貨用の変換処理が行われない場合は、これによりレポートに不適切な通貨記号が表示される可能性があります。 これを回避するには、変更する各アイテムに関する言語情報を設定するか、通貨データを含むアイテムに特定の言語を設定します。  
  
### <a name="identifying-userid-for-snapshot-or-history-reports"></a>スナップショット レポートまたは履歴レポートの UserID の識別  
 場合によっては、 *User!UserID* 変数を含むレポートは、レポートを参照している現在のユーザー固有のレポート データを表示することができません。  
  
## <a name="see-also"></a>参照  
 [式 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [[式] ダイアログ ボックス (レポート ビルダー)](https://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)   
 [式で使用されるデータ型 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [数値と日付の書式設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
