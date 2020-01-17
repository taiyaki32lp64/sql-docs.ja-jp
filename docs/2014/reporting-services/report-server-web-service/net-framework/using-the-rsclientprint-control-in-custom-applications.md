---
title: カスタム アプリケーション内での RSClientPrint コントロールの使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- RSPrintClient control
- print controls [Reporting Services]
- custom printing [Reporting Services]
- client-side printing
ms.assetid: 8c0bdd18-8905-4e22-9774-a240fc81a8a7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 52b4bc564c9ea8d105809a4d5225056a231ad2e7
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155001"
---
# <a name="using-the-rsclientprint-control-in-custom-applications"></a>カスタム アプリケーション内での RSClientPrint コントロールの使用
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ActiveX コントロールである **RSPrintClient** を使用すると、HTML ビューアーで表示されたレポートをクライアント側で印刷することができます。 このコントロールには **[印刷]** ダイアログ ボックスがあり、印刷ジョブの開始、レポートのプレビュー、印刷するページの指定、余白の変更を行うことができます。 クライアント側での印刷操作の間、レポート サーバーが画像 (EMF) 表示拡張機能でレポートを表示し、オペレーティング システムの印刷機能を使用して印刷ジョブを作成し、そのジョブをプリンターに送ります。  
  
 クライアント側の印刷機能を使用すると、ユーザーのコンピューター上のブラウザーの印刷設定を使用せずに、レポートのページのサイズ、余白、ヘッダー テキスト、フッター テキストを使用して印刷出力を生成できるため、HTML レポートの印刷を制御して品質を向上させることができます。 このコントロールは、レポートのプロパティ値を読み込んで、ページ サイズと余白を設定します。  
  
 開発者がサードパーティのツール バーやビューアーでクライアント側の印刷機能を有効にする場合は、**RSClientPrint** COM オブジェクトを通じて ActiveX コントロールにアクセスすることができます。 このコントロールは自由に配布してかまいません。 以下にコントロールを使用するうえでの推奨事項を示します。  
  
-   コントロールを使用して、Web ベースのレポートの印刷を強化することができます。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] と互換性のある任意のプログラミング言語またはスクリプトからオブジェクトを指定できます。 このコントロールは、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows フォーム アプリケーションからの利用は想定していません。  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] プログラム ファイルに含まれている .cab ファイルをコピーし、カスタム アプリケーションのコード ベースに追加します。  
  
-   \<OBJECT> タグを使用してコントロールを指定します。  
  
-   OBJECT CODEBASE 属性では、.cab ファイルに対する相対 URL または完全修飾 URL を指定します。  
  
-   アプリケーションで使用しているバージョンを追跡するため、.cab ファイルに対する固有のアプリケーション バージョン情報を指定します。  
  
-   オンライン ブックの画像 (EMF) 表示に関するトピックを参照し、印刷プレビューおよび出力用にページを表示する方法を確認します。  
  
## <a name="rsprintclient-overview"></a>RSPrintClient の概要  
 このコントロールによって表示されるカスタム印刷ダイアログ ボックスでは、印刷プレビュー、特定のページや範囲を指定するためのページ選択、ページ余白、ページの向きなど、一般的な印刷ダイアログ ボックスの機能がサポートされています。 コントロールは CAB ファイルとしてパッケージ化されています。 **[印刷]** ダイアログ ボックス内のテキストは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] がサポートするすべての言語に向けてローカライズされています。 **RSPrintClient** ActiveX コントロールでは、画像表示拡張機能 (EMF) を使用してレポートが印刷されます。 EMF デバイス情報として StartPage、EndPage、MarginBottom、MarginLeft、MarginTop、MarginRight、PageHeight、および PageWidth が使用されます。 画像表示に対するその他のデバイス情報の設定はサポートされません。  
  
### <a name="language-support"></a>言語サポート  
 印刷コントロールでは、ユーザー インターフェイスのテキストがさまざまな言語で表示され、異なる測定系を使用した入力値を受け付けます。 使われる言語と測定系は、**Culture** プロパティと **UICulture** プロパティで決まります。 どちらのプロパティも LCID 値を受け付けます。 サポートされている言語から派生した言語の LCID を指定すると、最も近い言語が選択されます。 サポート対象外で、近い言語もない LCID を指定すると、英語 (U.S.) となります。  
  
## <a name="using-rsclientprint-in-code"></a>コード内での RSClientPrint の使用  
 この ActiveX コントロールとそのメソッドおよびプロパティにプログラムからアクセスするには、**RSClientPrint** オブジェクトを使用します。 このコントロールでは、印刷プレビュー用のモーダル ダイアログが提供されます。  
  
### <a name="specifying-default-values"></a>既定値の指定  
 **[印刷]** ダイアログ ボックスに、レポートの余白やページの各値を初期設定することができます。 既定では、 **[印刷]** ダイアログ ボックスはレポート定義の値で初期化されます。 既定値を使用することも、オブジェクトのプロパティを設定して異なる値を指定することもできます。  
  
 サイズはすべて mm 単位で設定されます。 **Culture** および **UICulture** がメートル法を使わないロケールに設定されている場合は、実行時に単位が変換されます。  
  
 ページのサイズと余白でどの値が使用されるかを確認するために、**GetProperties** メソッドを使用して以下の既定値を取得することができます。  
  
-   **PageHeight** と **PageWidth** は、既定のページの高さと幅を示します。 印刷コントロールを起動すると、現在選択されているプリンターで利用できる用紙サイズの中から、これらのプロパティ値に最も近いサイズが選択されます。 **PageWidth** が **PageHeight** より大きい場合は横向きに設定されます。 そうでない場合は縦向きに設定されます。  
  
-   **LeftMargin**、**RightMargin**、**TopMargin**、および **BottomMargin** は、既定ではすべて 12.2 mm に設定されます。  
  
 これらのプロパティは、レポート サーバー上の **Item** プロパティ コレクションに格納されます。 値は、レポート定義が更新されるたびに上書きされます。  
  
### <a name="rsclientprint-properties"></a>RSClientPrint プロパティ  
  
|プロパティ|[型]|RW|既定値|[説明]|  
|--------------|----------|--------|-------------|-----------------|  
|MarginLeft|Double|RW|レポートにより設定|左余白を取得または設定します。 開発者が設定せず、レポートにも指定がない場合の既定値は 12.2 mm です。|  
|MarginRight|Double|RW|レポートにより設定|右余白を取得または設定します。 開発者が設定せず、レポートにも指定がない場合の既定値は 12.2 mm です。|  
|MarginTop|Double|RW|レポートにより設定|上余白を取得または設定します。 開発者が設定せず、レポートにも指定がない場合の既定値は 12.2 mm です。|  
|MarginBottom|Double|RW|レポートにより設定|下余白を取得または設定します。 開発者が設定せず、レポートにも指定がない場合の既定値は 12.2 mm です。|  
|PageWidth|Double|RW|レポートにより設定|ページの幅を取得または設定します。 開発者が設定せず、レポートにも定義がない場合の既定値は 215.9 mm です。|  
|PageHeight|Double|RW|レポートにより設定|ページの高さを取得または設定します。 開発者が設定せず、レポートにも定義がない場合の既定値は 279.4 mm です。|  
|カルチャ|Int32|RW|ブラウザーのロケール|ロケール ID (LCID) を指定します。 この値によりユーザー入力の測定単位が決まります。 たとえば、ユーザーが `3`を入力した場合、言語がフランス語 (米国) の場合、値はミリメートル単位で測定されます。 有効な値は、1028、1031、1033、1036、1040、1041、1042、2052、3082 です。|  
|UICulture|文字列|RW|クライアントのカルチャ|ダイアログ ボックスの文字列のローカライズを指定します。 [印刷] ダイアログ内のテキストは、簡体中国語、繁体中国語、英語、フランス語、ドイツ語、イタリア語、日本語、韓国語、スペイン語にローカライズされています。 有効な値は、1028、1031、1033、1036、1040、1041、1042、2052、3082 です。|  
|Authenticate|Boolean|RW|False|セッション外印刷の接続を開始するためにコントロールからレポート サーバーに GET コマンドを発行するかどうかを指定します。|  
  
### <a name="when-to-set-the-authenticate-property"></a>Authenticate プロパティを設定する状況  
 ブラウザー セッションの内部から印刷を行う場合は、`Authenticate` プロパティを設定する必要はありません。 アクティブなセッションのコンテキストでは、印刷コントロールからレポート サーバーへの要求はすべてブラウザーによって処理されます。 レポート サーバーへの通信に必要なセッション変数はブラウザーによって設定されます。  
  
 セッション外印刷を行う場合 (レポートを最初に開かずに直接プリンターに送る場合など) は、レポート サーバーとのセッションをセットアップするために、印刷コントロールが HTTP `GET` 要求を発行する必要があります。 `GET` 要求を発行するには、`Authenticate` を `True` に設定します。  
  
 Windows 統合セキュリティまたは基本認証を使用している場合は、`GET` 要求を発行するだけで済みます。 フォーム認証を使用している場合は、`Authenticate` プロパティは無視されます。 アプリケーション コードでセッションを設定し、用意したカスタム セキュリティ拡張機能を使用してユーザーを認証する必要があります。 フォーム認証を使用する場合は、認証クッキーの有効期限を、セッションが十分な期間にわたって維持される値に設定してください。 この値を低く設定しすぎると、クッキーの有効期限が切れるたびに、ユーザーにログオン資格情報の入力が要求されます。  
  
### <a name="clsids"></a>CLSID  
 レポートをオンプレミスで実行している場合は、次の CLSID 値を使用します。  
  
-   41861299-EAB2-4DCC-986C-802AE12AC499  
  
-   5554DCB0-700B-498D-9B58-4E40E5814405  
  
-   60677965-AB8B-464f-9B04-4BA871A2F17F  
  
 レポートを Azure SQL Reporting で実行している場合は、次の CLSID 値を使用します。  
  
-   3DD32426-554D-48C0-A200-65D3BF880E38  
  
-   05662494-ACF9-446A-BE4C-7D3F7EA7F62F  
  
### <a name="rsprintclient-support-for-the-print-method"></a>RSPrintClient による Print メソッドのサポート  
 **RSClientPrint** オブジェクトは、[印刷] ダイアログ ボックスを表示するための **Print** メソッドをサポートしています。 **Print** メソッドには、以下の引数があります。  
  
|引数|I/O|[型]|[説明]|  
|--------------|----------|----------|-----------------|  
|ServerPath|In|文字列|レポートサーバーの仮想ディレクトリ (https://adventure-works/reportserver)など) を指定します。|  
|ReportPathParameters|In|文字列|パラメーターを含む、レポート サーバー フォルダー名前空間内のレポートの完全な名前を指定します。 レポートは、URL にアクセスすることによって取得されます。 例: "/AdventureWorks Sample Reports/Employee Sales Summary&EmpID=1234"|  
|ReportName|In|文字列|レポートの短縮名です (上の例では、短縮名は「Employee Sales Summary」です)。 ここで設定した内容は、[印刷] ダイアログ ボックスと印刷キューに表示されます。|  
  
### <a name="example"></a>例  
 以下の HTML の例では、JavaScript 内で .cab ファイル、**Print** メソッド、プロパティを指定する方法を示します。  
  
 `<BODY onload="Print()">`  
  
 `<OBJECT ID="RSClientPrint" CLASSID="CLSID: 5554DCB0-700B-498D-9B58-4E40E5814405D3" CODEBASE="<URL to the .CAB file>#Version=<your application version information>" VIEWASTEXT></OBJECT>`  
  
 `<script language="javascript">`  
  
 `function Print()`  
  
 `{`  
  
 `RSClientPrint.MarginLeft = 12.7;`  
  
 `RSClientPrint.MarginTop = 12.7;`  
  
 `RSClientPrint.MarginRight = 12.7;`  
  
 `RSClientPrint.MarginBottom = 12.7;`  
  
 `RSClientPrint.Culture = 1033;`  
  
 `RSClientPrint.UICulture = 9;`  
  
 `RSClientPrint.Print('http://localhost/rtm', '%2fEmployee_Sales_Summary&ReportMonth=6&ReportYear=2004&EmpID=20', 'Employee_Sales_Summary')`  
  
 `}`  
  
 `</script>`  
  
 `</BODY>`  
  
## <a name="see-also"></a>参照  
 [印刷コントロールを使用したブラウザーからのレポートの印刷 &#40;レポート ビルダーおよび SSRS&#41;](../../report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)   
 [レポートの印刷 &#40;レポート ビルダーおよび SSRS&#41;](../../report-builder/print-reports-report-builder-and-ssrs.md)   
 [画像デバイス情報設定](../../image-device-information-settings.md)  
  
  
