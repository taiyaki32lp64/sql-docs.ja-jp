---
title: サポートされる Access レポート機能 (SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], Access reports
- functions [Reporting Services]
- controls [Reporting Services]
- Access reports [Reporting Services]
- properties [Reporting Services], Access reports
- importing reports
- modules [Reporting Services]
ms.assetid: 7ffec331-6365-4c13-8e58-b77a48cffb44
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9088ab3e90b4fb341cc8125e45d498783953039d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100576"
---
# <a name="supported-access-report-features-ssrs"></a>サポートされる Access レポート機能 (SSRS)
  レポート デザイナーにレポートをインポートすると、インポート処理の際に、[!INCLUDE[msCoName](../includes/msconame-md.md)] Access のレポートは、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のレポート定義言語 (RDL) ファイルに変換されます。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] は Access のいくつかの機能をサポートしていますが、Access と [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] の相違のため、アイテムの中には、若干変更されるものや、まったくサポートされないものがあります。 このトピックでは、Access のレポート機能を RDL に変換する方法を説明します。  
  
## <a name="importing-access-reports"></a>Access レポートのインポート  
 一部のクエリには、Access 固有のコードが含まれています。 Access のコードがレポートと一緒にインポートされることはありません。 また、クエリに埋め込み文字列が含まれている場合、レポートは正しくインポートされません。 これを修正するには、文字列を文字コードに置き換えます。 たとえば、コンマ (,) 文字を CHAR(34) に置き換えます。  
  
 インポート プロセスがセミコロン (;) を正しく渡していないや XML マークアップ文字 (\<、> など) で接続文字列情報。 接続文字列にセミコロンや XML マークアップ文字が含まれている場合は、レポートのインポート後に、新しいレポートでパスワードを手動で設定する必要があります。  
  
 インポート処理では、接続文字列に含まれる接続設定や全般的なタイムアウト設定がインポートされません。 レポートをインポートした後、これらの設定の調整が必要になる場合があります。  
  
 インポートするレポートにクエリ パラメーターを含むクエリがある場合、このクエリはレポートのインポート時に変換されません。 レポートと一緒にクエリをインポートするには、Access レポート内のクエリ パラメーターをハードコードされた値に一時的に置き換え、レポートのインポート後にこれらのハードコード値をクエリ パラメーターに置き換えます。  
  
## <a name="page-layout"></a>ページ レイアウト  
 Access のページ レイアウトは [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のページ レイアウトと異なっています。 Access では、"集合" 単位でアイテムがページ上に配置されます。つまり、各セクションはページ上に縦方向に並べて配置されます。 このようなセクションには、レポート ヘッダー、レポート フッター、ページ ヘッダー、ページ フッター、グループ、詳細などがあります。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、より柔軟にレイアウトできます。 データ領域では、グループ化と詳細を利用でき、レポート本文の希望する箇所に複数のデータ領域を配置することができます。横に並べて配置することもできます。 また、Access のページ ヘッダーおよびページ フッターと同様に、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] にもページ ヘッダーとページ フッターの "集合" があります。  
  
 レポートを Access からレポート デザイナーにインポートする際に、Access レポートのページ ヘッダーとページ フッターは [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポートのページ ヘッダーとページ フッターに変換されます。 グループと詳細は、一覧データ領域に変換されます。 レポート ヘッダーとレポート フッターは、個別の集合ではなく、レポート本文に配置されます。 このため、項目の配置が Access レポートの配置とは若干異なる可能性があります。  
  
> [!NOTE]  
>  一部の Access レポートでは、上下または左右に並べて配置されるようなレポート アイテムが実際には重なり合っていることがあります。 レポート デザイナーを使用してレポートをインポートすると、この重なりは修正されません。そのため、レポートの実行時に予期しない結果が発生する場合があります。  
  
## <a name="data-sources"></a>ソリューション エクスプローラー  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] などの OLE DB データ ソースをサポートします。 Access プロジェクト (.adp) ファイルからレポートをインポートする場合は、データ ソースの接続文字列は、.adp ファイルの接続文字列から取得されます。 Access データベース (.mdb または .accdb) ファイルからレポートをインポートする場合は、データ ソースの接続文字列が Access データベースを指していることがあるため、レポートのインポート後に修正が必要になる可能性があります。 Access レポートのデータ ソースがクエリである場合は、クエリ情報は変更されることなく RDL に保存されます。 Access レポートのデータ ソースがテーブルである場合は、変換処理の際、テーブル名およびテーブル内のフィールドを基にクエリが作成されます。  
  
## <a name="reports-with-custom-modules"></a>カスタム モジュールを含むレポート  
 ユーザー設定がある場合[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[vbprvb](../includes/vbprvb-md.md)]モジュール内に含まれるコードは変換されません。 レポート デザイナーでは、インポート処理中にコードを検出すると、警告が生成されに表示される、**タスク一覧**ウィンドウ。  
  
## <a name="report-controls"></a>レポート コントロール  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下の Access コントロールがサポートされ、これらは変換後のレポート定義に保持されます。  
  
|||||  
|-|-|-|-|  
|イメージ|group1|線|四角形|  
|サブフォーム|サブレポート<br /><br /> **注**サブレポート コントロールは、メイン レポート内で変換は、サブレポート自体は個別に変換されます。|テキスト ボックス||  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下のコントロールはサポートされません。  
  
|||||  
|-|-|-|-|  
|連結オブジェクト フレーム|チェック ボックス|コンボ ボックス|コマンド ボタン|  
|カスタム コントロール|リスト ボックス|オブジェクト フレーム|オプション ボタン|  
|タブ コントロール|トグル ボタン|||  
  
 レポート デザイナーは、インポート処理中にこれらのコントロールのいずれかのように検出すると、警告が生成されに表示される、**タスク一覧**ウィンドウ。  
  
 ActiveX や Office Web コンポーネントなどのその他のコントロールは、インポートされません。 たとえば、Access レポートに OWC Chart コントロールが含まれていても、インポート時に変換されません。  
  
## <a name="report-properties"></a>レポート プロパティ  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、Access のユーザー インターフェイスから利用できる以下のプロパティがサポートされます。 コード内でしか利用できないプロパティは、サポートされません。また、そのようなプロパティは、次の一覧には含まれていません。  
  
|||||  
|-|-|-|-|  
|背景色|背景スタイル|境界線色|BorderStyle|  
|境界線幅|下余白|印刷時拡張 (テキスト ボックス)|印刷時縮小 (テキスト ボックス)|  
|[キャプション]|フォント太字|フォント斜体|フォント名|  
|フォントサイズ|フォント下線|フォント太さ|改ページ|  
|ForeColor|[高さ]|重複データ非表示|ハイパーリンク|  
|ハイパーリンクあり|可視|同一ページ印刷 (グループ)|Left|  
|左余白|線傾斜|ラベル|リンク子フィールド|  
|リンク親フィールド|改段|ページフッター|ページヘッダー|  
|ページ数|画像|ピクチャ全体表示 (レポート)|読みの順序|  
|セクション繰り返し|右余白|集計実行|OLE サイズ|  
|TextAlign|TOP|上余白|[幅]|  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、Access のユーザー インターフェイスから利用できる以下のプロパティはサポートされません。  
  
|||||  
|-|-|-|-|  
|印刷時拡張 (セクション)|印刷時縮小 (セクション)|小数点以下表示桁数|高速レーザー印刷|  
|Assert|フィルター適用|形式|書式条件|  
|同一ページ印刷グループ|同一ページ印刷 (セクション)|数字の形態|方向|  
|ペイント パレット|パレット元|ピクチャ配置|ピクチャ表示ページ|  
|ピクチャサイズ|ピクチャ全体表示 (イメージ)|スクロールバー|立体表示|  
|[縦]||||  
  
## <a name="grouping"></a>グループ化  
 Access では、グループ式、`GroupOn` プロパティ、および `GroupInterval` プロパティの 3 つのプロパティを組み合わせてグループ レベルを定義します。 グループ ヘッダーまたはグループ フッターのないグループは、このグループに含まれているグループに結合されます。 グループに他のグループが含まれていない場合は、詳細セクションに並べ替えが適用され、このグループは削除されます。  
  
## <a name="expressions"></a>式  
 Access では、式を使用して、テキスト ボックスに表示する値を指定します。 Access では、いくつかの集計関数の他に、式の言語として [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] が使用されています。 レポート デザイナーは、これらの Access の式をレポートの式に変換します。  
  
### <a name="functions"></a>関数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のレポート定義では、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET がネイティブの式の言語として使用されていますが、Access 2002 では、Visual Basic が使用されています。 以下の一覧に、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] によってサポートされている関数を示します。  
  
#### <a name="array-functions"></a>配列関数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下の配列関数がサポートされています。  
  
-   LBound  
  
-   UBound  
  
#### <a name="conversion-functions"></a>変換関数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下の変換関数がサポートされています。  
  
|||||  
|-|-|-|-|  
|Asc|CBool|CByte|CCur|  
|CDate|CDbl|CDec|Chr|  
|Chr$|CInt|CLng|CSng|  
|CStr|CVar|CVDate|形式|  
|FormatCurrency|FormatDateTime|FormatNumber|FormatPercent|  
|Hex|Hex$|Nz|Oct|  
|Oct$|Str|Str$|StrConv|  
|Val||||  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下の変換関数はサポートされません。  
  
-   GUIDFromString  
  
-   StringFromGUID  
  
#### <a name="database-functions"></a>データベース関数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下のデータベース関数がサポートされています。  
  
|||||  
|-|-|-|-|  
|CreateReport|GetObject|HyperlinkPart|パーティション|  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下のデータベース関数はサポートされません。  
  
|||||  
|-|-|-|-|  
|CodeDb|CreateControl|CreateForm|CreateGroupLevel|  
|CreateObject|CreateReportControl|CurrentDb|CurrentUser|  
|DeleteControl|DeleteReportControl|Eval|IMEStatus|  
|SysCmd||||  
  
#### <a name="datetime-functions"></a>日付/時刻関数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下の日付/時刻関数がサポートされています。  
  
|||||  
|-|-|-|-|  
|date|Date$|DateAdd|DateDiff|  
|DatePart|DateSerial|DateValue|日|  
|Hour|Minute|Month|MonthName|  
|[今]|第 2 週|Time|Time$|  
|Timer|TimeSerial|TimeValue|Weekday|  
|WeekdayName|年|||  
  
#### <a name="ddeole-functions"></a>DDE/OLE 関数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下の DDE/OLE 関数はサポートされません。  
  
|||||  
|-|-|-|-|  
|DDE|DDEIntitate|DDERequest|DDESend|  
|LoadPicture||||  
  
#### <a name="domain-aggregate-functions"></a>定義域集計関数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下の定義域集計関数はサポートされません。  
  
|||||  
|-|-|-|-|  
|DAvg|DCount|DFirst|DLast|  
|DLookup|DMax|DMin|DStDev|  
|DStDevP|DSum|DVar|DVarP|  
  
#### <a name="error-handling-functions"></a>エラー処理関数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下のエラー処理関数がサポートされています。  
  
|||||  
|-|-|-|-|  
|Err|[エラー]|Error$|IsError|  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下のエラー処理関数はサポートされていません。  
  
-   CVErr  
  
#### <a name="financial-functions"></a>財務関数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下の財務関数がサポートされています。  
  
|||||  
|-|-|-|-|  
|DDB|FV|IPmt|IRR|  
|MIRR|NPer|NPV|Pmt|  
|PPmt|PV|Rate|SLN|  
|SYD||||  
  
#### <a name="interaction-functions"></a>インタラクティブ関数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下のインタラクティブ関数がサポートされています。  
  
|||||  
|-|-|-|-|  
|コマンド|Command$|CurDir|CurDir$|  
|DeleteSetting|Dir|Dir$|Environ|  
|Environ$|EOF|FileAttr|FileDateTime|  
|FileLen|FreeFile|GetAllSettings|GetAttr|  
|GetSetting|Loc|LOF|QBColor|  
|RGB|SaveSetting|Seek|SetAttr|  
|Shell|Spc|タブ||  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下のインタラクティブ関数はサポートされません。  
  
|||||  
|-|-|-|-|  
|DoEvents|In|入力|Input$|  
  
#### <a name="inspection-functions"></a>特殊評価関数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下の特殊評価関数がサポートされています。  
  
|||||  
|-|-|-|-|  
|IsArray|IsDate|IsEmpty|IsError|  
|IsNull|IsNumeric|IsObject|TypeName|  
|VarType||||  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下の特殊評価関数はサポートされません。  
  
-   IsMissing  
  
#### <a name="math-functions"></a>算術関数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下の算術関数がサポートされています。  
  
|||||  
|-|-|-|-|  
|Abs|Atn|Cos|Exp|  
|Fix|Int|Log|Rnd|  
|四捨五入|Sgn|Sin|Sqr|  
|Tan||||  
  
#### <a name="message-functions"></a>メッセージ関数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下のメッセージ関数はサポートされません。  
  
|||||  
|-|-|-|-|  
|InputBox|InputBox$|MsgBox||  
  
#### <a name="program-flow-functions"></a>プログラム フロー関数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下のプログラム フロー関数がサポートされています。  
  
|||||  
|-|-|-|-|  
|Choose|IIf|スイッチ||  
  
#### <a name="sql-aggregate-functions"></a>SQL 集計関数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下の SQL 集計関数がサポートされています。  
  
|||||  
|-|-|-|-|  
|Avg|Count|Max|Min|  
|StDev|StDevP|Sum|Var|  
|VarP||||  
  
#### <a name="text-functions"></a>文字列関数  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] では、以下の文字列関数がサポートされています。  
  
|||||  
|-|-|-|-|  
|形式|Format$|InStr|InStrRev|  
|LCase|LCase$|Left|Left$|  
|Len|LTrim|LTrim$|Mid|  
|Mid$|[置換]|Right|Right$|  
|RTrim|Space|Space$|StrComp|  
|StrConv|String|String$|StrReverse|  
|Trim|Trim$|UCase|UCase$|  
  
### <a name="constants"></a>定数  
 Access の式では [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] の特殊な定数 (`vbTrue` など) をサポートしていないので、変換は必要ありません。 ただし、例外が 1 つだけあります。キーワード `Null` は、`System.DbNull.Value` に変換されます。  
  
### <a name="parameters"></a>パラメーター  
 インポート処理中、レポート デザイナーによって、フィールド名またはコントロールに対応していない変数がないかどうか、レポート内の各式がスキャンされます。 これらの変数は、レポートのパラメーターに追加されます。  
  
 ストアド プロシージャのデータ型は、常に string としてインポートされます。 レポートのインポート後、パラメーターを手動で変更して、正しいデータ型が使用されるようにする必要があります。  
  
### <a name="object-names"></a>オブジェクト名  
 Access ではフィールドにコントロールと同じ名前を付けることができますが、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ではできません。 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 6.0 では変数名にスペースを使用することができますが、Visual Basic .NET ではできません。 このようなオブジェクト名はすべて、インポート処理の際、有効な名前に置き換えられ、複数のオブジェクトが同じ名前の場合は一意の名前が割り当てられます。 各式はスキャンされ、名前が変更されたオブジェクトに対応する変数の名前は、新しい名前に置き換えられます。  
  
## <a name="rectangles-and-containment"></a>四角形とその内容  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のレポート定義では、四角形内に他のレポート アイテムを含めることができます。 レポート アイテムよりも大きく、レポート アイテムの領域のうち 90% を超える領域と重なっている四角形は、そのレポート アイテムのコンテナーになります。  
  
## <a name="bitmaps"></a>ビットマップ  
 レポート内に埋め込まれているビットマップはすべて、インポート時に .bmp 形式に変換されます。これらのビットマップの最初の形式は無視されます。 たとえば、レポートに .jpg ファイルおよび .gif ファイルが含まれていた場合、レポートと一緒にインポートされるリソースは .bmp ファイルになります。 ビットマップは、レポートの埋め込み画像として保存されます。 埋め込みイメージについては、次を参照してください。[イメージ&#40;レポート ビルダーおよび SSRS&#41;](report-design/images-report-builder-and-ssrs.md)します。  
  
## <a name="other-considerations"></a>他の考慮事項  
 上記のほか、Access からインポートされるレポートについては以下の事項も適用されます。  
  
-   条件付き書式は、変換されません。  
  
-   Access のレポート プロパティの説明フィールドは、変換されません。  
  
  
