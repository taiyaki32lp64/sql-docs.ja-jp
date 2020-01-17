---
title: Integration Services のエラーおよびメッセージのリファレンス | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- error numbers [Integration Services]
- hresults [Integration Services]
- errors [Integration Services], listed
ms.assetid: 2c825c07-5074-42ad-90ea-0dc5a588dcf7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7d55050b132a3367ecc495d0afedcad6f0d2351b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284422"
---
# <a name="integration-services-error-and-message-reference"></a>Integration Services のエラーおよびメッセージのリファレンス

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  次の表に、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で事前定義されているエラー メッセージ、警告メッセージ、および情報メッセージの一覧を示します。この一覧では、数値コードおよびシンボル名と共に、メッセージをカテゴリごとに昇順の番号順に示します。 ここに示す各エラーは、 <xref:Microsoft.SqlServer.Dts.Runtime.Hresults> 名前空間の <xref:Microsoft.SqlServer.Dts.Runtime> クラスのフィールドとして定義されています。  
  
 この一覧は、説明のないエラー コードが表示された場合に便利です。 現時点では、この一覧にトラブルシューティング情報は含まれていません。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の使用時に表示されるエラー メッセージの多くは、他のコンポーネントが原因です。 このトピックには、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] コンポーネントが原因で発生するすべてのエラーを記載しています。 一覧でエラーが見つからない場合、そのエラーは [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]以外のコンポーネントが原因です。 これには、OLE DB プロバイダー、 [!INCLUDE[ssDE](../includes/ssde-md.md)] や [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] などの他のデータベース コンポーネント、またはファイル システム、SMTP サーバー、メッセージ キュー (MSMQ) などの他のサービスやコンポーネントなどがあります。 このような外部エラー メッセージの情報については、コンポーネント固有のドキュメントを参照してください。  
  
 この一覧には、次のようなメッセージのグループが含まれています。  
  
-   [エラー メッセージ (DTS_E_*)](#msgError)  
  
-   [警告メッセージ (DTS_W_*)](#msgWarning)  
  
-   [情報メッセージ (DTS_I_*)](#msgInfo)  
  
-   [一般的なメッセージおよびイベント メッセージ (DTS_MSG_*)](#msgGeneral)  
  
-   [成功時のメッセージ (DTS_S_*)](#msgSuccess)  
  
-   [データ フロー コンポーネントのエラー メッセージ (DTSBC_E_*)](#msgPipeline)  
  
##  <a name="msgError"></a> エラー メッセージ  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のエラー メッセージのシンボル名は、 **DTS_E_** で始まります。  
  
|16 進コード|10 進コード|シンボル名|[説明]|  
|----------------------|------------------|-------------------|-----------------|  
|0x8002F347|-2147290297|DTS_E_STOREDPROCSTASK_OVERWRITINGSPATDESTINATION|転送先でストアド プロシージャ "%1" を上書きしています。|  
|0x8020837E|-2145352834|DTS_E_ADOSRCUNKNOWNTYPEMAPPEDTONTEXT|列 "%2" のデータ型 "%1" は、%3 に対してはサポートされていません。 この列は DT_NTEXT に変換されます。|  
|0x8020838C|-2145352820|DTS_E_XMLSRCSCHEMACOLUMNNOTINEXTERNALMETADATA|XML スキーマのテーブル %2 の列 %1 には、外部メタデータ列のマッピングがありません。|  
|0xC0000032|-1073741774|DTS_E_NOTINITIALIZED|内部オブジェクトまたは変数が初期化されませんでした。 これは製品の内部エラーです。  変数に有効な値が指定されている必要がありますが、指定されていない場合にこのエラーが返されます。|  
|0xC0000033|-1073741773|DTS_E_EXPIRED|Integration Services の評価期間が終了しました。|  
|0xC0000034|-1073741772|DTS_E_NEGATIVEVALUESNOTALLOWED|このプロパティには負の値を代入できません。 このエラーは、COUNT プロパティのような正の値のみを含むことができるプロパティに負の値を代入した場合に発生します。|  
|0xC0000035|-1073741771|DTS_E_NEGATIVEINDEXNOTALLOWED|インデックスに負の値を指定することはできません。 このエラーは、コレクションへのインデックスとして負の値が使用された場合に発生します。|  
|0xC00060AB|-1073717077|DTS_E_INVALIDSSISSERVERNAME|サーバー名 "%1" は無効です。 SSIS サービスは複数インスタンスをサポートしていません。"server name\instance" ではなく、サーバー名のみを使用してください。|  
|0xC0008445|-1073707963|DTS_E_SCRIPTMIGRATIONFAILED64BIT|Visual Tools for Applications デザイナー サポートがないため、64 ビット プラットフォーム上で VSA スクリプトの移行を実行できません。 64 ビット プラットフォーム上では、WOW64 を利用して移行を実行してください。|  
|0xC000931A|-1073704166|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_ERRORSINCOMMAND|コマンドの実行でエラーが発生しました。|  
|0xC000F427|-1073679321|DTS_E_SSISSTANDALONENOTINSTALLED|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] の外部で SSIS パッケージを実行するには、Integration Services %1 以上をインストールする必要があります。|  
|0xC0010001|-1073676287|DTS_E_VARIABLENOTFOUND|変数が見つかりません。 このエラーは、パッケージの実行中にコンテナーの Variables コレクションから変数を取得しようとしたときに、その変数がない場合に発生します。 変数名が変更されたか、変数が作成されていない可能性があります。|  
|0xC0010003|-1073676285|DTS_E_VARIABLEREADONLY|読み取り専用の変数 "%1" に書き込もうとして、エラーが発生しました。|  
|0xC0010004|-1073676284|DTS_E_MANAGEDCOMPONENTSTORENOTFOUND|タスクとデータ フロー タスクのコンポーネントを含んでいるディレクトリが見つかりません。 インストールの整合性を確認してください。|  
|0xC0010006|-1073676282|DTS_E_PACKAGENAMETOOLONG|パッケージ名が長すぎます。 上限は 128 文字です。 パッケージ名を短くしてください。|  
|0xC0010007|-1073676281|DTS_E_PACKAGEDESCRIPTIONTOOLONG|パッケージの説明が長すぎます。 上限は 1,024 文字です。 パッケージの説明を短くしてください。|  
|0xC0010008|-1073676280|DTS_E_VERCOMMENTSTOOLONG|VersionComments プロパティが長すぎます。 上限は 1,024 文字です。 VersionComments を短くしてください。|  
|0xC0010009|-1073676279|DTS_E_ELEMENTNOTFOUND|要素がコレクションに見つかりません。 このエラーは、パッケージの実行中、コンテナーのコレクションから要素を取得しようとしたときに、要素がコレクションにない場合に発生します。|  
|0xC001000A|-1073676278|DTS_E_PACKAGENOTFOUND|指定されたパッケージを SQL Server データベースから読み込めませんでした。|  
|0xC001000C|-1073676276|DTS_E_INVALIDVARIABLEVALUE|変数値の代入が無効です。 このエラーは、クライアントまたはタスクがランタイム オブジェクトを変数値に代入した場合に発生します。|  
|0xC001000D|-1073676275|DTS_E_RESERVEDNAMESPACE|変数へ名前空間を割り当て中にエラーが発生しました。 "System" という名前空間は、システムで使用するために予約されています。 このエラーは、コンポーネントまたはタスクが、"System" という名前空間で変数を作成しようとした場合に発生します。|  
|0xC001000E|-1073676274|DTS_E_CONNECTIONNOTFOUND|接続 "%1" が見つかりません。 このエラーは、特定の接続要素が見つからない場合に接続のコレクションによってスローされます。|  
|0xC001000F|-1073676273|DTS_E_64BITVARIABLERECAST|変数 "%1" は、このオペレーティング システムでサポートされていない 64 ビット整数変数です。 この変数は 32 ビット整数に再キャストされました。|  
|0xC0010010|-1073676272|DTS_E_CANTCHANGEREADONLYATRUNTIME|変数 "%1" の読み取り専用属性を変更しようとしました。 このエラーは、変数の読み取り専用属性が実行時に変更されたときに発生します。 読み取り専用の属性を変更できるのはデザイン時のみです。|  
|0xC0010011|-1073676271|DTS_E_VARIABLEINVALIDCONTAINERREF|コンテナー参照に変数を設定しようとしましたが、これは無効です。  コンテナー参照には変数を設定できません。|  
|0xC0010013|-1073676269|DTS_E_INVALIDVARVALUE|変数 "%1" に無効な値またはオブジェクトを代入しています。 このエラーは、変数に指定した値が適切でない場合に発生します。|  
|0xC0010014|-1073676268|DTS_E_GENERICERROR|1 つ以上のエラーが発生しました。 このエラーの前により具体的なエラーが発生していて、そのエラーで詳細が説明されています。 このメッセージは、エラーの原因となった関数からの戻り値として使用されます。|  
|0xC0010016|-1073676266|DTS_E_INVALIDARRAYVALUE|配列値の取得時または設定時にエラーが発生しました。 型 "%1" は使用できません。 このエラーは、配列を変数に読み込んだときに発生します。|  
|0xC0010017|-1073676265|DTS_E_UNSUPPORTEDARRAYTYPE|配列でサポートされていない型です。 このエラーは、サポートされていない型の配列を変数に保存したときに発生します。|  
|0xC0010018|-1073676264|DTS_E_PERSISTENCEERROR|ノード "%2" から値 "%1" を読み込み中にエラーが発生しました。|  
|0xC0010019|-1073676263|DTS_E_INVALIDNODE|ノード "%1" は有効なノードではありません。 このエラーは、保存が失敗した場合に発生します。|  
|0xC0010020|-1073676256|DTS_E_ERRORLOADINGTASK|タスク "%1"、種類 "%2" を読み込めませんでした。 このタスクの連絡先に関する情報は "%3" です。|  
|0xC0010021|-1073676255|DTS_E_ERRORELEMENTNOTINCOLL|要素 "%1" がコレクション "%2" に存在しません。|  
|0xC0010022|-1073676254|DTS_E_MISSINGOBJECTDATA|ホストされたオブジェクトの XML ブロックに ObjectData 要素が見つかりません。 このエラーは、XML パーサーによってオブジェクトのデータ要素が検索され、見つからなかった場合に発生します。|  
|0xC0010023|-1073676253|DTS_E_VARIABLENOTFOUNDINCOLL|変数 "%1" が見つかりません。 このエラーは、パッケージの実行中にコンテナーの変数のコレクションから変数を取得しようとしたときに、その変数がない場合に発生します。  変数名が変更されたか、変数が作成されていない可能性があります。|  
|0xC0010025|-1073676251|DTS_E_HASEMPTYTASKHOSTS|読み込めなかったタスクがパッケージに含まれているので、パッケージを実行できません。|  
|0xC0010026|-1073676250|DTS_E_TASKISEMPTY|タスクを読み込めませんでした。 このタスクの連絡先に関する情報は "%1" です。|  
|0xC0010027|-1073676249|DTS_E_ERRORLOADINGTASKNOCONTACT|タスク "%1" を読み込み中にエラーが発生しました。|  
|0xC0010028|-1073676248|DTS_E_ERRORATLOADTASK|タスクを読み込み中にエラーが発生しました。 このエラーは、XML からのタスクの読み込みに失敗した場合に発生します。|  
|0xC0010200|-1073675776|DTS_E_MULTIPLECACHEWRITES|キャッシュは、%2 が既に書き込んでいるため、%1 は書き込むことができません。|  
|0xC0010201|-1073675775|DTS_E_SETCACHEFORINSERTFAILED|新しいデータ用のキャッシュを準備できませんでした。|  
|0xC0010202|-1073675774|DTS_E_SETCACHEFORFILLFAILED|データでいっぱいのため、キャッシュを設定できませんでした。|  
|0xC0010203|-1073675773|DTS_E_READUNINITIALIZEDCACHE|キャッシュは初期化されていないので、%1 は読み取ることができません。|  
|0xC0010204|-1073675772|DTS_E_SETCACHEFORREADFAILED|データを提供するためのキャッシュを準備できませんでした。|  
|0xC0010205|-1073675771|DTS_E_READNOTFILLEDCACHE|キャッシュは %1 が書き込んでいるため、%2 が読み取ることはできません。|  
|0xC0010206|-1073675770|DTS_E_WRITEWHILECACHEINUSE|キャッシュは %1 から読み取られているため、%2 が書き込むことはできません。|  
|0xC0011001|-1073672191|DTS_E_CANTLOADFROMNODE|指定された XML ノードからランタイム オブジェクトを読み込めません。  このエラーは、SSIS 以外の XML ノードなど、正しくない種類の XML ノードからパッケージや他のオブジェクトを読み込もうとしたときに発生します。|  
|0xC0011002|-1073672190|DTS_E_OPENPACKAGEFILE|エラー 0x%2!8.8X! "%3" により、パッケージ ファイル "%1" を開けませんでした 。  このエラーは、パッケージを読み込もうとして、ファイルを開けなかったり、XML ドキュメントに正しく読み込めなかった場合に発生します。 これは、LoadPackage の呼び出し時に正しくないファイル名が指定されたか、または指定された XML ファイルの形式が正しくなかった結果と考えられます。|  
|0xC0011003|-1073672189|DTS_E_LOADPACKAGEXML|エラー 0x%1!8.8X! "%2" により、XML を読み込めませんでした 。 このエラーは、パッケージを読み込もうとして、ファイルを開けなかったり、XML ドキュメントに正しく読み込めなかった場合に発生します。  これは、LoadPackage メソッドに正しくないファイル名が渡されたか、または指定された XML ファイルの形式が正しくなかった結果と考えられます。|  
|0xC0011004|-1073672188|DTS_E_LOADPACKAGEXMLFILE|エラー 0x%2!8.8X! "%3" により、パッケージ ファイル "%1" から XML を読み込めませんでした 。  このエラーは、パッケージを読み込もうとして、ファイルを開けなかったり、XML ドキュメントに正しく読み込めなかった場合に発生します。 これは、LoadPackage メソッドに正しくないファイル名が渡されたか、または指定された XML ファイルの形式が正しくなかった結果と考えられます。|  
|0xC0011005|-1073672187|DTS_E_OPENFILE|パッケージ ファイルを開けませんでした。 このエラーは、パッケージを読み込もうとして、ファイルを開けなかったり、XML ドキュメントに正しく読み込めなかった場合に発生します。 これは、LoadPackage メソッドに正しくないファイル名が渡されたか、または指定された XML ファイルの形式が正しくなかった結果と考えられます。|  
|0xC0011006|-1073672186|DTS_E_UNABLETODECODEBINARYFORMAT|パッケージでバイナリ形式をデコードできません。|  
|0xC0011007|-1073672185|DTS_E_FUNDAMENTALLOADINGERROR|パッケージが有効な XML 形式を保持していないので、パッケージを XML として読み込めません。 特定の XML パーサー エラーが通知されます。|  
|0xC0011008|-1073672184|DTS_E_LOADFROMXML|XML からの読み込み中にエラーが発生しました。 詳細なエラー情報を格納できる Events オブジェクトが渡されなかったので、この問題に関する詳細なエラー情報を特定できません。|  
|0xC0011009|-1073672183|DTS_E_XMLDOMERROR|XML ドキュメント オブジェクト モデルのインスタンスを作成できません。 MSXML を登録できない可能性があります。|  
|0xC001100D|-1073672179|DTS_E_CANNOTLOADOLDPACKAGES|パッケージを読み込めません。 このエラーは、古いバージョンのパッケージを読み込もうとしたか、パッケージ ファイルが無効な構造化オブジェクトを参照している場合に発生します。|  
|0xC001100E|-1073672178|DTS_E_SAVEFILE|パッケージ ファイルを保存できませんでした。|  
|0xC001100F|-1073672177|DTS_E_SAVEPACKAGEFILE|パッケージ ファイル "%1" を保存できませんでした。エラー 0x%2!8.8X! "%3" が発生しました 。|  
|0xC001200D|-1073668083|DTS_E_IDTSNAMENOTSUPPORTED|オブジェクトが IDTSName100 から継承される必要がありましたが、継承されませんでした。|  
|0xC0012018|-1073668072|DTS_E_CONFIGFORMATINVALID_PACKAGEDELIMITER|構成エントリ "%1" は、パッケージ区切り記号で開始されていないため、形式が正しくありません。 "\package" 区切り記号がありませんでした。|  
|0xC0012019|-1073668071|DTS_E_CONFIGFORMATINVALID|構成エントリ "%1" の形式が正しくありませんでした。 このエラーは、区切り記号がないか、配列の区切り記号が無効であるなどの形式エラーが原因で発生する可能性があります。|  
|0xC001201B|-1073668069|DTS_E_CONFIGFILEFAILEDEXPORT|構成ファイルのエクスポート中にエラーが発生しました。|  
|0xC0012021|-1073668063|DTS_E_PROPERTIESCOLLECTIONREADONLY|プロパティのコレクションは変更できません。|  
|0xC0012022|-1073668062|DTS_E_DTRXMLSAVEFAILURE|構成ファイルの保存に失敗しました。 ファイルが読み取り専用である可能性があります。|  
|0xC0012023|-1073668061|DTS_E_FAILPACKAGEONFAILURENA|FailPackageOnFailure プロパティはパッケージ コンテナーには適用できません。|  
|0xC0012024|-1073668060|DTS_E_TASKPRODUCTLEVEL|インストールされている Integration Services %2 ではタスク "%1" を実行できません。 %3 以上が必要です。|  
|0xC0012029|-1073668055|DTS_E_UNABLETOSAVETOFILE|XML を "%1" に保存できません。 ファイルが読み取り専用である可能性があります。|  
|0xC0012037|-1073668041|DTS_E_CONFIGTYPECONVERSIONFAILED|パッケージ パス "%2" の構成 "%1" の型を変換できませんでした。  このエラーは、構成値を文字列から適切な変換先の型に変換できない場合に発生します。 構成値を確実に変換先のプロパティまたは変数の型に変換できるように、構成値を確認してください。|  
|0xC0012049|-1073668023|DTS_E_CONFIGFAILED|構成エラーです。 これは、構成の種類すべてに対する汎用警告です。 この警告の前に他の警告が発生していて、その警告で詳細が説明されています。|  
|0xC0012050|-1073668016|DTS_E_REMOTEPACKAGEVALIDATION|ExecutePackage タスクからパッケージを検証できませんでした。 パッケージを実行できません。|  
|0xC0013001|-1073663999|DTS_E_FAILTOCREATEMUTEX|エラー 0x%2!8.8X! により、ミューテックス "%1" を作成できませんでした。|  
|0xC0013002|-1073663998|DTS_E_MUTEXOWNBYDIFFUSER|ミューテックス "%1" は既に存在し、別のユーザーによって所有されています。|  
|0xC0013003|-1073663997|DTS_E_WAITFORMUTEXFAILED|エラー 0x%2!8.8X! により、ミューテックス "%1" を取得できませんでした。|  
|0xC0013004|-1073663996|DTS_E_FAILTORELEASEMUTEX|エラー 0x%2!8.8X! により、ミューテックス "%1" を解放できませんでした。|  
|0xC0014003|-1073659901|DTS_E_INVALIDTASKPOINTER|ラッパーのタスク ポインターが無効です。 ラッパーがタスクへの無効なポインターを保持しています。|  
|0xC0014004|-1073659900|DTS_E_ALREADYADDED|この実行可能ファイルは、別のコンテナーの実行可能ファイルのコレクションに追加されています。 このエラーは、クライアントが、ある実行可能ファイルを複数の実行可能ファイルのコレクションに追加しようとした場合に発生します。 別の実行可能ファイルのコレクションに追加する前に、この実行可能ファイルを現在のコレクションから削除してください。|  
|0xC0014005|-1073659899|DTS_E_UNKNOWNCONNECTIONMANAGERTYPE|接続マネージャー "%2" に指定されている接続の種類 "%1" は、有効な接続マネージャーの種類として認識されません。 このエラーは、接続の種類が不明な接続マネージャーを作成しようとした場合に発生します。 接続の種類の名前が、正しいスペルになっていることを確認してください。|  
|0xC0014006|-1073659898|DTS_E_COLLECTIONCOULDNTADD|オブジェクトが作成されましたが、コレクションに追加できませんでした。 このエラーは、メモリ不足の状態が原因で発生する可能性があります。|  
|0xC0014007|-1073659897|DTS_E_ODBCERRORENV|Open Database Connectivity (ODBC) 環境を作成中にエラーが発生しました。|  
|0xC0014008|-1073659896|DTS_E_ODBCERRORDBC|Open Database Connectivity (ODBC) データベース接続を作成中にエラーが発生しました。|  
|0xC0014009|-1073659895|DTS_E_ODBCERRORCONNECT|データベース サーバーとの Open Database Connectivity (ODBC) 接続を確立中にエラーが発生しました。|  
|0xC001400A|-1073659894|DTS_E_CONNECTIONMANAGERQUALIFIERALREADYSET|この接続マネージャー インスタンスには、既に修飾子が設定されています。 各インスタンスに修飾子を設定できるのは一度だけです。|  
|0xC001400B|-1073659893|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSET|この接続マネージャーのインスタンスには、修飾子が設定されていません。 初期化を完了するには、修飾子を設定する必要があります。|  
|0xC001400C|-1073659892|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSUPPORTED|この接続マネージャーでは、修飾子の指定がサポートされていません。|  
|0xC001400D|-1073659891|DTS_E_CANNOTCLONECONNECTIONMANAGER|アウト プロセスで実行するために接続マネージャー "0x%1" を複製することはできません。|  
|0xC001400E|-1073659890|DTS_E_NOSQLPROFILERDLL|SQL Server Profiler のログ プロバイダーは、pfclnt.dll を読み込めませんでした。 SQL Server Profiler がインストールされていることを確認してください。|  
|0xC001400F|-1073659889|DTS_E_LOGFAILED|エラー コード 0x%1!8.8X! により、SSIS ログ記録インフラストラクチャが失敗しました。 このエラーは、特定のログ プロバイダーに起因しないログ記録エラーを示します。|  
|0xC0014010|-1073659888|DTS_E_LOGPROVIDERFAILED|エラー コード 0x%2!8.8X! (%3) により、SSIS ログ記録プロバイダー "%1" が失敗しました。 (%3)。  これは、指定されたログ プロバイダーに起因するログ記録エラーを示します。|  
|0xC0014011|-1073659887|DTS_E_SAVETOSQLSERVER_OLEDB|SaveToSQLServer メソッドで OLE DB エラー コード 0x%1!8.8X! (%2) が検出されました。  発行された SQL ステートメントは失敗しました。|  
|0xC0014012|-1073659886|DTS_E_LOADFROMSQLSERVER_OLEDB|LoadFromSQLServer メソッドで OLE DB エラー コード 0x%1!8.8X! (%2) が検出されました。  発行された SQL ステートメントは失敗しました。|  
|0xC0014013|-1073659885|DTS_E_REMOVEFROMSQLSERVER_OLEDB|RemoveFromSQLServer メソッドで OLE DB エラー コード 0x%1!8.8X! (%2) が検出されました。 発行された SQL ステートメントは失敗しました。|  
|0xC0014014|-1073659884|DTS_E_EXISTSONSQLSERVER_OLEDB|ExistsOnSQLServer メソッドで OLE DB エラー コード 0x%1!8.8X! (%2) が検出されました。 発行された SQL ステートメントは失敗しました。|  
|0xC0014015|-1073659883|DTS_E_CONNECTIONSTRING|指定された接続文字列が使用されたときに、OLE DB によるデータベース接続が失敗しました。|  
|0xC0014016|-1073659882|DTS_E_FROMEXECISNOTCHILD|優先順位制約を追加するときに、このコンテナーの子ではない From 実行可能ファイルが指定されました。|  
|0xC0014017|-1073659881|DTS_E_TOEXECISNOTCHILD|優先順位制約を追加するときに、このコンテナーの子ではない To 実行可能ファイルが指定されました。|  
|0xC0014018|-1073659880|DTS_E_ODBCTRANSACTIONENLIST|トランザクションで ODBC 接続への参加を試行中にエラーが発生しました。 SQLSetConnectAttr で、SQL_ATTR_ENLIST_IN_DTC 属性を設定できませんでした。|  
|0xC0014019|-1073659879|DTS_E_CONNECTIONOFFLINE|パッケージの OfflineMode プロパティが True に設定されているため、接続マネージャー "%1" は接続を取得できません。 OfflineMode が True に設定されている場合は、接続を取得できません。|  
|0xC001401A|-1073659878|DTS_E_BEGINTRANSACTION|エラー 0x%1!8.8X! "%2" により、SSIS ランタイムは分散トランザクションを開始できませんでした 。 DTC トランザクションを開始できませんでした。 このエラーは、MSDTC サービスが実行されていないことが原因で発生する可能性があります。|  
|0xC001401B|-1073659877|DTS_E_SETQUALIFIERDESIGNTIMEONLY|パッケージの実行中は、接続マネージャーで SetQualifier メソッドを呼び出すことができません。 このメソッドを使用できるのはデザイン時のみです。|  
|0xC001401C|-1073659876|DTS_E_SQLPERSISTENCEVERSION|SQL Server にパッケージを格納するか SQL Server でパッケージを変更するには、SSIS ランタイムおよびデータベースのバージョンが同じである必要があります。 古いバージョンのパッケージの格納はサポートされていません。|  
|0xC001401D|-1073659875|DTS_E_CONNECTIONVALIDATIONFAILED|接続 "%1" を検証できませんでした。|  
|0xC001401E|-1073659874|DTS_E_INVALIDFILENAMEINCONNECTION|接続に指定されたファイル名 "%1" は無効です。|  
|0xC001401F|-1073659873|DTS_E_MULTIPLEFILESONRETAINEDCONNECTION|Retain プロパティが True の場合、接続に対して複数のファイル名を指定できません。 複数のファイルが指定されていることを意味する縦棒が接続文字列に含まれています。また、Retain プロパティが True になっています。|  
|0xC0014020|-1073659872|DTS_E_ODBCERROR|ODBC エラー %1!d! が 発生しました。|  
|0xC0014021|-1073659871|DTS_E_PRECEDENCECONSTRAINT|"%1" から "%2" までの範囲の優先順位制約でエラーが発生しました。|  
|0xC0014022|-1073659870|DTS_E_FAILEDPOPNATIVEFEE|次のエラー コードにより、ForEachEnumeratorInfos コレクションにネイティブ ForEachEnumerators を設定できませんでした: %1。|  
|0xC0014023|-1073659869|DTS_E_GETENUMERATOR|エラー 0x%1!8.8X! "%2" により、ForEach 列挙子の GetEnumerator メソッドが失敗しました 。 このエラーは、ForEach 列挙子が列挙を実行できない場合に発生します。|  
|0xC0014024|-1073659868|DTS_E_CANTGETCERTDATA|指定された証明書オブジェクトから未加工の証明書データを取得できませんでした (エラー: %1)。 このエラーは、CPackage::put_CertificateObject が ManagedHelper オブジェクトのインスタンスを作成できない場合、ManagedHelper オブジェクトが失敗した場合、または ManagedHelper オブジェクトから正しくない形式の配列が返された場合に発生します。|  
|0xC0014025|-1073659867|DTS_E_CANTCREATECERTCONTEXT|証明書コンテキストを作成できませんでした (エラー: %1)。 このエラーは、対応する CryptoAPI 関数が失敗した場合に CPackage::put_CertificateObject または CPackage::LoadFromXML で発生します。|  
|0xC0014026|-1073659866|DTS_E_CANTOPENCERTSTORE|エラー "%1" により、MY 証明書ストアを開けませんでした。このエラーは、CPackage::LoadUserCertificateByName および CPackage::LoadUserCertificateByHash で発生します。|  
|0xC0014027|-1073659865|DTS_E_CANTFINDCERTBYNAME|名前で指定された MY ストアの証明書が見つかりません (エラー: %1)。 このエラーは、CPackage::LoadUserCertificateByName で発生します。|  
|0xC0014028|-1073659864|DTS_E_CANTFINDCERTBYHASH|ハッシュで指定された証明書が "MY" ストアに見つかりません (エラー: %1)。 このエラーは、CPackage::LoadUserCertificateByHash で発生します。|  
|0xC0014029|-1073659863|DTS_E_INVALIDCERTHASHFORMAT|ハッシュ値はバイトの 1 次元配列ではありません (エラー: %1)。 このエラーは、CPackage::LoadUserCertificateByHash で発生します。|  
|0xC001402A|-1073659862|DTS_E_CANTACCESSARRAYDATA|配列のデータにアクセスできません (エラー: %1)。 このエラーは、GetDataFromSafeArray が呼び出されるたびに発生する可能性があります。|  
|0xC001402B|-1073659861|DTS_E_CREATEMANAGEDHELPERFAILED|エラー 0x%1!8.8X! "%2" により、SSIS マネージド ヘルパー オブジェクトの作成中に失敗しました 。 このエラーは、CoCreateInstance CLSID_DTSManagedHelper が失敗するたびに発生します。|  
|0xC001402C|-1073659860|DTS_E_OLEDBTRANSACTIONENLIST|エラー 0x%1!8.8X! "%2" により、SSIS ランタイムは OLE DB 接続を分散トランザクションに参加させることができませんでした 。|  
|0xC001402D|-1073659859|DTS_E_SIGNPACKAGEFAILED|エラー 0x%1!8.8X! "%2" により、パッケージに署名できませんでした 。 このエラーは、ManagedHelper.SignDocument メソッドが失敗した場合に発生します。|  
|0xC001402E|-1073659858|DTS_E_CHECKENVELOPEFAILED|エラー 0x%1!8.8X! "%2" により、パッケージ XML の XML 署名エンベロープを確認できませんでした 。 このエラーは、CPackage::LoadFromXML で発生します。|  
|0xC001402F|-1073659857|DTS_E_GETXMLSOURCEFAILED|エラー 0x%1!8.8X! "%2" により、XML DOM オブジェクトから XML ソースを取得できませんでした 。 このエラーは、IXMLDOMDocument::get_xml が失敗した場合に発生します。|  
|0xC0014030|-1073659856|DTS_E_PACKAGEVERIFICATIONFAILED|エラー 0x%1!8.8X!"%2" により、パッケージの暗号化署名を検証できませんでした 。 このエラーは、署名の検証操作に失敗した場合に発生します。|  
|0xC0014031|-1073659855|DTS_E_GETKEYFROMCERTFAILED|エラー 0x%1!8.8X! "%2" により、指定された証明書に関連付けられた暗号化キー ペアを取得できませんでした 。 発行された証明書のキー ペアを所持していることを確認してください。 このエラーは、通常、個人が秘密キーを所持していない証明書を使用してドキュメントに署名しようとした場合に発生します。|  
|0xC0014032|-1073659854|DTS_E_INVALIDSIGNATURE|デジタル署名が無効です。 パッケージのコンテンツが変更されています。|  
|0xC0014033|-1073659853|DTS_E_UNTRUSTEDSIGNATURE|デジタル署名は有効ですが、署名者が信頼されていないので、信頼性は保証できません。|  
|0xC0014034|-1073659852|DTS_E_TRANSACTIONENLISTNOTSUPPORTED|この接続では、分散トランザクションへの参加がサポートされていません。|  
|0xC0014035|-1073659851|DTS_E_PACKAGEPROTECT|エラー 0x%1!8.8X! "%2" により、パッケージの保護を適用できませんでした 。 このエラーは、XML に保存するときに発生します。|  
|0xC0014036|-1073659850|DTS_E_PACKAGEUNPROTECT|エラー 0x%1!8.8X! "%2" により、パッケージの保護を削除できませんでした 。 このエラーは、CPackage::LoadFromXML メソッドで発生します。|  
|0xC0014037|-1073659849|DTS_E_PACKAGEPASSWORD|パッケージはパスワードで暗号化されています。 パスワードが指定されなかったか、正しくありません。|  
|0xC0014038|-1073659848|DTS_E_DUPLICATECONSTRAINT|優先順位制約が、指定された実行可能ファイル間に既に存在します。 複数の優先順位制約は許可されていません。|  
|0xC0014039|-1073659847|DTS_E_PACKAGELOADFAILED|エラー 0x%1!8.8X! "%2" により、パッケージを読み込めませんでした 。 このエラーは、CPackage::LoadFromXML が失敗した場合に発生します。|  
|0xC001403A|-1073659846|DTS_E_PACKAGEOBJECTNOTENVELOPED|エラー 0x%1!8.8X! "%2" により、署名付き XML エンベロープでパッケージ オブジェクトが見つかりませんでした 。 このエラーは、署名付き XML に SSIS パッケージが予想どおりに含まれていない場合に発生します。|  
|0xC001403B|-1073659845|DTS_E_JAGGEDEVENTINFO|パラメーター名、型、および説明の配列の長さが異なります。 これらの配列の長さは同じにする必要があります。 このエラーは、配列の長さが一致しない場合に発生します。 各配列の各パラメーターに設定できるエントリは 1 つです。|  
|0xC001403C|-1073659844|DTS_E_GETPACKAGEINFOS|パッケージの列挙中に OLE DB エラー 0x%1!8.8X! (%2) が発生しました。 SQL ステートメントが発行されましたが失敗しました。|  
|0xC001403D|-1073659843|DTS_E_UNKNOWNLOGPROVIDERTYPE|ログ プロバイダー "%2" に指定されたログ プロバイダーの種類 "%1" は、有効なログ プロバイダーの種類として認識されません。 このエラーは、不明な種類のログ プロバイダーを作成しようとした場合に発生します。 ログ プロバイダーの種類の名前が、正しいスペルになっていることを確認してください。|  
|0xC001403E|-1073659842|DTS_E_UNKNOWNLOGPROVIDERTYPENOSUBS|ログ プロバイダーの種類は、有効なログ プロバイダーの種類として認識されません。 このエラーは、不明な種類のログ プロバイダーを作成しようとした場合に発生します。 ログ プロバイダーの種類の名前が、正しいスペルになっていることを確認してください。|  
|0xC001403F|-1073659841|DTS_E_UNKNOWNCONNECTIONMANAGERTYPENOSUBS|接続マネージャーに指定されている接続の種類が、有効な接続マネージャーの種類ではありません。 このエラーは、接続の種類が不明な接続マネージャーを作成しようとした場合に発生します。 接続の種類の名前の綴りを確認してください。|  
|0xC0014040|-1073659840|DTS_E_PACKAGEREMOVEFAILED|SQL Server からパッケージ "%1" を削除中にエラーが発生しました。|  
|0xC0014042|-1073659838|DTS_E_FOLDERADDFAILED|"%1" という名前の SQL Server で、フォルダー "%2" にフォルダーを作成中にエラーが発生しました。|  
|0xC0014043|-1073659837|DTS_E_CREATEFOLDERONSQLSERVER_OLEDB|CreateFolderOnSQLServer メソッドで OLE DB エラー コード 0x%1!8.8X! (%2) が検出されました。 発行された SQL ステートメントは失敗しました。|  
|0xC0014044|-1073659836|DTS_E_FOLDERRENAMEFAILED|SQL Server にある " %1\\\\%2" というフォルダーの名前を "%1\\\\%3" に変更中にエラーが発生しました。|  
|0xC0014045|-1073659835|DTS_E_RENAMEFOLDERONSQLSERVER_OLEDB|RenameFolderOnSQLServer メソッドで OLE DB エラー コード 0x%1!8.8X! (%2) が検出されました。 発行された SQL ステートメントは失敗しました。|  
|0xC0014046|-1073659834|DTS_E_FOLDERDELETEFAILED|SQL Server フォルダー "%1" を削除中にエラーが発生しました。|  
|0xC0014047|-1073659833|DTS_E_REMOVEFOLDERFROMSQLSERVER_OLEDB|RemoveFolderOnSQLServer メソッドで OLE DB エラー コード 0x%1!8.8X! (%2) が検出されました。 発行された SQL ステートメントは失敗しました。|  
|0xC0014048|-1073659832|DTS_E_INVALIDPATHTOPACKAGE|指定されたパッケージ パスにパッケージ名が含まれていません。 このエラーは、パスに円記号またはスラッシュがまったく含まれていない場合に発生します。|  
|0xC0014049|-1073659831|DTS_E_FOLDERNOTFOUND|フォルダー "%1" が見つかりません。|  
|0xC001404A|-1073659830|DTS_E_FINDFOLDERONSQLSERVER_OLEDB|SQL のフォルダーを検索中に、OLE DB エラーが発生し、エラー コード 0x%1!8.8X! (%2) が検出されました。|  
|0xC001404B|-1073659829|DTS_E_OPENLOGFAILED|SSIS ログ記録プロバイダーは、ログを開けませんでした。 エラー コード:0x%1!8.8X!。|  
|0xC001404C|-1073659828|DTS_E_GETCONNECTIONINFOS|エラー 0x%1!8.8X! "%2" により、ConnectionInfos コレクションを取得できませんでした 。 このエラーは、IDTSApplication100::get_ConnectionInfos への呼び出しが失敗した場合に発生します。|  
|0xC001404D|-1073659827|DTS_E_VARIABLEDEADLOCK|変数をロックしようとしたときに、デッドロックが検出されました。 16 回試行しましたがロックを取得できません。 ロックはタイムアウトしました。|  
|0xC001404E|-1073659826|DTS_E_NOTDISPENSED|VariableDispenser から Variables コレクションが返されませんでした。 ディスペンサーで管理されているコレクションのみで許可されている操作が試行されました。|  
|0xC001404F|-1073659825|DTS_E_VARIABLESALREADYUNLOCKED|この Variables コレクションのロックは既に解除されています。 ディスペンサーで管理されている Variables コレクションでは、Unlock メソッドが 1 回だけ呼び出されます。|  
|0xC0014050|-1073659824|DTS_E_VARIABLEUNLOCKFAILED|1 つ以上の変数のロックを解除できませんでした。|  
|0xC0014051|-1073659823|DTS_E_DISPENSEDREADONLY|Variables コレクションは VariableDispenser から返されましたが、変更できません。 ディスペンサーで管理されているコレクションに対して、項目を追加または削除することはできません。|  
|0xC0014052|-1073659822|DTS_E_VARIABLEALREADYONREADLIST|変数 "%1" は読み取り一覧に既に存在します。 変数は、読み取りロック一覧または書き込みロック一覧に一度だけ追加できます。|  
|0xC0014053|-1073659821|DTS_E_VARIABLEALREADYONWRITELIST|変数 "%1" は書き込み一覧に既に存在します。 変数は、読み取りロック一覧または書き込みロック一覧に一度だけ追加できます。|  
|0xC0014054|-1073659820|DTS_E_LOCKVARIABLEFORREAD|エラー 0x%2!8.8X! "%3" により、読み取りアクセス用の変数 "%1" をロックできませんでした 。|  
|0xC0014055|-1073659819|DTS_E_LOCKVARIABLEFORWRITE|エラー 0x%2!8.8X! "%3" により、読み取り/書き込みアクセス用の変数 "%1" をロックできませんでした 。|  
|0xC0014056|-1073659818|DTS_E_CUSTOMEVENTCONFLICT|カスタム イベント "%1" は、別のパラメーター リストで既に宣言されています。 タスクにより、異なるパラメーター リストで別のタスクが既に宣言されているカスタム イベントを宣言しようとしています。|  
|0xC0014057|-1073659817|DTS_E_EVENTHANDLERNOTALLOWED|カスタム イベント "%1" が指定されているタスクでは、パッケージ内でこのイベントを処理できません。 このカスタム イベントは、AllowEventHandlers が False に指定された状態で宣言されました。|  
|0xC0014059|-1073659815|DTS_E_UNSAFEVARIABLESALREADYSET|VariableDispenser が安全ではない Variables コレクションを受け取りました。 この操作を繰り返すことはできません。|  
|0xC001405A|-1073659814|DTS_E_INVALIDPARENTPACKAGEPATH|GetPackagePath が ForEachEnumerator で呼び出されましたが、ForEachLoop パッケージ パスが指定されていませんでした。|  
|0xC001405B|-1073659813|DTS_E_VARIABLEDEADLOCK_READ|読み取りアクセス用の変数 "%1" をロックしようとしたときに、デッドロックが検出されました。 16 回試行しましたがロックを取得できなかったため、ロックはタイムアウトしました。|  
|0xC001405C|-1073659812|DTS_E_VARIABLEDEADLOCK_READWRITE|読み取り/書き込みアクセス用の変数 "%1" をロックしようとしたときに、デッドロックが検出されました。 16 回試行しましたがロックを取得できなかったため、 ロックはタイムアウトしました。|  
|0xC001405D|-1073659811|DTS_E_VARIABLEDEADLOCK_BOTH|読み取りアクセス用の変数 "%1" と読み取り/書き込みアクセス用の変数 "%2" をロックしようとしたときに、デッドロックが検出されました。 16 回試行しましたがロックを取得できなかったため、 ロックはタイムアウトしました。|  
|0xC001405E|-1073659810|DTS_E_PACKAGEPASSWORDEMPTY|パッケージの保護レベルではパスワードが必要ですが、PackagePassword プロパティが空です。|  
|0xC001405F|-1073659809|DTS_E_DECRYPTXML_PASSWORD|XML ノードの暗号化解除または暗号化に失敗しました。パスワードが指定されなかったか、正しくありませんでした。 暗号化された情報を読み込まずに、パッケージの読み込みが続行されます。|  
|0xC0014060|-1073659808|DTS_E_DECRYPTPACKAGE_USERKEY|ユーザー キーで暗号化されたパッケージの暗号化を解除できませんでした。 別のユーザーがこのパッケージを暗号化したか、パッケージが保存されたときのコンピューターが使用されていません。|  
|0xC0014061|-1073659807|DTS_E_SERVERSTORAGEDISALLOWED|この保存先に保存する場合は、保護レベル ServerStorage を使用できません。 保存先にセキュリティで保護されたストレージ機能があることを確認できませんでした。|  
|0xC0014062|-1073659806|DTS_E_LOADFROMSQLSERVER|LoadFromSQLServer メソッドが失敗しました。|  
|0xC0014063|-1073659805|DTS_E_SIGNATUREPOLICYVIOLATION|デジタル署名の状態が署名ポリシーに違反しているのでパッケージを読み込めません。 エラー 0x%1!8.8X! "%2"|  
|0xC0014064|-1073659804|DTS_E_SIGNATURENOTPRESENT|パッケージが署名されていません。|  
|0xC0014065|-1073659803|DTS_E_SQLPROFILERDLL_ONLY_X86|SQL Server Profiler のログ プロバイダーは、pfclnt.dll を読み込めませんでした。このプロバイダーは、32 ビット システムでのみサポートされています。|  
|0xC0014100|-1073659648|DTS_E_NAMEALREADYADDED|同じ名前のオブジェクトがコレクション内に既に存在するので、オブジェクトを追加できません。 このエラーを解決するには、別の名前を指定してください。|  
|0xC0014101|-1073659647|DTS_E_NAMEALREADYEXISTS|同じ名前のオブジェクトが既にコレクション内に存在するので、オブジェクト名を "%1" から "%2" に変更できません。 このエラーを解決するには、別の名前を指定してください。|  
|0xC0014103|-1073659645|DTS_E_FAILEDDEPENDENCIES|パッケージの依存関係を列挙中にエラーが発生しました。 詳細については、他のメッセージを確認してください。|  
|0xC0014104|-1073659644|DTS_E_INVALIDCHECKPOINT_TRANSACTION|現在のパッケージ設定はサポートされていません。  SaveCheckpoints プロパティまたは TransactionOption プロパティを変更してください。|  
|0xC001410E|-1073659634|DTS_E_CONNECTIONMANAGERJOINTRANSACTION|接続マネージャーは、トランザクションから参加解除できませんでした。|  
|0xC0015001|-1073655807|DTS_E_BPDUPLICATE|指定されたブレークポイント ID は既に存在します。 このエラーは、タスクが同じ ID で CreateBreakpoint を複数回呼び出した場合に発生します。 タスクが最初に作成したブレークポイントで RemoveBreakpoint を呼び出してから 2 つ目のブレークポイントを作成すると、同じ ID でブレークポイントが複数回作成される可能性があります。|  
|0xC0015002|-1073655806|DTS_E_BPUNKNOWNID|指定されたブレークポイント ID が存在しません。 このエラーは、存在しないブレークポイントをタスクが参照した場合に発生します。|  
|0xC0015004|-1073655804|DTS_E_CANTWRITETOFILE|書き込み用にファイル "%1" を開けませんでした。 ファイルが読み取り専用であるか、適切な権限がありません。|  
|0xC0015005|-1073655803|DTS_E_NOROWSETRETURNED|結果行セットがこのクエリの実行に関連付けられていません。 結果が正しく指定されていません。|  
|0xC0015105|-1073655547|DTS_E_DUMP_FAILED|デバッグ ダンプ ファイルを正しく生成できませんでした。 hresult は 0x%1!8.8X! です。|  
|0xC0016001|-1073651711|DTS_E_INVALIDURL|指定された URL が無効です。 このエラーは、サーバーまたはプロキシの URL に NULL が指定されたか、または URL の形式が正しくない場合に発生する可能性があります。 有効な URL 形式は、 https://ServerName:Port/ResourcePath または https://ServerName:Port/ResourcePath です。|  
|0xC0016002|-1073651710|DTS_E_INVALIDSCHEME|指定された URL %1 が無効です。 このエラーは、http または https 以外の構成が指定されたか、または URL の形式が正しくない場合に発生する可能性があります。 有効な URL 形式は、 https://ServerName:Port/ResourcePath または https://ServerName:Port/ResourcePath です。|  
|0xC0016003|-1073651709|DTS_E_WINHTTPCANNOTCONNECT|サーバー %1 への接続を確立できません。 このエラーは、サーバーが存在しない場合、またはプロキシの設定が正しくない場合に発生する可能性があります。|  
|0xC0016004|-1073651708|DTS_E_CONNECTIONTERMINATED|サーバーとの接続がリセットされたか、終了しました。 後で再試行してください。|  
|0xC0016005|-1073651707|DTS_E_LOGINFAILURE|%1 のログインに失敗しました。 このエラーは、指定されたログイン資格情報が正しくない場合に発生します。 ログイン資格情報を確認してください。|  
|0xC0016006|-1073651706|DTS_E_INVALIDSERVERNAME|URL %1 で指定されたサーバー名を解決できません。|  
|0xC0016007|-1073651705|DTS_E_PROXYAUTH|プロキシ認証が失敗しました。 このエラーは、ログイン資格情報を入力していない場合、または資格情報が正しくない場合に発生します。|  
|0xC0016008|-1073651704|DTS_E_SECUREFAILURE|サーバーから取得した SSL 証明書の応答が無効です。 要求を処理できません。|  
|0xC0016009|-1073651703|DTS_E_TIMEOUT|要求がタイムアウトしました。このエラーは、指定したタイムアウト値が小さすぎる場合や、サーバーまたはプロキシへの接続を確立できなかった場合に発生する可能性があります。 サーバーとプロキシの URL が正しいことを確認してください。|  
|0xC001600A|-1073651702|DTS_E_CLIENTAUTH|クライアント証明書がありません。 このエラーは、サーバーで SSL クライアント証明書が必要とされているときに、ユーザーが無効な証明書を指定したか、または証明書を指定しなかった場合に発生します。 この接続用にクライアント証明書を構成する必要があります。|  
|0xC001600B|-1073651701|DTS_E_REDIRECTFAILURE|指定されたサーバーの URL %1 にはリダイレクトが含まれていますが、リダイレクトの要求に失敗しました。|  
|0xC001600C|-1073651700|DTS_E_SERVERAUTH|サーバー認証が失敗しました。 このエラーは、ログイン資格情報を入力していない場合、または資格情報が正しくない場合に発生します。|  
|0xC001600D|-1073651699|DTS_E_WINHTTPUNKNOWNERROR|要求を処理できません。 後で再試行してください。|  
|0xC001600E|-1073651698|DTS_E_UNKNOWNSTATUSCODE|サーバーが状態コード %1!u!: %2 を返しました。 : %2 を返しました。 このエラーは、サーバーで問題が発生したときに発生します。|  
|0xC001600F|-1073651697|DTS_E_WINHTTPNOTSUPPORTED|このプラットフォームは、WinHttp サービスによってサポートされていません。|  
|0xC0016010|-1073651696|DTS_E_INVALIDTIMEOUT|タイムアウト値が無効です。 タイムアウトは %1!d! 秒から %2!d! 秒までの範囲内で、 秒単位で 指定する必要があります。|  
|0xC0016011|-1073651695|DTS_E_INVALIDCHUNKSIZE|チャンク サイズが無効です。 Chunksize プロパティは %1!d! から %2!d! までの範囲内で、 秒単位で 指定する必要があります。|  
|0xC0016012|-1073651694|DTS_E_CERTERROR|クライアント証明書を処理中にエラーが発生しました。 このエラーは、指定されたクライアント証明書が個人証明書ストアに見つからなかった場合に発生する可能性があります。 クライアント証明書が有効であることを確認してください。|  
|0xC0016013|-1073651693|DTS_E_FORBIDDEN|サーバーからエラー コード "403 - アクセス不可" が返されました。 このエラーは、"https" によるアクセスが必要な指定リソースにアクセスしたときに証明書の有効期限が終了している場合、要求した使用法に対して有効でない証明書が使用されている場合、または証明書が失効しているか失効を確認できない場合に発生する可能性があります。|  
|0xC0016014|-1073651692|DTS_E_WINHTTPOPEN|プロキシ "%1" で HTTP セッションを初期化できませんでした。 このエラーは、無効なプロキシが指定された場合に発生する可能性があります。 HTTP 接続マネージャーは CERN 型のプロキシのみをサポートしています。|  
|0xC0016015|-1073651691|DTS_E_OPENCERTSTORE|証明書ストアを開くときにエラーが発生しました。|  
|0xC0016016|-1073651690|DTS_E_UNPROTECTXMLFAILED|エラー 0x%2!8.8X! "%3" により、保護された XML ノード "%1" の暗号化を解除できませんでした 。 この情報にアクセスする権限がない可能性があります。 このエラーは、暗号化エラーが発生した場合に発生します。 正しいキーが使用可能であることを確認してください。|  
|0xC0016017|-1073651689|DTS_E_UNPROTECTCONNECTIONSTRINGFAILED|エラー 0x%2!8.8X! "%3" により、サーバー "%1" の保護された接続文字列の暗号化を解除できませんでした 。 この情報にアクセスする権限がない可能性があります。 このエラーは、暗号化エラーが発生した場合に発生します。 正しいキーが使用可能であることを確認してください。|  
|0xC0016018|-1073651688|DTS_E_NEGATIVEVERSION|バージョン番号には負の値を指定できません。 このエラーは、パッケージの VersionMajor、VersionMinor、または VersionBuild プロパティが負の値に設定されている場合に発生します。|  
|0xC0016019|-1073651687|DTS_E_PACKAGEMIGRATED|読み込み中に、パッケージがより新しいバージョンに移行されました。 処理を完了するには、パッケージを再読み込みする必要があります。 これは内部エラー コードです。|  
|0xC0016020|-1073651680|DTS_E_PACKAGEMIGRATIONFAILED|エラー 0x%3!8.8X! "%4" により、 パッケージを バージョン %1!d! から %2!d! に 移行できませんでした。|  
|0xC0016021|-1073651679|DTS_E_PACKAGEMIGRATIONMODULELOAD|パッケージ移行モジュールが読み込みに失敗しました。|  
|0xC0016022|-1073651678|DTS_E_PACKAGEMIGRATIONMODULE|パッケージ移行モジュールが失敗しました。|  
|0xC0016023|-1073651677|DTS_E_CANTDETERMINEWHICHPROPTOPERSIST|既定の永続性を使用してオブジェクトを永続化できません。 このエラーは、既定の永続性で、ホストされたオブジェクトに存在するオブジェクトを特定できない場合に発生します。|  
|0xC0016024|-1073651676|DTS_E_CANTADDREMOVEWHENEXECUTING|ランタイム モードでパッケージに要素を追加、またはパッケージから要素を削除できませんでした。 このエラーは、パッケージの実行中に、コレクションにオブジェクトを追加、またはコレクションからオブジェクトを削除しようとした場合に発生します。|  
|0xC0016025|-1073651675|DTS_E_NODENOTFOUND|カスタムの既定の永続性で "%1" ノードが見つかりません。 このエラーは、拡張可能なオブジェクトの既定の保存済み XML が変更され、保存したオブジェクトが見つからなくなった場合に発生します。または、拡張可能なオブジェクト自体が変更された場合に発生します。|  
|0xC0016026|-1073651674|DTS_E_COLLECTIONLOCKED|パッケージの検証中または実行中にこのコレクションを変更することはできません。|  
|0xC0016027|-1073651673|DTS_E_COLLOCKED|パッケージの検証中または実行中に "%1" コレクションを変更することはできません。 "%2" はこのコレクションに追加できません。|  
|0xC0016029|-1073651671|DTS_E_FTPNOTCONNECTED|FTP サーバーとの接続が確立されていません。|  
|0xC001602A|-1073651670|DTS_E_FTPERROR|要求された FTP 操作でエラーが発生しました。 エラーの詳細説明: %1。|  
|0xC001602B|-1073651669|DTS_E_FTPINVALIDRETRIES|再試行回数が無効です。 再試行回数には、%1!d! から %2!d! までの値を指定する必要があります。 指定する必要があります。|  
|0xC001602C|-1073651668|DTS_E_LOADWININET|FTP 接続マネージャーが機能するためには、次の DLL が必要です: %1。|  
|0xC001602D|-1073651667|DTS_E_FTPINVALIDCONNECTIONSTRING|接続文字列で指定されたポートが無効です。 ConnectionString の形式は ServerName:Port です。 ポートには、%1!d! から %2!d! までの整数値を 指定する必要があります。|  
|0xC001602E|-1073651666|DTS_E_FTPCREATEFOLDER|フォルダー "%1" を作成しています... %2。|  
|0xC001602F|-1073651665|DTS_E_FTPDELETEFOLDER|フォルダー "%1" を削除しています... %2。|  
|0xC0016030|-1073651664|DTS_E_FTPCHANGEFOLDER|現在のディレクトリを "%1" に変更しています。 %2。|  
|0xC0016031|-1073651663|DTS_E_FTPFILESEMPTY|転送するファイルがありません。 このエラーは、送信操作または受信操作を実行したときに、転送用に指定されたファイルがない場合に発生する可能性があります。|  
|0xC0016032|-1073651662|DTS_E_FTPINVALIDLOCALPATH|指定したローカル パスは無効です。 有効なローカル パスを指定してください。 このエラーは、指定したローカル パスが NULL の場合に発生する可能性があります。|  
|0xC0016033|-1073651661|DTS_E_FTPNOFILESTODELETE|削除するファイルが指定されていません。|  
|0xC0016034|-1073651660|DTS_E_WINHTTPCERTDECODE|証明書の読み込み中に内部エラーが発生しました。 このエラーは、証明書のデータが無効である場合に発生します。|  
|0xC0016035|-1073651659|DTS_E_WINHTTPCERTENCODE|証明書のデータを保存中に内部エラーが発生しました。|  
|0xC0016049|-1073651639|DTS_E_CHECKPOINTMISMATCH|チェックポイント ファイル "%1" がこのパッケージに一致しません。 パッケージの ID とチェックポイント ファイルの ID が一致していません。|  
|0xC001604A|-1073651638|DTS_E_CHECKPOINTFILEALREADYEXISTS|既存のチェックポイント ファイルが見つかりましたが、このパッケージ用ではないコンテンツが含まれています。そのため、このファイルを上書きして、新しいチェックポイントの保存を開始することはできません。 既存のチェックポイント ファイルを削除してから再試行してください。 このエラーは、チェックポイント ファイルが存在し、パッケージが、チェックポイント ファイルを使用せず、チェックポイントを保存するように設定されている場合に発生します。 既存のチェックポイント ファイルは上書きされません。|  
|0xC001604B|-1073651637|DTS_E_CHECKPOINTFILELOCKED|チェックポイント ファイル "%1" が別のプロセスによってロックされています。 このエラーは、このパッケージの別のインスタンスが現在実行中である場合に発生します。|  
|0xC001604C|-1073651636|DTS_E_OPENCHECKPOINTFILE|エラー 0x%2!8.8X! "%3" により、チェックポイント ファイル "%1" を開けませんでした 。|  
|0xC001604D|-1073651635|DTS_E_CREATECHECKPOINTFILE|エラー 0x%2!8.8X!"%3" により、チェックポイント ファイル "%1" を作成できませんでした 。|  
|0xC0016050|-1073651632|DTS_E_FTPINVALIDPORT|FTP ポートに無効な値が含まれています。 FTP ポートの値には、%1!d! から %2!d! までの整数値を 指定する必要があります。|  
|0xC00160AA|-1073651542|DTS_E_CONNECTTOSERVERFAILED|コンピューター "%1" の SSIS サービスに接続できませんでした:<br /><br /> %2。|  
|0xC0017002|-1073647614|DTS_E_PROPERTYEXPRESSIONSDISABLEDONVARIABLES|Expression プロパティは Variable オブジェクトでサポートされていません。 代わりに、EvaluateAsExpression プロパティを使用してください。|  
|0xC0017003|-1073647613|DTS_E_PROPERTYEXPRESSIONEVAL|プロパティ "%2" の式 "%1" を評価できません。 有効な式に変更してください。|  
|0xC0017004|-1073647612|DTS_E_PROPERTYEXPRESSIONSET|プロパティ "%2" の式 "%1" の結果をそのプロパティに書き込めません。 式は評価されましたが、プロパティに設定できません。|  
|0xC0017005|-1073647611|DTS_E_FORLOOPEVALEXPRESSIONINVALID|ループの評価式が無効です。 式を変更する必要があります。 関連するエラー メッセージが表示されます。|  
|0xC0017006|-1073647610|DTS_E_EXPRESSIONNOTBOOLEAN|式 "%1" は、True または False に評価される必要があります。 評価結果がブール値になるように式を変更してください。|  
|0xC0017007|-1073647609|DTS_E_FORLOOPHASNOEXPRESSION|評価するループの式がありません。 このエラーは、For ループの式が空の場合に発生します。 式を追加してください。|  
|0xC0017008|-1073647608|DTS_E_FORLOOPASSIGNEXPRESSIONINVALID|ループの代入式が無効であるため、式を変更する必要があります。 関連するエラー メッセージが表示されます。|  
|0xC0017009|-1073647607|DTS_E_FORLOOPINITEXPRESSIONINVALID|ループの初期化式が無効であるため、式を変更する必要があります。 関連するエラー メッセージが表示されます。|  
|0xC001700A|-1073647606|DTS_E_INVALIDVERSIONNUMBER|パッケージに含まれるバージョン番号が無効です。 バージョン番号を現在のバージョン番号より大きくすることはできません。|  
|0xC001700C|-1073647604|DTS_E_INVALIDVERNUMCANTBENEGATIVE|パッケージに含まれるバージョン番号が無効です。 バージョン番号が負の値です。|  
|0xC001700D|-1073647603|DTS_E_PACKAGEUPDATEDISABLED|パッケージの形式が古いバージョンですが、パッケージ形式の自動アップグレードは無効になっています。|  
|0xC001700E|-1073647602|DTS_E_EXPREVALTRUNCATIONASERROR|式の評価中に切り捨てが発生しました。|  
|0xC0019001|-1073639423|DTS_E_FAILEDSETEXECVALVARIABLE|ラッパーが ExecutionValueVariable プロパティに指定された変数の値を設定できませんでした。|  
|0xC0019004|-1073639420|DTS_E_VARIABLEEXPRESSIONERROR|変数 "%1" の式を評価できませんでした。 式にエラーがありました。|  
|0xC0019305|-1073638651|DTS_E_UNSUPPORTEDSQLVERSION|試行された操作は、このデータベース バージョンではサポートされていません。|  
|0xC001A003|-1073635325|DTS_E_TXNSPECINVALID|保持されている接続が使用されている場合、トランザクションを指定できません。 このエラーは、接続マネージャーで Retain が True に設定されているにもかかわらず、AcquireConnection が NULL 以外のトランザクション パラメーターを使用して呼び出された場合に発生します。|  
|0xC001A004|-1073635324|DTS_E_INCOMPATIBLETRANSACTIONCONTEXT|保持されている接続で互換性のないトランザクション コンテキストが指定されました。 この接続は別のトランザクション コンテキストで確立されています。 保持されている接続は 1 つのトランザクション コンテキストのみで使用できます。|  
|0xC001B001|-1073631231|DTS_E_NOTSUSPENDED|パッケージが中断されていないため、Resume を呼び出せませんでした。 このエラーは、クライアントが Resume を呼び出したときにパッケージが中断されていない場合に発生します。|  
|0xC001B002|-1073631230|DTS_E_ALREADYEXECUTING|実行可能ファイルが既に実行中であるため、Execute を呼び出せませんでした。 このエラーは、前回の Execute 呼び出しにより実行可能ファイルが継続して実行されているコンテナーで、クライアントが Execute を呼び出した場合に発生します。|  
|0xC001B003|-1073631229|DTS_E_NOTEXECUTING|実行可能ファイルが実行されていないか、または最上位の実行可能ファイルではないため、Suspend または Resume の呼び出しに失敗しました。 このエラーは、Execute 呼び出しが現在処理中ではない実行可能ファイルで、クライアントが Suspend または Resume を呼び出した場合に発生します。|  
|0xC001C002|-1073627134|DTS_E_INVALIDFILE|For Each File 列挙子に指定されたファイルが無効です。 For Each File 列挙子に指定されたファイルが存在することを確認してください。|  
|0xC001C010|-1073627120|DTS_E_VALUEINDEXNOTINTEGER|値インデックスが整数ではありません。 For Each 変数番号 %1!d! を変数 "%2" に マッピングしています。|  
|0xC001C011|-1073627119|DTS_E_VALUEINDEXNEGATIVE|値インデックスが負の値です 変数 "%2" への ForEach 変数マッピング番号 %1!d! です。|  
|0xC001C012|-1073627118|DTS_E_FOREACHVARIABLEMAPPING|ForEach 変数マッピング番号 %1!d! を 変数 "%2" に適用できません。|  
|0xC001C013|-1073627117|DTS_E_OBJECTNOTINFOREACHLOOP|ForEachLoop コンテナーの直接の子ではない ForEachPropertyMapping にオブジェクトを追加しているときにエラーが発生しました。|  
|0xC001F001|-1073614847|DTS_E_FAILEDSYSTEMVARIABLEREMOVE|システム変数を削除できませんでした。 このエラーは、必要な変数を削除しようとした場合に発生します。  必要な変数は、タスクとランタイムの間の通信を行うためにランタイムで作成される変数です。|  
|0xC001F002|-1073614846|DTS_E_CHANGESYSTEMVARIABLEREADONLYFAILED|システム変数なので、変数のプロパティを変更できませんでした。 システム変数は読み取り専用です。|  
|0xC001F003|-1073614845|DTS_E_CHANGESYSTEMVARIABLENAMEFAILED|システム変数なので、変数の名前を変更できませんでした。 システム変数は読み取り専用です。|  
|0xC001F004|-1073614844|DTS_E_CHANGESYSTEMVARIABLENAMESPACEFAILED|システム変数なので、変数の名前空間を変更できませんでした。 システム変数は読み取り専用です。|  
|0xC001F006|-1073614842|DTS_E_EVENTHANDLERNAMEREADONLY|イベント ハンドラー名を変更できませんでした。 イベント ハンドラー名は読み取り専用です。|  
|0xC001F008|-1073614840|DTS_E_PATHUNKNOWN|オブジェクトへのパスを取得できません。 これはシステム エラーです。|  
|0xC001F009|-1073614839|DTS_E_RUNTIMEVARIABLETYPECHANGE|変数 "%1" に代入されている値の型が、現在の変数の型と異なります。 変数の型は実行中に変更できません。 変数の型は厳密に一致している必要があります。ただし、オブジェクト型の変数は除きます。|  
|0xC001F010|-1073614832|DTS_E_INVALIDSTRING|文字列に無効な文字が含まれています: "%1"。 このエラーは、印刷できない文字を含む文字列がプロパティ値に指定された場合に発生します。|  
|0xC001F011|-1073614831|DTS_E_INVALIDOBJECTNAME|SSIS オブジェクト名が無効です。 名前付けの問題が的確に説明された、より具体的なエラーが発生している可能性があります。|  
|0xC001F021|-1073614815|DTS_E_PROPERTYREADONLY|プロパティ "%1" は読み取り専用です。 このエラーは、読み取り専用のプロパティを変更しようとした場合に発生します。|  
|0xC001F022|-1073614814|DTS_E_FAILEDGETTYPEINFO|オブジェクトでは、型情報がサポートされていません。 このエラーは、ランタイムがオブジェクトから型情報を取得して、プロパティのコレクションを設定しようとした場合に発生します。  オブジェクトでは型情報がサポートされている必要があります。|  
|0xC001F023|-1073614813|DTS_E_FAILEDPROPERTYGET|プロパティ "%1" の値を取得中に、エラーが発生しました。 エラー コードは 0x%2!8.8X! です。|  
|0xC001F024|-1073614812|DTS_E_FAILEDPROPERTYGET_ERRORINFO|プロパティ "%1" の値を取得中に、エラーが発生しました。 エラー コードは 0x%2!8.8X! 。|  
|0xC001F025|-1073614811|DTS_E_FAILEDPROPERTYSET|プロパティ "%1" の値を設定中に、エラーが発生しました。 返されたエラーは 0x%2!8.8X! です。|  
|0xC001F026|-1073614810|DTS_E_FAILEDPROPERTYSET_ERRORINFO|プロパティ "%1" の値を設定中に、エラーが発生しました。 返されたエラーは 0x%2!8.8X! 。|  
|0xC001F027|-1073614809|DTS_E_PROPERTYWRITEONLY|プロパティ "%1" は書き込み専用です。 このエラーは、プロパティ オブジェクトを使用してプロパティの値を取得しようとしたときに、そのプロパティが書き込み専用である場合に発生します。|  
|0xC001F028|-1073614808|DTS_E_NODISPATCH|オブジェクトには IDispatch インターフェイスが実装されていません。 このエラーは、プロパティ オブジェクトまたはプロパティのコレクションでオブジェクトの IDispatch インターフェイスにアクセスしようとした場合に発生します。|  
|0xC001F029|-1073614807|DTS_E_NOCONTAININGTYPELIB|オブジェクトのタイプ ライブラリを取得できません。 このエラーは、プロパティのコレクションで IDispatch インターフェイスによりオブジェクトのタイプ ライブラリを取得しようとした場合に発生します。|  
|0xC001F02A|-1073614806|DTS_E_INVALIDTASKMONIKER|XML からタスクを作成できません。タスク " %1!s!"、型 " %2!s!"。 エラー: 0x%3!8.8X! " %4!s!"。|  
|0xC001F02C|-1073614804|DTS_E_FAILEDCREATEXMLDOCUMENT|XML ドキュメント "%1" を作成できませんでした。|  
|0xC001F02D|-1073614803|DTS_E_PMVARPROPTYPESDIFFERENT|型の異なる変数からプロパティへのプロパティ マッピングが存在したため、エラーが発生しました。 プロパティの型は変数の型と一致する必要があります。|  
|0xC001F02E|-1073614802|DTS_E_PMINVALIDPROPMAPTARGET|プロパティ マッピングで、サポートされていないオブジェクト型を対象に設定しようとしました。 このエラーは、サポートされていないオブジェクト型をプロパティ マッピングに渡した場合に発生します。|  
|0xC001F02F|-1073614801|DTS_E_COULDNOTRESOLVEPACKAGEPATH|パッケージ "%1" のオブジェクトへのパッケージ パスを解決できません。  パッケージ パスが有効であることを確認してください。|  
|0xC001F030|-1073614800|DTS_E_PMNODESTPROPERTY|プロパティ マッピングの変換先プロパティが空です。 変換先プロパティの名前を設定してください。|  
|0xC001F031|-1073614799|DTS_E_INVALIDPROPERTYMAPPINGSFOUND|パッケージで、少なくとも 1 つのプロパティ マッピングを復元できませんでした。|  
|0xC001F032|-1073614798|DTS_E_AMBIGUOUSVARIABLENAME|この名前を持つ複数の変数が、異なる名前空間に存在するため、変数名があいまいになります。 名前空間で修飾された名前を指定して、変数名があいまいにならないようにしてください。|  
|0xC001F033|-1073614797|DTS_E_DESTINATIONOBJECTPARENTLESS|プロパティ マッピングの変換先オブジェクトには親オブジェクトがありません。 変換先オブジェクトはどのコンテナーの子オブジェクトでもありません。 パッケージから削除された可能性があります。|  
|0xC001F036|-1073614794|DTS_E_INVALIDPROPERTYMAPPING|プロパティ マッピングが無効です。 マッピングは無視されました。|  
|0xC001F038|-1073614792|DTS_E_PMFAILALERTREMOVE|プロパティ マッピングの警告時のエラー。プロパティ マッピングの対象を削除しています。|  
|0xC001F03A|-1073614790|DTS_E_INVALIDFOREACHPROPERTYMAPPING|For Each ループで見つかったプロパティ マッピングが無効です。 このエラーは、For Each プロパティ マッピングの復元に失敗した場合に発生します。|  
|0xC001F040|-1073614784|DTS_E_PMPROPERTYINVALID|プロパティ マッピングで、無効な変換先プロパティが指定されました。 このエラーは、変換先オブジェクトに、そのオブジェクトで見つからないプロパティが指定された場合に発生します。|  
|0xC001F041|-1073614783|DTS_E_INVALIDTASKMONIKERNOPARAM|XML からタスクを作成できません。 このエラーは、ランタイムがタスクを作成するための名前を解決できない場合に発生します。 名前が正しいことを確認してください。|  
|0xC001F080|-1073614720|DTS_E_COULDNOTREPLACECHECKPOINTFILE|既存のチェックポイント ファイルを、更新されたチェックポイント ファイルに置き換えることができません。 チェックポイントは一時ファイルに正常に作成されましたが、既存のファイルを新しいファイルに置き換えることができませんでした。|  
|0xC001F081|-1073614719|DTS_E_CHECKPOINTFILENOTSPECIFIED|パッケージは常にチェックポイントから再開するように構成されていますが、チェックポイント ファイルが指定されていません。|  
|0xC001F082|-1073614718|DTS_E_CHECKPOINTLOADXML|エラー 0x%2!8.8X!"%3" により、XML チェックポイント ファイル "%1" を読み込めませんでした 。 指定されたファイル名が正しいこと、およびそのファイルが存在することを確認してください。|  
|0xC001F083|-1073614717|DTS_E_LOADCHECKPOINT|チェックポイント ファイルを読み込めないのでパッケージを実行できませんでした。 これ以上のパッケージの実行にはチェックポイント ファイルが必要です。 このエラーは、通常、CheckpointUsage プロパティが ALWAYS に設定されている場合に発生します。この設定は、パッケージが常にチェックポイントから再開されるように指定されていることを意味します。|  
|0xC001F185|-1073614459|DTS_E_NOEVALEXPRESSION|For ループの評価条件式 "%1" が空です。 For ループにはブール型の評価式が必要です。|  
|0xC001F186|-1073614458|DTS_E_EXPREVALASSIGNMENTTYPEMISMATCH|代入式 "%1" の結果を、代入先の変数と互換性のある型に変換できません。|  
|0xC001F187|-1073614457|DTS_E_EXPREVALASSIGNMENTTOREADONLYVARIABLE|代入式の読み取り専用の変数 "%1"を使用中にエラーが発生しました。 この変数は読み取り専用なので、式の結果を代入することはできません。 書き込み可能な変数を選択するか、この変数から式を削除してください。|  
|0xC001F188|-1073614456|DTS_E_EXPREVALASSIGNMENTVARIABLELOCKFORWRITEFAILED|変数 "%2" が存在しないか、または書き込みアクセスができないため、式 "%1" を評価できません。 変数が見つからなかったか、または書き込みアクセス用にロックできなかったので、式の結果は変数に代入されません。|  
|0xC001F189|-1073614455|DTS_E_EXPREVALRESULTTYPENOTSUPPORTED|式 "%1" の結果の型 "%2" を、サポートされている型に変換できません。|  
|0xC001F18A|-1073614454|DTS_E_EXPREVALRESULTTYPECONVERSIONFAILED|エラー コード 0x%3!8.8X! により、式 "%1" の結果を型 "%2" からサポートされている型に変換できませんでした。 型変換はサポートされていますが、ランタイム エンジンで式の結果をサポートされている型に変換しようとしたときに、予期しないエラーが発生しました。|  
|0xC001F200|-1073614336|DTS_E_DTSNAME_NOTNULL|オブジェクト名が無効です。 名前を NULL にすることはできません。|  
|0xC001F201|-1073614335|DTS_E_DTSNAME_NOTEMPTY|オブジェクト名が無効です。 名前を空にすることはできません。|  
|0xC001F202|-1073614334|DTS_E_DTSNAME_LEGAL|オブジェクト名 "%1" は無効です。 名前には次のどの文字も含めることができません: / \ : [ ] . =|  
|0xC001F203|-1073614333|DTS_E_DTSNAME_PRINTABLE|オブジェクト名 "%1" は無効です。 名前の印刷が不可能になる制御文字を含めることはできません。|  
|0xC001F204|-1073614332|DTS_E_DTSNAME_NOLEADWHITESP|オブジェクト名 "%1" は無効です。 名前の先頭を空白にすることはできません。|  
|0xC001F205|-1073614331|DTS_E_DTSNAME_NOTRAILWHITESP|オブジェクト名 "%1" は無効です。 名前の末尾を空白にすることはできません。|  
|0xC001F206|-1073614330|DTS_E_DTSNAME_BEGINSWITHALPHA|オブジェクト名 "%1" は無効です。 名前の先頭は英文字にする必要があります。|  
|0xC001F207|-1073614329|DTS_E_DTSNAME_BEGINSWITHALPHAUNDERBAR|オブジェクト名 "%1" は無効です。 名前の先頭は英文字またはアンダースコア "_" にする必要があります。|  
|0xC001F208|-1073614328|DTS_E_DTSNAME_ALPHADIGITUNDERBAR|オブジェクト名 "%1" は無効です。 名前には英数字またはアンダースコア "_" のみを指定する必要があります。|  
|0xC001F209|-1073614327|DTS_E_DTSNAME_VALIDFILENAME|オブジェクト名 "%1" は無効です。 名前には次のどの文字も含めることができません: / \ : ? " < > &#124;|  
|0xC001F420|-1073613792|DTS_E_FAILLOADINGPROPERTY|既定の永続性を使用して値プロパティ "%1" を読み込めませんでした。|  
|0xC001F422|-1073613790|DTS_E_NODELISTENUM_INVALIDCONNMGRTYPE|接続マネージャー "%1" の種類は "%2" ではありません|  
|0xC001F423|-1073613789|DTS_E_NODELISTENUM_XPATHISEMPTY|"%1" が空です|  
|0xC001F424|-1073613788|DTS_E_NODELISTENUM_INVALIDDATANODE|ノード一覧の列挙子セクションに無効なデータ ノードがあります|  
|0xC001F425|-1073613787|DTS_E_NODELISTENUM_NOENUMERATORCREATED|列挙子を作成できません|  
|0xC001F427|-1073613785|DTS_E_OPERATIONFAILCACHEINUSE|キャッシュが使用中のため、操作は失敗しました。|  
|0xC001F428|-1073613784|DTS_E_PROPERTYCANNOTBEMODIFIED|プロパティは変更できません。|  
|0xC001F429|-1073613783|DTS_E_PACKAGEUPGRADEFAILED|パッケージのアップグレードに失敗しました。|  
|0xC00220DE|-1073602338|DTS_E_TKEXECPACKAGE_UNABLETOLOADFILE|エラー 0x%1!8.8X! がパッケージ ファイル "%3" の読み込み中に発生しました。 %2。|  
|0xC00220DF|-1073602337|DTS_E_TKEXECPACKAGE_UNSPECIFIEDPACKAGE|パッケージが指定されていません。|  
|0xC00220E0|-1073602336|DTS_E_TKEXECPACKAGE_UNSPECIFIEDCONNECTION|接続が指定されていません。|  
|0xC00220E2|-1073602334|DTS_E_TKEXECPACKAGE_INCORRECTCONNECTIONMANAGERTYPE|接続マネージャー "%1" は、サポートされていない種類 "%2" です。 ファイル接続マネージャーおよび OLE DB 接続マネージャーのみがサポートされています。|  
|0xC00220E3|-1073602333|DTS_E_TKEXECPACKAGE_UNABLETOLOADXML|エラー 0x%1!8.8X! がパッケージ ファイル "%3" を XML ドキュメントに読み込み中に発生しました。 %2。|  
|0xC00220E4|-1073602332|DTS_E_TKEXECPACKAGE_UNABLETOLOAD|エラー 0x%1!8.8X! がパッケージの読み込みを準備中に発生しました。 %2。|  
|0xC0024102|-1073594110|DTS_E_TASKVALIDATIONFAILED|タスクの Validate メソッドが失敗し、エラー コード 0x%1!8.8X! (%2) が検出されました。 タスクの Validate メソッドが成功し、"out" パラメーターを使用して結果が示される必要があります。|  
|0xC0024104|-1073594108|DTS_E_TASKEXECUTEFAILED|タスクの Execute メソッドが失敗し、エラー コード 0x%1!8.8X! (%2) が検出されました。 タスクの Execute メソッドは成功し、"out" パラメーターを使用して結果が示される必要があります。|  
|0xC0024105|-1073594107|DTS_E_RETRIEVINGDEPENDENCIES|タスク "%1" で依存関係を取得中にエラー 0x%2!8.8X! が 発生しました。 エラーが発生したとき、ランタイムがタスクの依存関係のコレクションから依存関係を取得しようとしていました。 タスクにより、いずれかの依存関係のインターフェイスが正しく実装されなかった可能性があります。|  
|0xC0024107|-1073594105|DTS_E_TASKVALIDATIONERROR|タスクの検証中にエラーが発生しました。|  
|0xC0024108|-1073594104|DTS_E_CONNECTIONSTRINGFORMAT|接続文字列の形式が無効です。 セミコロンで区切った X=Y という形式が 1 つ以上含まれている必要があります。 このエラーは、データベース接続マネージャーに、コンポーネントを持たない接続文字列が設定されている場合に発生します。|  
|0xC0024109|-1073594103|DTS_E_UNQUOTEDSEMICOLON|接続文字列コンポーネントには、引用符で囲まれていないセミコロンを含めることはできません。 値にセミコロンを含める必要がある場合は、値全体を引用符で囲みます。 このエラーは、InitialCatalog プロパティなどの接続文字列の値に引用符で囲まれていないセミコロンが含まれている場合に発生します。|  
|0xC002410A|-1073594102|DTS_E_LOGPROVIDERVALIDATIONFAILED|1 つ以上のログ プロバイダーの検証に失敗しました。 パッケージを実行できません。 ログ プロバイダーによる検証が失敗した場合、パッケージは実行されません。|  
|0xC002410B|-1073594101|DTS_E_INVALIDVALUEINARRAY|配列内の値が無効です。|  
|0xC002410C|-1073594100|DTS_E_ENUMERATIONELEMENTNOTENUMERABLE|ForEach 列挙子から返された列挙子の要素が IEnumerator を実装していません。ForEach 列挙子の CollectionEnumerator プロパティと矛盾しています。|  
|0xC002410D|-1073594099|DTS_E_INVALIDENUMERATORINDEX|列挙子はインデックス "%1!d!" で要素を取得できませんでした。|  
|0xC0029100|-1073573632|DTS_E_AXTASK_MISSING_ENTRY_METHOD_NAME|関数が見つかりませんでした。|  
|0xC0029101|-1073573631|DTS_E_AXTASK_EMPTY_SCRIPT|関数が見つかりませんでした。|  
|0xC0029102|-1073573630|DTS_E_AXTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|ActiveX スクリプト タスクは正しくない XML 要素を使用して開始されました。|  
|0xC0029105|-1073573627|DTS_E_AXTASK_HANDLER_NOT_FOUND|ハンドラーが見つかりませんでした。|  
|0xC0029106|-1073573626|DTS_E_AXTASKUTIL_ENUMERATE_LANGUAGES_FAILED|システムにインストールされているスクリプト言語を取得中にエラーが発生しました。|  
|0xC0029107|-1073573625|DTS_E_AXTASKUTIL_SCRIPTHOST_CREATE_FAILED|ActiveX スクリプト ホストを作成中にエラーが発生しました。 スクリプト ホストが正しくインストールされていることを確認してください。|  
|0xC0029108|-1073573624|DTS_E_AXTASKUTIL_SCRIPTHOSTINIT_FAILED|選択した言語のスクリプト ホストのインスタンスを作成中にエラーが発生しました。 選択したスクリプト言語がシステムにインストールされていることを確認してください。|  
|0xC0029109|-1073573623|DTS_E_AXTASKUTIL_ADDVARIABLES_FAILED|SSIS 変数をスクリプト ホストの名前空間に追加中にエラーが発生しました。 これにより、タスクでスクリプト内の SSIS 変数が使用されない可能性があります。|  
|0xC002910A|-1073573622|DTS_E_AXTASKUTIL_SCRIPT_PARSING_FAILED|スクリプト テキストを解析中に致命的なエラーが発生しました。 選択した言語のスクリプト エンジンが正しくインストールされていることを確認してください。|  
|0xC002910B|-1073573621|DTS_E_AXTASKUTIL_MSG_BAD_FUNCTION|入力した関数名が無効です。 有効な関数名を指定したかどうかを確認してください。|  
|0xC002910C|-1073573620|DTS_E_AXTASKUTIL_EXECUTION_FAILED|スクリプトを実行中にエラーが発生しました。 選択した言語のスクリプト エンジンが正しくインストールされていることを確認してください。|  
|0xC002910D|-1073573619|DTS_E_AXTASKUTIL_ADDTYPELIB_FAILED|マネージド タイプ ライブラリをスクリプト ホストに追加中にエラーが発生しました。 DTS 2000 ランタイムがインストールされていることを確認してください。|  
|0xC002910E|-1073573618|DTS_E_BITASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|正しくない XML 要素を使用して、一括挿入タスクが開始されました。|  
|0xC002910F|-1073573617|DTS_E_BITASK_DATA_FILE_NOT_SPECIFIED|データ ファイル名が指定されていません。|  
|0xC0029110|-1073573616|DTS_E_BITASK_HANDLER_NOT_FOUND|ハンドラーが見つかりませんでした。|  
|0xC0029111|-1073573615|DTS_E_BITASK_CANNOT_ACQUIRE_CONNECTION|指定された接続を取得できませんでした: "%1"。|  
|0xC0029112|-1073573614|DTS_E_BITASK_NO_CONNECTION_MANAGER_SPECIFIED|接続マネージャーを取得できませんでした。|  
|0xC0029113|-1073573613|DTS_E_BITASK_INVALID_CONNECTION|接続が無効です。|  
|0xC0029114|-1073573612|DTS_E_BITASK_NULL_CONNECTION|接続が NULL です。|  
|0xC0029115|-1073573611|DTS_E_BITASK_EXECUTE_FAILED|実行に失敗しました。|  
|0xC0029116|-1073573610|DTS_E_BITASK_CANNOT_RETRIEVE_TABLES|データベースからテーブルを取得中にエラーが発生しました。|  
|0xC0029117|-1073573609|DTS_E_BITASK_CANNOT_RETRIEVE_COLUMN_INFO|テーブルの列を取得中にエラーが発生しました。|  
|0xC0029118|-1073573608|DTS_E_BITASK_ERROR_IN_DB_OPERATION|データベース操作でエラーが発生しました。|  
|0xC0029119|-1073573607|DTS_E_BITASK_INVALIDSOURCECONNECTIONNAME|指定された接続 "%1" は無効であるか、無効なオブジェクトを参照しています。 続行するには、有効な接続を指定してください。|  
|0xC002911A|-1073573606|DTS_E_BITASK_INVALIDDESTCONNECTIONNAME|対象になる接続の指定が無効です。 続行するには、有効な接続を指定してください。|  
|0xC002911B|-1073573605|DTS_E_BITASK_DESTINATION_TABLE_NOT_SPECIFIED|続行するには、テーブル名を指定する必要があります。|  
|0xC002911C|-1073573604|DTS_E_BITASK_ERROR_IN_LOAD_FROM_XML|LoadFromXML のタグ "%1" でエラーが発生しました。|  
|0xC002911D|-1073573603|DTS_E_BITASK_ERROR_IN_SAVE_TO_XML|SaveToXML のタグ "%1" でエラーが発生しました。|  
|0xC002911E|-1073573602|DTS_E_BITASKUNMANCONNECTION_INVALID_CONNECTION|接続が無効です。|  
|0xC002911F|-1073573601|DTS_E_BITASKUNMANCONNECTION_EXECUTE_FAILED|実行に失敗しました。|  
|0xC0029120|-1073573600|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_TABLES|データベースからテーブルを取得中にエラーが発生しました。|  
|0xC0029121|-1073573599|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_COLUMN_INFO|テーブルの列を取得中にエラーが発生しました。|  
|0xC0029122|-1073573598|DTS_E_BITASKUNMANCONNECTION_CANNOT_OPEN_FILE|データ ファイルを開こうとして、エラーが発生しました。|  
|0xC0029123|-1073573597|DTS_E_BITASKUNMANCONNECTION_OEM_CONVERSION_FAILED|指定された形式に入力 OEM ファイルを変換できません。|  
|0xC0029124|-1073573596|DTS_E_BITASKUNMANCONNECTION_ERROR_IN_DB_OPERATION|データベース操作でエラーが発生しました。|  
|0xC0029125|-1073573595|DTS_E_DTSPROCTASK_NOCONNECTIONSPECIFIED|接続マネージャーが指定されていません。|  
|0xC0029126|-1073573594|DTS_E_DTSPROCTASK_CONNECTIONMANAGERNOTOLAP|接続 "%1" は Analysis Services 接続ではありません。|  
|0xC0029127|-1073573593|DTS_E_DTSPROCTASK_UNABLETOLOCATECONNECTIONMANAGER|接続 "%1" が見つかりません。|  
|0xC0029128|-1073573592|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEEXE|Analysis Services DDL 実行タスクに無効なタスク データ ノードが返されました。|  
|0xC0029129|-1073573591|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEPROC|Analysis Services 処理タスクに無効なタスク データ ノードが返されました。|  
|0xC002912A|-1073573590|DTS_E_DTSPROCTASK_INVALIDDDL|DDL が無効です。|  
|0xC002912B|-1073573589|DTS_E_DTSPROCTASK_INVALIDDDLPROCESSINGCOMMANDS|ProcessingCommands の DDL が無効です。|  
|0xC002912C|-1073573588|DTS_E_DTSPROCTASK_CANNOTWRITEINAREADONLYVARIABLE|実行結果を読み取り専用の変数に保存することはできません。|  
|0xC002912D|-1073573587|DTS_E_DTSPROCTASK_INVALIDVARIABLE|変数 "%1" は定義されていません。|  
|0xC002912E|-1073573586|DTS_E_DTSPROCTASK_CONNECTIONNOTFOUND|接続マネージャー "%1" は定義されていません。|  
|0xC002912F|-1073573585|DTS_E_DTSPROCTASK_INVALIDCONNECTION|接続マネージャー "%1" は FILE 接続マネージャーではありません。|  
|0xC0029130|-1073573584|DTS_E_DTSPROCTASK_NONEXISTENTATTRIBUTE|シリアル化解除中に "%1" が見つかりませんでした。|  
|0xC0029131|-1073573583|DTS_E_DTSPROCTASK_TRACEHASBEENSTOPPED|例外が発生したため、トレースは停止しました。|  
|0xC0029132|-1073573582|DTS_E_DTSPROCTASK_DDLEXECUTIONFAILED|DDL を実行できませんでした。|  
|0xC0029133|-1073573581|DTS_E_DTSPROCTASK_FILEDOESNOTEXIST|接続 "%1" に関連付けられたファイルがありません。|  
|0xC0029134|-1073573580|DTS_E_DTSPROCTASK_VARIABLENOTDEFINED|変数 "%1" が定義されていません。|  
|0xC0029135|-1073573579|DTS_E_DTSPROCTASK_FILECONNECTIONNOTDEFINED|ファイル接続 "%1" が定義されていません。|  
|0xC0029136|-1073573578|DTS_E_EXEC2000PKGTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|DTS 2000 パッケージ実行タスクが正しくない XML 要素を使用して開始されています。|  
|0xC0029137|-1073573577|DTS_E_EXEC2000PKGTASK_HANDLER_NOT_FOUND|ハンドラーが見つかりませんでした。|  
|0xC0029138|-1073573576|DTS_E_EXEC2000PKGTASK_PACKAGE_NAME_NOT_SPECIFIED|パッケージ名が指定されていません。|  
|0xC0029139|-1073573575|DTS_E_EXEC2000PKGTASK_PACKAGE_ID_NOT_SPECIFIED|パッケージ ID が指定されていません。|  
|0xC002913A|-1073573574|DTS_E_EXEC2000PKGTASK_PACKAGE_VERSIONGUID_NOT_SPECIFIED|パッケージ バージョン GUID が指定されていません。|  
|0xC002913B|-1073573573|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_SPECIFIED|SQL Server が指定されていません。|  
|0xC002913C|-1073573572|DTS_E_EXEC2000PKGTASK_SQL_USERNAME_NOT_SPECIFIED|SQL Server ユーザー名が指定されていません。|  
|0xC002913D|-1073573571|DTS_E_EXEC2000PKGTASK_FILE_NAME_NOT_SPECIFIED|ストレージ ファイル名が指定されていません。|  
|0xC002913E|-1073573570|DTS_E_EXEC2000PKGTASK_DTS2000CANTBEEMPTY|DTS 2000 パッケージ プロパティが空です。|  
|0xC002913F|-1073573569|DTS_E_EXEC2000PKGTASK_ERROR_IN_PACKAGE_EXECUTE|DTS 2000 パッケージの実行中にエラーが発生しました。|  
|0xC0029140|-1073573568|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_AVAILABLE_NETWORK|使用できる SQL Server をネットワークから読み込めません。 ネットワーク接続を確認してください。|  
|0xC0029141|-1073573567|DTS_E_EXEC2000PKGTASK_DATATYPE_NULL|データ型を NULL にすることはできません。 値の検証に使用できる正しいデータ型を指定してください。|  
|0xC0029142|-1073573566|DTS_E_EXEC2000PKGTASK_NULL_VALUE|どのデータ型に対しても NULL を有効値とすることはできません。|  
|0xC0029143|-1073573565|DTS_E_EXEC2000PKGTASK_NULL_VALUE_ARGUMENT|必須の引数が NULL です。|  
|0xC0029144|-1073573564|DTS_E_EXEC2000PKGTASK_CLS_NOT_REGISTRED_EXCEPTION|DTS 2000 パッケージ タスクを実行するには、SQL Server セットアップを起動し、[インストールするコンポーネント] ページの [詳細設定] を使用して、[レガシ コンポーネント] を選択します。|  
|0xC0029145|-1073573563|DTS_E_EXEC2000PKGTASK_NOT_PRIMITIVE_TYPE|"%1" は値の型ではありません。|  
|0xC0029146|-1073573562|DTS_E_EXEC2000PKGTASK_CONVERT_FAILED|"%1" を "%2" に変換できませんでした。|  
|0xC0029147|-1073573561|DTS_E_EXEC2000PKGTASK_ERROR_IN_VALIDATE|"%1" を "%2" に対して検証できませんでした。|  
|0xC0029148|-1073573560|DTS_E_EXEC2000PKGTASK_ERROR_IN_LOAD_FROM_XML|LoadFromXML のタグ "%1" でエラーが発生しました。|  
|0xC0029149|-1073573559|DTS_E_EXEC2000PKGTASK_ERROR_IN_SAVE_TO_XML|SaveToXML のタグ "%1" でエラーが発生しました。|  
|0xC002914A|-1073573558|DTS_E_EXECPROCTASK_INVALIDTIMEOUT|指定されたタイムアウト値は無効です。 タスクでプロセスの実行を許可する時間を秒単位で指定してください。 タイムアウトの最小値は 0 です。これは、タイムアウト値を使用せず、プロセスを最後またはエラーが発生するまで実行することを示します。 タイムアウトの最大値は 2147483 (((2^31) - 1)/1000) です。|  
|0xC002914B|-1073573557|DTS_E_EXECPROCTASK_CANTREDIRECTIO|タスクの有効期間が切れても処理を続行できる場合、ストリームをリダイレクトできません。|  
|0xC002914C|-1073573556|DTS_E_EXECPROCTASK_PROCESSHASTIMEDOUT|プロセスがタイムアウトしました。|  
|0xC002914D|-1073573555|DTS_E_EXECPROCTASK_EXECUTABLENOTSPECIFIED|実行可能ファイルが指定されていません。|  
|0xC002914E|-1073573554|DTS_E_EXECPROCTASK_STDOUTVARREADONLY|標準的な外部変数は読み取り専用です。|  
|0xC002914F|-1073573553|DTS_E_EXECPROCTASK_STDERRVARREADONLY|標準的なエラー変数は読み取り専用です。|  
|0xC0029150|-1073573552|DTS_E_EXECPROCTASK_RECEIVEDINVALIDTASKDATANODE|プロセス実行タスクは無効なタスク データ ノードを受け取りました。|  
|0xC0029151|-1073573551|DTS_E_EXECPROCTASK_PROCESSEXITCODEEXCEEDS|"%1" で "%2" "%3" を実行中のプロセス終了コードは "%4" でしたが、予期されたコードは "%5" でした。|  
|0xC0029152|-1073573550|DTS_E_EXECPROCTASK_WORKINGDIRDOESNOTEXIST|ディレクトリ "%1" が存在しません。|  
|0xC0029153|-1073573549|DTS_E_EXECPROCTASK_FILEDOESNOTEXIST|ファイル/プロセス "%1" がディレクトリ "%2" に存在しません。|  
|0xC0029154|-1073573548|DTS_E_EXECPROCTASK_FILENOTINPATH|ファイル/プロセス "%1" がパス上にありません。|  
|0xC0029156|-1073573546|DTS_E_EXECPROCTASK_WORKINGDIRECTORYDOESNOTEXIST|作業ディレクトリ "%1" が存在しません。|  
|0xC0029157|-1073573545|DTS_E_EXECPROCTASK_ERROREXECUTIONVALUE|プロセスはリターン コード "%1" で終了しましたが、 想定されていたのは "%2" です。|  
|0xC0029158|-1073573544|DTS_E_FSTASK_SYNCFAILED|同期オブジェクトが失敗しました。|  
|0xC0029159|-1073573543|DTS_E_FSTASK_INVALIDDATA|ファイル システム タスクは無効なタスク データ ノードを受け取りました。|  
|0xC002915A|-1073573542|DTS_E_FSTASK_DIRECTORYEXISTS|このディレクトリは既に存在します。|  
|0xC002915B|-1073573541|DTS_E_FSTASK_PATHNOTVALID|"%1" は操作の種類 "%2" では無効です。|  
|0xC002915C|-1073573540|DTS_E_FSTASK_DESTINATIONNOTSET|操作 "%1" の対象になるプロパティが設定されていません。|  
|0xC002915D|-1073573539|DTS_E_FSTASK_SOURCENOTSET|操作 "%1" の基になるプロパティが設定されていません。|  
|0xC002915E|-1073573538|DTS_E_FSTASK_CONNECTIONTYPENOTFILE|接続 "%1" の種類はファイルではありません。|  
|0xC002915F|-1073573537|DTS_E_FSTASK_VARIABLEDOESNTEXIST|変数 "%1" が存在しません。|  
|0xC0029160|-1073573536|DTS_E_FSTASK_VARIABLENOTASTRING|変数 "%1" は文字列ではありません。|  
|0xC0029163|-1073573533|DTS_E_FSTASK_FILEDOESNOTEXIST|接続 "%2" によって示されているファイルまたはディレクトリ "%1" が存在しません。|  
|0xC0029165|-1073573531|DTS_E_FSTASK_DESTCONNUSAGETYPEINVALID|対象になるファイル接続マネージャー "%1" に無効な使用法の種類 "%2" が設定されています。|  
|0xC0029166|-1073573530|DTS_E_FSTASK_SRCCONNUSAGETYPEINVALID|基になるファイル接続マネージャー "%1" に無効な使用法の種類 "%2" が設定されています。|  
|0xC0029167|-1073573529|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATION|FileSystemOperation|  
|0xC0029168|-1073573528|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATIONDESC|ファイル システム操作に関する情報を提供します。|  
|0xC0029169|-1073573527|DTS_E_FSTASK_TASKDISPLAYNAME|ファイル システム タスク|  
|0xC002916A|-1073573526|DTS_E_FSTASK_TASKDESCRIPTION|ファイルのコピーや削除などのファイル システム操作を実行します。|  
|0xC002916B|-1073573525|DTS_E_FTPTASK_SYNCOBJFAILED|同期オブジェクトが失敗しました。|  
|0xC002916C|-1073573524|DTS_E_FTPTASK_UNABLETOOBTAINFILELIST|ファイルの一覧を取得できません。|  
|0xC002916D|-1073573523|DTS_E_FTPTASK_LOCALPATHEMPTY|ローカル パスが空です。|  
|0xC002916E|-1073573522|DTS_E_FTPTASK_REMOTEPATHEMPTY|リモート パスが空です。|  
|0xC002916F|-1073573521|DTS_E_FTPTASK_LOCALVARIBALEEMPTY|ローカル変数が空です。|  
|0xC0029170|-1073573520|DTS_E_FTPTASK_REMOTEVARIBALEEMPTY|リモート変数が空です。|  
|0xC0029171|-1073573519|DTS_E_FTPTASK_FTPRCVDINVLDDATANODE|FTP タスクは無効なタスク データ ノードを受け取りました。|  
|0xC0029172|-1073573518|DTS_E_FTPTASK_CONNECTION_NAME_NULL|接続が空です。 有効な FTP 接続が指定されていることを確認してください。|  
|0xC0029173|-1073573517|DTS_E_FTPTASK_CONNECTION_NOT_FTP|指定された接続は FTP 接続ではありません。 有効な FTP 接続が指定されていることを確認してください。|  
|0xC0029175|-1073573515|DTS_E_FTPTASK__INITIALIZATION_WITH_NULL_XML_ELEMENT|XML 要素が NULL であるタスクを初期化できません。|  
|0xC0029176|-1073573514|DTS_E_FTPTASK_SAVE_TO_NULL_XML_ELEMENT|NULL の XML ドキュメントにタスクを保存できません。|  
|0xC0029177|-1073573513|DTS_E_FTPTASK_ERROR_IN_LOAD_FROM_XML|LoadFromXML のタグ "%1" でエラーが発生しました。|  
|0xC0029178|-1073573512|DTS_E_FTPTASK_NOFILESATLOCATION|"%1" にファイルが存在しません。|  
|0xC0029179|-1073573511|DTS_E_FTPTASK_LOCALVARIABLEISEMPTY|変数 "%1" が空です。|  
|0xC002917A|-1073573510|DTS_E_FTPTASK_REMOTEVARIABLEISEMPTY|変数 "%1" が空です。|  
|0xC002917B|-1073573509|DTS_E_FTPTASK_NOFILESINCONNMGR|ファイル "%1" にファイル パスが指定されていません。|  
|0xC002917C|-1073573508|DTS_E_FTPTASK_NOFILEPATHSINLOCALVAR|変数 "%1" にファイル パスが格納されていません。|  
|0xC002917D|-1073573507|DTS_E_FTPTASK_VARIABLENOTASTRING|変数 "%1" は文字列ではありません。|  
|0xC002917E|-1073573506|DTS_E_FTPTASK_VARIABLENOTFOUND|変数 "%1" が存在しません。|  
|0xC002917F|-1073573505|DTS_E_FTPTASK_INVALIDPATHONOPERATION|操作 "%1" のパスが無効です。|  
|0xC0029180|-1073573504|DTS_E_FTPTASK_DIRECTORYEXISTS|"%1" は既に存在します。|  
|0xC0029182|-1073573502|DTS_E_FTPTASK_CONNECTIONTYPENOTFILE|接続 "%1" の種類はファイルではありません。|  
|0xC0029183|-1073573501|DTS_E_FTPTASK_FILEDOESNOTEXIST|"%1" によって示されているファイルが存在しません。|  
|0xC0029184|-1073573500|DTS_E_FTPTASK_INVALIDDIRECTORY|変数 "%1" にディレクトリが指定されていません。|  
|0xC0029185|-1073573499|DTS_E_FTPTASK_NOFILESFOUND|"%1" にファイルが見つかりません。|  
|0xC0029186|-1073573498|DTS_E_FTPTASK_NODIRECTORYPATHINCONMGR|ファイル接続マネージャー "%1" にディレクトリが指定されていません。|  
|0xC0029187|-1073573497|DTS_E_FTPTASK_UNABLETODELETELOCALEFILE|ローカル ファイル "%1" を削除できません。|  
|0xC0029188|-1073573496|DTS_E_FTPTASK_UNABLETOREMOVELOCALDIRECTORY|ローカル ディレクトリ "%1" を削除できません。|  
|0xC0029189|-1073573495|DTS_E_FTPTASK_UNABLETOCREATELOCALDIRECTORY|ローカル ディレクトリ "%1" を作成できません。|  
|0xC002918A|-1073573494|DTS_E_FTPTASK_UNABLETORECEIVEFILES|"%1" を使用してファイルを受け取れません。|  
|0xC002918B|-1073573493|DTS_E_FTPTASK_UNABLETOSENDFILES|"%1" を使用してファイルを送信できません。|  
|0xC002918C|-1073573492|DTS_E_FTPTASK_UNABLETOMAKEDIRREMOTE|"%1" を使用してリモート ディレクトリを作成できません。|  
|0xC002918D|-1073573491|DTS_E_FTPTASK_UNABLETOREMOVEDIRREMOTE|"%1" を使用してリモート ディレクトリを削除できません。|  
|0xC002918E|-1073573490|DTS_E_FTPTASK_UNABLETODELETEREMOTEFILES|"%1" を使用してリモート ファイルを削除できません。|  
|0xC002918F|-1073573489|DTS_E_FTPTASK_UNABLETOCONNECTTOSERVER|"%1" を使用して FTP サーバーに接続できません。|  
|0xC0029190|-1073573488|DTS_E_FTPTASK_INVALIDVARIABLEVALUE|変数 "%1" の先頭が "/" ではありません。|  
|0xC0029191|-1073573487|DTS_E_FTPTASK_INVALIDREMOTEPATH|リモート パス "%1" の先頭が "/" ではありません。|  
|0xC0029192|-1073573486|DTS_E_DTS_E_FTPTASK_CANNOT_ACQUIRE_CONNECTION|FTP 接続の取得中にエラーが発生しました。 指定した接続の種類 "%1" が有効かどうかを確認してください。|  
|0xC0029193|-1073573485|DTS_E_MSGQTASKUTIL_CERT_OPEN_STORE_FAILED|証明書ストアを開けませんでした。|  
|0xC0029194|-1073573484|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_DISPLAY_NAME|証明書の表示名を取得中にエラーが発生しました。|  
|0xC0029195|-1073573483|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_ISSUER_NAME|証明書の発行者名を取得中にエラーが発生しました。|  
|0xC0029196|-1073573482|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_FRIENDLY_NAME|証明書の表示名を取得中にエラーが発生しました。|  
|0xC0029197|-1073573481|DTS_E_MSMQTASK_NO_CONNECTION|MSMQ 接続名が設定されていません。|  
|0xC0029198|-1073573480|DTS_E_MSMQTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|タスクは正しくない XML 要素を使用して初期化されました。|  
|0xC0029199|-1073573479|DTS_E_MSMQTASK_DATA_FILE_NAME_EMPTY|データ ファイル名が空です。|  
|0xC002919A|-1073573478|DTS_E_MSMQTASK_DATA_FILE_SAVE_NAME_EMPTY|データ ファイルを保存するために指定された名前が空です。|  
|0xC002919B|-1073573477|DTS_E_MSMQTASK_DATA_FILE_SIZE_ERROR|ファイルのサイズは 4 MB 未満である必要があります。|  
|0xC002919C|-1073573476|DTS_E_MSMQTASK_DATA_FILE_SAVE_FAILED|データ ファイルを保存できませんでした。|  
|0xC002919D|-1073573475|DTS_E_MSMQTASK_STRING_COMPARE_VALUE_MISSING|文字列のフィルター値が空です。|  
|0xC002919E|-1073573474|DTS_E_MSMQTASK_INVALID_QUEUE_PATH|キューのパスが無効です。|  
|0xC002919F|-1073573473|DTS_E_MSMQTASK_NOT_TRANSACTIONAL|このメッセージ キュー タスクでは、分散トランザクションへの参加がサポートされていません。|  
|0xC00291A0|-1073573472|DTS_E_MSMQTASK_INVALID_MESSAGE_TYPE|メッセージ型が無効です。|  
|0xC00291A1|-1073573471|DTS_E_MSMQTASK_TASK_TIMEOUT|メッセージ キューがタイムアウトしました。メッセージは受信されませんでした。|  
|0xC00291A2|-1073573470|DTS_E_MSMQTASK_INVALID_PROPERTY_VALUE|指定されたプロパティが無効です。 引数の型が正しいことを確認してください。|  
|0xC00291A3|-1073573469|DTS_E_MSMQTASK_MESSAGE_NON_AUTHENTICATED|メッセージが認証されていません。|  
|0xC00291A4|-1073573468|DTS_E_MSMQTASK_INVALID_ENCRYPTION_ALGO_WRAPPER|暗号化アルゴリズムの値を無効なオブジェクトで設定しようとしています。|  
|0xC00291A5|-1073573467|DTS_E_MSMQTASK_VARIABLE_TO_RECEIVE_STRING_MSG_EMPTY|文字列メッセージを受信するための変数が空です。|  
|0xC00291A6|-1073573466|DTS_E_MSMQTASK_RECEIVE_VARIABLE_EMPTY|変数メッセージを受信する変数が空です。|  
|0xC00291A7|-1073573465|DTS_E_MSMQTASK_CONNECTIONTYPENOTMSMQ|接続 "%1" の種類は MSMQ ではありません。|  
|0xC00291A8|-1073573464|DTS_E_MSMQTASK_DATAFILE_ALREADY_EXISTS|データ ファイル "%1" は指定した場所に既に存在します。 上書きオプションが False に設定されている場合はファイルを上書きできません。|  
|0xC00291A9|-1073573463|DTS_E_MSMQTASK_STRING_MSG_TO_VARIABLE_NOT_FOUND|文字列メッセージを受信するために指定された変数 "%1" が、パッケージ変数のコレクションに見つかりません。|  
|0xC00291AA|-1073573462|DTS_E_MSMQTASK_CONNMNGRNULL|接続マネージャー "%1" が空です。|  
|0xC00291AB|-1073573461|DTS_E_MSMQTASK_CONNMNGRDOESNOTEXIST|接続マネージャー "%1" が存在しません。|  
|0xC00291AC|-1073573460|DTS_E_SCRIPTTASK_COMPILEERRORMSG|エラー "%1": "%2"\r\n行 "%3"   列 "%4" ～ "%5"。|  
|0xC00291AD|-1073573459|DTS_E_SCRIPTTASK_COMPILEERRORMSG2|スクリプトのコンパイル中にエラーが発生しました: "%1"。|  
|0xC00291AE|-1073573458|DTS_E_SCRIPTTASK_COMPILEERRORMSG3|エラー "%1": "%2"\r\n行 "%3" 列 "%4" ～ "%5"\r\n行のテキスト: "%6"。|  
|0xC00291AF|-1073573457|DTS_E_SCRIPTTASK_SCRIPTREPORTEDFAILURE|ユーザー スクリプトでエラーが返されました。|  
|0xC00291B0|-1073573456|DTS_E_SCRIPTTASK_SCRIPTFILESFAILEDTOLOAD|ユーザー スクリプト ファイルを読み込むことができませんでした。|  
|0xC00291B1|-1073573455|DTS_E_SCRIPTTASK_SCRIPTTHREWEXCEPTION|ユーザー スクリプトで例外が返されました: "%1"。|  
|0xC00291B2|-1073573454|DTS_E_SCRIPTTASK_COULDNOTCREATEENTRYPOINTCLASS|エントリポイント クラス "%1" のインスタンスを作成できませんでした。|  
|0xC00291B3|-1073573453|DTS_E_SCRIPTTASK_LOADFROMXMLEXCEPTION|XML からスクリプト タスクを読み込み中に例外が発生しました: "%1"。|  
|0xC00291B4|-1073573452|DTS_E_SCRIPTTASK_SOURCEITEMNOTFOUNDEXCEPTION|ソース項目 "%1" がパッケージに見つかりませんでした。|  
|0xC00291B5|-1073573451|DTS_E_SCRIPTTASK_BINARYITEMNOTFOUNDEXCEPTION|バイナリ項目 "%1" がパッケージに見つかりませんでした。|  
|0xC00291B6|-1073573450|DTS_E_SCRIPTTASK_UNRECOGNIZEDSCRIPTLANGUAGEEXCEPTION|"%1" は有効なスクリプト言語として認識されませんでした。|  
|0xC00291B7|-1073573449|DTS_E_SCRIPTTASK_ILLEGALSCRIPTNAME|スクリプト名が無効です。 プロジェクト名に空白文字、スラッシュ、特殊文字を使用することはできません。また、数字で始まる名前も指定できません。|  
|0xC00291B8|-1073573448|DTS_E_SCRIPTTASK_INVALIDSCRIPTLANGUAGE|指定されたスクリプト言語は無効です。|  
|0xC00291B9|-1073573447|DTS_E_SCRIPTTASK_CANTINITNULLTASK|NULL タスクに初期化できません。|  
|0xC00291BA|-1073573446|DTS_E_SCRIPTTASK_MUSTINITWITHRIGHTTASK|スクリプト タスクのユーザー インターフェイスはスクリプト タスクに初期化する必要があります。|  
|0xC00291BB|-1073573445|DTS_E_SCRIPTTASK_WASNOTINITED|スクリプト タスクのユーザー インターフェイスは初期化されていません。|  
|0xC00291BC|-1073573444|DTS_E_SCRIPTTASK_HOST_NAME_CANT_EMPTY|名前を空にすることはできません。|  
|0xC00291BD|-1073573443|DTS_E_SCRIPTTASK_INVALID_SCRIPT_NAME|プロジェクト名が無効です。 プロジェクト名に空白文字、スラッシュ、特殊文字を使用することはできません。また、数字で始まる名前も指定できません。|  
|0xC00291BE|-1073573442|DTS_E_SCRIPTTASK_INVALID_SCRIPT_LANGUAGE|指定されたスクリプト言語は無効です。|  
|0xC00291BF|-1073573441|DTS_E_SCRIPTTASK_INVALID_ENTRY_POINT|エントリ ポイントが見つかりません。|  
|0xC00291C0|-1073573440|DTS_E_SCRIPTTASK_LANGUAGE_EMPTY|スクリプト言語が指定されていません。 有効なスクリプト言語が指定されていることを確認してください。|  
|0xC00291C1|-1073573439|DTS_E_SCRIPTTASK_INITIALIZATION_WITH_NULL_TASK|ユーザー インターフェイスの初期化。タスクが NULL です。|  
|0xC00291C2|-1073573438|DTS_E_SCRIPTTASK_UI_INITIALIZATION_WITH_WRONG_TASK|スクリプト タスクのユーザー インターフェイスが、正しくないタスクで初期化されています。|  
|0xC00291C3|-1073573437|DTS_E_SENDMAILTASK_RECIPIENT_EMPTY|受信者が指定されていません。|  
|0xC00291C4|-1073573436|DTS_E_SENDMAILTASK_SMTP_SERVER_NOT_SPECIFIED|簡易メール転送プロトコル (SMTP) サーバーが指定されていません。 SMTP サーバーの有効な名前または IP アドレスを指定してください。|  
|0xC00291C5|-1073573435|DTS_E_SENDMAILTASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|メール送信タスクは、正しくない XML 要素を使用して開始されています。|  
|0xC00291CB|-1073573429|DTS_E_SENDMAILTASK_INVALIDATTACHMENT|ファイル "%1" が存在しないか、このファイルにアクセスするための権限がありません。|  
|0xC00291CD|-1073573427|DTS_E_SENDMAILTASK_CHECK_VALID_SMTP_SERVER|指定した簡易メール転送プロトコル (SMTP) サーバーが有効であることを確認してください。|  
|0xC00291CE|-1073573426|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTFILE|接続 "%1" の種類は "File" ではありません。|  
|0xC00291CF|-1073573425|DTS_E_SENDMAILTASK_FILEDOESNOTEXIST|操作 "%1" にファイル "%2" が存在しません。|  
|0xC00291D0|-1073573424|DTS_E_SENDMAILTASK_VARIABLETYPEISNOTSTRING|変数 "%1" は文字列型ではありません。|  
|0xC00291D1|-1073573423|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTSMTP|接続 "%1" の種類は SMTP ではありません。|  
|0xC00291D2|-1073573422|DTS_E_SENDMAILTASK_CONNMNGRNULL|接続 "%1" が空です。|  
|0xC00291D3|-1073573421|DTS_E_SENDMAILTASK_NOCONNMNGR|指定された接続 "%1" が存在しません。|  
|0xC00291D4|-1073573420|DTS_E_SQLTASK_NOSTATEMENTSPECIFIED|Transact-SQL ステートメントが指定されていません。|  
|0xC00291D5|-1073573419|DTS_E_SQLTASK_NOXMLSUPPORT|この接続では、XML の結果セットがサポートされていません。|  
|0xC00291D6|-1073573418|DTS_E_SQLTASK_NOHANDLERFORCONNECTION|指定された接続の種類のハンドラーが見つかりません。|  
|0xC00291D7|-1073573417|DTS_E_SQLTASK_NOCONNECTIONMANAGER|接続マネージャーが指定されていません。|  
|0xC00291D8|-1073573416|DTS_E_SQLTASK_CANNOTACQUIRECONNMANAGER|接続マネージャーからの接続を取得できません。|  
|0xC00291D9|-1073573415|DTS_E_SQLTASK_NULLPARAMETERNAME|NULL のパラメーター名は指定できません。|  
|0xC00291DA|-1073573414|DTS_E_SQLTASK_INVALIDPARAMETERNAME|パラメーター名が無効です。|  
|0xC00291DB|-1073573413|DTS_E_SQLTASK_VALIDPARAMETERTYPES|有効なパラメーター名の型は Int または String です。|  
|0xC00291DC|-1073573412|DTS_E_SQLTASK_READONLYVARIABLE|変数 "%1" は読み取り専用なので、結果のバインドには使用できません。|  
|0xC00291DD|-1073573411|DTS_E_SQLTASK_INDESNOTINCOLLECTION|このコレクションにはインデックスが割り当てられていません。|  
|0xC00291DE|-1073573410|DTS_E_SQLTASK_ROVARINOUTPARAMETER|変数 "%1" は読み取り専用なので、パラメーターのバインドで "out" パラメーターまたは戻り値としては使用できません。|  
|0xC00291DF|-1073573409|DTS_E_SQLTASK_OBJECTNOTINCOLLECTION|このコレクションにはオブジェクトが存在しません。|  
|0xC00291E0|-1073573408|DTS_E_SQLTASK_UNABLETOACQUIREMANAGEDCONN|マネージド接続を取得できません。|  
|0xC00291E1|-1073573407|DTS_E_UNABLETOPOPRESULT|単一行の結果の種類に結果列を作成できません。 クエリから空の結果セットが返されました。|  
|0xC00291E2|-1073573406|DTS_E_SQLTASK_INVALIDNUMOFRESULTBINDINGS|ResultSetType に返された結果バインドの数が無効です: "%1"。|  
|0xC00291E3|-1073573405|DTS_E_SQLTASK_RESULTBINDTYPEFORROWSETXML|完全な結果セットおよび XML の結果に対する結果バインド名を 0 に設定する必要があります。|  
|0xC00291E4|-1073573404|DTS_E_SQLTASK_INVALIDEPARAMDIRECTIONFALG|パラメーター方向フラグが無効です。|  
|0xC00291E5|-1073573403|DTS_E_SQLTASK_NOSQLTASKDATAINXMLFRAGMENT|XML フラグメントに SQL タスク データが含まれていません。|  
|0xC00291E6|-1073573402|DTS_E_SQLTASK_MULTIPLERETURNVALUEPARAM|戻り値型のパラメーターが第 1 パラメーターではないか、戻り値型のパラメーターが複数あります。|  
|0xC00291E7|-1073573401|DTS_E_SQLTASK_CONNECTIONTYPENOTFILE|接続 "%1" はファイル接続マネージャーではありません。|  
|0xC00291E8|-1073573400|DTS_E_SQLTASK_FILEDOESNOTEXIST|"%1" によって示されているファイルが存在しません。|  
|0xC00291E9|-1073573399|DTS_E_SQLTASK_VARIABLETYPEISNOTSTRING|変数 "%1" は文字列型ではありません。|  
|0xC00291EA|-1073573398|DTS_E_SQLTASK_VARIABLENOTFOUND|変数 "%1" は存在しないか、ロックできませんでした。|  
|0xC00291EB|-1073573397|DTS_E_SQLTASK_CANNOTLOCATECONNMANAGER|接続マネージャー "%1" が存在しません。|  
|0xC00291EC|-1073573396|DTS_E_SQLTASK_FAILEDTOACQUIRECONNECTION|接続 "%1" を取得できませんでした。 接続が正しく構成されていないか、この接続に必要な権限が不足している可能性があります。|  
|0xC00291ED|-1073573395|DTS_E_SQLTASK_RESULTBYNAMENOTSUPPORTED|この接続の種類では、名前 "%1" による結果バインドはサポートされていません。|  
|0xC00291EE|-1073573394|DTS_E_SQLTASKCONN_ERR_NO_ROWS|結果セットの種類に単一行が指定されましたが、行が返されませんでした。|  
|0xC00291EF|-1073573393|DTS_E_SQLTASKCONN_ERR_NO_DISCONNECTED_RS|Transact-SQL ステートメントで、接続が切断されたレコードセットを使用できません。|  
|0xC00291F0|-1073573392|DTS_E_SQLTASKCONN_ERR_UNSUPPORTED_TYPE|サポートされていない型です。|  
|0xC00291F1|-1073573391|DTS_E_SQLTASKCONN_ERR_UNKNOWN_TYPE|不明な型です。|  
|0xC00291F2|-1073573390|DTS_E_SQLTASKCONN_ERR_PARAM_DATA_TYPE|パラメーター バインド \\"%s\\" でサポートされていないデータ型です。|  
|0xC00291F3|-1073573389|DTS_E_SQLTASKCONN_ERR_PARAM_NAME_MIX|パラメーター名に序数と名前付きの型を混在させることはできません。|  
|0xC00291F4|-1073573388|DTS_E_SQLTASKCONN_ERR_PARAM_DIR|パラメーター バインド \\"%s\\" のパラメーター方向が無効です。|  
|0xC00291F5|-1073573387|DTS_E_SQLTASKCONN_ERR_RESULT_DATA_TYPE|結果セットのバインド \\"%s\\" のデータ型はサポートされていません。|  
|0xC00291F6|-1073573386|DTS_E_SQLTASKCONN_ERR_RESULT_COL_INDEX|結果列インデックス %d が無効です。|  
|0xC00291F7|-1073573385|DTS_E_SQLTASKCONN_ERR_UNKNOWN_RESULT_COL|結果セットに列 \\"%s\\" が見つかりません。|  
|0xC00291F9|-1073573383|DTS_E_SQLTASKCONN_ERR_NOROWSET|結果行セットがこのクエリの実行に関連付けられていません。|  
|0xC00291FA|-1073573382|DTS_E_SQLTASKCONN_ERR_ODBC_DISCONNECTED|切断されているレコードセットは、ODBC 接続からは使用できません。|  
|0xC00291FB|-1073573381|DTS_E_SQLTASKCONN_ERR_RESULT_SET_DATA_TYPE|結果セットと列 %hd のデータ型はサポートされていません。|  
|0xC00291FC|-1073573380|DTS_E_SQLTASKCONN_ERR_CANT_LOAD_XML|クエリの結果を含む XML を読み込めません。|  
|0xC00291FD|-1073573379|DTS_E_TTGENTASK_NOCONNORVARIABLE|パッケージの接続名または変数名を指定する必要があります。|  
|0xC00291FE|-1073573378|DTS_E_TTGENTASK_FAILEDCREATE|パッケージの作成に失敗しました。|  
|0xC00291FF|-1073573377|DTS_E_TTGENTASK_BADTABLEMETADATA|TableMetaDataNode は XMLNode ではありません。|  
|0xC0029200|-1073573376|DTS_E_TTGENTASK_FAILEDCREATEPIPELINE|パイプラインの作成に失敗しました。|  
|0xC0029201|-1073573375|DTS_E_TTGENTASK_BADVARIABLETYPE|変数の型が正しくありません。|  
|0xC0029202|-1073573374|DTS_E_TTGENTASK_NOTFILECONNECTION|指定された接続マネージャーは FILE 接続マネージャーではありません。|  
|0xC0029203|-1073573373|DTS_E_TTGENTASK_BADFILENAME|接続マネージャー "%1" に指定されたファイル名が無効です。|  
|0xC0029204|-1073573372|DTS_E_WEBSERVICETASK_CONNECTION_NAME_NULL|接続が空です。 有効な HTTP 接続が指定されていることを確認してください。|  
|0xC0029205|-1073573371|DTS_E_WEBSERVICETASK_CONNECTION_NOT_FOUND|接続が存在しません。 指定された既存の HTTP 接続が有効であることを確認してください。|  
|0xC0029206|-1073573370|DTS_E_WEBSERVICETASK_CONNECTION_NOT_HTTP|指定された接続は HTTP 接続ではありません。 有効な HTTP 接続が指定されていることを確認してください。|  
|0xC0029207|-1073573369|DTS_E_WEBSERVICETASK_SERVICE_NULL|Web サービス名が空です。 有効な Web サービス名が指定されていることを確認してください。|  
|0xC0029208|-1073573368|DTS_E_WEBSERVICETASK_METHODNAME_NULL|Web メソッド名が空です。 有効な Web メソッド名が指定されていることを確認してください。|  
|0xC0029209|-1073573367|DTS_E_WEBSERVICETASK_WEBMETHODINFO_NULL|Web メソッドが空か、存在しない可能性があります。 指定可能な既存の Web メソッドが存在することを確認してください。|  
|0xC002920A|-1073573366|DTS_E_WEBSERVICETASK_OUTPUTLOC_NULL|出力場所が空です。 既存のファイル接続または変数が指定されていることを確認してください。|  
|0xC002920B|-1073573365|DTS_E_WEBSERVICETASK_VARIABLE_NOT_FOUND|変数が見つかりません。 パッケージ内に変数が存在することを確認してください。|  
|0xC002920C|-1073573364|DTS_E_WEBSERVICETASK_VARIABLE_READONLY|結果を保存できません。 変数が読み取り専用ではないことを確認してください。|  
|0xC002920D|-1073573363|DTS_E_WEBSERVICETASK_ERROR_IN_LOAD_FROM_XML|LoadFromXML のタグ "%1" でエラーが発生しました。|  
|0xC002920E|-1073573362|DTS_E_WEBSERVICETASK_ERROR_IN_SAVE_TO_XML|SaveToXML のタグ "%1" でエラーが発生しました。|  
|0xC002920F|-1073573361|DTS_E_WEBSERVICETASK_TASK_SAVE_TO_NULL_XML_ELEMENT|NULL の XML ドキュメントにタスクを保存できません。|  
|0xC0029210|-1073573360|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_NULL_XML_ELEMENT|XML 要素が NULL であるタスクを初期化できません。|  
|0xC0029211|-1073573359|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|正しくない XML 要素を使用して、Web サービス タスクが開始されています。|  
|0xC0029212|-1073573358|DTS_E_WEBSERVICETASK_UNEXPECTED_XML_ELEMENT|予期しない XML 要素が見つかりました。|  
|0xC0029213|-1073573357|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_CONNECTION|HTTP 接続の取得中にエラーが発生しました。 有効な接続の種類が指定されていることを確認してください。|  
|0xC0029214|-1073573356|DTS_E_WEBSERVICETASK_FILE_CONN_NOT_FOUND|結果を保存できません。 既存のファイル接続が存在することを確認してください。|  
|0xC0029215|-1073573355|DTS_E_WEBSERVICETASK_FILE_NOT_FOUND|結果を保存できません。 ファイルが存在することを確認してください。|  
|0xC0029216|-1073573354|DTS_E_WEBSERVICETASK_FILE_NULL|結果を保存できません。 ファイル名が空であるか、ファイルが別のプロセスによって使用されています。|  
|0xC0029217|-1073573353|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_FILE_CONNECTION|ファイル接続の取得中にエラーが発生しました。 有効なファイル接続が指定されていることを確認してください。|  
|0xC0029218|-1073573352|DTS_E_WEBSERVICETASK_DATATYPE_NOT_SUPPORTED|プリミティブ型の値、プリミティブ型の配列、および列挙値を含む複合型のみがサポートされています。|  
|0xC0029219|-1073573351|DTS_E_WEBSERVICETASK_PARAMTYPE_NOT_SUPPORTED|Primitive 型、Enum 型、Complex 型、PrimitiveArray 型、および ComplexArray 型のみがサポートされています。|  
|0xC002921A|-1073573350|DTS_E_WEBSERVICETASK_WSDL_VERSION_NOT_SUPPORTED|このバージョンの WSDL はサポートされていません。|  
|0xC002921B|-1073573349|DTS_E_WEBSERVICETASK_WRONG_XML_ELEMENT|正しくない XML 要素を使用して初期化されました。|  
|0xC002921C|-1073573348|DTS_E_WEBSERVICETASK_XML_ATTRIBUTE_NOT_FOUND|必須の属性が見つかりません。|  
|0xC002921D|-1073573347|DTS_E_WEBSERVICETASK_ENUM_NO_VALUES|列挙 "%1" は値を保持していません。 WSDL が壊れています。|  
|0xC002921E|-1073573346|DTS_E_WEBSERVICETASK_CONNECTIONNOTFOUND|接続が見つかりません。|  
|0xC002921F|-1073573345|DTS_E_WEBSERVICETASK_CONNECTION_ALREADY_EXISTS|この名前の接続は既に存在します。|  
|0xC0029220|-1073573344|DTS_E_WEBSERVICETASK_NULL_CONNECTION|接続を NULL または空にすることはできません。|  
|0xC0029221|-1073573343|DTS_E_WEBSERVICETASK_NOT_HTTP_CONNECTION|指定された接続は HTTP 接続ではありません。 有効な HTTP 接続が指定されていることを確認してください。|  
|0xC0029222|-1073573342|DTS_E_WEBSERVICETASK_WSDL_NOT_FOUND|指定された Uniform Resource Identifier (URI) には、有効な WSDL が含まれていません。|  
|0xC0029223|-1073573341|DTS_E_WEBSERVICETASK_ERROR_IN_DOWNLOAD|WSDL ファイルを読み取れませんでした。 入力 WSDL ファイルが無効です。 リーダーにより、次のエラーがスローされました: "%1"。|  
|0xC0029224|-1073573340|DTS_E_WEBSERVICETASK_SERVICE_DESC_NULL|サービスの説明を NULL にすることはできません。|  
|0xC0029225|-1073573339|DTS_E_WEBSERVICETASK_SERVICENULL|サービス名を NULL にすることはできません。|  
|0xC0029226|-1073573338|DTS_E_WEBSERVICETASK_WSDL_NULL|URL を NULL にすることはできません。|  
|0xC0029227|-1073573337|DTS_E_WEBSERVICETASK_SERVICE_NOT_FOUND|サービスは現在使用できません。|  
|0xC0029228|-1073573336|DTS_E_WEBSERVICETASK_SOAPPORT_NOT_FOUND|このサービスは SOAP ポートでは利用できません。|  
|0xC0029229|-1073573335|DTS_E_WEBSERVICETASK_SOAPBINDING_NOT_FOUND|Web サービス記述言語 (WSDL) を解析できませんでした。 SOAP ポートに対応するバインドが見つかりません。|  
|0xC002922A|-1073573334|DTS_E_WEBSERVICETASK_SOAPPORTTYPE_NOT_FOUND|Web サービス記述言語 (WSDL) を解析できませんでした。 SOAP ポートに対応する PortType が見つかりません。|  
|0xC002922B|-1073573333|DTS_E_WEBSERVICETASK_MSG_NOT_FOUND|指定されたメソッドに対応するメッセージが見つかりません。|  
|0xC002922C|-1073573332|DTS_E_WEBSERVICETASK_CANNOT_GEN_PROXY|指定された Web サービスのプロキシを生成できませんでした。 プロキシ "%1" の生成中に次のエラーが発生しました。|  
|0xC002922D|-1073573331|DTS_E_WEBSERVICETASK_CANNOT_LOAD_PROXY|指定された Web サービスのプロキシを読み込めません。 正確なエラーは次のとおりです: "%1"。|  
|0xC002922E|-1073573330|DTS_E_WEBSERVICETASK_INVALID_SERVICE|指定されたサービスが見つかりませんでした。 正確なエラーは次のとおりです: "%1"。|  
|0xC002922F|-1073573329|DTS_E_WEBSERVICETASK_WEBMETHOD_INVOKE_FAILED|メソッドの実行中に、Web サービスから次のエラーがスローされました: "%1"。|  
|0xC0029230|-1073573328|DTS_E_WEBSERVICETASK_INVOKE_ERR|Web メソッドを実行できませんでした。 正確なエラーは次のとおりです: "%1"。|  
|0xC0029231|-1073573327|DTS_E_WEBSERVICETASK_METHODINFO_NULL|MethodInfo を NULL にすることはできません。|  
|0xC0029232|-1073573326|DTS_E_WEBSERVICETASK_VALUE_NOT_PRIMITIVE|指定された WebMethodInfo が正しくありません。 指定された ParamValue が ParamType と一致しません。 見つかった DTSParamValue の型が PrimitiveValue ではありません。|  
|0xC0029233|-1073573325|DTS_E_WEBSERVICETASK_VALUE_NOT_ENUM|指定された WebMethodInfo が正しくありません。 指定された ParamValue が ParamType と一致しません。 見つかった DTSParamValue の型が EnumValue ではありません。|  
|0xC0029234|-1073573324|DTS_E_VALUE_WEBSERVICETASK_NOT_COMPLEX|指定された WebMethodInfo が正しくありません。 指定された ParamValue が ParamType と一致しません。 見つかった DTSParamValue の型が ComplexValue ではありません。|  
|0xC0029235|-1073573323|DTS_E_WEBSERVICETASK_VALUE_NOT_ARRAY|指定された WebMethodInfo が正しくありません。 指定された ParamValue が ParamType と一致しません。 見つかった DTSParamValue の型が ArrayValue ではありません。|  
|0xC0029236|-1073573322|DTS_E_WEBSERVICETASK_TYPE_NOT_PRIMITIVE|指定された WebMethodInfo が正しくありません。 "%1" は Primitive 型ではありません。|  
|0xC0029237|-1073573321|DTS_E_WEBSERVICETASK_ARRAY_VALUE_INVALID|ArrayValue の形式が無効です。 配列には少なくとも 1 つの要素が必要です。|  
|0xC0029238|-1073573320|DTS_E_WEBSERVICETASK_SELECTED_VALUE_NULL|列挙の値を NULL にすることはできません。 列挙の既定値を選択してください。|  
|0xC0029239|-1073573319|DTS_E_WEBSERVICETASK_NULL_VALUE|どのデータ型に対しても NULL を検証することはできません。|  
|0xC002923A|-1073573318|DTS_E_WEBSERVICETASK_ENUM_VALUE_NOT_FOUND|列挙値が正しくありません。|  
|0xC002923B|-1073573317|DTS_E_WEBSERVICETASK_PROP_NOT_EXISTS|指定されたクラスには、名前 "%1" のパブリック プロパティが含まれていません。|  
|0xC002923C|-1073573316|DTS_E_WEBSERVICETASK_CONVERT_FAILED|"%1" を "%2" に変換できませんでした。|  
|0xC002923D|-1073573315|DTS_E_WEBSERVICETASK_CLEANUP_FAILED|クリーンアップに失敗しました。 Web サービス用に作成されたプロキシが削除された可能性があります。|  
|0xC002923E|-1073573314|DTS_E_WEBSERVICETASK_CREATE_INSTANCE_FAILED|型 "%1" のオブジェクトを作成できませんでした。 既定のコンストラクターが存在するかどうかを確認してください。|  
|0xC002923F|-1073573313|DTS_E_WEBSERVICETASK_NOT_PRIMITIVE_TYPE|"%1" は値の型ではありません。|  
|0xC0029240|-1073573312|DTS_E_WEBSERVICETASK_ERROR_IN_VALIDATE|"%1" を "%1" に対して検証できませんでした。|  
|0xC0029241|-1073573311|DTS_E_WEBSERVICETASK_DATATYPE_NULL|データ型を NULL にすることはできません。 検証するデータ型の値を指定してください。|  
|0xC0029242|-1073573310|DTS_E_WEBSERVICETASK_INDEX_OUT_OF_BOUNDS|ParamValue をこの位置に挿入できません。 指定されたインデックスが 0 未満であるか、最大の長さを超えています。|  
|0xC0029243|-1073573309|DTS_E_WEBSERVICETASK_WRONG_WSDL|入力 WSDL ファイルが無効です。|  
|0xC0029244|-1073573308|DTS_E_WMIDRTASK_SYNCOBJECTFAILED|同期オブジェクトが失敗しました。|  
|0xC0029245|-1073573307|DTS_E_WMIDRTASK_MISSINGWQLQUERY|WQL クエリがありません。|  
|0xC0029246|-1073573306|DTS_E_WMIDRTASK_DESTINATIONMUSTBESET|変換先を指定する必要があります。|  
|0xC0029247|-1073573305|DTS_E_WMIDRTASK_MISSINGCONNECTION|WMI 接続が設定されていません。|  
|0xC0029248|-1073573304|DTS_E_WMIDRTASK_INVALIDDATANODE|WMI データ リーダー タスクは無効なタスク データ ノードを受け取りました。|  
|0xC0029249|-1073573303|DTS_E_WMIDRTASK_FAILEDVALIDATION|タスクが検証に失敗しました。|  
|0xC002924A|-1073573302|DTS_E_WMIDRTASK_FILEDOESNOTEXIST|ファイル "%1" が存在しません。|  
|0xC002924B|-1073573301|DTS_E_WMIDRTASK_CONNECTIONMNGRDOESNTEXIST|接続マネージャー "%1" が存在しません。|  
|0xC002924C|-1073573300|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRINGOROBJECT|変数 "%1" は文字列型またはオブジェクト型ではありません。|  
|0xC002924D|-1073573299|DTS_E_WMIDRTASK_CONNECTIONTYPENOTFILE|接続 "%1" の種類は "FILE" ではありません。|  
|0xC002924E|-1073573298|DTS_E_WMIDRTASK_CONNECTIONTYPENOTWMI|接続 "%1" の種類は "WMI" ではありません。|  
|0xC002924F|-1073573297|DTS_E_WMIDRTASK_FILEALREADYEXISTS|ファイル "%1" は既に存在します。|  
|0xC0029250|-1073573296|DTS_E_WMIDRTASK_CONNECTIONMANAGEREMPTY|接続マネージャー "%1" が空です。|  
|0xC0029251|-1073573295|DTS_E_WMIDRTASK_VARNOTOBJECT|変数 "%1" をデータ テーブルに割り当てるには、オブジェクト型を指定する必要があります。|  
|0xC0029252|-1073573294|DTS_E_WMIDRTASK_TASKFAILURE|タスクは次の無効な WMI クエリにより失敗しました: "%1"。|  
|0xC0029253|-1073573293|DTS_E_WMIDRTASK_CANTWRITETOVAR|変数 "%1" は元の値を保持するように設定されているので、この変数には書き込めません。|  
|0xC0029254|-1073573292|DTS_E_WMIEWTASK_SYNCOBJECTFAILED|同期オブジェクトが失敗しました。|  
|0xC0029255|-1073573291|DTS_E_WMIEWTASK_MISSINGWQLQUERY|WQL クエリがありません。|  
|0xC0029256|-1073573290|DTS_E_WMIEWTASK_MISSINGCONNECTION|WMI 接続がありません。|  
|0xC0029257|-1073573289|DTS_E_WMIEWTASK_QUERYFAILURE|タスクが WMI クエリの実行に失敗しました。|  
|0xC0029258|-1073573288|DTS_E_WMIEWTASK_INVALIDDATANODE|WMI イベント監視タスクは無効なタスク データ ノードを受け取りました。|  
|0xC0029259|-1073573287|DTS_E_WMIEWTASK_CONNECTIONMNGRDOESNTEXIST|接続マネージャー "%1" が存在しません。|  
|0xC002925A|-1073573286|DTS_E_WMIEWTASK_FILEDOESNOTEXIST|ファイル "%1" が存在しません。|  
|0xC002925B|-1073573285|DTS_E_WMIEWTASK_VARIABLETYPEISNOTSTRING|変数 "%1" は文字列型ではありません。|  
|0xC002925C|-1073573284|DTS_E_WMIEWTASK_CONNECTIONTYPENOTFILE|接続 "%1" の種類は "FILE" ではありません。|  
|0xC002925D|-1073573283|DTS_E_WMIEWTASK_CONNECTIONTYPENOTWMI|接続 "%1" の種類は "WMI" ではありません。|  
|0xC002925E|-1073573282|DTS_E_WMIEWTASK_FILEALREADYEXISTS|ファイル "%1" は既に存在します。|  
|0xC002925F|-1073573281|DTS_E_WMIEWTASK_CONNECTIONMANAGEREMPTY|接続マネージャー "%1" が空です。|  
|0xC0029260|-1073573280|DTS_E_WMIEWTASK_TIMEOUTOCCURRED|"%1" 秒のタイムアウトが、"%2" によって示されているイベントの前に発生しました。|  
|0xC0029261|-1073573279|DTS_E_WMIEWTASK_ERRMESSAGE|Wql クエリの監視で、次のシステム例外が発生しました: "%1"。 クエリにエラーがないか、または WMI 接続にアクセス権があるかどうかを確認してください。|  
|0xC0029262|-1073573278|DTS_E_XMLTASK_NODEFAULTOPERTION|指定された操作は定義されていません。|  
|0xC0029263|-1073573277|DTS_E_XMLTASK_CONNECTIONTYPENOTFILE|接続の種類が FILE ではありません。|  
|0xC0029264|-1073573276|DTS_E_XMLTASK_CANTGETREADERFROMSOURCE|基になる XML ドキュメントから XmlReader を取得できません。|  
|0xC0029265|-1073573275|DTS_E_XMLTASK_CANTGETREADERFROMDEST|変更された XML ドキュメントから XmlReader を取得できません。|  
|0xC0029266|-1073573274|DTS_E_XMLTASK_CANTGETREADERFROMDIFFGRAM|XDL DiffGram リーダーを XDL DiffGram XML から取得できません。|  
|0xC0029268|-1073573272|DTS_E_XMLTASK_EMPTYNODELIST|ノード リストが空です。|  
|0xC0029269|-1073573271|DTS_E_XMLTASK_NOELEMENTFOUND|要素が見つかりませんでした。|  
|0xC002926A|-1073573270|DTS_E_XMLTASK_UNDEFINEDOPERATION|指定された操作は定義されていません。|  
|0xC002926B|-1073573269|DTS_E_XMLTASK_XPATHNAVERROR|XPathNavigator の予期しないコンテンツ アイテムです。|  
|0xC002926C|-1073573268|DTS_E_XMLTASK_NOSCHEMAFOUND|検証の対象になるスキーマがありません。|  
|0xC002926D|-1073573267|DTS_E_XMLTASK_VALIDATIONERROR|インスタンス ドキュメントの検証中に検証エラーが発生しました。|  
|0xC002926E|-1073573266|DTS_E_XMLTASK_SYNCOBJECTFAILED|同期オブジェクトが失敗しました。|  
|0xC002926F|-1073573265|DTS_E_XMLTASK_ROOTNOODESNOTMATCHED|ルート ノードが一致しません。|  
|0xC0029270|-1073573264|DTS_E_XMLTASK_INVALIDEDITSCRIPT|最後の編集スクリプトの編集スクリプト操作の種類が無効です。|  
|0xC0029271|-1073573263|DTS_E_XMLTASK_CDATANODESISSUE|CDATA ノードは、DiffgramAddSubtrees クラスを使用して追加する必要があります。|  
|0xC0029272|-1073573262|DTS_E_XMLTASK_COMMENTSNODEISSUE|コメント ノードは、DiffgramAddSubtrees クラスを使用して追加する必要があります。|  
|0xC0029273|-1073573261|DTS_E_XMLTASK_TEXTNODEISSUES|テキスト ノードは、DiffgramAddSubtrees クラスを使用して追加する必要があります。|  
|0xC0029274|-1073573260|DTS_E_XMLTASK_WHITESPACEISSUE|意味のある空白ノードは、DiffgramAddSubtrees クラスを使用して追加する必要があります。|  
|0xC0029275|-1073573259|DTS_E_XMLTASK_DIFFENUMISSUE|XmlDiffOperation 列挙が反映されるように OperationCost 配列を修正してください。|  
|0xC0029276|-1073573258|DTS_E_XMLTASK_TASKISEMPTY|タスクに操作がありません。|  
|0xC0029277|-1073573257|DTS_E_XMLTASK_DOCUMENTHASDATA|ドキュメントに既にデータが含まれているため、再利用しないでください。|  
|0xC0029278|-1073573256|DTS_E_XMLTASK_INVALIDENODETYPE|ノードの種類が無効です。|  
|0xC0029279|-1073573255|DTS_E_XMLTASK_INVALIDDATANODE|XML タスクは無効なタスク データ ノードを受け取りました。|  
|0xC002927B|-1073573253|DTS_E_XMLTASK_VARIABLETYPEISNOTSTRING|変数データ型が文字列ではありません。|  
|0xC002927C|-1073573252|DTS_E_XMLTASK_COULDNOTGETENCODINGFROMDOCUMENT|XML からエンコード情報を取得できません。|  
|0xC002927D|-1073573251|DTS_E_XMLTASK_MISSINGSOURCE|ソースが指定されていません。|  
|0xC002927E|-1073573250|DTS_E_XMLTASK_MISSINGSECONDOPERAND|2 番目のオペランドが指定されていません。|  
|0xC002927F|-1073573249|DTS_E_XMLTASK_INVALIDPATHDESCRIPTOR|XDL DiffGram が無効です。 "%1" は無効なパス記述子です。|  
|0xC0029280|-1073573248|DTS_E_XMLTASK_NOMATCHINGNODE|XDL DiffGram が無効です。 パス記述子 "%1" と一致するノードがありません。|  
|0xC0029281|-1073573247|DTS_E_XMLTASK_EXPECTINGDIFFGRAMELEMENT|XDL DiffGram が無効です。 名前空間 URI "%1" を持つルート要素としては xd:xmldiff が想定されています。|  
|0xC0029282|-1073573246|DTS_E_XMLTASK_MISSINGSRCDOCATTRIBUTE|XDL DiffGram が無効です。 xd:xmldiff 要素に srcDocHash 属性が見つかりません。|  
|0xC0029283|-1073573245|DTS_E_XMLTASK_MISSINGOPTIONSATTRIBUTE|XDL DiffGram が無効です。 xd:xmldiff 要素にオプションの属性が見つかりません。|  
|0xC0029284|-1073573244|DTS_E_XMLTASK_INVALIDSRCDOCATTRIBUTE|XDL DiffGram が無効です。 srcDocHash 属性に無効な値が指定されています。|  
|0xC0029285|-1073573243|DTS_E_XMLTASK_INVALIDOPTIONSATTRIBUTE|XDL DiffGram が無効です。 オプションの属性に無効な値が指定されています。|  
|0xC0029286|-1073573242|DTS_E_XMLTASK_SRCDOCMISMATCH|XDL DiffGram はこの XML ドキュメントには適用できません。 srcDocHash 値が一致しません。|  
|0xC0029287|-1073573241|DTS_E_XMLTASK_MORETHANONENODEMATCHED|XDL DiffGram が無効です。複数のノードが xd:node 要素または xd:change 要素の "%1" パス記述子と一致します。|  
|0xC0029288|-1073573240|DTS_E_XMLTASK_XMLDECLMISMATCH|XDL DiffGram はこの XML ドキュメントには適用できません。 新しい XML 宣言を追加できません。|  
|0xC0029289|-1073573239|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODEINLIST|内部エラー。 XmlDiffPathSingleNodeList は 1 つのノードのみを含むことができます。|  
|0xC002928A|-1073573238|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODELEFT|内部エラー。 修正後に "%1" 個のノードが残っていますが、予期されたのは 1 個のノードでした。|  
|0xC002928B|-1073573237|DTS_E_XMLTASK_XSLTRESULTFILEISNOTXML|XSLT で生成されたファイルやテキストは有効な XmlDocument ではないので、操作の結果として設定できません: "%1"。|  
|0xC002928E|-1073573234|DTS_E_XMLTASK_FILEDOESNOTEXIST|接続 "%1" に関連付けられたファイルがありません。|  
|0xC002928F|-1073573233|DTS_E_XMLTASK_XMLTEXTEMPTY|プロパティ "%1" に、ソース XML テキストがありません。XML テキストが無効であるか、NULL または空の文字列です。|  
|0xC0029290|-1073573232|DTS_E_XMLTASK_FILEALREADYEXISTS|ファイル "%1" は既に存在します。|  
|0xC0029293|-1073573229|DTS_E_TRANSFERTASKS_SRCCONNECTIONREQUIRED|変換元接続を指定してください。|  
|0xC0029294|-1073573228|DTS_E_TRANSFERTASKS_DESTCONNECTIONREQUIRED|変換先接続を指定してください。|  
|0xC0029295|-1073573227|DTS_E_TRANSFERTASKS_CONNECTIONNOTFOUND|パッケージに接続 "%1" が見つかりませんでした。|  
|0xC0029296|-1073573226|DTS_E_TRANSFERTASKS_SERVERVERSIONNOTALLOWED|接続 "%1" では、転送がサポートされていないバージョンの SQL Server インスタンスが指定されています。  サポートされているバージョンは、7、2000、および 2005 だけです。|  
|0xC0029297|-1073573225|DTS_E_TRANSFERTASKS_SRCSERVERLESSEQUALDESTSERVER|転送元接続 "%1" には、転送先接続 "%2" 以前のバージョンの SQL Server インスタンスを指定する必要があります。|  
|0xC0029298|-1073573224|DTS_E_TRANSFERTASKS_SRCDBREQUIRED|転送元データベースを指定してください。|  
|0xC0029299|-1073573223|DTS_E_TRANSFERTASKS_SRCDBMUSTEXIST|転送元データベース "%1" は、転送先サーバーに存在する必要があります。|  
|0xC002929A|-1073573222|DTS_E_TRANSFERTASKS_DESTDBREQUIRED|転送先データベースを指定してください。|  
|0xC002929B|-1073573221|DTS_E_TRANSFERTASKS_SRCDBANDDESTDBTHESAME|転送元データベースと転送先データベースには、同じデータベースを指定できません。|  
|0xC002929C|-1073573220|DTS_E_TRANSFERDBTASK_FILENAMEREQUIRED|転送ファイル情報 %1 にファイル名がありません。|  
|0xC002929D|-1073573219|DTS_E_TRANSFERDBTASK_FOLDERREQUIRED|転送ファイル情報 %1 にフォルダー部分がありません。|  
|0xC002929E|-1073573218|DTS_E_TRANSFERTASKS_NETSHAREREQUIRED|転送ファイル情報 %1 にネットワーク共有部分がありません。|  
|0xC002929F|-1073573217|DTS_E_TRANSFERTASKS_FILELISTSCOUNTMISMATCH|転送元の転送ファイルの数と転送先の転送ファイルの数は同じである必要があります。|  
|0xC00292A0|-1073573216|DTS_E_DOESNOTSUPPORTTRANSACTIONS|トランザクションの参加はサポートされていません。|  
|0xC00292A1|-1073573215|DTS_E_TRANSFERDBTASK_OFFLINEERROR|オフライン データベースの転送中に次の例外が発生しました: %1。|  
|0xC00292A2|-1073573214|DTS_E_TRANSFERDBTASK_NETSHAREDOESNOTEXIST|ネットワーク共有 "%1" が見つかりませんでした。|  
|0xC00292A3|-1073573213|DTS_E_TRANSFERDBTASK_NETSHARENOACCESS|ネットワーク共有 "%1" にアクセスできませんでした。  エラー: %2。|  
|0xC00292A4|-1073573212|DTS_E_TRANSFERDBTASK_USERMUSTBEDBOORSYSADMIN|オンライン データベース転送を実行するには、ユーザー "%1" は DBO または "%2" の sysadmin である必要があります。|  
|0xC00292A5|-1073573211|DTS_E_TRANSFERDBTASK_USERMUSTBESYSADMIN|オフライン データベース転送を実行するには、ユーザー "%1" は "%2" の sysadmin である必要があります。|  
|0xC00292A6|-1073573210|DTS_E_TRANSFERDBTASK_FTCATALOGSOFFLINEYUKONONLY|フルテキスト カタログを含めることができるのは、2 台の SQL Server 2005 サーバー間でオフライン データベース転送を実行しているときだけです。|  
|0xC00292A7|-1073573209|DTS_E_TRANSFERDBTASK_NOOVERWRITEDB|データベース "%1" は、転送先サーバー "%2" に既に存在します。|  
|0xC00292A8|-1073573208|DTS_E_TRANSFERDBTASK_MUSTHAVESOURCEFILES|少なくとも 1 つの転送元ファイルを指定してください。|  
|0xC00292A9|-1073573207|DTS_E_TRANSFERDBTASKS_SRCFILENOTFOUND|転送元データベース "%2" に、ファイル "%1" が見つかりませんでした。|  
|0xC00292B3|-1073573197|DTS_E_MSMQTASK_FIPS1402COMPLIANCE|U.S. FIPS 140-2 と互換性のあるシステムでは、要求された操作は許可されません。|  
|0xC002F210|-1073548784|DTS_E_SQLTASK_ERROREXECUTINGTHEQUERY|クエリ "%1" の実行が次のエラーで失敗しました: "%2"。 考えられるエラーの理由: クエリに問題がある、"ResultSet" プロパティが正しく設定されていない、パラメーターが正しく設定されていない、または接続が正しく確立されていない。|  
|0xC002F300|-1073548544|DTS_E_TRANSFERSPTASK_ERRORREADINGSPNAMES|XML ファイルからストアド プロシージャ名の読み取り中にエラーが発生しました。|  
|0xC002F301|-1073548543|DTS_E_TRANSFERSPTASK_INVALIDDATANODE|ストアド プロシージャ転送タスクでは無効なデータ ノードです。|  
|0xC002F302|-1073548542|DTS_E_TRANSFERTASKS_CONNECTIONTYPEISNOTSMOSERVER|接続 "%1" の種類は、"SMOServer" ではありません。|  
|0xC002F303|-1073548541|DTS_E_TRANSFERSPTASK_EXECUTIONFAILED|次のエラーにより実行が失敗しました: "%1"。|  
|0xC002F304|-1073548540|DTS_E_ERROROCCURREDWITHFOLLOWINGMESSAGE|エラーが次のエラー メッセージで発生しました: "%1"。|  
|0xC002F305|-1073548539|DTS_E_BITASK_EXECUTION_FAILED|一括挿入の実行に失敗しました。|  
|0xC002F306|-1073548538|DTS_E_FSTASK_INVALIDDESTPATH|対象になるパスが無効です。|  
|0xC002F307|-1073548537|DTS_E_FSTASK_CANTCREATEDIR|ディレクトリを作成できません。 ユーザーにより、ディレクトリが存在する場合にタスクを失敗させるように選択されました。|  
|0xC002F308|-1073548536|DTS_E_SQLTASK_ODBCNOSUPPORTTRANSACTION|タスクのトランザクション オプションは "Required" で、接続 "%1" の種類は "ODBC" です。 ODBC 接続では、トランザクションはサポートされません。|  
|0xC002F309|-1073548535|DTS_E_SQLTASK_ERRORASSIGINGVALUETOVAR|変数 "%1" の値を割り当て中にエラーが発生しました: "%2"。|  
|0xC002F30A|-1073548534|DTS_E_FSTASK_SOURCEISEMPTY|転送元が空です。|  
|0xC002F30B|-1073548533|DTS_E_FSTASK_DESTINATIONISEMPTY|転送先が空です。|  
|0xC002F30C|-1073548532|DTS_E_FSTASK_FILEDIRNOTFOUND|ファイルまたはディレクトリ "%1" が存在しません。|  
|0xC002F30D|-1073548531|DTS_E_FSTASK_VARSRCORDESTISEMPTY|転送元または転送先として変数 "%1" が使用されますが、空です。|  
|0xC002F30E|-1073548530|DTS_E_FSTASK_FILEDELETED|ファイルまたはディレクトリ "%1" は削除されました。|  
|0xC002F30F|-1073548529|DTS_E_FSTASK_DIRECTORYDELETED|ディレクトリ "%1" は削除されました。|  
|0xC002F310|-1073548528|DTS_E_WMIDRTASK_VARIABLETYPEISNOTOBJECT|変数 "%1" をデータ テーブルに割り当てるには、オブジェクト型を指定する必要があります。|  
|0xC002F311|-1073548527|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRING|変数 "%1" は文字列データ型ではありません。|  
|0xC002F312|-1073548526|DTS_E_FTPTASK_CANNOTACQUIRECONNECTION|FTP 接続の取得中にエラーが発生しました。 有効な接続の種類が "%1" に指定されていることを確認してください。|  
|0xC002F313|-1073548525|DTS_E_FTPTASK_CONNECTIONNOTFOUND|FTP 接続マネージャー "%1" が見つかりません。|  
|0xC002F314|-1073548524|DTS_E_FTPTASK_FILEUSAGETYPEERROR|操作 "%3" では、接続 "%1" のファイルの使用法の種類が "%2" である必要があります。|  
|0xC002F315|-1073548523|DTS_E_TRANSFERTASKS_SOURCECANTBESAMEASDESTINATION|転送元のサーバーを転送先のサーバーと同じにすることはできません。|  
|0xC002F316|-1073548522|DTS_E_ERRMSGTASK_EMPTYSOURCELIST|転送するエラー メッセージはありません。|  
|0xC002F317|-1073548521|DTS_E_ERRMSGTASK_DIFFERENTMESSAGEANDLANGUAGESIZES|エラー メッセージの一覧とそれに対応する言語の一覧のサイズが異なります。|  
|0xC002F318|-1073548520|DTS_E_ERRMSGTASK_ERRORMESSAGEOUTOFRANGE|エラー メッセージ ID "%1" は、ユーザー定義エラー メッセージの許容範囲外です。 ユーザー定義エラー メッセージ ID は、50000 から 2147483647 までです。|  
|0xC002F319|-1073548519|DTS_E_TRANSFERTASKS_NOTRANSACTIONSUPPORT|このタスクはトランザクションに参加できません。|  
|0xC002F320|-1073548512|DTS_E_ERRMSGTASK_FAILEDTOTRANSFERERRORMESSAGES|一部またはすべてのエラー メッセージを転送できませんでした。|  
|0xC002F321|-1073548511|DTS_E_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|エラー メッセージ "%1" は、既に転送先サーバーに存在します。|  
|0xC002F324|-1073548508|DTS_E_ERRMSGTASK_ERRORMESSAGECANTBEFOUND|転送元のサーバーでエラー メッセージ "%1" が見つかりません。|  
|0xC002F325|-1073548507|DTS_E_TRANSFERTASKS_EXECUTIONFAILED|次のエラーにより実行が失敗しました: "%1"。|  
|0xC002F327|-1073548505|DTS_E_JOBSTASK_FAILEDTOTRANSFERJOBS|ジョブを転送できませんでした。|  
|0xC002F330|-1073548496|DTS_E_JOBSTASK_EMPTYSOURCELIST|転送するジョブはありません。|  
|0xC002F331|-1073548495|DTS_E_JOBSTASK_JOBEXISTSATDEST|ジョブ "%1" は、既に転送先サーバーに存在します。|  
|0xC002F334|-1073548492|DTS_E_JOBSTASK_JOBCANTBEFOUND|転送元のサーバーでジョブ "%1" が見つかりません。|  
|0xC002F337|-1073548489|DTS_E_LOGINSTASK_EMPTYLIST|転送する "ログイン" の一覧は空です。|  
|0xC002F338|-1073548488|DTS_E_LOGINSTASK_CANTGETLOGINSNAMELIST|転送元サーバーから "ログイン" の一覧を取得できません。|  
|0xC002F340|-1073548480|DTS_E_LOGINSTASK_ERRORLOGINEXISTS|ログイン "%1" は、既に転送先サーバーに存在します。|  
|0xC002F342|-1073548478|DTS_E_LOGINSTASK_LOGINNOTFOUND|ログイン "%1" が転送元に存在しません。|  
|0xC002F344|-1073548476|DTS_E_LOGINSTASK_FAILEDTOTRANSFERLOGINS|一部またはすべてのログインを転送できませんでした。|  
|0xC002F345|-1073548475|DTS_E_STOREDPROCSTASK_FAILEDTOTRANSFERSPS|ストアド プロシージャの転送に失敗しました。 詳細な情報を示すエラーが発生している場合があります。|  
|0xC002F346|-1073548474|DTS_E_STOREDPROCSTASK_STOREDPROCNOTFOUND|ストアド プロシージャ "%1" が転送元にありません。|  
|0xC002F349|-1073548471|DTS_E_STOREDPROCSTASK_ERRORSTOREDPROCEDUREEXISTS|ストアド プロシージャ "%1" は、既に転送先サーバーに存在します。|  
|0xC002F350|-1073548464|DTS_E_STOREDPROCSTASK_EMPTYSOURCELIST|転送するストアド プロシージャはありません。|  
|0xC002F353|-1073548461|DTS_E_TRANSOBJECTSTASK_FAILEDTOTRANSFEROBJECTS|オブジェクトを転送できませんでした。|  
|0xC002F354|-1073548460|DTS_E_TRANSOBJECTSTASK_EMPTYLIST|転送する "オブジェクト" の一覧は空です。|  
|0xC002F355|-1073548459|DTS_E_TRANSOBJECTSTASK_NOSPATSOURCE|ストアド プロシージャ "%1" が転送元に存在しません。|  
|0xC002F356|-1073548458|DTS_E_TRANSOBJECTSTASK_SPALREADYATDEST|ストアド プロシージャ "%1" は、既に転送先に存在します。|  
|0xC002F357|-1073548457|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSPS|転送するストアド プロシージャ一覧の設定中に次のエラーが発生しました: "%1"。|  
|0xC002F359|-1073548455|DTS_E_TRANSOBJECTSTASK_NORULEATSOURCE|ルール "%1" が転送元に存在しません。|  
|0xC002F360|-1073548448|DTS_E_TRANSOBJECTSTASK_RULEALREADYATDEST|ルール "%1" は、既に転送先に存在します。|  
|0xC002F361|-1073548447|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGRULES|転送するルール一覧の設定中に次のエラーが発生しました: "%1"。|  
|0xC002F363|-1073548445|DTS_E_TRANSOBJECTSTASK_NOTABLEATSOURCE|テーブル "%1" が転送元に存在しません。|  
|0xC002F364|-1073548444|DTS_E_TRANSOBJECTSTASK_TABLEALREADYATDEST|テーブル "%1" は、既に転送先に存在します。|  
|0xC002F365|-1073548443|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTABLES|転送するテーブル一覧の設定中に次のエラーが発生しました: "%1"。|  
|0xC002F367|-1073548441|DTS_E_TRANSOBJECTSTASK_NOVIEWATSOURCE|ビュー "%1" が転送元に存在しません。|  
|0xC002F368|-1073548440|DTS_E_TRANSOBJECTSTASK_VIEWALREADYATDEST|ビュー "%1" は、既に転送先に存在します。|  
|0xC002F369|-1073548439|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGVIEWS|転送するビュー一覧の設定中に次のエラーが発生しました: "%1"。|  
|0xC002F371|-1073548431|DTS_E_TRANSOBJECTSTASK_NOUDFATSOURCE|ユーザー定義関数 "%1" が転送元に存在しません。|  
|0xC002F372|-1073548430|DTS_E_TRANSOBJECTSTASK_UDFALREADYATDEST|ユーザー定義関数 "%1" は、既に転送先に存在します。|  
|0xC002F373|-1073548429|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDFS|転送するユーザー定義関数一覧の設定中に次のエラーが発生しました: "%1"。|  
|0xC002F375|-1073548427|DTS_E_TRANSOBJECTSTASK_NODEFAULTATSOURCE|既定値 "%1" が転送元に存在しません。|  
|0xC002F376|-1073548426|DTS_E_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|既定値 "%1" は、既に転送先に存在します。|  
|0xC002F377|-1073548425|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGDEFAULTS|転送する既定値一覧の設定中に次のエラーが発生しました: "%1"。|  
|0xC002F379|-1073548423|DTS_E_TRANSOBJECTSTASK_NOUDDTATSOURCE|ユーザー定義データ型 "%1" が転送元に存在しません。|  
|0xC002F380|-1073548416|DTS_E_TRANSOBJECTSTASK_UDDTALREADYATDEST|ユーザー定義データ型 "%1" は、既に転送先に存在します。|  
|0xC002F381|-1073548415|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDDTS|転送するユーザー定義データ型一覧の設定中に次のエラーが発生しました: "%1"。|  
|0xC002F383|-1073548413|DTS_E_TRANSOBJECTSTASK_NOPFATSOURCE|パーティション関数 "%1" が転送元に存在しません。|  
|0xC002F384|-1073548412|DTS_E_TRANSOBJECTSTASK_PFALREADYATDEST|パーティション関数 "%1" は、既に転送先に存在します。|  
|0xC002F385|-1073548411|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPFS|転送するパーティション関数一覧の設定中に次のエラーが発生しました: "%1"。|  
|0xC002F387|-1073548409|DTS_E_TRANSOBJECTSTASK_NOPSATSOURCE|パーティション構成 "%1" が転送元に存在しません。|  
|0xC002F388|-1073548408|DTS_E_TRANSOBJECTSTASK_PSALREADYATDEST|パーティション構成 "%1" は、既に転送先に存在します。|  
|0xC002F389|-1073548407|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPSS|転送するパーティション構成一覧の設定中に次のエラーが発生しました: "%1"。|  
|0xC002F391|-1073548399|DTS_E_TRANSOBJECTSTASK_NOSCHEMAATSOURCE|スキーマ "%1" が転送元に存在しません。|  
|0xC002F392|-1073548398|DTS_E_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|スキーマ "%1" は、既に転送先に存在します。|  
|0xC002F393|-1073548397|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSCHEMAS|転送するスキーマ一覧の設定中に次のエラーが発生しました: "%1"。|  
|0xC002F395|-1073548395|DTS_E_TRANSOBJECTSTASK_NOSQLASSEMBLYATSOURCE|SqlAssembly "%1" が転送元に存在しません。|  
|0xC002F396|-1073548394|DTS_E_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|SqlAssembly "%1" は、既に転送先に存在します。|  
|0xC002F397|-1073548393|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSQLASSEMBLIES|転送する SqlAssemblies 一覧の設定中に次のエラーが発生しました: "%1"。|  
|0xC002F399|-1073548391|DTS_E_TRANSOBJECTSTASK_NOAGGREGATEATSOURCE|ユーザー定義集計 "%1" が転送元に存在しません。|  
|0xC002F400|-1073548288|DTS_E_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|ユーザー定義集計 "%1" は、既に転送先に存在します。|  
|0xC002F401|-1073548287|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGAGGREGATES|転送するユーザー定義集計一覧の設定中に次のエラーが発生しました: "%1"。|  
|0xC002F403|-1073548285|DTS_E_TRANSOBJECTSTASK_NOTYPEATSOURCE|ユーザー定義型 "%1" が転送元に存在しません。|  
|0xC002F404|-1073548284|DTS_E_TRANSOBJECTSTASK_TYPEALREADYATDEST|ユーザー定義型 "%1" は、既に転送先に存在します。|  
|0xC002F405|-1073548283|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTYPES|転送するユーザー定義型一覧の設定中に次のエラーが発生しました: "%1"。|  
|0xC002F407|-1073548281|DTS_E_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONATSOURCE|XmlSchemaCollection "%1" が転送元に存在しません。|  
|0xC002F408|-1073548280|DTS_E_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|XmlSchemaCollection "%1" は、既に転送先に存在します。|  
|0xC002F409|-1073548279|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGXMLSCHEMACOLLECTIONS|転送する XmlSchemaCollections 一覧の設定中に次のエラーが発生しました: "%1"。|  
|0xC002F411|-1073548271|DTS_E_TRANSOBJECTSTASK_SUPPORTEDONYUKONONLY|型 "%1" のオブジェクトは、SQL Server 2005 以降のサーバー間だけでサポートされています。|  
|0xC002F413|-1073548269|DTS_E_LOGINSTASK_EMPTYDATABASELIST|データベースの一覧が空です。|  
|0xC002F414|-1073548268|DTS_E_TRANSOBJECTSTASK_NOLOGINATSOURCE|ログイン "%1" が転送元に存在しません。|  
|0xC002F416|-1073548266|DTS_E_TRANSOBJECTSTASK_LOGINALREADYATDEST|ログイン "%1" は、既に転送先に存在します。|  
|0xC002F417|-1073548265|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGLOGINS|転送するログイン一覧の設定中に次のエラーが発生しました: "%1"。|  
|0xC002F419|-1073548263|DTS_E_TRANSOBJECTSTASK_NOUSERATSOURCE|ユーザー "%1" が転送元に存在しません。|  
|0xC002F41B|-1073548261|DTS_E_TRANSOBJECTSTASK_USERALREADYATDEST|ユーザー "%1" は、既に転送先に存在します。|  
|0xC002F41C|-1073548260|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUSERS|転送するユーザー一覧の設定中に次のエラーが発生しました: "%1"。|  
|0xC002F41F|-1073548257|DTS_E_BITASK_CANNOTRETAINCONNINTRANSACTION|このタスクでは、接続が保持されている接続マネージャーをトランザクション内に含めることはできません。|  
|0xC002F421|-1073548255|DTS_E_SQLTASKOUTPUTENCODINGNOTSUPPORTED|プロバイダーが OUTPUTENCODING プロパティをサポートしていないため、SQL Server の XML データを Unicode として取得できません。|  
|0xC002F426|-1073548250|DTS_E_FTPTASK_FILECONNECTIONNOTFOUND|FTP 操作 "%1" で、FILE 接続マネージャー "%2" が見つかりません。|  
|0xC002F428|-1073548248|DTS_E_TRANSOBJECTSTASK_CANNOTDROPOBJECTS|"ログイン" はサーバー レベルのオブジェクトで、転送元と転送先が同じサーバーなので最初に削除できません。 オブジェクトを最初に削除すると、転送元のログインも削除されます。|  
|0xC002F429|-1073548247|DTS_E_SQLTASK_PARAMSIZEERROR|パラメーター "%1" に負の値を指定することはできません。 (-1) が既定値として使用されます。|  
|0xC0040019|-1073479655|DTS_E_UNREGISTEREDPIPELINEXML_LOAD|データ フロー オブジェクトを読み込めません。 Microsoft.SqlServer.PipelineXml.dll が正しく登録されていることを確認してください。|  
|0xC0040020|-1073479648|DTS_E_UNREGISTEREDPIPELINEXML_SAVE|データ フロー オブジェクトを保存できません。 Microsoft.SqlServer.PipelineXml.dll が正しく登録されていることを確認してください。|  
|0xC0040040|-1073479616|DTS_E_PIPELINE_SAVE|データ フロー オブジェクトを保存できませんでした。|  
|0xC0040041|-1073479615|DTS_E_PIPELINE_LOAD|データ フロー オブジェクトを読み込めませんでした|  
|0xC0040042|-1073479614|DTS_E_SAVE_PERSTFORMAT|データ フロー オブジェクトを保存できませんでした。 指定した形式はサポートされていません。|  
|0xC0040043|-1073479613|DTS_E_LOAD_PERSTFORMAT|データ フロー オブジェクトを読み込めませんでした。 指定した形式はサポートされていません。|  
|0xC0040044|-1073479612|DTS_E_SETPERSIST_PROPEVENTS|データ フロー オブジェクトの XML 永続性イベント プロパティを設定できませんでした。|  
|0xC0040045|-1073479611|DTS_E_SETPERSIST_XMLDOM|データ フロー オブジェクトの永続性 XML DOM プロパティを設定できませんでした。|  
|0xC0040046|-1073479610|DTS_E_SETPERSIST_XMLNODE|データ フロー オブジェクトの永続性 XML ELEMENT プロパティを設定できませんでした。|  
|0xC0040047|-1073479609|DTS_E_SETPERSISTPROP_FAILED|データ フロー オブジェクトの xml 永続性プロパティを設定できませんでした。|  
|0xC0040048|-1073479608|DTS_E_NOCUSTOMPROPCOL|データ フロー コンポーネントのカスタム プロパティ コレクションを取得できませんでした。|  
|0xC0047000|-1073451008|DTS_E_CYCLEINEXECUTIONTREE|実行ツリーに循環参照が含まれています。|  
|0xC0047001|-1073451007|DTS_E_DISCONNECTEDOBJECT|%1 オブジェクト "%2" (%3!d!) はレイアウトから切断されます。|  
|0xC0047002|-1073451006|DTS_E_INVALIDOBJECTID|レイアウト オブジェクトの ID が無効です。|  
|0xC0047003|-1073451005|DTS_E_INPUTWITHOUTPATHS|必要な入力オブジェクトが、パス オブジェクトに接続されていません。|  
|0xC0047005|-1073451003|DTS_E_INVALIDSYNCHRONOUSINPUT|%1 の同期入力 ID %2!d! は無効です。|  
|0xC0047006|-1073451002|DTS_E_INVALIDOUTPUTLINEAGEID|%1 には系列 ID %2!d! が指定されていますが、%3!d! を指定する必要があります。|  
|0xC0047008|-1073451000|DTS_E_DUPLICATENAMESINCOLLECTION|パッケージには、同じ名前の 2 つのオブジェクト "%1" と "%2" が含まれています。|  
|0xC0047009|-1073450999|DTS_E_INVALIDEXCLUSIONGROUP|"%1" と "%2" は同一の除外グループに存在しますが、同じ同期入力がありません。|  
|0xC004700A|-1073450998|DTS_E_DUPLICATELINEAGEIDSINCOLLECTION|同一コレクション内の 2 つのオブジェクトが重複した系列 ID %1!d! を保持しています。 オブジェクトは %2 と %3 です。|  
|0xC004700B|-1073450997|DTS_E_VALIDATIONFAILEDONLAYOUT|レイアウトで検証に失敗しました。|  
|0xC004700C|-1073450996|DTS_E_VALIDATIONFAILEDONCOMPONENTS|1 つ以上のコンポーネントで検証に失敗しました。|  
|0xC004700D|-1073450995|DTS_E_VALIDATIONFAILED|レイアウトと 1 つ以上のコンポーネントで検証に失敗しました。|  
|0xC004700E|-1073450994|DTS_E_THREADSTARTUPFAILED|1 つ以上の必要なスレッドを作成できないので、データ フロー タスク エンジンはスタートアップ時に失敗しました。|  
|0xC004700F|-1073450993|DTS_E_CANTGETMUTEX|初期化時に、スレッドでミューテックスを作成できませんでした。|  
|0xC0047010|-1073450992|DTS_E_CANTGETSEMAPHORE|初期化時に、スレッドでセマフォを作成できませんでした。|  
|0xC0047011|-1073450991|DTS_E_BUFFERFAILUREDETAILS|システムから %1!d! パーセントのメモリの読み込みが報告されています。 物理メモリは %2 バイトで %3 バイトの空き領域があります。 仮想メモリは %4 バイトで %5 の空き領域があります。 ページング ファイルは %6 バイトで %7 バイトの空き領域があります。|  
|0xC0047012|-1073450990|DTS_E_BUFFERALLOCFAILED|バッファーが %1!d! バイトです。|  
|0xC0047013|-1073450989|DTS_E_CANTCREATEBUFFERMANAGER|バッファー マネージャーを作成できませんでした。|  
|0xC0047015|-1073450987|DTS_E_BUFFERBADSIZE|バッファーの種類 %1!d! のサイズは %2!I64d! バイトです。|  
|0xC0047016|-1073450986|DTS_E_DANGLINGWITHPATH|%1 はぶら下がりとしてマークされていますが、パスがアタッチされています。|  
|0xC0047017|-1073450985|DTS_E_INDIVIDUALVALIDATIONFAILED|%1 が検証に失敗し、エラー コード 0x%2!8.8X! が返されました。|  
|0xC0047018|-1073450984|DTS_E_INDIVIDUALPOSTEXECUTEFAILED|%1 が実行後フェーズに失敗し、エラー コード 0x%2!8.8X! が返されました。|  
|0xC0047019|-1073450983|DTS_E_INDIVIDUALPREPAREFAILED|%1 が準備フェーズに失敗し、エラー コード 0x%2!8.8X! が返されました。|  
|0xC004701A|-1073450982|DTS_E_INDIVIDUALPREEXECUTEFAILED|%1 が実行前フェーズに失敗し、エラー コード 0x%2!8.8X! が返されました。|  
|0xC004701B|-1073450981|DTS_E_INDIVIDUALCLEANUPFAILED|%1 がクリーンアップ フェーズに失敗し、エラー コード 0x%2!8.8X! が返されました。|  
|0xC004701C|-1073450980|DTS_E_INVALIDINPUTLINEAGEID|%1 に、 以前データ フロー タスクで使用されなかった系列 ID %2!d! が指定されています。|  
|0xC004701E|-1073450978|DTS_E_EXECUTIONTREECYCLE|循環参照が作成されるので、%1 を %2 に接続できません。|  
|0xC004701F|-1073450977|DTS_E_CANTCOMPARE|データ型 "%1" は比較できません。 このデータ型の比較はサポートされていないので、このデータ型を並べ替えたり、キーとして使用することはできません。|  
|0xC0047020|-1073450976|DTS_E_REFUSEDFORSHUTDOWN|このスレッドはシャットダウンされたので、入力バッファーを受け取りません。|  
|0xC0047021|-1073450975|DTS_E_THREADFAILED|SSIS エラー コード DTS_E_THREADFAILED。  エラー コード 0x%2!8.8X! により、スレッド "%1" は終了しました。  このエラーの前に、スレッドが終了した理由の詳細が記載されたエラー メッセージが報告されている可能性があります。|  
|0xC0047022|-1073450974|DTS_E_PROCESSINPUTFAILED|SSIS エラー コード DTS_E_PROCESSINPUTFAILED。  入力 "%4" (%5!d!) の処理中に、コンポーネント "%1" (%2!d!) の ProcessInput メソッドがエラー コード 0x%3!8.8X! で失敗しました。 このコンポーネントは、ProcessInput メソッドからエラーを返しました。 このエラーはコンポーネントに固有のものですが、致命的なエラーであるため、データ フロー タスクの実行は停止されます。  このエラーの前に、エラーの詳細が記載されたエラー メッセージが報告されている可能性があります。|  
|0xC0047023|-1073450973|DTS_E_CANTREALIZEVIRTUALBUFFERS|一連の仮想バッファーを認識できません。|  
|0xC0047024|-1073450972|DTS_E_PIPELINETOOCOMPLEX|このパイプラインに必要なスレッド数は %1!d! ですが、これはシステムの制限値 %2!d! を超えています。 パイプラインに必要なスレッドが多すぎるため構成できません。 非同期出力の数が多すぎるか、EngineThreads プロパティに設定された値が大きすぎます。 パイプラインを複数のパッケージに分割するか、EngineThreads プロパティの値を減らしてください。|  
|0xC0047028|-1073450968|DTS_E_SCHEDULERCOULDNOTCOUNTSOURCES|データ フロー エンジン スケジューラがレイアウト内の変換元の数を取得できません。|  
|0xC0047029|-1073450967|DTS_E_SCHEDULERCOULDNOTCOUNTDESTINATIONS|データ フロー エンジン スケジューラがレイアウト内の変換先の数を取得できません。|  
|0xC004702A|-1073450966|DTS_E_COMPONENTVIEWISUNAVAILABLE|コンポーネント ビューを使用できません。 コンポーネント ビューが作成されていることを確認してください。|  
|0xC004702B|-1073450965|DTS_E_INCORRECTCOMPONENTVIEWID|コンポーネント ビュー ID が正しくありません。 コンポーネント ビューの同期が取れません。 コンポーネント ビューを解放して再作成してください。|  
|0xC004702C|-1073450964|DTS_E_BUFFERNOTLOCKED|このバッファーはロックされていないので、操作できません。|  
|0xC004702D|-1073450963|DTS_E_CANTBUILDBUFFERTYPE|データ フロー タスクは、バッファーの定義を作成するためのメモリを割り当てることができません。 バッファーの定義には %1!d! 含まれています。|  
|0xC004702E|-1073450962|DTS_E_CANTREGISTERBUFFERTYPE|データ フロー タスクは、バッファーの種類を登録できません。 この種類には %1!d! 列含まれており、 これは実行ツリー %2!d! 用の種類です。|  
|0xC004702F|-1073450961|DTS_E_INVALIDUSESDISPOSITIONSVALUE|UsesDispositions プロパティは初期値から変更できません。 XML が編集され、UsesDispositions 値が変更された場合に発生します。 この値は、パッケージに追加されるときにコンポーネントによって設定されるので、変更は許可されていません。|  
|0xC0047030|-1073450960|DTS_E_THREADFAILEDINITIALIZE|データ フロー タスクは、必要なスレッドを初期化できなかったため、実行を開始できません。 スレッドから、具体的なエラーが以前に報告されています。|  
|0xC0047031|-1073450959|DTS_E_THREADFAILEDCREATE|データ フロー タスクは、必要なスレッドを作成できなかったため、実行を開始できません。 このエラーは、通常、メモリが不足しているときに発生します。|  
|0xC0047032|-1073450958|DTS_E_EXECUTIONTREECYCLEADDINGSYNCHRONOUSINPUT|循環参照が発生するので、"%1" の同期入力を "%2" に設定できません。|  
|0xC0047033|-1073450957|DTS_E_INVALIDCUSTOMPROPERTYNAME|同じ名前のストック プロパティが存在するので、"%1" という名前のカスタム プロパティは無効です。 カスタム プロパティに、同じオブジェクトのストック プロパティと同じ名前を指定することはできません。|  
|0xC0047035|-1073450955|DTS_E_BUFFERLOCKUNDERFLOW|バッファーのロックは既に解除されています。|  
|0xC0047036|-1073450954|DTS_E_INDIVIDUALCACHEINTERFACESFAILED|%1 が初期化に失敗し、エラー コード 0x%2!8.8X! が返されました。|  
|0xC0047037|-1073450953|DTS_E_INDIVIDUALRELEASEINTERFACESFAILED|%1 がシャットダウン中に失敗し、エラー コード 0x%2!8.8X! が返されました。 コンポーネントがインターフェイスを解放できませんでした。|  
|0xC0047038|-1073450952|DTS_E_PRIMEOUTPUTFAILED|SSIS エラー コード DTS_E_PRIMEOUTPUTFAILED。  %1 の PrimeOutput メソッドからエラー コード 0x%2!8.8X! が返されました。  パイプライン エンジンが PrimeOutput() を呼び出したときに、このコンポーネントからエラー コードが返されました。 このエラー コードの詳細はコンポーネントで定義されていますが、これは致命的なエラーであり、パイプラインの実行は停止されました。  このエラーの前に、エラーの詳細が記載されたエラー メッセージが報告されている可能性があります。|  
|0xC0047039|-1073450951|DTS_E_THREADCANCELLED|SSIS エラー コード DTS_E_THREADCANCELLED。  スレッド "%1" はシャットダウンの通知を受け取ったので終了処理中です。 ユーザーがシャットダウンを要求したか、別のスレッド内でエラーが発生したため、パイプラインがシャットダウンされます。  このエラーの前に、スレッドが取り消された理由の詳細が記載されたエラー メッセージが報告されている可能性があります。|  
|0xC004703A|-1073450950|DTS_E_DISTRIBUTORCANTSETPROPERTY|エラー 0x%8.8X により、スレッド "%1" のディストリビューターが、コンポーネント "%3" のプロパティ "%2" を初期化できませんでした。 ディストリビューターがコンポーネントのプロパティを初期化できなかったので、続行できません。|  
|0xC004703B|-1073450949|DTS_E_CANTREGISTERVIEWBUFFERTYPE|データ フロー タスクは、ビュー バッファーの種類を登録できません。 この種類には %1!d! 列含まれており、 これは入力 ID  %2!d! 用の種類です。|  
|0xC004703F|-1073450945|DTS_E_CANTCREATEEXECUTIONTREE|実行ツリーを作成するために必要なメモリが不足しています。|  
|0xC0047040|-1073450944|DTS_E_CANTINSERTINTOHASHTABLE|ハッシュ テーブルにオブジェクトを挿入するために必要なメモリが不足しています。|  
|0xC0047041|-1073450943|DTS_E_OBJECTNOTINHASHTABLE|オブジェクトはハッシュ テーブルに存在しません。|  
|0xC0047043|-1073450941|DTS_E_CANTCREATECOMPONENTVIEW|コンポーネント ビューを作成できません。別のコンポーネント ビューが既に存在します。 コンポーネント ビューは、一度に 1 つしか存在できません。|  
|0xC0047046|-1073450938|DTS_E_LAYOUTCANTSETUSAGETYPE|入力 "%1" (%2!d!) で、仮想入力列のコレクションに、系列 ID %3!d! の仮想入力列が含まれていません。|  
|0xC0047047|-1073450937|DTS_E_WRONGOBJECTTYPE|要求されたオブジェクトで、オブジェクトの種類が正しくありません。|  
|0xC0047048|-1073450936|DTS_E_CANTCREATESPOOLFILE|バッファー マネージャーで、BufferTempStoragePath プロパティのどのパスにも一時ストレージ ファイルを作成できません。 ファイル名が無効であるか、権限がないか、すべてのパスが使用済みです。|  
|0xC0047049|-1073450935|DTS_E_SEEKFAILED|バッファー マネージャーはファイル "%2" のオフセット %1!d! に シークできませんでした。 ファイルが破損しています。|  
|0xC004704A|-1073450934|DTS_E_EXTENDFAILED|バッファー マネージャーはファイル "%1" を長さ %2!lu! バイトです。  ディスク領域が不足しています。|  
|0xC004704B|-1073450933|DTS_E_FILEWRITEFAILED|バッファー マネージャーはファイル "%2" に %1!d! バイトを %1!d! バイトを書き込めません。 ディスク領域またはクォータが不足しています。|  
|0xC004704C|-1073450932|DTS_E_FILEREADFAILED|バッファー マネージャーはファイル "%2" から %1!d! バイトを 読み取れません。 ファイルが破損しています。|  
|0xC004704D|-1073450931|DTS_E_VIRTUALNOTSEQUENTIAL|バッファー ID %1!d! は、 他の仮想バッファーをサポートしているので、シーケンシャル モードに設定できません。 仮想バッファーがサポートされているバッファーで IDTSBuffer100.SetSequentialMode が呼び出されました。|  
|0xC004704E|-1073450930|DTS_E_BUFFERISREADONLY|バッファーは読み取り専用モードなので、この操作を実行できませんでした。 読み取り専用のバッファーは変更できません。|  
|0xC004704F|-1073450929|DTS_E_EXECUTIONTREECYCLESETTINGID|循環参照が作成されるので、ID %1 を %2!d! に 設定できません。|  
|0xC0047050|-1073450928|DTS_E_NOMOREBUFFERTYPES|バッファー マネージャーでバッファーの種類のテーブルを拡張中に、メモリが不足しました。 このエラーは、メモリ不足の状態が原因で発生します。|  
|0xC0047051|-1073450927|DTS_E_CANTCREATENEWTYPE|バッファー マネージャーは新しいバッファーの種類を作成できませんでした。|  
|0xC0047053|-1073450925|DTS_E_SCHEDULERBADTREE|データ フロー エンジン スケジューラはインデックス %1!d! の実行ツリーをレイアウトから 取得できませんでした。 スケジューラが、実在するよりも多くの実行ツリーを含んでいる数を受け取りました。|  
|0xC0047056|-1073450922|DTS_E_CANTCREATEPRIMEOUTPUTBUFFER|データ フロー タスクは、コンポーネント "%1" (%2!d!) の出力 "%3" (%4!d!) で PrimeOutput を呼び出すためのバッファーを作成できませんでした。 このエラーは、通常、メモリ不足の状態が原因で発生します。|  
|0xC0047057|-1073450921|DTS_E_SCHEDULERTHREADMEMORY|データ フロー エンジン スケジューラは、メモリ不足によりスレッド オブジェクトを作成できませんでした。 このエラーは、メモリ不足の状態が原因で発生します。|  
|0xC004705A|-1073450918|DTS_E_SCHEDULEROBJECT|データ フロー エンジン スケジューラは、ID %1!d! のオブジェクトをレイアウトから 取得できませんでした。 以前は存在し、現在は使用できなくなったオブジェクトが、データ フロー エンジン スケジューラにあります。|  
|0xC004705B|-1073450917|DTS_E_PREPARETREENODEFAILED|データ フロー タスクは、出力 "%1" (%2!d!) で始まる実行ツリー ノードのバッファーを準備できませんでした。|  
|0xC004705C|-1073450916|DTS_E_CANTCREATEVIRTUALBUFFER|データ フロー タスクは、実行の準備のための仮想バッファーを作成できません。|  
|0xC004705E|-1073450914|DTS_E_NOMOREIDS|ID の最大数に達しました。 オブジェクトへの割り当てに使用できる ID がありません。|  
|0xC004705F|-1073450913|DTS_E_ALREADYATTACHED|%1 は既にアタッチされているので、再度アタッチすることはできません。  デタッチしてから再度アタッチしてください。|  
|0xC0047060|-1073450912|DTS_E_OUTPUTCOLUMNNAMECONFLICT|出力 "%2" の列名 "%1" は、同期入力 "%3" の同じ名前の列と競合するので使用できません。|  
|0xC0047061|-1073450911|DTS_E_EOFANNOUNCEMENTFAILED|データ フロー タスクは、行セットの末尾を設定するためのバッファーを作成できません。|  
|0xC0047062|-1073450910|DTS_E_USERCOMPONENTEXCEPTION|マネージド ユーザー コンポーネントにより例外 "%1" がスローされました。|  
|0xC0047063|-1073450909|DTS_E_SCHEDULERMEMORY|データ フロー エンジン スケジューラの実行構造に十分なメモリを割り当てられません。 実行を開始する前に、システムのメモリが不足していました。|  
|0xC0047064|-1073450908|DTS_E_BUFFERNOOBJECTMEMORY|メモリ不足の状態により、バッファー オブジェクトを作成できませんでした。|  
|0xC0047065|-1073450907|DTS_E_BUFFERNOMAPMEMORY|メモリ不足の状態により、バッファーの系列 ID を DTP_HCOL インデックスにマップできません。|  
|0xC0047066|-1073450906|DTS_E_INDIVIDUALPUTVARIABLESFAILED|"%1!s!" が Variables コレクションをキャッシュできず、エラー コード 0x%2!8.8X が返されました。|  
|0xC0047067|-1073450905|DTS_E_INDIVIDUALPUTCOMPONENTMETADATAFAILED|"%1" がコンポーネント メタデータ オブジェクトをキャッシュできなかったので、エラー コード 0x%2!8.8X! が返されました。|  
|0xC0047068|-1073450904|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITION|"%1" には 0 以外の SortKeyPosition がありますが、その値 (%2!ld!) が大きすぎます。 値は、列数以下である必要があります。|  
|0xC004706A|-1073450902|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITIONS|%1 の IsSorted プロパティは True に設定されていますが、0 以外の出力列 SortKeyPositions の絶対値では、1 から始まり単調に増加するシーケンスが形成されません。|  
|0xC004706B|-1073450901|DTS_E_INDIVIDUALVALIDATIONSTATUSFAILED|"%1" が検証に失敗し、検証状態 "%2" が返されました。|  
|0xC004706C|-1073450900|DTS_E_CANTCREATECOMPONENT|コンポーネント "%1!s!" を 作成できなかったので、エラー コード 0x%2!8.8X!"%3!s!" が返されました 。 コンポーネントが正しく登録されていることを確認してください。|  
|0xC004706D|-1073450899|DTS_E_COMPONENTNOTREGISTERED|"%1" を含むモジュールは、登録されていないか、正しくインストールされていません。|  
|0xC004706E|-1073450898|DTS_E_COMPONENTNOTFOUND|"%1" を含むモジュールは登録されていますが、見つかりません。|  
|0xC004706F|-1073450897|DTS_E_BINARYCODENOTFOUND|スクリプト コンポーネントはスクリプトをプリコンパイルするように構成されていますが、バイナリ コードが見つかりません。 バイナリ コードを生成する [スクリプトのデザイン] をクリックして、スクリプト コンポーネント エディターの IDE にアクセスしてください。|  
|0xC0047070|-1073450896|DTS_E_CANTCREATEBLOBFILE|バッファー マネージャーはサイズの大きなオブジェクトをスプールするためのファイルを、BLOBTempStoragePath プロパティで指定されたディレクトリに作成できません。  指定されたファイル名が正しくないか、権限がないか、すべてのパスが使用済みです。|  
|0xC0047071|-1073450895|DTS_E_SYNCHRONOUSIDMISMATCH|"%1" の SynchronousInputID プロパティは %2!d! でしたが、%3!d! が 必要でした。|  
|0xC0047072|-1073450894|DTS_E_OBJECTIDNOTFOUND|ID が %1!d! のオブジェクトは存在しません。|  
|0xC0047073|-1073450893|DTS_E_OBJECTIDLOOKUPFAILED|エラー コード 0x%2!8.8X! により、 ID が %1!d! のオブジェクトが見つかりません。|  
|0xC0047074|-1073450892|DTS_E_INVALIDCODEPAGE|出力列 "%2" (%3!d!) で指定されている コード ページ %1!d! は無効です。 出力列 "%2" に別のコード ページを選択してください。|  
|0xC0047075|-1073450891|DTS_E_INDIVIDUALPUTEVENTINFOSFAILED|"%1" が EventInfos コレクションをキャッシュできなかったので、エラー コード 0x%2!8.8X! が返されました。|  
|0xC0047077|-1073450889|DTS_E_DUPLICATEOUTPUTCOLUMNNAMES|"%1" の名前が重複しています。  すべての名前は一意である必要があります。|  
|0xC0047078|-1073450888|DTS_E_NOOUTPUTCOLUMNFORINPUTCOLUMN|入力列 "%1" (%2!d!) に関連付けられた出力列がありません。|  
|0xC0047079|-1073450887|DTS_E_EXCLGRPNOSYNCINP|"%1" には、ルート ソースから拡張している仮想バッファーが存在します。 同期入力が 0 である、0 以外の除外グループが存在します。|  
|0xC004707A|-1073450886|DTS_E_ERROROUTCANTBEONSYNCNONEXCLUSIVEOUTPUT|エラー出力は非排他的な同期出力に設定できないので、"%1" をエラー出力にすることはできません。|  
|0xC004707B|-1073450885|DTS_E_EXPREVALDIVBYZERO|0 除算エラーが発生しました。 右辺のオペランドが式 "%1" で 0 に評価されます。|  
|0xC004707C|-1073450884|DTS_E_EXPREVALLITERALOVERFLOW|リテラル値 "%1" は、型 %2 には大きすぎます。 リテラル値が大きすぎて、型でオーバーフローが発生しています。|  
|0xC004707D|-1073450883|DTS_E_EXPREVALBINARYOPNUMERICOVERFLOW|データ型 %2 と %3 のバイナリ演算 "%1" の結果が数値型の最大サイズを超えています。 オペランドの型を、有効桁数または小数点以下桁数を失うことなく、数値型 (DT_NUMERIC) の結果に暗黙的にキャストできませんでした。 この演算を実行するには、演算子の一方または両方のオペランドでキャスト演算子により明示的にキャストする必要があります。|  
|0xC004707E|-1073450882|DTS_E_EXPREVALBINARYOPOVERFLOW|バイナリ演算 "%1" の結果が、結果のデータ型 "%2" の最大サイズを超えています。 演算結果の大きさが、結果の型をオーバーフローしています。|  
|0xC004707F|-1073450881|DTS_E_EXPREVALFUNCTIONOVERFLOW|関数呼び出し "%1" の結果が、型 "%2" には大きすぎます。 関数呼び出し結果の大きさが、オペランドの型をオーバーフローしています。 より大きい型に明示的にキャストする必要があります。|  
|0xC0047080|-1073450880|DTS_E_EXPREVALBINARYTYPEMISMATCH|データ型 "%1" と "%2" は、バイナリ演算子 "%3" と互換性がありません。 オペランドの型を、この演算と互換性のある型に暗黙的にキャストできませんでした。 この演算を実行するには、演算子の一方または両方のオペランドでキャスト演算子により明示的にキャストする必要があります。|  
|0xC0047081|-1073450879|DTS_E_EXPREVALUNSUPPORTEDBINARYTYPE|データ型 "%1" は、バイナリ演算子 "%2" と共に使用できません。 この演算では、一方または両方のオペランドの型がサポートされていません。 この演算を実行するには、演算子の一方または両方のオペランドでキャスト演算子により明示的にキャストする必要があります。|  
|0xC0047082|-1073450878|DTS_E_EXPREVALBINARYSIGNMISMATCH|演算 "%2" のビットごとのバイナリ演算子 "%1" で符号が一致しません。 この演算子のオペランドは、いずれも正またはいずれも負である必要があります。|  
|0xC0047083|-1073450877|DTS_E_EXPREVALBINARYOPERATIONFAILED|エラー コード 0x%2!8.8X! により、バイナリ演算 "%1" が失敗しました。 内部エラーが発生したか、メモリが不足しています。|  
|0xC0047084|-1073450876|DTS_E_EXPREVALBINARYOPERATIONSETTYPEFAILED|エラー コード 0x%2!8.8X! により、バイナリ演算 "%1" の結果の型を設定できませんでした。|  
|0xC0047085|-1073450875|DTS_E_EXPREVALSTRINGCOMPARISONFAILED|文字列 "%1" を文字列 "%2" と比較できませんでした。|  
|0xC0047086|-1073450874|DTS_E_EXPREVALUNSUPPORTEDUNNARYTYPE|データ型 "%1" は、単項演算子 "%2" と共に使用できません。 この演算では、このオペランドの型がサポートされていません。 この演算を実行するには、オペランドでキャスト演算子により明示的にキャストする必要があります。|  
|0xC0047087|-1073450873|DTS_E_EXPREVALUNARYOPERATIONFAILED|エラー コード 0x%2!8.8X! により、単項演算 "%1" が失敗しました。 内部エラーが発生したか、メモリが不足しています。|  
|0xC0047088|-1073450872|DTS_E_EXPREVALUNARYOPERATIONSETTYPEFAILED|エラー コード 0x%2!8.8X! により、単項演算 "%1" の結果の型を設定できませんでした。|  
|0xC0047089|-1073450871|DTS_E_EXPREVALPARAMTYPEMISMATCH|関数 "%1" は、パラメーター番号 %3!d! のデータ型 "%2" をサポートしていません。 パラメーターの型を、関数と互換性のある型に暗黙的にキャストできませんでした。 この演算を実行するには、オペランドでキャスト演算子により明示的にキャストする必要があります。|  
|0xC004708A|-1073450870|DTS_E_EXPREVALINVALIDFUNCTION|関数 "%1" は認識されませんでした。 関数名が正しくないか、または存在しません。|  
|0xC004708B|-1073450869|DTS_E_EXPREVALFNSUBSTRINGINVALIDLENGTH|長さ %1!d! は、 関数 "%2" では無効です。 長さのパラメーターには、負の数を指定できません。 長さのパラメーターを 0 または正の値に変更してください。|  
|0xC004708C|-1073450868|DTS_E_EXPREVALFNSUBSTRINGINVALIDSTARTINDEX|開始インデックス %1!d! は、 関数 "%2" では無効です。 開始インデックスの値には、0 より大きい整数値を指定する必要があります。 開始インデックスは 0 からではなく、1 から始める必要があります。|  
|0xC004708E|-1073450866|DTS_E_EXPREVALCHARMAPPINGFAILED|関数 "%1" は、文字列 "%2" で文字マッピングを実行できません。|  
|0xC004708F|-1073450865|DTS_E_EXPREVALINVALIDDATEPART|"%1" は、関数 "%2" に対して有効な日付部分ではありません。|  
|0xC0047090|-1073450864|DTS_E_EXPREVALINVALIDNULLPARAM|データ型が "%2" である 関数 NULL の %1!d! 番目のパラメーターが無効です。 NULL() のパラメーターは静的である必要があり、入力列などの動的な要素を含めることはできません。|  
|0xC0047091|-1073450863|DTS_E_EXPREVALINVALIDNULLPARAMTYPE|データ型が "%2" である 関数 NULL の %1!d! 番目のパラメーターが整数ではありません。 NULL() のパラメーターは、整数または整数に変換できる型である必要があります。|  
|0xC0047092|-1073450862|DTS_E_EXPREVALFUNCTIONPARAMNOTSTATIC|データ型が "%2" である 静的ではありません。 このパラメーターは静的である必要があり、入力列などの動的な要素を含めることはできません。|  
|0xC0047093|-1073450861|DTS_E_EXPREVALINVALIDCASTPARAM|データ型が "%2" である パラメーターが無効です。 キャスト演算子のパラメーターは静的である必要があり、入力列などの動的な要素を含めることはできません。|  
|0xC0047094|-1073450860|DTS_E_EXPREVALINVALIDCASTPARAMTYPE|データ型が "%2" である 整数ではありません。 キャスト演算子のパラメーターは、整数または整数に変換できる型である必要があります。|  
|0xC0047095|-1073450859|DTS_E_EXPREVALINVALIDCAST|式 "%1" をデータ型 "%2" からデータ型 "%3" にキャストできません。 要求されたキャストはサポートされていません。|  
|0xC0047096|-1073450858|DTS_E_EXPREVALINVALIDTOKEN|式 "%1" を解析できませんでした。  行番号 "%3"、文字番号 "%4" のトークン "%2" が認識されませんでした。 この式の、指定された場所に無効な要素が含まれているので、この式を解析できません。|  
|0xC0047097|-1073450857|DTS_E_EXPREVALUNEXPECTEDPARSEERROR|式 "%1" の解析中にエラーが発生しました。 式を解析できませんでした。原因は不明です。|  
|0xC0047098|-1073450856|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONWITHHR|式 "%1" を解析できませんでした。エラー コード 0x%2!8.8X! が返されました。 この式を解析できません。 無効な要素が含まれているか、適切な形式ではない可能性があります。 また、メモリが不足している可能性もあります。|  
|0xC0047099|-1073450855|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSION|式 "%1" は無効なので解析できません。 この式に無効な要素が含まれているか、式が適切な形式ではない可能性があります。|  
|0xC004709A|-1073450854|DTS_E_EXPREVALEXPRESSIONEMPTY|計算する式がありませんでした。 空の式の文字列を計算または取得しようとしました。|  
|0xC004709B|-1073450853|DTS_E_EXPREVALCOMPUTEFAILED|エラー コード 0x%2!8.8X! により、式 "%1" を計算できませんでした。|  
|0xC004709C|-1073450852|DTS_E_EXPREVALBUILDSTRINGFAILED|エラー コード 0x%1!8.8X! により、式の文字列表記を生成できませんでした。 式を表す表示可能な文字列の生成中に失敗しました。|  
|0xC004709D|-1073450851|DTS_E_EXPREVALCANNOTCONVERTRESULT|式の結果のデータ型 "%1" を列のデータ型 "%2" に変換できません。 式の結果は、入力列または出力列に書き込まれる必要がありますが、式のデータ型を列のデータ型に変換することができません。|  
|0xC004709E|-1073450850|DTS_E_EXPREVALCONDITIONALOPINVALIDCONDITIONTYPE|条件演算子の条件式 "%1" に無効なデータ型 "%2" が使用されています。 条件演算子の条件式は DT_BOOL 型のブール値を返す必要があります。|  
|0xC004709F|-1073450849|DTS_E_EXPREVALCONDITIONALOPTYPEMISMATCH|データ型 "%1" と "%2" は、条件演算子と互換性がありません。 オペランドの型を暗黙的に条件演算子と互換性のある型にキャストできません。 この演算を実行するには、演算子の一方または両方のオペランドでキャスト演算子により明示的にキャストする必要があります。|  
|0xC00470A0|-1073450848|DTS_E_EXPREVALCONDITIONALOPSETTYPEFAILED|エラー コード 0x%2!8.8X! により、条件演算 "%1" の結果の型を設定できませんでした。|  
|0xC00470A1|-1073450847|DTS_E_BUFFERORPHANED|このバッファーは孤立しています。 未解決のバッファーを残したまま、バッファー マネージャーがシャットダウンされたため、バッファーがクリーンアップされません。 メモリ リークや他の問題が発生する可能性があります。|  
|0xC00470A2|-1073450846|DTS_E_EXPREVALINPUTCOLUMNNAMENOTFOUND|エラー コード 0x%2!8.8X! により、"%1" という名前の入力列を検索できませんでした。 指定された入力列が入力列のコレクションに見つかりませんでした。|  
|0xC00470A3|-1073450845|DTS_E_EXPREVALINPUTCOLUMNIDNOTFOUND|エラー コード 0x%2!8.8X! により、系列 ID %1!d! の入力列を 検索できませんでした。 入力列が入力列のコレクションに見つかりませんでした。|  
|0xC00470A4|-1073450844|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNNAME|式に、認識できないトークン "%1" が含まれています。 "%1" が変数の場合、トークンは "\@%1" と表記される必要があります。 指定されたトークンが無効です。 トークンが変数名である場合、先頭に \@ 記号を付ける必要があります。|  
|0xC00470A5|-1073450843|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNID|式に、認識できないトークン "#%1!d!" が含まれています。|  
|0xC00470A6|-1073450842|DTS_E_EXPREVALVARIABLENOTFOUND|変数 "%1" が Variables コレクションに見つかりませんでした。 変数が正しいスコープに存在しない可能性があります。|  
|0xC00470A7|-1073450841|DTS_E_EXPREVALINVALIDTOKENSTATE|式 "%1" を解析できませんでした。 この式には無効なトークン、不完全なトークン、または無効な要素が含まれている可能性があります。 また、適切な形式ではないか、かっこなどの必要な要素の一部が不足している可能性があります。|  
|0xC00470A8|-1073450840|DTS_E_BLANKOUTPUTCOLUMNNAME|"%1" の名前が指定されていません。名前を空白にすることはできません。|  
|0xC00470A9|-1073450839|DTS_E_HASSIDEEFFECTSWITHSYNCINP|"%1" では HasSideEffects プロパティが True に設定されていますが、"%1" は同期型なので副作用は発生しません。 HasSideEffects プロパティを False に設定してください。|  
|0xC00470AA|-1073450838|DTS_E_EXPREVALINVALIDCASTCODEPAGE|データ型 "%2" へのキャストのコード ページ パラメーターに指定された値 %1!d! が無効です。 指定されたコード ページはコンピューターにインストールされていません。|  
|0xC00470AB|-1073450837|DTS_E_EXPREVALINVALIDCASTPRECISION|値 %1!d! は キャストの有効桁数のパラメーターに指定された値 %1!d! が無効です。 有効桁数は %3!d! から %4!d! までの範囲で指定する 必要がありますが、 有効桁数が型キャストの範囲外です。|  
|0xC00470AC|-1073450836|DTS_E_EXPREVALINVALIDCASTSCALE|値 %1!d! は キャストの小数点以下桁数のパラメーターに指定された値 %1!d! が無効です。 小数点以下桁数は %3!d! から %4!d! までの範囲で指定する 必要がありますが、 小数点以下桁数が型キャストの範囲外です。 小数点以下桁数は有効桁数よりも大きい値にすることはできず、正の値にする必要があります。|  
|0xC00470AD|-1073450835|DTS_E_NONSORTEDOUTPUTHASSORTKEYPOSITIONS|"%1" の IsSorted プロパティは false に設定されていますが、 出力列 SortKeyPositions の %2!lu! は 0 以外です。|  
|0xC00470AF|-1073450833|DTS_E_EXPREVALCONDITIONALOPCODEPAGEMISMATCH|型 %2 の条件演算子 "%1" のオペランドでは、コード ページが一致している必要があります。 左辺オペランドのコード ページと右辺オペランドのコード ページが一致しません。 指定された型の条件演算子では、コード ページが同一である必要があります。|  
|0xC00470B1|-1073450831|DTS_E_REFERENCEDMETADATABADCOUNT|入力 "%1" (%2!d!) は入力 "%3" (%4!d!) を参照しますが、両方の入力に含まれる列数が同じではありません。 入力 %5!d! には %6!d! 列が含まれていますが、 入力 %7!d! には %8!d! 列 含まれています。|  
|0xC00470B2|-1073450830|DTS_E_OBJECTLINEAGEIDNOTFOUND|系列 ID が %1!d! のオブジェクトは存在しません。|  
|0xC00470B3|-1073450829|DTS_E_FILENAMEOUTPUTCOLUMNOTFOUND|ファイル名の出力列が見つかりません。|  
|0xC00470B4|-1073450828|DTS_E_FILENAMEOUTPUTCOLUMNINVALIDDATATYPE|ファイル名の出力列のデータ型は DT_WSTR ですが、NULL 終端の Unicode 文字列ではありません。|  
|0xC00470B5|-1073450827|DTS_E_DISTRIBUTORADDFAILED|エラー 0x%2!8.8X! により、ディストリビューターはスレッド "%1" にバッファーを提供できませんでした。 対象のスレッドが終了する可能性があります。|  
|0xC00470B6|-1073450826|DTS_E_LOCALENOTINSTALLED|このシステムには、 LocaleID 1!ld! がインストールされていません。|  
|0xC00470B7|-1073450825|DTS_E_EXPREVALILLEGALHEXESCAPEINSTRINGLITERAL|文字列リテラル "%1" に、無効な 16 進数のエスケープ シーケンス "\x%2" が含まれています。 このエスケープ シーケンスは、式エバリュエーターの文字列リテラルでサポートされていません。 16 進数のエスケープ シーケンスは、\xhhhh という形式で表す必要があります。ここで、h は有効な 16 進数の桁を示します。|  
|0xC00470B8|-1073450824|DTS_E_EXPREVALILLEGALESCAPEINSTRINGLITERAL|文字列リテラル "%1" に、無効なエスケープ シーケンス "\\%2!c!" が含まれています。 このエスケープ シーケンスは、式エバリュエーターの文字列リテラルでサポートされていません。 文字列に円記号が必要な場合は、2 つの円記号 "\\\\" を続けて入力してください。|  
|0xC00470B9|-1073450823|DTS_E_NOOUTPUTCOLUMNS|"%1" には出力列が含まれていません。 非同期出力には出力列が必要です。|  
|0xC00470BA|-1073450822|DTS_E_LOBDATATYPENOTSUPPORTED|"%1" には、サポートされていない大きなサイズのオブジェクトのデータ型 (DT_TEXT、DT_NTEXT、または DT_IMAGE) があります。|  
|0xC00470BB|-1073450821|DTS_E_OUTPUTWITHMULTIPLEERRORS|出力 ID %1!d! が複数のエラー出力の構成に指定されました。 最初は %2!d! と %3!d!、次は %4!d! と %5!d! です。|  
|0xC00470BC|-1073450820|DTS_E_FAILEDDURINGOLEDBDATATYPECONVERSIONCHECK|OLE DB プロバイダーが、"%1" のデータ型変換の確認中に失敗しました。|  
|0xC00470BD|-1073450819|DTS_E_BUFFERISEOR|このバッファーは行セットの末尾を表すので、その行数を変更できません。  行セット フラグの末尾を保持するバッファーで AddRow または RemoveRow が呼び出されました。|  
|0xC00470BE|-1073450818|DTS_E_EXPREVALUNSUPPORTEDTYPE|データ型 "%1" は、式ではサポートされていません。 指定した型がサポートされていないか、無効です。|  
|0xC00470BF|-1073450817|DTS_E_PRIMEOUTPUTNOEOR|"%1" の PrimeOutput メソッドからサクセス コードが返されましたが、行セットの末尾が報告されませんでした。 コンポーネントでエラーが発生しています。 通常は、このコンポーネントから行の末尾が報告されます。 予期されない結果が返されることを回避するため、パイプラインはシャットダウンされます。|  
|0xC00470C0|-1073450816|DTS_E_EXPREVALDATACONVERSIONOVERFLOW|データ型 "%1" からデータ型 "%2" への変換中にオーバーフローが発生しました。 変換先の型に対して変換元の型が大きすぎます。|  
|0xC00470C1|-1073450815|DTS_E_EXPREVALDATACONVERSIONNOTSUPPORTED|データ型 "%1" からデータ型 "%2" への変換はサポートされていません。 変換元のデータ型を変換先のデータ型に変換できません。|  
|0xC00470C2|-1073450814|DTS_E_EXPREVALDATACONVERSIONFAILED|データ型 %2 からデータ型 %3 への変換中に エラー コード 0x%1!8.8X! が返されました。|  
|0xC00470C3|-1073450813|DTS_E_EXPREVALCONDITIONALOPERATIONFAILED|エラー コード 0x%2!8.8X! により、条件演算 "%1" が失敗しました。 内部エラーが発生したか、メモリが不足しています。|  
|0xC00470C4|-1073450812|DTS_E_EXPREVALCASTFAILED|エラー コード 0x%4!8.8X! により、データ型 "%2" からデータ型 "%3" に式 "%1" をキャストできませんでした。|  
|0xC00470C5|-1073450811|DTS_E_EXPREVALFUNCTIONCOMPUTEFAILED|エラー コード 0x%2!8.8X! により、関数 "%1" を評価できませんでした。|  
|0xC00470C6|-1073450810|DTS_E_EXPREVALFUNCTIONCONVERTPARAMTOMEMBERFAILED|データ型が "%2" である 静的な値に変換できません。|  
|0xC00470C7|-1073450809|DTS_E_REDIRECTROWUNAVAILABLEWITHFASTLOADANDZEROMAXINSERTCOMMITSIZE|高速読み込みオプションが有効で、挿入コミット サイズの最大値が 0 に設定されている場合、"%1" のエラー行の処理を行のリダイレクトに設定することはできません。|  
|0xC00470CE|-1073450802|DTS_E_EXPREVALBINARYOPERATORCODEPAGEMISMATCH|型 "%2" のバイナリ演算子 "%1" のオペランドに対するコード ページは一致する必要があります。 現在、左辺オペランドのコード ページと右辺オペランドのコード ページが一致しません。 指定された型の指定されたバイナリ演算子では、コード ページが同一である必要があります。|  
|0xC00470CF|-1073450801|DTS_E_EXPREVALVARIABLECOMPUTEFAILED|エラー コード 0x%2!8.8X! により、変数 "%1" の値を取得できませんでした。|  
|0xC00470D0|-1073450800|DTS_E_EXPREVALVARIABLETYPENOTSUPPORTED|変数 "%1" のデータ型は、式ではサポートされていません。|  
|0xC00470D1|-1073450799|DTS_E_EXPREVALCASTCODEPAGEMISMATCH|式 "%1" をデータ型 "%2" からデータ型 "%3" にキャストできません。キャストされている値のコード ページ (%4!d!) が、要求された結果コード ページ (%5!d!) と一致しません。 キャスト元のコード ページは、キャスト先として要求されているコード ページと一致する必要があります。|  
|0xC00470D2|-1073450798|DTS_E_BUFFERSIZEOUTOFRANGE|既定のバッファー サイズは、%1!d! から %2!d! バイトです。 DefaultBufferSize プロパティに設定しようとした値が小さすぎるか、大きすぎます。|  
|0xC00470D3|-1073450797|DTS_E_BUFFERMAXROWSIZEOUTOFRANGE|バッファー最大行数の既定値は、%1!d! キャッシュされました。 DefaultBufferMaxRows プロパティに設定しようとした値が小さすぎます。|  
|0xC00470D4|-1073450796|DTS_E_EXTERNALCOLUMNMETADATACODEPAGEMISMATCH|%1 のコード ページは %2!d! ですが、 %3!d! である必要があります。|  
|0xC00470D5|-1073450795|DTS_E_THREADCOUNTOUTOFRANGE|データ フロー タスクの EngineThreads プロパティに %3!d! を 割り当てることができませんでした。 %1!d! ～ %2!d! の値を 指定する必要があります。|  
|0xC00470D6|-1073450794|DTS_E_EXPREVALINVALIDTOKENSINGLEQUOTE|式 "%1" を解析できませんでした。 行番号 "%2"、文字番号 "%3" の単一引用符は予期されていませんでした。|  
|0xC00470D7|-1073450793|DTS_E_EXPREVALINVALIDTOKENSINGLEEQUAL|式 "%1" を解析できませんでした。 行番号 "%2"、文字番号 "%3" の等号 (=) は予期されていませんでした。 指定された場所に 2 つの等号 (==) が必要である可能性があります。|  
|0xC00470DA|-1073450790|DTS_E_INDIVIDUALPUTREFTRACKERFAILED|コンポーネント "%1" はランタイム オブジェクト参照トラッカーのコレクションをキャッシュできませんでした。エラー コード 0x%2!8.8X! が返されました。|  
|0xC00470DB|-1073450789|DTS_E_EXPREVALAMBIGUOUSINPUTCOLUMNNAME|名前 "%1" の入力列が複数あります。 必要な入力列を [コンポーネント名].[%2] という形式で一意に指定するか、系列 ID で参照する必要があります。 現在、指定された入力列が複数のコンポーネントに存在します。|  
|0xC00470DC|-1073450788|DTS_E_EXPREVALDOTTEDINPUTCOLUMNNAMENOTFOUND|エラー コード 0x%3!8.8X! により、"[%1].[%2]" という名前の入力列を検出できませんでした。 入力列が入力列のコレクションに見つかりませんでした。|  
|0xC00470DD|-1073450787|DTS_E_EXPREVALAMBIGUOUSVARIABLENNAME|名前 "%1" の変数が複数あります。 必要な変数を \@[Namespace::%2] という形式で一意に指定する必要があります。 この変数が複数の名前空間に存在します。|  
|0xC00470DE|-1073450786|DTS_E_REDUCTIONFAILED|データ フロー エンジン スケジューラがパイプラインの実行プランを短縮できませんでした。 OptimizedMode プロパティを False に設定してください。|  
|0xC00470DF|-1073450785|DTS_E_EXPREVALSQRTINVALIDPARAM|関数 SQRT は負の値では演算できませんが、SQRT 関数に負の値が渡されました。|  
|0xC00470E0|-1073450784|DTS_E_EXPREVALLNINVALIDPARAM|関数 LN は 0 または負の値では演算できませんが、LN 関数に 0 または負の値が渡されました。|  
|0xC00470E1|-1073450783|DTS_E_EXPREVALLOGINVALIDPARAM|関数 LOG は 0 または負の値では演算できませんが、LOG 関数に 0 または負の値が渡されました。|  
|0xC00470E2|-1073450782|DTS_E_EXPREVALPOWERINVALIDPARAM|関数 POWER に渡されたパラメーターを評価できません。不確定な結果が生じます。|  
|0xC00470E3|-1073450781|DTS_E_NOCANCELEVENT|エラー 0x%1!8.8X! により、ランタイムがキャンセル イベントを提供できません。|  
|0xC00470E4|-1073450780|DTS_E_CANCELRECEIVED|パイプラインはキャンセル要求を受け取ったので、シャットダウンされています。|  
|0xC00470E5|-1073450779|DTS_E_EXPREVALUNARYOPOVERFLOW|単項マイナス (否定) 演算 "%1" の結果が、結果のデータ型 "%2" の最大サイズを超えています。 演算結果の大きさが、結果の型をオーバーフローしています。|  
|0xC00470E6|-1073450778|DTS_E_EXPREVALPLACEHOLDERINEXPRESSION|式にプレースホルダー "%1" が見つかりました。 このプレースホルダーは、実際のパラメーターまたはオペランドに置き換える必要があります。|  
|0xC00470E7|-1073450777|DTS_E_EXPREVALFNRIGHTINVALIDLENGTH|長さ %1!d! は、 負の値なので無効です。 長さのパラメーターは正の値にする必要があります。|  
|0xC00470E8|-1073450776|DTS_E_EXPREVALFNREPLICATEINVALIDREPEATCOUNT|繰り返し回数 %1!d! は 負の値なので、関数 "%2" には無効です。 繰り返し回数のパラメーターには負の値を指定できません。|  
|0xC00470EA|-1073450774|DTS_E_EXPREVALVARIABLECOULDNOTBEREAD|エラー コード 0x%2!8.8X! により、変数 "%1" を読み取れませんでした。|  
|0xC00470EC|-1073450772|DTS_E_EXPREVALBINARYOPDTSTRNOTSUPPORTED|バイナリ演算のオペランドでは、データ型 DT_STR は入力列およびキャスト演算のみでサポートされています。 式 "%1" には、入力列またはキャストの結果ではない DT_STR オペランドが含まれています。このオペランドはバイナリ演算では使用できません。 この演算を実行するには、オペランドでキャスト演算子により明示的にキャストする必要があります。|  
|0xC00470ED|-1073450771|DTS_E_EXPREVALCONDITIONALOPDTSTRNOTSUPPORTED|条件演算子のオペランドでは、データ型 DT_STR は入力列およびキャスト演算のみでサポートされています。 式 "%1" には、入力列またはキャストの結果ではない DT_STR オペランドが含まれています。このオペランドは条件演算では使用できません。 この演算を実行するには、オペランドでキャスト演算子により明示的にキャストする必要があります。|  
|0xC00470EE|-1073450770|DTS_E_EXPREVALFNFINDSTRINGINVALIDOCCURRENCECOUNT|発生回数 %1!d! は、 関数 "%2" では無効です。 このパラメーターには、0 より大きい値を指定する必要があります。|  
|0xC00470EF|-1073450769|DTS_E_INDIVIDUALPUTLOGENTRYINFOS|"%1" は LogEntryInfos コレクションをキャッシュできませんでした。エラー コード 0x%2!8.8X! が返されました。|  
|0xC00470F0|-1073450768|DTS_E_EXPREVALINVALIDDATEPARTNODE|関数 "%1" に指定された日付部分のパラメーターが無効です。 静的な文字列を指定する必要があります。  日付部分のパラメーターには、入力列などの動的な要素を含めることはできません。また、型は DT_WSTR である必要があります。|  
|0xC00470F1|-1073450767|DTS_E_EXPREVALINVALIDCASTLENGTH|値 %1!d! は キャストの長さのパラメーターに指定された値 %1!d! は、負の値なので無効です。 長さには正の値を指定してください。|  
|0xC00470F2|-1073450766|DTS_E_EXPREVALINVALIDNULLCODEPAGE|値 %1!d! は NULL 関数のコード ページ パラメーターに指定された値 %1!d! が無効です。 指定されたコード ページはコンピューターにインストールされていません。|  
|0xC00470F3|-1073450765|DTS_E_EXPREVALINVALIDNULLPRECISION|値 %1!d! は 指定された NULL 関数の有効桁数のパラメーターに指定された値 %1!d! が範囲外です。 有効桁数は %3!d! から %4!d! までの範囲で指定する %4!d! までの範囲で指定する必要があります。|  
|0xC00470F4|-1073450764|DTS_E_EXPREVALINVALIDNULLSCALE|値 %1!d! は 指定された NULL 関数の小数点以下桁数のパラメーターに指定された値 %1!d! が範囲外です。 小数点以下桁数は %3!d! から %4!d! までの範囲で指定する必要があります。 小数点以下桁数は、有効桁数よりも大きい値にすることも負の値にすることもできません。|  
|0xC00470F5|-1073450763|DTS_E_EXPREVALINVALIDNULLLENGTH|値 %1!d! は 指定された "NULL" 関数の長さのパラメーターに指定された値 %1!d! は、負の値なので無効です。 長さには正の値を指定してください。|  
|0xC00470F6|-1073450762|DTS_E_NEGATIVESNOTALLOWED|%1 には負の値を代入できません。|  
|0xC00470F7|-1073450761|DTS_E_FASTPARSENOTALLOWED|"%2" の "%1" カスタム プロパティを True に設定できません。  列のデータ型には次のいずれかを指定する必要があります: DT_I1、DT_I2、DT_I4、DT_I8、DT_UI1、DT_UI2、DT_UI4、DT_UI8、DT_DBTIMESTAMP、DT_DBTIMESTAMP2、DT_DBTIMESTAMPOFFSET、DT_DATE、DT_DBDATE、DT_DBTIME、DT_DBTIME2、または DT_FILETIME。|  
|0xC00470F8|-1073450760|DTS_E_CANNOTREATTACHPATH|"%1" を再アタッチできません。 パスを削除し、新しいパスを追加してから、アタッチしてください。|  
|0xC00470F9|-1073450759|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALSINGULAR|関数 "%1" に必要なパラメーター数は %3!d! ではなく %2!d! です。 関数名は認識されましたが、パラメーター数が無効です。|  
|0xC00470FA|-1073450758|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSSINGULARPLURAL|関数 "%1" に必要なパラメーター数は %3!d! ではなく %2!d! です。 関数名は認識されましたが、パラメーター数が無効です。|  
|0xC00470FB|-1073450757|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALPLURAL|関数 "%1" に必要なパラメーター数は %3!d! ではなく %2!d! です。 関数名は認識されましたが、パラメーター数が無効です。|  
|0xC00470FC|-1073450756|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONOUTOFMEMORY|式 "%1" を解析しようとしましたが失敗しました。メモリが不足しています。|  
|0xC00470FD|-1073450755|DTS_E_INDIVIDUALCHECKPRODUCTLEVELFAILED|%1 は、必要な製品レベル チェックを実行できず、エラー コード 0x%2!8.8X! を返しました。|  
|0xC00470FE|-1073450754|DTS_E_PRODUCTLEVELTOLOW|SSIS エラー コード DTS_E_PRODUCTLEVELTOLOW。  インストールされている Integration Services %2 では %1 を実行できません。 %3 以上が必要です。|  
|0xC00470FF|-1073450753|DTS_E_EXPREVALSTRINGLITERALTOOLONG|式の文字列リテラルの長さが許容最大長の %1!d! 文字を 超えています。|  
|0xC0047100|-1073450752|DTS_E_EXPREVALSTRINGVARIABLETOOLONG|変数 %1 に許容最大長の %2!d! 文字を超える文字列が 超えています。|  
|0xC0047101|-1073450751|DTS_E_COMPONENT_NOINTERFACE|%1 は検出されましたが、必要な Integration Services インターフェイス (IDTSRuntimeComponent100) をサポートしていません。  このコンポーネントの更新バージョンをコンポーネント プロバイダーから入手してください。|  
|0xC0048000|-1073446912|DTS_E_CANNOTOPENREGISTRYKEY|レジストリ キー "%1" を開けません。|  
|0xC0048001|-1073446911|DTS_E_INVALIDCOMPONENTFILENAME|CLSID "%1" のコンポーネントのファイル名を取得できません。 コンポーネントが正しく登録されていること、または指定された CLSID が正しいことを確認してください。|  
|0xC0048002|-1073446910|DTS_E_UNKNOWNCOMPONENTHASINVALIDCLSID|コンポーネントのいずれかの CLSID が無効です。 パイプラインに含まれているすべてのコンポーネントの CLSID が有効であることを確認してください。|  
|0xC0048003|-1073446909|DTS_E_COMPONENTHASINVALIDCLSID|ID %1!d! のコンポーネントのいずれかの CLSID が 無効です。|  
|0xC0048004|-1073446908|DTS_E_INVALIDINDEX|インデックスが無効です。|  
|0xC0048005|-1073446907|DTS_E_CANNOTACCESSDTSAPPLICATIONOBJECT|アプリケーション オブジェクトにアクセスできません。 SSIS が正しくインストールされていることを確認してください。|  
|0xC0048006|-1073446906|DTS_E_ERROROCCURREDWHILERETRIEVINGFILENAME|エラー コード 0x%1!8.8X! により、コンポーネントのファイル名を取得できませんでした。|  
|0xC0048007|-1073446905|DTS_E_CANNOTRETRIEVEPROPERTYFORCOMPONENT|ID %2!d! のコンポーネントからプロパティ "%1" を取得できません。|  
|0xC0048008|-1073446904|DTS_E_DUPLICATEIDFOUND|データ フロー タスクで ID %1!d! を 複数回使用しようとしています。|  
|0xC0048009|-1073446903|DTS_E_CANNOTRETRIEVEBYLINEAGE|列を含まないコレクションから系列 ID で項目を取得できません。|  
|0xC004800B|-1073446901|DTS_E_CANNOTMAPRUNTIMECONNECTIONMANAGER|エラー コード 0x%2!8.8X! により、接続マネージャー コレクションに ID "%1" の接続マネージャーが見つかりません。 この接続マネージャーは、%4 の接続マネージャー コレクションに含まれる "%3" で必要です。 接続マネージャー コレクションである Connections に含まれる接続マネージャーが、同じ ID で作成されていることを確認してください。|  
|0xC004800E|-1073446898|DTS_E_INPUTNOTKNOWN|スレッド "%1" で入力 %2!d! のバッファーを受け取りましたが、スレッドがこの入力に対応していません。 データ フロー エンジン スケジューラで正しくない実行プランが構築されたことが原因で、エラーが発生しました。|  
|0xC004800F|-1073446897|DTS_E_GETRTINTERFACEFAILED|コンポーネント "%1" (%2!d!) により IDTSRuntimeComponent100 インターフェイスを提供できません。|  
|0xC0048011|-1073446895|DTS_E_CANTGIVEAWAYBUFFER|データ フロー タスク エンジンは、別のスレッドに割り当てるバッファーをコピーしようとして失敗しました。|  
|0xC0048012|-1073446894|DTS_E_CANTCREATEVIEWBUFFER|データ フロー タスク エンジンは、バッファー %3!d の 種類 %2!d! に対して種類 %1!d! のバッファー ビューを 作成できませんでした。|  
|0xC0048013|-1073446893|DTS_E_UNUSABLETEMPORARYPATH|バッファー マネージャーはパス "%1" に一時ファイルを作成できませんでした。 このパスは一時保存域として見なされません。|  
|0xC0048014|-1073446892|DTS_E_DIRECTTONONERROROUTPUT|バッファー マネージャーは、エラー出力として登録されていない出力に、エラー行を出力しようとしました。 IsErrorOut プロパティが True に設定されていない出力で DirectErrorRow が呼び出されました。|  
|0xC0048015|-1073446891|DTS_E_BUFFERISPRIVATE|プライベート バッファーでバッファー メソッドが呼び出されましたが、プライベート バッファーではこの操作がサポートされていません。|  
|0xC0048016|-1073446890|DTS_E_BUFFERISFLAT|プライベート モードのバッファーでは、この操作がサポートされていません。|  
|0xC0048017|-1073446889|DTS_E_BUFFERISPRIMEOUTPUT|PrimeOutput に渡されたバッファーではこの操作を呼び出せません。 PrimeOutput の呼び出し中にバッファー メソッドが呼び出されましたが、この呼び出しを PrimeOutput の呼び出し中に行うことはできません。|  
|0xC0048018|-1073446888|DTS_E_BUFFERISPROCESSINPUT|ProcessInput に渡されたバッファーではこの操作を呼び出せません。 ProcessInput の呼び出し中にバッファー メソッドが呼び出されましたが、この呼び出しを ProcessInput の呼び出し中に行うことはできません。|  
|0xC0048019|-1073446887|DTS_E_BUFFERGETTEMPFILENAME|バッファー マネージャーは一時ファイルの名前を取得できませんでした。|  
|0xC004801A|-1073446886|DTS_E_REFERENCECOLUMNTOOWIDE|コードにより、幅が大きすぎる列が検出されました。|  
|0xC004801B|-1073446885|DTS_E_CANNOTGETRUNTIMECONNECTIONMANAGERID|エラー コード 0x%3!8.8X! により、"%2" の接続マネージャー コレクション Connections の "%1" で指定されているランタイム接続マネージャーの ID を取得できません。 ランタイム接続オブジェクトの ConnectionManager.ID プロパティが、コンポーネントに設定されていることを確認してください。|  
|0xC004801C|-1073446884|DTS_E_EMPTYRUNTIMECONNECTIONMANAGERID|"%2" の接続マネージャー コレクション Connections の "%1" には ID プロパティの値がありません。 このコンポーネントに、ランタイム接続オブジェクトの ConnectionManagerID プロパティが設定されていることを確認してください。|  
|0xC004801D|-1073446883|DTS_E_METADATAREADONLY|実行中にメタデータを変更することはできません。|  
|0xC004801F|-1073446881|DTS_E_UPGRADEFAILED|"%1" のコンポーネント メタデータをコンポーネントの新しいバージョンにアップグレードできませんでした。 PerformUpgrade メソッドを実行できませんでした。|  
|0xC0048020|-1073446880|DTS_E_COMPONENTVERSIONMISMATCH|%1 のバージョンは、このバージョンの DataFlow と互換性がありません。|  
|0xC0048021|-1073446879|DTS_E_ERRORCOMPONENT|コンポーネントが見つからないか、登録されていないか、アップグレードできないか、コンポーネントに必要なインターフェイスが見つかりません。 このコンポーネントの連絡先情報は "%1" です。|  
|0xC0048022|-1073446878|DTS_E_BUFFERISNOTPRIMEOUTPUT|正しくないバッファーでメソッドが呼び出されました。 コンポーネントの出力に使用されていないバッファーでは、この操作はサポートされていません。|  
|0xC0049014|-1073442796|DTS_E_EXPREVALSTATIC_COMPUTATIONFAILED|式の計算中にエラーが発生しました。|  
|0xC0049030|-1073442768|DTS_E_EXPREVALSTATIC_DIVBYZERO|式で 0 除算が発生しました。|  
|0xC0049031|-1073442767|DTS_E_EXPREVALSTATIC_LITERALOVERFLOW|リテラル値の大きさが、大きすぎて要求された型に収まりませんでした。|  
|0xC0049032|-1073442766|DTS_E_EXPREVALSTATIC_BINARYOPNUMERICOVERFLOW|バイナリ演算の結果が数値型の最大サイズに対して大きすぎます。 オペランドの型を、有効桁数または小数点以下桁数を失うことなく、数値型 (DT_NUMERIC) の結果に暗黙的にキャストできませんでした。 この演算を実行するには、演算子の一方または両方のオペランドでキャスト演算子により明示的にキャストする必要があります。|  
|0xC0049033|-1073442765|DTS_E_EXPREVALSTATIC_BINARYOPOVERFLOW|バイナリ演算結果の大きさが、結果のデータ型の最大サイズをオーバーフローしています。|  
|0xC0049034|-1073442764|DTS_E_EXPREVALSTATIC_FUNCTIONOVERFLOW|関数呼び出し結果の大きさが、大きすぎて結果の型に収まらず、オペランドの型をオーバーフローしました。 より大きい型に明示的にキャストする必要があります。|  
|0xC0049035|-1073442763|DTS_E_EXPREVALSTATIC_BINARYTYPEMISMATCH|互換性のないデータ型がバイナリ演算子と一緒に使用されました。 オペランドの型を、この演算と互換性のある型に暗黙的にキャストできませんでした。 この演算を実行するには、演算子の一方または両方のオペランドでキャスト演算子により明示的にキャストする必要があります。|  
|0xC0049036|-1073442762|DTS_E_EXPREVALSTATIC_UNSUPPORTEDBINARYTYPE|サポートされていないデータ型が、バイナリ演算子と共に使用されました。 この演算では、一方または両方のオペランドの型がサポートされていません。 この演算を実行するには、演算子の一方または両方のオペランドでキャスト演算子により明示的にキャストする必要があります。|  
|0xC0049037|-1073442761|DTS_E_EXPREVALSTATIC_BINARYSIGNMISMATCH|ビットごとのバイナリ演算子の符号が一致しません。 この演算子のオペランドは、いずれも正またはいずれも負である必要があります。|  
|0xC0049038|-1073442760|DTS_E_EXPREVALSTATIC_BINARYOPERATIONFAILED|バイナリ演算が失敗しました。 メモリが不足していたか、内部エラーが発生しました。|  
|0xC0049039|-1073442759|DTS_E_EXPREVALSTATIC_BINARYOPERATIONSETTYPEFAILED|バイナリ演算の結果の型を設定できませんでした。|  
|0xC004903A|-1073442758|DTS_E_EXPREVALSTATIC_STRINGCOMPARISONFAILED|2 つの文字列を比較できません。|  
|0xC004903B|-1073442757|DTS_E_EXPREVALSTATIC_UNSUPPORTEDUNNARYTYPE|サポートされていないデータ型が、単項演算子と共に使用されました。 この演算では、このオペランドの型がサポートされていません。 この演算を実行するには、オペランドでキャスト演算子により明示的にキャストする必要があります。|  
|0xC004903C|-1073442756|DTS_E_EXPREVALSTATIC_UNARYOPERATIONFAILED|単項演算が失敗しました。 メモリが不足しているか、内部エラーが発生しました。|  
|0xC004903D|-1073442755|DTS_E_EXPREVALSTATIC_UNARYOPERATIONSETTYPEFAILED|単項演算の結果の型を設定できませんでした。|  
|0xC004903E|-1073442754|DTS_E_EXPREVALSTATIC_PARAMTYPEMISMATCH|関数にサポートされていないデータ型を持つパラメーターがあります。 パラメーターの型を、関数と互換性のある型に暗黙的にキャストできません。 この演算を実行するには、オペランドでキャスト演算子により明示的にキャストする必要があります。|  
|0xC004903F|-1073442753|DTS_E_EXPREVALSTATIC_INVALIDFUNCTION|式に無効な関数名があります。 関数名が正しく、存在することを確認してください。|  
|0xC0049040|-1073442752|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDLENGTH|長さのパラメーターが、関数 SUBSTRING では無効です。 長さのパラメーターには、負の数を指定できません。|  
|0xC0049041|-1073442751|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDSTARTINDEX|開始インデックスは、関数 SUBSTRING では無効です。 開始インデックスの値には、0 より大きい整数値を指定する必要があります。 開始インデックスは 0 からではなく、1 から始まります。|  
|0xC0049042|-1073442750|DTS_E_EXPREVALSTATIC_INVALIDNUMBEROFPARAMS|関数に指定されたパラメーターの数が正しくありませんでした。 関数名は認識されましたが、パラメーター数が正しくありませんでした。|  
|0xC0049043|-1073442749|DTS_E_EXPREVALSTATIC_CHARMAPPINGFAILED|文字マッピング関数が失敗しました。|  
|0xC0049044|-1073442748|DTS_E_EXPREVALSTATIC_INVALIDDATEPART|日付関数に無効な日付部分のパラメーターが指定されました。|  
|0xC0049045|-1073442747|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAM|関数 NULL に無効なパラメーターが指定されました。 NULL のパラメーターは静的である必要があります。入力列などの動的な要素を含めることはできません。|  
|0xC0049046|-1073442746|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAMTYPE|関数 NULL に無効なパラメーターが指定されました。 NULL のパラメーターは、整数または整数に変換できる型である必要があります。|  
|0xC0049047|-1073442745|DTS_E_EXPREVALSTATIC_FUNCTIONPARAMNOTSTATIC|関数に無効なパラメーターが指定されました。 このパラメーターは静的である必要があります。入力列などの動的な要素を含めることはできません。|  
|0xC0049048|-1073442744|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAM|キャスト演算に無効なパラメーターが指定されました。 キャスト演算子のパラメーターは静的である必要があります。入力列などの動的な要素を含めることはできません。|  
|0xC0049049|-1073442743|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAMTYPE|キャスト演算に無効なパラメーターが指定されました。 キャスト演算子のパラメーターは、整数または整数に変換できる型である必要があります。|  
|0xC004904A|-1073442742|DTS_E_EXPREVALSTATIC_INVALIDCAST|サポートされていない型のキャストが式に含まれていました。|  
|0xC004904B|-1073442741|DTS_E_EXPREVALSTATIC_INVALIDTOKEN|式に認識されないトークンが含まれていました。 無効な要素が含まれているので、式を解析できませんでした。|  
|0xC004904C|-1073442740|DTS_E_EXPREVALSTATIC_FAILEDTOPARSEEXPRESSION|式が無効なので、解析できませんでした。 無効な要素が含まれているか、または適切な形式ではない可能性があります。|  
|0xC004904D|-1073442739|DTS_E_EXPREVALSTATIC_UNARYOPOVERFLOW|単項マイナス (否定) 演算が、結果のデータ型の最大サイズをオーバーフローしました。 演算結果の大きさが、結果の型をオーバーフローしています。|  
|0xC004904E|-1073442738|DTS_E_EXPREVALSTATIC_COMPUTEFAILED|式を計算できませんでした。|  
|0xC004904F|-1073442737|DTS_E_EXPREVALSTATIC_BUILDSTRINGFAILED|式の文字列表記を生成できませんでした。|  
|0xC0049050|-1073442736|DTS_E_EXPREVALSTATIC_CANNOTCONVERTRESULT|式の結果のデータ型を列のデータ型に変換できません。 式の結果は、入力列または出力列に書き込まれる必要がありますが、式のデータ型を列のデータ型に変換することができません。|  
|0xC0049051|-1073442735|DTS_E_EXPREVALSTATIC_CONDITIONALOPINVALIDCONDITIONTYPE|条件演算子の条件式に無効なデータ型が使用されています。 この条件式は DT_BOOL 型である必要があります。|  
|0xC0049052|-1073442734|DTS_E_EXPREVALSTATIC_CONDITIONALOPTYPEMISMATCH|条件演算子のオペランドのデータ型に互換性がありませんでした。 オペランドの型を暗黙的に条件演算と互換性のある型にキャストできませんでした。 この演算を実行するには、演算子の一方または両方のオペランドでキャスト演算子により明示的にキャストする必要があります。|  
|0xC0049053|-1073442733|DTS_E_EXPREVALSTATIC_CONDITIONALOPSETTYPEFAILED|条件演算の結果の型を設定できませんでした。|  
|0xC0049054|-1073442732|DTS_E_EXPREVALSTATIC_INPUTCOLUMNNAMENOTFOUND|指定された入力列が入力列のコレクションに見つかりませんでした。|  
|0xC0049055|-1073442731|DTS_E_EXPREVALSTATIC_INPUTCOLUMNIDNOTFOUND|系列 ID で入力列を検索できませんでした。 入力列が入力列のコレクションに見つかりませんでした。|  
|0xC0049056|-1073442730|DTS_E_EXPREVALSTATIC_NOINPUTCOLUMNCOLLECTION|入力列のコレクションは入力列の処理には使用できませんが、式には、入力列の参照と見なされる認識できないトークンが含まれています。 入力列のコレクションは式エバリュエーターに指定されていませんが、入力列が式に含まれていました。|  
|0xC0049057|-1073442729|DTS_E_EXPREVALSTATIC_VARIABLENOTFOUND|指定された変数が、コレクションに見つかりませんでした。 正しいスコープに存在しない可能性があります。 変数が存在すること、およびスコープが正しいことを確認してください。|  
|0xC0049058|-1073442728|DTS_E_EXPREVALSTATIC_INVALIDTOKENSTATE|この式を解析できませんでした。 この式には無効または不完全なトークンが含まれています。 この式には、無効な要素が含まれているか、閉じかっこなどの必要な要素の一部が不足している可能性があります。または、適切な形式ではない可能性があります。|  
|0xC0049059|-1073442727|DTS_E_EXPREVALSTATIC_INVALIDCASTCODEPAGE|データ型 DT_STR または DT_TEXT へのキャストのコード ページ パラメーターに指定された値が無効です。 指定されたコード ページは、コンピューターにインストールされていません。|  
|0xC004905A|-1073442726|DTS_E_EXPREVALSTATIC_INVALIDCASTPRECISION|キャスト演算の有効桁数のパラメーターに指定された値が、型キャストの範囲外です。|  
|0xC004905B|-1073442725|DTS_E_EXPREVALSTATIC_INVALIDCASTSCALE|キャスト演算の小数点以下桁数のパラメーターに指定された値が、型キャストの範囲外です。 小数点以下桁数は、有効桁数よりも大きい値にすることも負の値にすることもできません。|  
|0xC004905C|-1073442724|DTS_E_EXPREVALSTATIC_CONDITIONALOPCODEPAGEMISMATCH|条件演算のコード ページが一致しません。 左辺オペランドのコード ページと右辺オペランドのコード ページが一致しません。 この型の条件演算子では、コード ページが同一である必要があります。|  
|0xC004905D|-1073442723|DTS_E_EXPREVALSTATIC_ILLEGALHEXESCAPEINSTRINGLITERAL|文字列リテラルに、無効な 16 進数のエスケープ シーケンスが含まれています。 このエスケープ シーケンスは、式エバリュエーターの文字列リテラルでサポートされていません。 16 進数のエスケープ シーケンスは、\xhhhh という形式で表す必要があります。ここで、h は有効な 16 進数の桁を示します。|  
|0xC004905E|-1073442722|DTS_E_EXPREVALSTATIC_ILLEGALESCAPEINSTRINGLITERAL|文字列リテラルに、無効なエスケープ シーケンスが含まれています。 このエスケープ シーケンスは、式エバリュエーターの文字列リテラルでサポートされていません。 文字列に円記号が必要な場合は、二重の円記号 "\\\\" として文字列の書式を設定してください。|  
|0xC004905F|-1073442721|DTS_E_EXPREVALSTATIC_UNSUPPORTEDTYPE|式で、サポートされていないデータ型または認識できないデータ型が使用されました。|  
|0xC0049060|-1073442720|DTS_E_EXPREVALSTATIC_DATACONVERSIONOVERFLOW|データ型の変換中にオーバーフローが発生しました。 変換元の型が大きすぎて、変換先の型に収まりません。|  
|0xC0049061|-1073442719|DTS_E_EXPREVALSTATIC_DATACONVERSIONNOTSUPPORTED|式にサポートされていないデータ型の変換が含まれています。 変換元のデータ型を変換先のデータ型に変換できません。|  
|0xC0049062|-1073442718|DTS_E_EXPREVALSTATIC_DATACONVERSIONFAILED|データ変換の実行中にエラーが発生しました。 変換元の型を変換先の型に変換できませんでした。|  
|0xC0049063|-1073442717|DTS_E_EXPREVALSTATIC_CONDITIONALOPERATIONFAILED|条件演算が失敗しました。|  
|0xC0049064|-1073442716|DTS_E_EXPREVALSTATIC_CASTFAILED|型キャストの実行中にエラーが発生しました。|  
|0xC0049065|-1073442715|DTS_E_EXPREVALFAILEDTOCONVERTSTRCOLUMNTOWSTR|エラー コード 0x%2!8.8X! により、型 DT_STR から型 DT_WSTR に "%1" を変換できませんでした。 入力列で暗黙的な変換を実行中にエラーが発生しました。|  
|0xC0049066|-1073442714|DTS_E_EXPREVALSTATIC_FAILEDTOCONVERTSTRCOLUMNTOWSTR|型 DT_STR から型 DT_WSTR に入力列を変換できませんでした。 入力列で暗黙的な変換を実行中にエラーが発生しました。|  
|0xC0049067|-1073442713|DTS_E_EXPREVALSTATIC_FUNCTIONCOMPUTEFAILED|関数の評価中にエラーが発生しました。|  
|0xC0049068|-1073442712|DTS_E_EXPREVALSTATIC_FUNCTIONCONVERTPARAMTOMEMBERFAILED|関数のパラメーターを静的な値に変換できません。 このパラメーターは静的である必要があります。入力列などの動的な要素を含めることはできません。|  
|0xC0049088|-1073442680|DTS_E_EXPREVALSTATIC_FNRIGHTINVALIDLENGTH|長さのパラメーターは、関数 RIGHT では無効です。 長さのパラメーターには、負の数を指定できません。|  
|0xC0049089|-1073442679|DTS_E_EXPREVALSTATIC_FNREPLICATEINVALIDREPEATCOUNT|繰り返し回数のパラメーターは、関数 REPLICATE では無効です。 このパラメーターには負の数を指定できません。|  
|0xC0049096|-1073442666|DTS_E_EXPREVALSTATIC_BINARYOPERATORCODEPAGEMISMATCH|バイナリ演算のコード ページが一致しません。 左辺オペランドのコード ページと右辺オペランドのコード ページが一致しません。 このバイナリ演算では、コード ページが同一である必要があります。|  
|0xC0049097|-1073442665|DTS_E_EXPREVALSTATIC_VARIABLECOMPUTEFAILED|変数の値を取得できませんでした。|  
|0xC0049098|-1073442664|DTS_E_EXPREVALSTATIC_VARIABLETYPENOTSUPPORTED|式にサポートされていないデータ型の変数が含まれています。|  
|0xC004909B|-1073442661|DTS_E_EXPREVALSTATIC_CASTCODEPAGEMISMATCH|式をキャストできません。キャストされている値のコード ページが、要求された結果コード ページと一致しません。 キャスト元のコード ページは、キャスト先として要求されているコード ページと一致する必要があります。|  
|0xC004909C|-1073442660|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEQUOTE|式に予期しない単一引用符が含まれています。 二重引用符が必要な可能性があります。|  
|0xC004909D|-1073442659|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEEQUAL|式に予期しない等号 (=) が含まれています。 このエラーは通常、連続する 2 つの等号 (==) が必要な場合に発生します。|  
|0xC00490AA|-1073442646|DTS_E_EXPREVALSTATIC_AMBIGUOUSINPUTCOLUMNNAME|指定された入力列名があいまいです。  この列は、[コンポーネント名].[列名] という形式で修飾するか、または系列 ID によって参照される必要があります。 このエラーは、入力列が複数のコンポーネントに存在する場合で、コンポーネント名を追加するか、系列 ID を使用して入力列を区別する必要がある場合に発生します。|  
|0xC00490AB|-1073442645|DTS_E_EXPREVALSTATIC_PLACEHOLDERINEXPRESSION|式内にプレースホルダー関数のパラメーターまたはオペランドが見つかりました。 実際のパラメーターまたはオペランドに置き換える必要があります。|  
|0xC00490AC|-1073442644|DTS_E_EXPREVALSTATIC_AMBIGUOUSVARIABLENNAME|指定された変数名があいまいです。 必要な変数を \@[Namespace::Variable] という形式で修飾する必要があります。 このエラーは、変数が複数の名前空間に存在する場合に発生します。|  
|0xC00490D3|-1073442605|DTS_E_EXPREVALSTATIC_BINARYOPDTSTRNOTSUPPORTED|バイナリ演算のオペランドでは、入力列およびキャスト演算にデータ型 DT_STR のみがサポートされています。 入力列またはキャストの結果ではない DT_STR オペランドは、バイナリ演算では使用できません。 この演算を実行するには、オペランドでキャスト演算子により明示的にキャストする必要があります。|  
|0xC00490D4|-1073442604|DTS_E_EXPREVALSTATIC_CONDITIONALOPDTSTRNOTSUPPORTED|条件演算子のオペランドでは、入力列およびキャスト演算にデータ型 DT_STR のみがサポートされています。 入力列またはキャストの結果ではない DT_STR オペランドは、条件演算では使用できません。 この演算を実行するには、オペランドでキャスト演算子により明示的にキャストする必要があります。|  
|0xC00490D5|-1073442603|DTS_E_EXPREVALSTATIC_FNFINDSTRINGINVALIDOCCURRENCECOUNT|発生回数パラメーターは、関数 FINDSTRING では有効ではありません。 このパラメーターには、0 より大きい値を指定する必要があります。|  
|0xC00490DD|-1073442595|DTS_E_EXPREVALSTATIC_INVALIDDATEPARTNODE|日付関数に指定された "日付部分" のパラメーターが無効です。 "日付部分" のパラメーターには、静的な文字列を指定する必要があり、入力列などの動的な要素を含めることはできません。 型は DT_WSTR である必要があります。|  
|0xC00490DE|-1073442594|DTS_E_EXPREVALSTATIC_INVALIDCASTLENGTH|キャスト演算の長さのパラメーターに指定された値が無効です。 長さには正の値を指定してください。 型キャストに指定された長さが負の値になっています。 正の値に変更してください。|  
|0xC00490DF|-1073442593|DTS_E_EXPREVALSTATIC_INVALIDNULLLENGTH|NULL 関数の長さのパラメーターに指定された値が無効です。 長さには正の値を指定してください。 NULL 関数に指定された長さが負の値になっています。 正の値に変更してください。|  
|0xC00490E0|-1073442592|DTS_E_EXPREVALSTATIC_INVALIDNULLCODEPAGE|データ型 DT_STR または DT_TEXT が指定された NULL 関数のコード ページ パラメーターに指定された値が無効です。 指定されたコード ページは、コンピューターにインストールされていません。 指定したコード ページを変更するか、コード ページをコンピューターにインストールしてください。|  
|0xC00490E1|-1073442591|DTS_E_EXPREVALSTATIC_INVALIDNULLPRECISION|NULL 関数の有効桁数のパラメーターに指定された値が無効です。 指定された有効桁数は、NULL 関数の範囲外です。|  
|0xC00490E2|-1073442590|DTS_E_EXPREVALSTATIC_INVALIDNULLSCALE|NULL 関数の小数点以下桁数のパラメーターに指定された値が無効です。 指定された小数点以下桁数は、NULL 関数の範囲外です。 小数点以下桁数は有効桁数よりも大きい値にすることはできず、正の値にする必要があります。|  
|0xC00490E8|-1073442584|DTS_E_XMLSRCERRORSETTINGERROROUTPUTCOLUMNDATA|%1 はデータを %2 (%3 上) に書き込めませんでした。 %4|  
|0xC00490F5|-1073442571|DTS_E_TXLOOKUP_CANCEL_REQUESTED|参照変換がユーザーからキャンセル要求を受け取りました。|  
|0xC00490F6|-1073442570|DTS_E_LOBLENGTHLIMITEXCEEDED|4 GB の制限に達したため、文字またはバイナリ ラージ オブジェクト (LOB) の処理が停止しました。|  
|0xC00490F7|-1073442569|DTS_E_CANNOTLOADCOMPONENT|マネージド パイプライン コンポーネント "%1" を読み込めませんでした。  例外: %2。|  
|0xC00F9304|-1072721148|DTS_E_OLEDB_EXCEL_NOT_SUPPORTED|SSIS エラー コード DTS_E_OLEDB_EXCEL_NOT_SUPPORTED: 64 ビット バージョンの SSIS では OLE DB プロバイダーを使用できないため、Excel 接続マネージャーがサポートされません。|  
|0xC00F9310|-1072721136|DTS_E_CACHEBADHEADER|キャッシュ ファイルが破損しているか、ファイルがキャッシュ接続マネージャーを使用して作成されませんでした。  有効なキャッシュ ファイルを指定してください。|  
|0xC0202001|-1071636479|DTS_E_MISSINGSQLCOMMAND|SQL コマンドが正しく設定されていません。 SQLCommand プロパティを確認してください。|  
|0xC0202002|-1071636478|DTS_E_COMERROR|COM エラー オブジェクト情報があります。  ソース: "%1" エラー コード: 0x%2!8.8X!  説明: "%3"。|  
|0xC0202003|-1071636477|DTS_E_ACQUIREDCONNECTIONUNAVAILABLE|取得した接続にアクセスできません。|  
|0xC0202004|-1071636476|DTS_E_INCORRECTCOLUMNCOUNT|列数が正しくありません。|  
|0xC0202005|-1071636475|DTS_E_COLUMNNOTFOUND|列 "%1" がデータ ソースに見つかりません。|  
|0xC0202007|-1071636473|DTS_E_OLEDBRECORD|OLE DB レコードを使用できます。  ソース: "%1"  Hresult: 0x%2!8.8X!  説明: "%3"。|  
|0xC0202009|-1071636471|DTS_E_OLEDBERROR|SSIS エラー コード DTS_E_OLEDBERROR。  OLE DB エラーが発生しました。 エラー コード:0x%1!8.8X!。|  
|0xC020200A|-1071636470|DTS_E_ALREADYCONNECTED|コンポーネントの接続は完了しています。 コンポーネントに接続する前に、接続を切断する必要があります。|  
|0xC020200B|-1071636469|DTS_E_INCORRECTSTOCKPROPERTYVALUE|プロパティ "%1" の値が正しくありません。|  
|0xC020200E|-1071636466|DTS_E_CANNOTOPENDATAFILE|データ ファイル "%1" を開けません。|  
|0xC0202010|-1071636464|DTS_E_DESTINATIONFLATFILEREQUIRED|対象になるフラット ファイル名が指定されませんでした。 フラット ファイル接続マネージャーが接続文字列を使用して構成されていることを確認してください。 フラット ファイル接続マネージャーが複数のコンポーネントで使用されている場合は、接続文字列に十分なファイル名が含まれていることを確認してください。|  
|0xC0202011|-1071636463|DTS_E_TEXTQUALIFIERNOTFOUND|列 "%1" のテキスト修飾子が見つかりません。|  
|0xC0202014|-1071636460|DTS_E_CANNOTCONVERTTYPES|"%1" から "%2" への変換はサポートされていません。|  
|0xC0202015|-1071636459|DTS_E_PROBLEMDETECTINGTYPECOMPATIBILITY|%2 から %3 への型変換の検証中に、 エラー コード 0x%1!8.8X! が返されました。|  
|0xC0202016|-1071636458|DTS_E_CANNOTMAPINPUTCOLUMNTOOUTPUTCOLUMN|"%2" で必要とされている系列 ID "%1!d!" の入力列が 見つかりません。 出力列の SourceInputColumnLineageID カスタム プロパティを確認してください。|  
|0xC0202017|-1071636457|DTS_E_INCORRECTMINIMUMNUMBEROFOUTPUTS|出力件数が正しくありません。 少なくとも %1!d! 件の 出力が必要です。|  
|0xC0202018|-1071636456|DTS_E_INCORRECTEXACTNUMBEROFOUTPUTS|出力件数が正しくありません。 正しくは、%1!d! 件の 出力が必要です。|  
|0xC0202019|-1071636455|DTS_E_STRINGCONVERSIONTOOLONG|文字列が長すぎて変換できません。|  
|0xC020201A|-1071636454|DTS_E_INCORRECTEXACTNUMBEROFINPUTS|入力件数が正しくありません。 正しくは、%1!d! 件の 入力が必要です。|  
|0xC020201B|-1071636453|DTS_E_CANNOTHAVEZEROINPUTCOLUMNS|%1 の入力列数を 0 にすることはできません。|  
|0xC020201C|-1071636452|DTS_E_CANNOTHAVEINPUTS|このコンポーネントには %1!d! 件の 入力が必要です。  このコンポーネントでは入力が許可されていません。|  
|0xC020201D|-1071636451|DTS_E_PROCESSINPUTCALLEDWITHINVALIDINPUTID|無効な入力 ID %1!d! を指定して ProcessInput が呼び出されました。|  
|0xC020201F|-1071636449|DTS_E_INCORRECTCUSTOMPROPERTYTYPE|カスタム プロパティ "%1" は、%2 型にする必要があります。|  
|0xC0202020|-1071636448|DTS_E_INVALIDBUFFERTYPE|バッファーの種類が無効です。 パイプラインのレイアウトおよびすべてのコンポーネントが検証に合格していることを確認してください。|  
|0xC0202021|-1071636447|DTS_E_INCORRECTCUSTOMPROPERTYVALUE|カスタム プロパティ "%1" の値が正しくありません。|  
|0xC0202022|-1071636446|DTS_E_CONNECTIONREQUIREDFORMETADATA|接続が確立されていないのでエラーが発生しました。 メタデータを要求するときは、接続を確立する必要があります。 オフラインで作業している場合は、[SSIS] メニューの [オフライン作業] をオフにし、接続を有効にしてください。|  
|0xC0202023|-1071636445|DTS_E_CANTCREATECUSTOMPROPERTY|カスタム プロパティ "%1" を作成できません。|  
|0xC0202024|-1071636444|DTS_E_CANTGETCUSTOMPROPERTYCOLLECTION|初期化用にカスタム プロパティのコレクションを取得できません。|  
|0xC0202025|-1071636443|DTS_E_CANNOTCREATEACCESSOR|OLE DB アクセサーを作成できません。 列のメタデータが有効であることを確認してください。|  
|0xC0202026|-1071636442|DTS_E_PRIMEOUTPUTCALLEDWITHINVALIDOUTPUTID|無効な出力 ID %1!d! を指定して PrimeOutput が呼び出されました。|  
|0xC0202027|-1071636441|DTS_E_INCORRECTSTOCKPROPERTY|"%2" のプロパティ "%1" の値が無効です。|  
|0xC0202028|-1071636440|DTS_E_CONNECTIONREQUIREDFORREAD|データを読み取るには接続する必要があります。|  
|0xC020202C|-1071636436|DTS_E_ERRORWHILEREADINGHEADERROWS|ヘッダー行の読み取り中にエラーが発生しました。|  
|0xC020202D|-1071636435|DTS_E_DUPLICATECOLUMNNAME|列名 "%1" が重複しています。|  
|0xC0202030|-1071636432|DTS_E_CANNOTGETCOLUMNNAME|ID %1!d! の列の名前を取得できません。|  
|0xC0202031|-1071636431|DTS_E_CANTDIRECTROW|出力 "%1" (%2!d!) への行の出力指定に失敗しました。|  
|0xC020203A|-1071636422|DTS_E_CANNOTCREATEBULKINSERTHREAD|エラー "%1" により、一括挿入スレッドを作成できません。|  
|0xC020203B|-1071636421|DTS_E_BULKINSERTHREADINITIALIZATIONFAILED|SSIS 一括挿入タスクのスレッドの初期化に失敗しました。|  
|0xC020203E|-1071636418|DTS_E_BULKINSERTTHREADALREADYRUNNING|SSIS 一括挿入タスクのスレッドは、既に実行されています。|  
|0xC020203F|-1071636417|DTS_E_BULKINSERTTHREADABNORMALCOMPLETION|エラーまたは警告が発生したため、SSIS 一括挿入タスクのスレッドが終了されました。|  
|0xC0202040|-1071636416|DTS_E_CANNOTGETIROWSETFASTLOAD|"%1" の Fastload 行セットを開けませんでした。 オブジェクトがデータベース内に存在することを確認してください。|  
|0xC0202041|-1071636415|DTS_E_CONNECTREQUIREDFORMETADATAVALIDATION|接続されていないのでエラーが発生しました。 メタデータの検証を続行する前に、接続する必要があります。|  
|0xC0202042|-1071636414|DTS_E_DESTINATIONTABLENAMENOTPROVIDED|対象になるテーブルの名前が指定されていません。|  
|0xC0202043|-1071636413|DTS_E_ICONVERTTYPEUNAVAILABLE|OLE DB アダプターで使用される OLE DB プロバイダーでは、IConvertType はサポートされていません。 アダプターの ValidateColumnMetaData プロパティを False に設定してください。|  
|0xC0202044|-1071636412|DTS_E_OLEDBPROVIDERDATATYPECONVERSIONUNSUPPORTED|OLE DB アダプターで使用される OLE DB プロバイダーでは、"%3" を "%1" 型と "%2" 型の間で変換できません。|  
|0xC0202045|-1071636411|DTS_E_VALIDATECOLUMNMETADATAFAILED|列のメタデータを検証できませんでした。|  
|0xC0202047|-1071636409|DTS_E_ATTEMPTINGTOINSERTINTOAROWIDCOLUMN|"%1" は行 ID 列なので、データの挿入操作に含めることはできません。|  
|0xC0202048|-1071636408|DTS_E_ATTEMPTINGTOINSERTINTOAROWVERCOLUMN|行バージョン列 "%1" に挿入しようとしています。 行バージョン列には挿入できません。|  
|0xC0202049|-1071636407|DTS_E_ATTEMPTINGTOINSERTINTOAREADONLYCOLUMN|読み取り専用の列 "%1" に挿入できませんでした。|  
|0xC020204A|-1071636406|DTS_E_UNABLETORETRIEVECOLUMNINFO|データ ソースから列情報を取得できません。 データベース内の取得先のテーブルが使用できることを確認してください。|  
|0xC020204B|-1071636405|DTS_E_CANTLOCKBUFFER|バッファーをロックできませんでした。 システムのメモリが不足しているか、バッファー マネージャーがクォータに達しました。|  
|0xC020204C|-1071636404|DTS_E_INVALIDCOMPARISONFLAGS|%1 の ComparisonFlags プロパティに、値が %2!d! の余分なフラグが含まれています。|  
|0xC020204D|-1071636403|DTS_E_COLUMNMETADATAUNAVAILABLEFORVALIDATION|列のメタデータを検証に使用できませんでした。|  
|0xC0202053|-1071636397|DTS_E_CANNOTWRITETODATAFILE|データ ファイルに書き込めません。|  
|0xC0202055|-1071636395|DTS_E_COLUMNDELIMITERNOTFOUND|列 "%1" の列区切り記号が見つかりませんでした。|  
|0xC0202058|-1071636392|DTS_E_COLUMNPARSEFAILED|データ ファイルの列 "%1" を解析できませんでした。|  
|0xC020205A|-1071636390|DTS_E_RAWFILENAMEREQUIRED|ファイル名が正しく指定されていません。  FileName プロパティに直接指定するか、FileNameVariable プロパティに変数を指定して、RAW ファイルにパスと名前を指定してください。|  
|0xC020205B|-1071636389|DTS_E_RAWFILECANTOPEN|ファイル "%1" を書き込み用に開けません。 権限がないか、ディスクがいっぱいのときに、エラーが発生することがあります。|  
|0xC020205C|-1071636388|DTS_E_RAWFILECANTBUFFER|出力ファイルの I/O バッファーを作成できません。 権限がないか、ディスクがいっぱいのときに、エラーが発生することがあります。|  
|0xC020205D|-1071636387|DTS_E_RAWCANTWRITE|ファイル "%2" に %1!d! バイトを書き込めません。 詳細については、以前のエラー メッセージを参照してください。|  
|0xC020205E|-1071636386|DTS_E_RAWBADHEADER|ファイル ヘッダーに無効なメタデータが見つかりました。 ファイルが破損しているか、SSIS で生成された未加工のデータ ファイルではありません。|  
|0xC020205F|-1071636385|DTS_E_RAWEXISTSCREATEONCE|出力ファイルが既に存在していて、WriteOption が [1 回だけ作成する] に設定されているので、エラーが発生しました。 WriteOption プロパティを [常に作成する] に設定するか、ファイルを削除してください。|  
|0xC0202060|-1071636384|DTS_E_RAWCANTAPPENDTRUNCATE|プロパティ設定の競合により、エラーが発生しました。 AllowAppend プロパティと ForceTruncate プロパティの両方が True に設定されています。 両方のプロパティを True に設定することはできません。 2 つのプロパティのいずれかを False に設定してください。|  
|0xC0202061|-1071636383|DTS_E_RAWBADVERSION|ファイルには、バージョンとフラグに関する無効な情報が含まれています。 ファイルが破損しているか、SSIS で生成された未加工のデータ ファイルではありません。|  
|0xC0202062|-1071636382|DTS_E_RAWVERSIONINCOMPATIBLEAPPEND|出力ファイルは、互換性のないバージョンで書き込まれているので、追加できません。 ファイルは、使用できなくなった古いファイル形式の可能性があります。|  
|0xC0202064|-1071636380|DTS_E_RAWMETADATAMISMATCH|既存のファイルには、入力からの列 "%1" と一致する列がないので、出力ファイルは追加できません。 古いファイルがメタデータと一致しません。|  
|0xC0202065|-1071636379|DTS_E_RAWMETADATACOUNTMISMATCH|出力ファイルの列数は、追加先のファイルの列数と一致しないので、出力ファイルは追加できません。 古いファイルがメタデータと一致しません。|  
|0xC0202067|-1071636377|DTS_E_ERRORRETRIEVINGCOLUMNCODEPAGE|列コード ページ情報を取得中にエラーが発生しました。|  
|0xC0202068|-1071636376|DTS_E_RAWCANTREAD|ファイル "%2" から 読み取れません。 このエラーの原因は、これ以前に報告されています。|  
|0xC0202069|-1071636375|DTS_E_RAWUNEXPECTEDEOF|ファイル "%2" から %1!d! バイトを読み取り中に予期しないファイルの末尾が 読み取れません。 ファイルに無効な書式が含まれていたため、ファイルが途中で終了しました。|  
|0xC020206A|-1071636374|DTS_E_RAWNOLONGTYPES|列 %1 を使用できません。 未加工アダプターでは、image、text、ntext データはサポートされていません。|  
|0xC020206B|-1071636373|DTS_E_RAWUNEXPECTEDTYPE|アダプターにより、認識できないデータ型 %1!d! が検出されました。 入力ファイル (ソース) が破損しているか、バッファーの種類 (出力先) が無効である可能性があります。|  
|0xC020206C|-1071636372|DTS_E_RAWSTRINGTOOLONG|文字列が長すぎます。 アダプターが読み取った文字列の長さは %1!d! バイトでしたが、 想定した文字列はオフセットが %3!d! で %2!d! バイト未満でした。 これは、入力ファイルが破損していることを示しています。 このファイルに書き込まれている文字列の長さは、バッファー列に対して大きすぎます。|  
|0xC020206E|-1071636370|DTS_E_RAWSKIPFAILED|未加工アダプターで、入力ファイルから 系列 ID %3!d! の参照されない列 "%2" の %1!d! バイトをスキップ中にエラーが発生しました。 オペレーティング システムから、これ以前にエラーが報告されています。|  
|0xC020206F|-1071636369|DTS_E_RAWREADFAILED|未加工アダプターで、入力ファイルから 系列 ID %3!d! の列 "%2" の %1!d! バイトを読み取り中にエラーが発生しました。 オペレーティング システムから、これ以前にエラーが報告されています。|  
|0xC0202070|-1071636368|DTS_E_RAWFILENAMEINVALID|ファイル名のプロパティが無効です。 ファイル名がデバイス名であるか、ファイル名に無効な文字が使用されています。|  
|0xC0202071|-1071636367|DTS_E_BULKINSERTAPIPREPARATIONFAILED|データを挿入するための SSIS 一括挿入を準備できません。|  
|0xC0202072|-1071636366|DTS_E_INVALIDDATABASEOBJECTNAME|データベース オブジェクト名 "%1" は有効ではありません。|  
|0xC0202073|-1071636365|DTS_E_INVALIDORDERCLAUSE|ORDER 句が有効ではありません。|  
|0xC0202074|-1071636364|DTS_E_RAWFILECANTOPENREAD|ファイル "%1" を読み取り用に開けません。 権限がないか、ファイルが見つからないときに、エラーが発生することがあります。 正確な原因は、これ以前のエラー メッセージで報告されています。|  
|0xC0202075|-1071636363|DTS_E_TIMEGENCANTCREATE|Microsoft.AnalysisServices.TimeDimGenerator.TimeDimGenerator を作成できません。|  
|0xC0202076|-1071636362|DTS_E_TIMEGENCANTCONFIGURE|Microsoft.AnalysisServices.TimeDimGenerator を構成できません。|  
|0xC0202077|-1071636361|DTS_E_TIMEGENCANTCONVERT|列 %1!d! に対してサポートされていないデータ型です。|  
|0xC0202079|-1071636359|DTS_E_TIMEGENCANTREAD|エラー コード 0x%1!8.8X! で Microsoft.AnalysisServices.TimeDimGenerator からの読み取りに失敗しました。|  
|0xC020207A|-1071636358|DTS_E_TIMEGENCANTREADCOLUMN|列 "%2!d!" のデータの Microsoft.AnalysisServices.TimeDimGenerator からの読み取りはエラー コード 0x%2!8.8X! で失敗しました。|  
|0xC020207B|-1071636357|DTS_E_RSTDESTBADVARIABLENAME|VariableName プロパティが有効な変数の名前に設定されていません。 書き込み先のランタイム変数の名前が必要です。|  
|0xC020207C|-1071636356|DTS_E_RSTDESTRSTCONFIGPROBLEM|ADODB.Recordset オブジェクトを作成または構成できません。|  
|0xC020207D|-1071636355|DTS_E_RSTDESTRSTWRITEPROBLEM|ADODB.Recordset オブジェクトへの書き込み中にエラーが発生しました。|  
|0xC020207E|-1071636354|DTS_E_FILENAMEINVALID|ファイル名が無効です。 ファイル名がデバイス名であるか、ファイル名に無効な文字が使用されています。|  
|0xC020207F|-1071636353|DTS_E_FILENAMEINVALIDWITHPARAM|ファイル名 "%1" が無効です。 ファイル名がデバイス名であるか、ファイル名に無効な文字が使用されています。|  
|0xC0202080|-1071636352|DTS_E_CMDDESTNOPARAMS|SQL コマンドのパラメーターから変換先列の説明を取得できません。|  
|0xC0202081|-1071636351|DTS_E_CMDDESTNOTBOUND|パラメーターがバインドされていません。 SQL コマンドのすべてのパラメーターを入力列にバインドする必要があります。|  
|0xC0202082|-1071636350|DTS_E_TXPIVOTBADUSAGE|入力列 "%1" (%2!d!) の PivotUsage 値が無効です。|  
|0xC0202083|-1071636349|DTS_E_TXPIVOTTOOMANYPIVOTKEYS|見つかったピボット キーが多すぎます。 1 つの入力列のみをピボット キーとして使用できます。|  
|0xC0202084|-1071636348|DTS_E_TXPIVOTNOPIVOTKEY|ピボット キーが見つかりませんでした。 1 つの入力列をピボット キーとして使用する必要があります。|  
|0xC0202085|-1071636347|DTS_E_TXPIVOTINPUTALREADYMAPPED|複数の出力列 ("%1" (%2!d!) など) が入力列 "%3" (%4!d!) にマップされます。|  
|0xC0202086|-1071636346|DTS_E_TXPIVOTCANTMAPPIVOTKEY|出力列 "%1" (%2!d!) を PivotKey 入力列にマップできません。|  
|0xC0202087|-1071636345|DTS_E_TXPIVOTCANTMAPPINGNOTFOUND|出力列 "%1" (%2!d!) に、入力列の系列 ID が 無効な SourceColumn %3!d! があります。|  
|0xC0202088|-1071636344|DTS_E_TXPIVOTEMPTYPIVOTKEYVALUE|出力列 "%1" (%2!d!) は、ピボット値の入力列にマップされますが、その PivotKeyValue プロパティの値がありません。|  
|0xC0202089|-1071636343|DTS_E_TXPIVOTDUPLICATEPIVOTKEYVALUE|出力列 "%1" (%2!d!) には、一意ではない PivotKeyValue プロパティ値が指定されたピボット値の入力列がマップされます。|  
|0xC020208A|-1071636342|DTS_E_TXPIVOTOUTPUTNOTMAPPED|入力列 "%1" (%2!d!) はどの出力列にもマップされません。|  
|0xC020208B|-1071636341|DTS_E_TXPIVOTCANTCOMPARESETKEYS|設定キーの値を比較しているときに、エラーが発生しました。|  
|0xC020208D|-1071636339|DTS_E_TXPIVOTNOBLOB|入力列 "%1" (%2!d!) には長い形式のデータが含まれているため、設定キー、ピボット キー、またはピボット値として使用できません。|  
|0xC020208E|-1071636338|DTS_E_TXPIVOTBADOUTPUTTYPE|出力の種類が無効です。 出力列 "%1" (%2!d!) には、マップ先の入力列と同じデータ型およびメタデータが設定されている必要があります。|  
|0xC020208F|-1071636337|DTS_E_TXPIVOTPROCESSERROR|基になるレコードでピボットを実行中にエラーが発生しました。|  
|0xC0202090|-1071636336|DTS_E_TXPIVOTBADPIVOTKEYVALUE|ピボット キーの値 "%1" は無効です。|  
|0xC0202091|-1071636335|DTS_E_ERRORWHILESKIPPINGDATAROWS|データ行のスキップ中にエラーが発生しました。|  
|0xC0202092|-1071636334|DTS_E_ERRORWHILEREADINGDATAROWS|データ行 %2!I64d! で、ファイル "%1" の処理中にエラーが発生しました。|  
|0xC0202093|-1071636333|DTS_E_FAILEDTOINITIALIZEFLATFILEPARSER|フラット ファイル パーサーの初期化中にエラーが発生しました。|  
|0xC0202094|-1071636332|DTS_E_UNABLETORETRIEVECOLUMNINFOFROMFLATFILECONNECTIONMANAGER|フラット ファイル接続マネージャーから列情報を取得できません。|  
|0xC0202095|-1071636331|DTS_E_FAILEDTOWRITEOUTCOLUMNNAME|列 "%1" の列名を書き出せませんでした。|  
|0xC0202096|-1071636330|DTS_E_INVALIDFLATFILECOLUMNTYPE|列 "%1" の列の型が無効です。 列の型が "%2" になっています。 この列に指定できる型は、"%3" または "%4" のみです。|  
|0xC0202097|-1071636329|DTS_E_DISKIOBUFFEROVERFLOW|ディスク I/O に %1!d! バイトの データを書き込めませんでした。 ディスク I/O バッファーには、%2!d! バイトの 空き容量があります。|  
|0xC0202098|-1071636328|DTS_E_FAILEDTOWRITEOUTHEADER|ファイル ヘッダーの書き出し中にエラーが発生しました。|  
|0xC0202099|-1071636327|DTS_E_FAILEDTOGETFILESIZE|ファイル "%1" のファイル サイズを取得中にエラーが発生しました。|  
|0xC020209A|-1071636326|DTS_E_FAILEDTOSETFILEPOINTER|ファイル "%1" のファイル ポインターを設定中にエラーが発生しました。|  
|0xC020209B|-1071636325|DTS_E_UNABLETOSETUPDISKIOBUFFER|ディスク I/O バッファーの設定中にエラーが発生しました。|  
|0xC020209C|-1071636324|DTS_E_COLUMNDATAOVERFLOWDISKIOBUFFER|列 "%1" の列データによって、ディスク I/O バッファーがオーバーフローしました。|  
|0xC020209D|-1071636323|DTS_E_DISKIOFAILED|ファイルの読み取り中に予期しないディスク I/O エラーが発生しました。|  
|0xC020209E|-1071636322|DTS_E_DISKIOTIMEDOUT|ファイルの読み取り中にディスク I/O タイムアウトが発生しました。|  
|0xC020209F|-1071636321|DTS_E_INPUTSNOTREADONLY|この変換に対する入力列に指定された使用法の種類を読み取り/書き込みにすることはできません。 使用法の種類を読み取り専用に変更してください。|  
|0xC02020A0|-1071636320|DTS_E_CANNOTCOPYORCONVERTFLATFILEDATA|列 "%1" のフラット ファイル データをコピーまたは変換できません。|  
|0xC02020A1|-1071636319|DTS_E_FAILEDCOLUMNDATACONVERSIONSTATUS|データ変換に失敗しました。 列 "%1" のデータ変換から、状態値 %2!d! と 状態を示すテキスト "%3" が返されました。|  
|0xC02020A2|-1071636318|DTS_E_VARIABLESCOLLECTIONUNAVAILABLE|Variables コレクションを使用できません。|  
|0xC02020A3|-1071636317|DTS_E_TXUNPIVOTDUPLICATEPIVOTKEYVALUE|PivotKeyValue が重複しています。 入力列 "%1" (%2!d!) は、ピボット値の出力列にマップされ、一意ではない PivotKeyValue が指定されています。|  
|0xC02020A4|-1071636316|DTS_E_TXUNPIVOTNOUNPIVOTDESTINATION|ピボット解除されていない出力先が見つかりませんでした。 PivotKeyValue を使用して、少なくとも 1 つの入力列を出力の DestinationColumn にマップする必要があります。|  
|0xC02020A5|-1071636315|DTS_E_TXUNPIVOTBADKEYLIST|PivotKeyValue が無効です。 UnPivot が解除された複数の DestinationColumn を使用するピボット解除変換では、各変換先の PivotKeyValues のセットが完全に一致する必要があります。|  
|0xC02020A6|-1071636314|DTS_E_TXUNPIVOTBADUNPIVOTMETADATA|UnPivot メタデータが正しくありません。 UnPivot 変換では、同じ DestinationColumn を参照する PivotKeyValue が設定されたすべての入力列において、DestinationColumn と完全に一致するメタデータが必要です。|  
|0xC02020A7|-1071636313|DTS_E_TXPIVOTBADPIVOTKEYCONVERT|ピボット キーの値 "%1" をピボット キー列のデータ型に変換できません。|  
|0xC02020A8|-1071636312|DTS_E_TXUNPIVOTTOOMANYPIVOTKEYS|指定されたピボット キーが多すぎます。 1 つの出力列のみをピボット キーとして使用できます。|  
|0xC02020A9|-1071636311|DTS_E_TXUNPIVOTUNMAPPEDOUTPUT|出力列 "%1" (%2!d!) には、どの入力列の DestinationColumn プロパティによってもマップされません。|  
|0xC02020AA|-1071636310|DTS_E_TXUNPIVOTNOPIVOT|PivotKey として設定されている出力列はありません。|  
|0xC02020AB|-1071636309|DTS_E_TXUNPIVOTNOTINPUTMAP|入力列 "%1" (%2!d!) には、有効な出力列の LineageID を参照しない DestinationColumn プロパティ値が指定されています。|  
|0xC02020AC|-1071636308|DTS_E_TXUNPIVOTDUPLICATEDESTINATION|マップ先の重複エラー。 複数のピボットが行われていない入力列が同じマップ先の出力列にマップされます。|  
|0xC02020AD|-1071636307|DTS_E_TOTALINPUTCOLSCANNOTBEZERO|入力列が見つかりませんでした。 少なくとも 1 つの入力列を出力列にマップする必要があります。|  
|0xC02020AE|-1071636306|DTS_E_TXMERGEJOINMUSTHAVESAMENUMBEROFINPUTANDOUTPUTCOLS|入力列と出力列の数が等しくありません。 すべての入力の合計入力列数は、合計出力列数と同じである必要があります。|  
|0xC02020AF|-1071636305|DTS_E_INPUTMUSTBESORTED|入力が並べ替えられていません。 "%1" を並べ替える必要があります。|  
|0xC02020B0|-1071636304|DTS_E_TXMERGEJOININVALIDJOINTYPE|%1 の JoinType カスタム プロパティに、無効な値 %2!ld! が含まれています。 有効な値は 0 (完全)、1 (左)、または 2 (内部) です。|  
|0xC02020B1|-1071636303|DTS_E_TXMERGEJOININVALIDNUMKEYCOLS|NumKeyColumns の値が無効です。 %1 では、NumKeyColumns カスタム プロパティの値は 1 から %2!lu! までの範囲で指定する必要があります。|  
|0xC02020B2|-1071636302|DTS_E_NOKEYCOLS|キー列が見つかりませんでした。 %1 には、SortKeyPosition の値が 0 以外の列が少なくとも 1 列必要です。|  
|0xC02020B3|-1071636301|DTS_E_TXMERGEJOINNOTENOUGHKEYCOLS|キー列が不足しています。 %1 には、 SortKeyPosition の値が 0 以外の列が少なくとも %2!ld! 列必要です。|  
|0xC02020B4|-1071636300|DTS_E_TXMERGEJOINDATATYPEMISMATCH|データ型の不一致が発生しました。 SortKeyPosition 値が %1!ld! である列のデータ型が 一致しません。|  
|0xC02020B5|-1071636299|DTS_E_TXMERGEJOININVALIDSORTKEYPOS|SortKeyPosition 値が %1!ld! の列は 無効です。 適切な値は %2!ld! です。|  
|0xC02020B6|-1071636298|DTS_E_TXMERGEJOINSORTDIRECTIONMISMATCH|並べ替え方向が一致しません。 SortKeyPosition 値 %1!ld! である列の並べ替え方向が 一致しません。|  
|0xC02020B7|-1071636297|DTS_E_TXMERGEJOINOUTPUTCOLMUSTHAVEASSOCIATEDINPUTCOL|列がありません。 %1 を入力列に関連付ける必要があります。|  
|0xC02020B8|-1071636296|DTS_E_TXMERGEJOINREADONLYINPUTCOLSWITHNOOUTPUTCOL|入力列には出力列が必要です。 使用法の種類が読み取り専用で、出力列に関連付けられていない入力列があります。|  
|0xC02020B9|-1071636295|DTS_E_TXMERGEJOINNONSTRINGCOMPARISONFLAGSNOTZERO|比較フラグが 0 ではありません。 文字列型でない列の比較フラグは、0 にする必要があります。|  
|0xC02020BA|-1071636294|DTS_E_TXMERGEJOINCOMPARISONFLAGSMISMATCH|SortKeyPosition 値 %1!ld! を持つ列の比較フラグが 一致しません。|  
|0xC02020BB|-1071636293|DTS_E_TXPIVOTBADPIVOTKEYVALUENOSTRING|ピボット キーの値を認識できませんでした。|  
|0xC02020BC|-1071636292|DTS_E_TXLINEAGEINVALIDLINEAGEITEM|系列項目の値 %1!ld! が 無効です。 有効範囲は %2!ld! から %3!ld! までです。|  
|0xC02020BD|-1071636291|DTS_E_CANNOTHAVEANYINPUTCOLUMNS|入力列は許可されていません。 入力列数を 0 にする必要があります。|  
|0xC02020BE|-1071636290|DTS_E_TXLINEAGEDATATYPEMISMATCH|"%1" のデータ型は、指定された系列項目に対して無効です。|  
|0xC02020BF|-1071636289|DTS_E_TXLINEAGEINVALIDLENGTH|"%1" の長さは、指定された系列項目に対して無効です。|  
|0xC02020C1|-1071636287|DTS_E_METADATAMISMATCHWITHOUTPUTCOLUMN|"%1" のメタデータは、関連付けられている出力列のメタデータと一致しません。|  
|0xC02020C3|-1071636285|DTS_E_TXMERGESORTKEYPOSMISMATCH|SortKeyPosition 値が、関連付けられた入力列の SortKeyPosition と一致しない出力列があります。|  
|0xC02020C4|-1071636284|DTS_E_ADDROWTOBUFFERFAILED|エラー コード 0x%1!8.8X! により、データ フロー タスク バッファーに行を追加できませんでした。|  
|0xC02020C5|-1071636283|DTS_E_DATACONVERSIONFAILED|列 "%1" (%2!d!) を列 "%3" (%4!d!) に変換しているときに、データ変換に失敗しました。  この変換により、状態値 %5!d! と 状態を示すテキスト "%6" が返されました。|  
|0xC02020C6|-1071636282|DTS_E_FAILEDTOALLOCATEROWHANDLEBUFFER|エラー コード 0x%1!8.8X! により、行ハンドルのバッファーを割り当てることができませんでした。|  
|0xC02020C7|-1071636281|DTS_E_FAILEDTOSENDROWTOSQLSERVER|エラー コード 0x%1!8.8X! により、SQL Server に行を送信できませんでした。|  
|0xC02020C8|-1071636280|DTS_E_FAILEDTOPREPAREBUFFERSTATUS|エラー コード 0x%1!8.8X! により、バッファー状態を準備できませんでした。|  
|0xC02020C9|-1071636279|DTS_E_FAILEDTOBUFFERROWSTARTS|エラー コード 0x%1!8.8X! により、バッファー行の先頭を取得できませんでした。|  
|0xC02020CA|-1071636278|DTS_E_BULKINSERTTHREADTERMINATED|SSIS 一括挿入スレッドは実行されていません。  これ以上行を挿入できません。 一括挿入スレッドのタイムアウトを増やしてください。|  
|0xC02020CB|-1071636277|DTS_E_RAWTOOMANYCOLUMNS|変換元ファイルは無効です。 変換元ファイルにより、131,072 列より多くの列数が返されています。 このエラーは通常、変換元ファイルが RAW ファイルの変換先で生成されないときに発生します。|  
|0xC02020CC|-1071636276|DTS_E_TXUNIONALL_EXTRADANGLINGINPUT|%1 はアタッチされていない余分な入力なので削除されます。|  
|0xC02020CD|-1071636275|DTS_E_TXUNIONALL_NONDANGLINGUNATTACHEDINPUT|%1 はアタッチされていませんが、ぶら下がりとしてもマークされていません。  ぶら下がりとしてマークされます。|  
|0xC02020CF|-1071636273|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUE|ピボット キーの値 "%1" が重複しています。|  
|0xC02020D0|-1071636272|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUENOSTRING|ピボット キーの値が重複しています。|  
|0xC02020D1|-1071636271|DTS_E_FAILEDTOGETCOMPONENTLOCALEID|コンポーネントのロケール ID を取得中にエラーが発生しました。 エラー コードは 0x%1!8.8X! です。|  
|0xC02020D2|-1071636270|DTS_E_MISMATCHCOMPONENTCONNECTIONMANAGERLOCALEID|ロケール ID が一致しません。 コンポーネントのロケール ID (%1!d!) が接続マネージャーのロケール ID (%2!d!) と一致しません。|  
|0xC02020D3|-1071636269|DTS_E_LOCALEIDNOTSET|コンポーネントのロケール ID が設定されていません。 フラット ファイル アダプターによって、フラット ファイル接続マネージャーのロケール ID を設定する必要があります。|  
|0xC02020D4|-1071636268|DTS_E_RAWBYTESTOOLONG|バイナリ フィールドが大きすぎます。 アダプターが読み取ろうとしたバイナリ フィールドの長さは %1!d! バイトでしたが、想定したフィールドはオフセットが %3!d! で %2!d! バイト未満でした。 このエラーは通常、入力ファイルが無効であるときに発生します。 このファイルに書き込まれている文字列の長さは、バッファー列に対して大きすぎます。|  
|0xC02020D5|-1071636267|DTS_E_TXSAMPLINGINVALIDPCT|"%1" プロパティの比率 %2!ld! が無効です。 0 から 100 の範囲である必要があります。|  
|0xC02020D6|-1071636266|DTS_E_TXSAMPLINGINVALIDROWS|行数 %2!ld! は、"%1" プロパティでは有効ではありません。 行数は 0 よりも大きな値にする必要があります。|  
|0xC02020D7|-1071636265|DTS_E_RAWSTRINGINPUTTOOLONG|アダプターは、長さ %1!I64d! バイトの文字列を書き込むように要求されましたが、 すべてのデータの長さは 4,294,967,295 バイト未満である必要があります。|  
|0xC02020D9|-1071636263|DTS_E_ATLEASTONEINPUTMUSTBEMAPPEDTOOUTPUT|入力が出力にマップされませんでした。 "%1" は、少なくとも 1 つの入力列を出力列にマップする必要があります。|  
|0xC02020DB|-1071636261|DTS_E_CANNOTCONVERTDATATYPESWITHDIFFERENTCODEPAGES|コード ページ %2!d! の "%1" から コード ページ %4!d! の "%3" への変換は サポートされていません。|  
|0xC02020DC|-1071636260|DTS_E_COLUMNNOTMAPPEDTOEXTERNALMETADATACOLUMN|%1 に対する外部メタデータ列マッピングは無効です。  外部メタデータ列 ID を 0 にすることはできません。|  
|0xC02020DD|-1071636259|DTS_E_COLUMNMAPPEDTONONEXISTENTEXTERNALMETADATACOLUMN|%1 が、存在しない外部メタデータ列にマップされています。|  
|0xC02020E5|-1071636251|DTS_E_UNABLETOWRITELOBDATATOBUFFER|DT_TEXT、DT_NTEXT、または DT_IMAGE 型の大きなサイズのオブジェクト データを、列 "%1" のデータ フロー タスク バッファーに書き込めませんでした。|  
|0xC02020E8|-1071636248|DTS_E_CANNOTGETIROWSET|"%1" の行セットを開けませんでした。 オブジェクトがデータベース内に存在することを確認してください。|  
|0xC02020E9|-1071636247|DTS_E_VARIABLEACCESSFAILED|変数 "%1" にアクセスできませんでした。エラー コード 0x%2!8.8X!。|  
|0xC02020EA|-1071636246|DTS_E_CONNECTIONMANAGERNOTFOUND|接続マネージャー "%1" が見つかりません。 コンポーネントが接続のコレクションから接続マネージャーを検索できませんでした。|  
|0xC02020EB|-1071636245|DTS_E_VERSIONUPGRADEFAILED|バージョン "%1" からバージョン %2!d! にアップグレード できませんでした。|  
|0xC02020EC|-1071636244|DTS_E_RSTDESTBIGBLOB|入力列の値が、大きすぎて ADODB.Recordset オブジェクトに格納できません。|  
|0xC02020ED|-1071636243|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|列 "%1" と列 "%2" では、Unicode 形式の文字列データ型と Unicode 以外の形式の文字列データ型を変換できません。|  
|0xC02020EE|-1071636242|DTS_E_ROWCOUNTBADVARIABLENAME|VariableName プロパティで指定された変数 "%1" は、有効な変数ではありません。 書き込み先の有効な変数の名前が必要です。|  
|0xC02020EF|-1071636241|DTS_E_ROWCOUNTBADVARIABLETYPE|VariableName プロパティで指定された変数 "%1" は、整数型ではありません。 変数を VT_I4、VT_UI4、VT_I8、または VT_UI8 型に変更してください。|  
|0xC02020F0|-1071636240|DTS_E_NOCOLUMNADVANCETHROUGHFILE|ファイルによりコンポーネントを強化できるようにする列が指定されませんでした。|  
|0xC02020F1|-1071636239|DTS_E_MERGEJOINSORTEDOUTPUTHASNOSORTKEYPOSITIONS|"%1" では IsSorted が True に設定されていますが、すべての出力列の SortKeyPosition が 0 です。 IsSorted を False に変更するか、0 以外の SortKeyPosition を含む出力列を少なくとも 1 つ選択してください。|  
|0xC02020F2|-1071636238|DTS_E_METADATAMISMATCHWITHINPUTCOLUMN|"%1" のメタデータは、入力列のメタデータと一致しません。|  
|0xC02020F3|-1071636237|DTS_E_RSTDESTBADVARIABLE|指定された変数の値が見つからないか、ロックまたは設定できません。|  
|0xC02020F4|-1071636236|DTS_E_CANTPROCESSCOLUMNTYPECODEPAGE|列 "%1" には複数のコード ページ (%2!d! と %3!d!) が 指定されているので、処理できません。|  
|0xC02020F5|-1071636235|DTS_E_CANTINSERTCOLUMNTYPE|型 %2 および %3 の間での変換がサポートされていないため、列 "%1" を挿入できません。|  
|0xC02020F6|-1071636234|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|列 "%1" では、Unicode 形式の文字列データ型と Unicode 以外の形式の文字列データ型を変換できません。|  
|0xC02020F8|-1071636232|DTS_E_COULDNOTFINDINPUTBUFFERCOLUMNBYLINEAGE|%1 で、入力バッファーに LineageID %2!ld! が指定された列が 見つかりません。|  
|0xC02020F9|-1071636231|DTS_E_COULDNOTGETCOLUMNINFOFORINPUTBUFFER|%1 で、コピー バッファーから列 %2!lu! の列情報を 取得できません。|  
|0xC02020FA|-1071636230|DTS_E_COULDNOTGETCOLUMNINFOFORCOPYBUFFER|%1 で、コピー バッファーから列 "%2!lu!" の列情報を 取得できません。|  
|0xC02020FB|-1071636229|DTS_E_COULDNOTREGISTERCOPYBUFFER|%1 で、コピー バッファーのバッファーの種類を登録できません。|  
|0xC02020FC|-1071636228|DTS_E_COULDNOTCREATECOPYBUFFER|%1 で、並べ替えに使用するデータのコピー先のバッファーを作成できません。|  
|0xC02020FD|-1071636227|DTS_E_DATAREADERDESTREADFAILED|DataReader クライアントが Read の呼び出しに失敗したか、DataReader が閉じられています。|  
|0xC02020FE|-1071636226|DTS_E_NOSCHEMAINFOFOUND|SQL コマンドによって列情報が返されませんでした。|  
|0xC02020FF|-1071636225|DTS_E_GETSCHEMATABLEFAILED|%1 は SQL コマンドの列情報を取得できませんでした。 次のエラーが発生しました: %2|  
|0xC0202100|-1071636224|DTS_E_SOURCETABLENAMENOTPROVIDED|変換元テーブルの名前が指定されていません。|  
|0xC0203110|-1071632112|DTS_E_CACHE_INVALID_INDEXPOS|キャッシュのインデックス位置 %1!d! が無効です。 インデックス以外の列では、インデックス位置を 0 にする必要があります。 インデックス列では、インデックス位置に連続する正の数値を指定する必要があります。|  
|0xC0203111|-1071632111|DTS_E_CACHE_DUPLICATE_INDEXPOS|インデックス位置 %1!d! が重複しています。 インデックス以外の列では、インデックス位置を 0 にする必要があります。 インデックス列では、インデックス位置に連続する正の数値を指定する必要があります。|  
|0xC0203112|-1071632110|DTS_E_CACHE_TOO_FEW_INDEX_COLUMNS|キャッシュ接続マネージャーには少なくとも 1 つのインデックス列を指定する必要があります。 インデックス列を指定するには、キャッシュ列のインデックス位置プロパティを設定してください。|  
|0xC0203113|-1071632109|DTS_E_CACHE_INDEXPOS_NOT_CONTINUOUS|キャッシュのインデックス位置は連続している必要があります。 インデックス以外の列では、インデックス位置を 0 にする必要があります。 インデックス列では、インデックス位置に連続する正の数値を指定する必要があります。|  
|0xC0204000|-1071628288|DTS_E_PROPERTYNOTSUPPORTED|プロパティ "%1" は "%2" に設定できません。 設定しているプロパティは、指定したオブジェクトでサポートされていません。 プロパティの名前、大文字と小文字、綴りを確認してください。|  
|0xC0204002|-1071628286|DTS_E_CANTCHANGEPROPERTYTYPE|プロパティの型を、コンポーネントによって設定された型から変更できません。|  
|0xC0204003|-1071628285|DTS_E_CANTADDOUTPUTID|出力 ID %1!d! を挿入できませんでした。 新しい出力は作成されませんでした。|  
|0xC0204004|-1071628284|DTS_E_CANTDELETEOUTPUTID|出力 ID %1!d! を 出力のコレクションから削除できません。  この ID は無効であったか、既定の出力またはエラー出力であった可能性があります。|  
|0xC0204006|-1071628282|DTS_E_FAILEDTOSETPROPERTY|"%2" のプロパティ "%1" を設定できませんでした。|  
|0xC0204007|-1071628281|DTS_E_FAILEDTOSETOUTPUTCOLUMNTYPE|%1 の型を、型 "%2"、長さ %3!d!、有効桁数 %4!d!、小数点以下桁数 %5!d!、コード ページ %6!d! に設定できませんでした。|  
|0xC0204008|-1071628280|DTS_E_MORETHANONEERROROUTPUTFOUND|複数のエラー出力がコンポーネントに見つかりました。エラー出力は 1 つしか存在できません。|  
|0xC020400A|-1071628278|DTS_E_CANTSETOUTPUTCOLUMNPROPERTY|出力列のプロパティを設定できません。|  
|0xC020400B|-1071628277|DTS_E_CANTMODIFYERROROUTPUTCOLUMNDATATYPE|エラー "%2" で、"%1" のデータ型を変更できません。|  
|0xC020400E|-1071628274|DTS_E_CANONLYSETISSORTEDONSOURCE|"%1" はソース出力ではないので、その IsSorted プロパティを True に設定することはできません。 ソース出力は SynchronousInputID 値が 0 です。|  
|0xC020400F|-1071628273|DTS_E_CANONLYSETSORTKEYONSOURCE|"%2" はソース出力ではないので、"%1" の SortKeyPosition プロパティを 0 以外に設定することはできません。 出力 "outputname" (ID) がソース出力ではないので、出力列 "colname" (ID) の SortKeyPosition プロパティを 0 以外に設定することはできません。|  
|0xC0204010|-1071628272|DTS_E_CANONLYSETCOMPFLAGSONSOURCE|"%2" はソース出力ではないので、"%1" の ComparisonFlags プロパティを 0 以外の値に設定することはできません。 出力 "outputname" (ID) がソース出力ではないので、出力列 "colname" (ID) の ComparisonFlags プロパティを 0 以外に設定することはできません。|  
|0xC0204011|-1071628271|DTS_E_NONSTRINGCOMPARISONFLAGSNOTZERO|"%1" は文字列型でないため、比較フラグを 0 にする必要があります。 文字列型の列では ComparisonFlags を 0 以外にしか設定できません。|  
|0xC0204012|-1071628270|DTS_E_COMPFLAGSONLYONSORTCOL|"%1" の SortKeyPosition が 0 に設定されているため、ComparisonFlags プロパティを 0 以外に設定することはできません。 出力列の SortKeyPosition が 0 以外の場合のみ、ComparisonFlags も 0 以外に設定できます。|  
|0xC0204013|-1071628269|DTS_E_READONLYSTOCKPROPERTY|プロパティは読み取り専用です。|  
|0xC0204014|-1071628268|DTS_E_INVALIDDATATYPE|%1 には無効なデータ型の値 (%2!ld!) が設定されています。|  
|0xC0204015|-1071628267|DTS_E_CODEPAGEREQUIRED|"%1" にはコード ページを設定する必要がありますが、渡された値は 0 でした。|  
|0xC0204016|-1071628266|DTS_E_INVALIDSTRINGLENGTH|"%1" の長さは無効です。 %2!ld! から %3!ld! までの長さにする %3!ld! までです。|  
|0xC0204017|-1071628265|DTS_E_INVALIDSCALE|"%1" の小数点以下桁数は無効です。 %2!ld! から %3!ld! までの小数点以下桁数にする %3!ld! までです。|  
|0xC0204018|-1071628264|DTS_E_INVALIDPRECISION|"%1" の有効桁数は無効です。 %2!ld! から %3!ld! までの有効桁数にする %3!ld! までです。|  
|0xC0204019|-1071628263|DTS_E_PROPVALUEIGNORED|"%1" では長さ、有効桁数、小数点以下桁数、またはコード ページの値が 0 以外に設定されていますが、このデータ型では値を 0 にする必要があります。|  
|0xC020401A|-1071628262|DTS_E_CANTSETOUTPUTCOLUMNDATATYPEPROPERTIES|%1 では出力列のデータ型プロパティの設定を行うことができません。|  
|0xC020401B|-1071628261|DTS_E_INVALIDDATATYPEFORERRORCOLUMNS|"%1" に無効なデータ型が含まれています。 "%1" は特殊なエラー列であり、有効なデータ型は DT_I4 のみです。|  
|0xC020401C|-1071628260|DTS_E_NOERRORDESCFORCOMPONENT|コンポーネントからエラー コードの説明が提供されていません。|  
|0xC020401D|-1071628259|DTS_E_UNRECOGNIZEDERRORCODE|指定されたエラー コードはこのコンポーネントに関連付けられていません。|  
|0xC020401F|-1071628257|DTS_E_TRUNCATIONTRIGGEREDREDIRECTION|切り捨てにより、切り捨て処理の設定に基づいて行がリダイレクトされました。|  
|0xC0204020|-1071628256|DTS_E_CANTSETUSAGETYPETOREADWRITE|"%1" では、系列 ID が %2!d! の入力列を読み取り/書き込みに設定できません。 この列でその使用法の種類は使用できません。 入力列の使用法の種類を、このコンポーネントではサポートされていない種類 UT_READWRITE に変更しようとしました。|  
|0xC0204023|-1071628253|DTS_E_CANTSETUSAGETYPE|%1 は、系列 ID が %2!d! の入力列を、要求された使用法の種類で使用することを禁止されています。|  
|0xC0204024|-1071628252|DTS_E_FAILEDTOSETUSAGETYPE|"%1" は、系列 ID が %2!d! の入力列に対して、要求された変更を行うことができませんでした。 エラー コード 0x%3!8.8X! により、要求が失敗しました。 入力列の使用法の種類を設定しようとして、このエラーが発生しました。|  
|0xC0204025|-1071628251|DTS_E_FAILEDTOSETOUTPUTCOLUMNDATATYPEPROPERTIES|エラー コード 0x%2!8.8X! により、"%1" にデータ型のプロパティを設定できませんでした。 出力列の 1 つ以上のデータ型のプロパティを設定中に、エラーが発生しました。|  
|0xC0204026|-1071628250|DTS_E_UNABLETORETRIEVEMETADATA|"%1" のメタデータを取得できません。 オブジェクト名が正しくて、オブジェクトが存在することを確認してください。|  
|0xC0204027|-1071628249|DTS_E_CANNOTMAPOUTPUTCOLUMN|出力列は、外部メタデータ列にマッピングできません。|  
|0xC0204028|-1071628248|DTS_E_UNSUPPORTEDVARIABLETYPE|変数 %1 は、"%2" 型にする必要があります。|  
|0xC020402A|-1071628246|DTS_E_CANTSETEXTERNALMETADATACOLUMNDATATYPEPROPERTIES|%1 では外部メタデータ列のデータ型プロパティの設定を行うことができません。|  
|0xC020402B|-1071628245|DTS_E_IDNOTINPUTNOROUTPUT|ID %1!lu! は入力 ID でも出力 ID でもありません。 指定された ID は、外部メタデータのコレクションが関連付けられている入力 ID または出力 ID である必要があります。|  
|0xC020402C|-1071628244|DTS_E_METADATACOLLECTIONNOTUSED|"%1" の外部メタデータのコレクションは、使用しないように設定されています。そのため、実行できる操作がありません。|  
|0xC020402D|-1071628243|DTS_E_NOBUFFERTYPEONSYNCOUTPUT|%1 は同期出力なので、同期出力のバッファーの種類を取得できません。|  
|0xC0207000|-1071616000|DTS_E_INPUTCOLUMNUSAGETYPENOTREADONLY|入力列 "%1" は読み取り専用にする必要があります。 入力列が、許可されていない読み取り専用以外の種類の使用法になっています。|  
|0xC0207001|-1071615999|DTS_E_MISSINGCUSTOMPROPERTY|要求されたプロパティ "%2" は "%1" にありません。 このオブジェクトには、ここで示されたカスタム プロパティが必要です。|  
|0xC0207002|-1071615998|DTS_E_ILLEGALCUSTOMOUTPUTPROPERTY|出力 %1 ではプロパティ "%2" を使用できませんが、現在はこのプロパティが割り当てられています。|  
|0xC0207003|-1071615997|DTS_E_INVALIDOUTPUTEXCLUSIONGROUP|%1 は、除外グループ %2!d! に存在する必要があります。 すべての出力は、この除外グループに存在する必要があります。|  
|0xC0207004|-1071615996|DTS_E_PROPERTYISEMPTY|プロパティ "%1" が空です。 プロパティを空にすることはできません。|  
|0xC0207005|-1071615995|DTS_E_CREATEEXPRESSIONOBJECTFAILED|式 "%1" にメモリを割り当てられません。 式を保持する内部オブジェクトを作成中にメモリ不足になりました。|  
|0xC0207006|-1071615994|DTS_E_EXPRESSIONPARSEFAILED|式 "%1" を解析できません。 式が無効であったか、メモリが不足しています。|  
|0xC0207007|-1071615993|DTS_E_EXPRESSIONCOMPUTEFAILED|エラー コード 0x%2!8.8X! により、式 "%1" を計算できませんでした。 式に、解析時に検出できなかった 0 除算などのエラーが含まれているか、メモリが不足している可能性があります。|  
|0xC0207008|-1071615992|DTS_E_FAILEDTOCREATEEXPRESSIONARRAY|式オブジェクトにメモリを割り当てられません。 式オブジェクト ポインターの配列を作成中にメモリ不足になりました。|  
|0xC020700A|-1071615990|DTS_E_FAILEDTOCREATEEXPRESSIONMANANGER|エラー コード 0x%2!8.8X! により、 式マネージャーの作成中に %1 に失敗しました。|  
|0xC020700B|-1071615989|DTS_E_SPLITEXPRESSIONNOTBOOLEAN|式 "%1" はブール式ではありません。 この式の結果は、ブール型になる必要があります。|  
|0xC020700C|-1071615988|DTS_E_EXPRESSIONVALIDATIONFAILED|"%2" の式 "%1" が無効です。|  
|0xC020700E|-1071615986|DTS_E_COLUMNNOTMATCHED|列 "%1" (%2!d!) が、入力ファイルのどの列とも一致しません。 出力列名または入力列名が、ファイル内に見つかりません。|  
|0xC020700F|-1071615985|DTS_E_SETRESULTCOLUMNFAILED|エラー コード 0x%3!8.8X! により、式 "%1" の結果列を %2 に設定できませんでした。 この式の結果を受け取る予定であった入力列または出力列を判断できないか、列の型にこの式の結果をキャストできません。|  
|0xC0207011|-1071615983|DTS_E_FAILEDTOGETLOCALEIDFROMPACKAGE|%1 はパッケージからロケール ID を取得できませんでした。|  
|0xC0207012|-1071615982|DTS_E_INCORRECTPARAMETERMAPPINGFORMAT|パラメーター マッピング文字列の形式が正しくありません。|  
|0xC0207013|-1071615981|DTS_E_NOTENOUGHPARAMETERSPROVIDED|SQL コマンドには %1!d! 個の パラメーターが必要ですが、パラメーター マッピングには %2!d! 個の %2!d! です。|  
|0xC0207014|-1071615980|DTS_E_PARAMETERNOTFOUNDINMAPPING|SQL コマンドには "%1" という名前のパラメーターが必要ですが、パラメーター マッピングに見つかりません。|  
|0xC0207015|-1071615979|DTS_E_DUPLICATEDATASOURCECOLUMNNAME|名前 "%1" のデータ ソース列が複数あります。  データ ソース列の名前は一意である必要があります。|  
|0xC0207016|-1071615978|DTS_E_DATASOURCECOLUMNWITHNONAMEFOUND|名前が指定されていないデータ ソース列があります。  各データ ソース列には名前を付ける必要があります。|  
|0xC0208001|-1071611903|DTS_E_DISCONNECTEDCOMPONENT|コンポーネントがレイアウトから切断されています。|  
|0xC0208002|-1071611902|DTS_E_INVALIDCOMPONENTID|レイアウト コンポーネントの ID が無効です。|  
|0xC0208003|-1071611901|DTS_E_INVALIDINPUTCOUNT|コンポーネントの入力数が無効です。|  
|0xC0208004|-1071611900|DTS_E_INVALIDOUTPUTCOUNT|コンポーネントの出力数が無効です。|  
|0xC0208005|-1071611899|DTS_E_NOINPUTSOROUTPUTS|コンポーネントに入力または出力がありません。|  
|0xC0208007|-1071611897|DTS_E_CANTALLOCATECOLUMNINFO|メモリ不足のため、このコンポーネントで操作されている列の一覧を割り当てることができませんでした。|  
|0xC0208008|-1071611896|DTS_E_OUTPUTCOLUMNNOTININPUT|出力列 "%1" (%2!d!) は、系列 ID が %3!d! の入力列を参照しますが、その系列 ID が指定された入力が見つかりませんでした。|  
|0xC0208009|-1071611895|DTS_E_SORTNEEDSONEKEY|少なくとも 1 つの入力列が並べ替えキーとして設定されている必要がありますが、キーが見つかりませんでした。|  
|0xC020800A|-1071611894|DTS_E_SORTDUPLICATEKEYWEIGHT|列 "%1" (%2!d!) と列 "%3" (%4!d!) はどちらも並べ替えキーの加重値 %5!d! が設定されました。|  
|0xC020800D|-1071611891|DTS_E_CANTMODIFYINVALID|この検証問題が解決されるまでは、このコンポーネントで要求されたメタデータの変更を実行できません。|  
|0xC020800E|-1071611890|DTS_E_CANTADDINPUT|入力のコレクションに入力を追加できません。|  
|0xC020800F|-1071611889|DTS_E_CANTADDOUTPUT|出力のコレクションに出力を追加できません。|  
|0xC0208010|-1071611888|DTS_E_CANTDELETEINPUT|入力のコレクションから入力を削除できません。|  
|0xC0208011|-1071611887|DTS_E_CANTDELETEOUTPUT|出力のコレクションから出力を削除できません。|  
|0xC0208014|-1071611884|DTS_E_CANTCHANGEUSAGETYPE|列の使用法の種類を変更できません。|  
|0xC0208016|-1071611882|DTS_E_INVALIDUSAGETYPEFORCUSTOMPROPERTY|カスタム プロパティ "%2" を使用するには、%1 を読み取り/書き込みに設定する必要があります。 入力列または出力列にはこのカスタム プロパティが存在しますが、読み取り/書き込みではありません。 プロパティを削除するか、この列を読み取り/書き込みに設定してください。|  
|0xC0208017|-1071611881|DTS_E_READWRITECOLUMNMISSINGREQUIREDCUSTOMPROPERTY|%1 には、読み取り/書き込みが設定されているので、カスタム プロパティ "%2" が必要です。 プロパティを追加するか、列から読み取り/書き込み属性を削除してください。|  
|0xC0208018|-1071611880|DTS_E_CANTDELETECOLUMN|列を削除できません。 このコンポーネントでは、この入力または出力から列を削除できません。|  
|0xC0208019|-1071611879|DTS_E_CANTADDCOLUMN|このコンポーネントでは、この入力または出力に列を追加できません。|  
|0xC020801A|-1071611878|DTS_E_CANNOTTFINDRUNTIMECONNECTIONOBJECT|接続 "%1" が見つかりません。 接続マネージャーに、同じ名前の接続が存在することを確認してください。|  
|0xC020801B|-1071611877|DTS_E_CANNOTFINDRUNTIMECONNECTIONMANAGER|ID "%1" のランタイム接続マネージャーが見つかりません。 接続マネージャー コレクションに、同じ ID の接続マネージャーが存在することを確認してください。|  
|0xC020801C|-1071611876|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|SSIS エラー コード DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER。  エラー コード 0x%2!8.8X! により、接続マネージャー "%1" に対する AcquireConnection メソッドの呼び出しが失敗しました。  このエラーの前に、AcquireConnection メソッドの呼び出しが失敗した理由の詳細が記載されたエラー メッセージが報告されている可能性があります。|  
|0xC020801D|-1071611875|DTS_E_ACQUIREDCONNECTIONISINVALID|接続マネージャー "%1" から取得した接続は無効です。|  
|0xC020801E|-1071611874|DTS_E_INCORRECTCONNECTIONMANAGERTYPE|接続マネージャー "%1" は種類が正しくありません。  必要な種類は "%2" です。 コンポーネントに使用できる種類は "%3" です。|  
|0xC020801F|-1071611873|DTS_E_CANNOTACQUIREMANAGEDCONNECTIONFROMCONNECTIONMANAGER|ランタイム接続マネージャーからマネージド接続を取得できません。|  
|0xC0208020|-1071611872|DTS_E_CANTINITINPUT|入力のコレクションを初期化するために入力を作成できません。|  
|0xC0208021|-1071611871|DTS_E_CANTINITOUTPUT|出力のコレクションを初期化するために出力を作成できません。|  
|0xC0208023|-1071611869|DTS_E_EXTRACTORCANTWRITE|エラー コード 0x%2!8.8X! により、ファイル "%1" に書き込めませんでした。|  
|0xC0208024|-1071611868|DTS_E_INCORRECTCONNECTIONOBJECTTYPE|接続マネージャー "%1" によって、AcquireConnection メソッドから種類の正しくないオブジェクトが返されました。|  
|0xC0208025|-1071611867|DTS_E_INPUTCOLPROPERTYNOTFOUND|入力列 "%1" (%2!d!) の "%3" プロパティが要求されましたが、見つかりません。 見つからないプロパティを追加してください。|  
|0xC0208026|-1071611866|DTS_E_EXTRACTORUNREFERENCED|"%1" は読み取り専用に設定されていますが、他のどの列からも参照されていません。 参照されていない列は許可されません。|  
|0xC0208027|-1071611865|DTS_E_EXTRACTORREFERENCEDCOLUMNNOTFOUND|"%1" は列 ID %2!d! を参照していますが、この列は入力にありません。 存在しない列を参照しています。|  
|0xC0208028|-1071611864|DTS_E_EXTRACTORDATACOLUMNNOTBLOB|"%1" は "%2" を参照していますが、この列は BLOB 型ではありません。|  
|0xC0208029|-1071611863|DTS_E_INSERTERREFERENCEDCOLUMNNOTFOUND|"%1" は ID が %2!d! の出力列を参照していますが、この列は出力にありません。|  
|0xC020802A|-1071611862|DTS_E_INSERTERCANTREAD|エラー コード 0x%2!8.8X! により、ファイル "%1" から読み取れませんでした。|  
|0xC020802B|-1071611861|DTS_E_TXSCD_NOTYPEDCOLUMNSATINPUT|緩やかに変化するディメンション変換では、入力の種類が固定属性、変化する属性、または履歴属性である列が少なくとも 1 列必要です。 少なくとも 1 つの列が FixedAttribute、ChangingAttribute、または HistoricalAttribute であることを確認してください。|  
|0xC020802C|-1071611860|DTS_E_TXSCD_INVALIDINPUTCOLUMNTYPE|"%1" の ColumnType プロパティが無効です。 現在の値が、許容される値の範囲内にありません。|  
|0xC020802D|-1071611859|DTS_E_TXSCD_CANNOTMAPDIFFERENTTYPES|入力列 "%1" を外部列 "%2" にマップできません。列のデータ型が異なります。 緩やかに変化するディメンション変換では、DT_STR および DT_WSTR 以外の型の列間でマッピングを行えません。|  
|0xC020802E|-1071611858|DTS_E_NTEXTDATATYPENOTSUPPORTEDWITHANSIFILES|"%1" のデータ型は DT_NTEXT ですが、この型は ANSI 形式のファイルではサポートされていません。 代わりに、DT_TEXT 型を使用し、データ変換コンポーネントでデータを DT_NTEXT 型に変換してください。|  
|0xC020802F|-1071611857|DTS_E_TEXTDATATYPENOTSUPPORTEDWITHUNICODEFILES|"%1" のデータ型は DT_TEXT ですが、この型は Unicode 形式のファイルではサポートされていません。 代わりに、DT_NTEXT 型を使用し、データ変換コンポーネントでデータを DT_TEXT 型に変換してください。|  
|0xC0208030|-1071611856|DTS_E_IMAGEDATATYPENOTSUPPORTED|"%1" のデータ型は DT_IMAGE ですが、この型はサポートされていません。 代わりに、DT_TEXT 型または DT_NTEXT 型を使用し、データ変換コンポーネントでデータを DT_IMAGE 型との間で変換してください。|  
|0xC0208031|-1071611855|DTS_E_FLATFILEFORMATNOTSUPPORTED|形式 "%1" はフラット ファイル接続マネージャーでサポートされていません。 サポートされている形式は、Delimited、FixedWidth、RaggedRight、および Mixed です。|  
|0xC0208032|-1071611854|DTS_E_EXTRACTORFILENAMECOLUMNNOTSTRING|"%1" にはファイル名を含める必要がありますが、文字列型ではありません。|  
|0xC0208033|-1071611853|DTS_E_EXTRACTORCANTAPPENDTRUNCATE|プロパティ設定の競合により、エラーが発生しました。 "%1" では、AllowAppend プロパティと ForceTruncate プロパティの両方が True に設定されています。 両方のプロパティを True に設定することはできません。 2 つのプロパティのいずれかを False に設定してください。|  
|0xC0208034|-1071611852|DTS_E_EXTRACTORCOLUMNALREADYREFERENCED|%1 は列 ID %2!d! を参照していますが、この列は既に %3 が参照しています。 列への 2 つの参照のうち、いずれかを削除してください。|  
|0xC0208035|-1071611851|DTS_E_CONNECTIONMANANGERNOTASSIGNED|%1 に接続マネージャーが割り当てられていません。|  
|0xC0208036|-1071611850|DTS_E_INSERTERCOLUMNALREADYREFERENCED|%1 は ID が %2!d! の出力列を参照していますが、この列は既に %3 が参照しています。|  
|0xC0208037|-1071611849|DTS_E_INSERTERCOLUMNNOTREFERENCED|"%1" はどの入力列からも参照されていません。 各出力列は、1 つの入力列によって参照される必要があります。|  
|0xC0208038|-1071611848|DTS_E_INSERTERDATACOLUMNNOTBLOB|"%1" は "%2" を参照していますが、この列は型が正しくありません。 DT_TEXT、DT_NTEXT、DT_IMAGE のいずれかにする必要があります。 BLOB である必要がある列を参照しています。|  
|0xC0208039|-1071611847|DTS_E_INSERTERFILENAMECOLUMNNOTSTRING|"%1" にはファイル名を含める必要がありますが、文字列型ではありません。|  
|0xC020803A|-1071611846|DTS_E_INSERTEREXPECTBOMINVALIDTYPE|"%1" では %2 の ExpectBOM プロパティが True に設定されていますが、この列は NT_NTEXT 型ではありません。 ExpectBOM により、列インポート変換でバイト順マーク (BOM) が予期されることが示されます。 ExpectBOM プロパティを False に設定するか、出力列のデータ型を DT_NTEXT に変更してください。|  
|0xC020803B|-1071611845|DTS_E_INSERTERINVALIDDATACOLUMNSETTYPE|データ出力列には、DT_TEXT、DT_NTEXT、または DT_IMAGE を指定する必要があります。 データ出力列は BLOB 型にのみ設定できます。|  
|0xC020803C|-1071611844|DTS_E_TXSCD_FIXEDATTRIBUTECHANGE|FailOnFixedAttributeChange プロパティが True に設定されている場合、固定属性の変更が検出されると変換が行われません。 行を固定属性の出力に送信するには、FailOnFixedAttributeChange プロパティを False に設定します。|  
|0xC020803D|-1071611843|DTS_E_TXSCD_LOOKUPFAILURE|参照変換で行を取得できませんでした。 FailOnLookupFailure が True に設定されている場合は、変換が行われず、行が取得されません。|  
|0xC020803E|-1071611842|DTS_E_TXSCD_INVALIDNUMBERSOFPARAMETERS|緩やかに変化するディメンション変換では、入力列の種類がキーである列が少なくとも 1 列必要です。 少なくとも 1 列の種類をキーに設定してください。|  
|0xC020803F|-1071611841|DTS_E_TXSCD_CANNOTFINDEXTERNALCOLUMN|名前 "%1" の外部列が見つかりません。|  
|0xC0208040|-1071611840|DTS_E_TXSCD_INFFEREDINDICATORNOTBOOL|推定インジケーター列 "%1" の型は DT_BOOL である必要があります。|  
|0xC0208107|-1071611641|DTS_E_ERRORROWDISPMUSTBENOTUSED|%1 は、エラー行の処理の値を RD_NotUsed に設定する必要があります。|  
|0xC0208108|-1071611640|DTS_E_TRUNCROWDISPMUSTBENOTUSED|%1 は、切り捨て行の処理の値を RD_NotUsed に設定する必要があります。|  
|0xC0208201|-1071611391|DTS_E_TXAGG_INPUTNOTFOUNDFOROUTPUT|ID %2!d! の出力列で必要とされている 系列 ID %1!d! の入力列が見つかりません。|  
|0xC0208202|-1071611390|DTS_E_TXAGG_INVALIDOUTPUTDATATYPEFORAGGREGATE|出力列 ID %1!d! で指定された集計の型に対する出力データ型が無効です。|  
|0xC0208203|-1071611389|DTS_E_TXAGG_INVALIDINPUTDATATYPEFORAGGREGATE|%2 で指定された集計に使用される %1 の入力データ型が無効です。|  
|0xC0208204|-1071611388|DTS_E_TXAGG_INPUTOUTPUTDATATYPEMISMATCH|入力列の系列 ID %1!d! と 出力列の ID %2!d! のデータ型が 一致しません。|  
|0xC0208205|-1071611387|DTS_E_UNABLETOGETINPUTBUFFERHANDLE|入力 ID %1!d! の入力バッファー ハンドルを取得できません。|  
|0xC0208206|-1071611386|DTS_E_UNABLETOGETOUTPUTBUFFERHANDLE|出力 ID %1!d! の出力バッファー ハンドルを取得できません。|  
|0xC0208207|-1071611385|DTS_E_UNABLETOFINDCOLUMNHANDLEINOUTPUTBUFFER|出力バッファーに系列 ID %1!d! の列が 見つかりません。|  
|0xC0208208|-1071611384|DTS_E_UNABLETOFINDCOLUMNHANDLEININPUTBUFFER|出力バッファーに系列 ID %1!d! の列が 見つかりません。|  
|0xC0208209|-1071611383|DTS_E_CANNOTHAVEZEROOUTPUTCOLUMNS|%1 の出力列数を 0 にすることはできません。|  
|0xC020820A|-1071611382|DTS_E_CONNECTIONMANAGERCOLUMNCOUNTMISMATCH|フラット ファイル接続マネージャー内の列数は、フラット ファイル アダプター内の列数と一致している必要があります。 フラット ファイル接続マネージャーには %1!d! 列ありますが、フラット ファイル アダプターには %2!d! 列あります。|  
|0xC020820B|-1071611381|DTS_E_MISMATCHCONNECTIONMANAGERCOLUMN|フラット ファイル接続マネージャーの インデックス %2!d! の列 "%1" が、フラット ファイル アダプターの 列コレクションのインデックス %3!d! にありませんでした。|  
|0xC020820D|-1071611379|DTS_E_EXTERNALMETADATACOLUMNISALREADYMAPPED|ID %1!d! の外部メタデータ列は、 %2 に既にマップされています。|  
|0xC020820E|-1071611378|DTS_E_TXAGG_STRING_TOO_LONG|変換で、%1!u! 文字を超えるキー列が 超えています。|  
|0xC020820F|-1071611377|DTS_E_DERIVEDRESULT_TOO_LONG|変換で、%1!u! バイトを超える結果値が バイトです。|  
|0xC0208210|-1071611376|DTS_E_TXAGG_MEMALLOCERROUTPUTDESCRIPTORS|メモリを割り当てられません。|  
|0xC0208211|-1071611375|DTS_E_TXAGG_MEMALLOCERRWORKSPACEDESCRIPTORS|メモリを割り当てられません。|  
|0xC0208212|-1071611374|DTS_E_TXAGG_MEMALLOCERRSORTORDERDESCRIPTORS|メモリを割り当てられません。|  
|0xC0208213|-1071611373|DTS_E_TXAGG_MEMALLOCERRNUMERICDESCRIPTORS|メモリを割り当てられません。|  
|0xC0208214|-1071611372|DTS_E_TXAGG_MEMALLOCERRCOUNTDISTINCTDESCRIPTOR|メモリを割り当てられません。|  
|0xC0208215|-1071611371|DTS_E_TXAGG_MEMALLOCERRWORKSPACESORTORDERDESCRIPTORS|メモリを割り当てられません。|  
|0xC0208216|-1071611370|DTS_E_TXAGG_MEMALLOCERRWORKSPACENUMERICDESCRIPTORS|メモリを割り当てられません。|  
|0xC0208217|-1071611369|DTS_E_TXAGG_MEMALLOCERRWORKSPACEBUFFCOLS|メモリを割り当てられません。|  
|0xC0208218|-1071611368|DTS_E_UNREFERENCEDINPUTCOLUMN|入力列 "%1" は参照されていません。|  
|0xC0208219|-1071611367|DTS_E_CANTBUILDTHREADPOOL|並べ替え変換で、%1!d! 個のスレッドを持つスレッド プールを 作成できませんでした。 メモリが不足しています。|  
|0xC020821A|-1071611366|DTS_E_QUEUEWORKITEMFAILED|並べ替え変換では、作業項目をスレッド プールのキューに登録できません。 メモリが不足しています。|  
|0xC020821B|-1071611365|DTS_E_SORTTHREADSTOPPED|エラー コード 0x%1!8.8X! により、並べ替え変換のワーカー スレッドが停止しました。 バッファーの並べ替え中に致命的なエラーが発生しました。|  
|0xC020821E|-1071611362|DTS_E_SORTBADTHREADCOUNT|MaxThreads は %1!ld! でした。1 から %2!ld! までの値を指定するか、または -1 を指定して CPU の既定の数が設定されるようにする必要があります。|  
|0xC020821F|-1071611361|DTS_E_DTPXMLLOADFAILURE|XML から読み込めません。|  
|0xC0208220|-1071611360|DTS_E_DTPXMLSAVEFAILURE|XML に保存できません。|  
|0xC0208221|-1071611359|DTS_E_DTPXMLINT32CONVERTERR|値 "%1" を整数値に変換できません。|  
|0xC0208222|-1071611358|DTS_E_DTPXMLBOOLCONVERTERR|値 "%1" をブール値に変換できません。|  
|0xC0208223|-1071611357|DTS_E_DTPXMLPARSEERRORNEARID|ID %1!d! のオブジェクト付近で読み込みエラーが発生しました。|  
|0xC0208226|-1071611354|DTS_E_DTPXMLPROPERTYTYPEERR|値 "%1" は属性 "%2" に対しては無効です。|  
|0xC0208228|-1071611352|DTS_E_DTPXMLSETUSAGETYPEERR|値 "%1" は属性 "%2" に対しては無効です。|  
|0xC0208229|-1071611351|DTS_E_DTPXMLDATATYPEERR|値 "%1" は属性 "%2" に対しては無効です。|  
|0xC020822A|-1071611350|DTS_E_UNMAPPEDINPUTCOLUMN|%1 は出力列にマップされません。|  
|0xC020822B|-1071611349|DTS_E_INPUTCOLUMNBADMAP|%1 に無効なマッピングがあります。  このコンポーネントには ID が %2!ld! の出力列は 存在しません。|  
|0xC020822D|-1071611347|DTS_E_MULTIPLYMAPPEDOUTCOL|%1 が出力列にマップされていますが、この出力列には、この入力へのマッピングが既に存在しています。|  
|0xC020822E|-1071611346|DTS_E_TXAGG_STRINGPROMOTIONFAILED|エラー 0x%2!8.8X! により、系列 ID %1!ld! の 入力列を DT_WSTR に変換できませんでした。|  
|0xC0208230|-1071611344|DTS_E_DTPXMLIDLOOKUPERR|ID が %1!d! の参照先オブジェクトが パッケージに見つかりませんでした。|  
|0xC0208231|-1071611343|DTS_E_DTPXMLINVALIDXMLPERSISTPROPERTY|pipelinexml モジュールに必要な永続プロパティを読み取れません。 このプロパティは、パイプラインで指定されていませんでした。|  
|0xC0208232|-1071611342|DTS_E_DTPXMLPROPERTYSTATEERR|値 "%1" は属性 "%2" に対しては無効です。|  
|0xC0208233|-1071611341|DTS_E_CANTGETCUSTOMPROPERTY|カスタム プロパティ "%1" を取得できません。|  
|0xC0208234|-1071611340|DTS_E_UNABLETOLOCATEINPUTCOLUMNID|位置番号 %2!d! のパラメーターの ParameterMap カスタム プロパティで参照される系列 ID %1!d! の入力列が入力列のコレクションに見つかりません。|  
|0xC0208235|-1071611339|DTS_E_TXLOOKUP_UNABLETOLOCATEREFCOLUMN|参照列 "%1!s!" が見つかりません。|  
|0xC0208236|-1071611338|DTS_E_TXLOOKUP_INCOMPATIBLEDATATYPES|%1 および "%2" という名前の参照列に、互換性のないデータ型が設定されています。|  
|0xC0208237|-1071611337|DTS_E_TXLOOKUP_PARAMMETADATAMISMATCH|パラメーター化 SQL ステートメントによって、メインの SQL ステートメントに一致しないメタデータが生成されました。|  
|0xC0208238|-1071611336|DTS_E_TXLOOKUP_INCORRECTNUMOFPARAMETERS|パラメーター化 SQL ステートメントに含まれているパラメーターの数が正しくありません。 必要なのは %1!d! 個ですが、%2!d! 個あります。|  
|0xC0208239|-1071611335|DTS_E_TXLOOKUP_INVALIDJOINTYPE|%1 に、結合できないデータ型が設定されています。|  
|0xC020823A|-1071611334|DTS_E_TXLOOKUP_INVALIDCOPYTYPE|%1 に、コピーできないデータ型が設定されています。|  
|0xC020823B|-1071611333|DTS_E_INSERTERINVALIDCOLUMNDATATYPE|%1 には、サポートされていないデータ型が含まれています。 DT_STR または DT_WSTR を指定する必要があります。|  
|0xC020823C|-1071611332|DTS_E_EXTRACTORINVALIDCOLUMNDATATYPE|%1 には、サポートされていないデータ型が含まれています。 DT_STR、DT_WSTR、DT_TEXT、DT_NTEXT、DT_IMAGE のいずれかを指定する必要があります。|  
|0xC020823D|-1071611331|DTS_E_TXCHARMAPINVALIDCOLUMNDATATYPE|%1 には、サポートされていないデータ型が含まれています。 DT_STR、DT_WSTR、DT_TEXT、DT_NTEXT のいずれかを指定する必要があります。|  
|0xC020823E|-1071611330|DTS_E_SORTCANTCREATEEVENT|並べ替え変換では、ワーカー スレッドと通信するイベントを作成できません。 並べ替え変換に使用できるシステム ハンドルが不足しています。|  
|0xC020823F|-1071611329|DTS_E_SORTCANTCREATETHREAD|並べ替え変換では、ワーカー スレッドを作成できません。 並べ替え変換に使用できるメモリが不足しています。|  
|0xC0208240|-1071611328|DTS_E_SORTCANTCOMPARE|並べ替え変換で、バッファー ID %2!d! の行 %1!d! を バッファー ID %4!d! の 行 %3!d! と 比較できませんでした。|  
|0xC0208242|-1071611326|DTS_E_TXLOOKUP_TOOFEWREFERENCECOLUMNS|参照変換の参照メタデータに含まれている列が少なすぎます。 SQLCommand プロパティを確認してください。 SELECT ステートメントから、少なくとも 1 つの列が返される必要があります。|  
|0xC0208243|-1071611325|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNINFO|ColumnInfo 構造体の配列にメモリを割り当てられません。|  
|0xC0208244|-1071611324|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNPAIR|ColumnPair 構造体の配列にメモリを割り当てられませんでした。|  
|0xC0208245|-1071611323|DTS_E_TXLOOKUP_MALLOCERR_BUFFCOL|メイン ワークスペースを作成するために、BUFFCOL 構造体の配列にメモリを割り当てられません。|  
|0xC0208246|-1071611322|DTS_E_TXLOOKUP_MAINWORKSPACE_CREATEERR|メイン ワークスペース バッファーを作成できません。|  
|0xC0208247|-1071611321|DTS_E_TXLOOKUP_HASHTABLE_MALLOCERR|ハッシュ テーブルにメモリを割り当てられません。|  
|0xC0208248|-1071611320|DTS_E_TXLOOKUP_HASHNODEHEAP_CREATEERR|ハッシュ ノードのヒープを作成するために、メモリを割り当てられません。|  
|0xC0208249|-1071611319|DTS_E_TXLOOKUP_HASHNODEHEAP_MALLOCERR|ハッシュ ノード ヒープにメモリを割り当てられません。|  
|0xC020824A|-1071611318|DTS_E_TXLOOKUP_LRUNODEHEAP_CREATEERR|LRU ノードのヒープを作成できません。 メモリ不足になりました。|  
|0xC020824B|-1071611317|DTS_E_TXLOOKUP_LRUNODEHEAP_MALLOCERR|LRU ノード ヒープにメモリを割り当てられません。 メモリ不足になりました。|  
|0xC020824C|-1071611316|DTS_E_TXLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|列のメタデータを読み込み中に OLE DB エラーが発生しました。 SQLCommand プロパティおよび SqlCommandParam プロパティを確認してください。|  
|0xC020824D|-1071611315|DTS_E_TXLOOKUP_OLEDBERR_GETIROWSET|行セットをフェッチ中に OLE DB エラーが発生しました。 SQLCommand プロパティおよび SqlCommandParam プロパティを確認してください。|  
|0xC020824E|-1071611314|DTS_E_TXLOOKUP_OLEDBERR_FILLBUFFER|内部キャッシュを設定中に OLE DB エラーが発生しました。 SQLCommand プロパティおよび SqlCommandParam プロパティを確認してください。|  
|0xC020824F|-1071611313|DTS_E_TXLOOKUP_OLEDBERR_BINDPARAMETERS|パラメーターのバインド中に OLE DB エラーが発生しました。 SQLCommand プロパティおよび SqlCommandParam プロパティを確認してください。|  
|0xC0208250|-1071611312|DTS_E_TXLOOKUP_OLEDBERR_CREATEBINDING|バインドの作成中に OLE DB エラーが発生しました。 SQLCommand プロパティおよび SqlCommandParam プロパティを確認してください。|  
|0xC0208251|-1071611311|DTS_E_TXLOOKUP_INVALID_CASE|実行時に switch ステートメントで無効なケースが発生しました。|  
|0xC0208252|-1071611310|DTS_E_TXLOOKUP_MAINWORKSPACE_MALLOCERR|メイン ワークスペース バッファーの新しい行にメモリを割り当てられません。 メモリ不足になりました。|  
|0xC0208253|-1071611309|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMIROWSET|パラメーター化された行セットをフェッチ中に OLE DB エラーが発生しました。 SQLCommand プロパティおよび SqlCommandParam プロパティを確認してください。|  
|0xC0208254|-1071611308|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMSINGLEROW|パラメーター化された行をフェッチ中に OLE DB エラーが発生しました。 SQLCommand プロパティおよび SqlCommandParam プロパティを確認してください。|  
|0xC0208255|-1071611307|DTS_E_TXAGG_MAINWORKSPACE_MALLOCERR|メイン ワークスペース バッファーの新しい行にメモリを割り当てられません。 メモリ不足になりました。|  
|0xC0208256|-1071611306|DTS_E_TXAGG_MAINWORKSPACE_CREATEERR|メイン ワークスペース バッファーを作成できません。|  
|0xC0208257|-1071611305|DTS_E_TXAGG_HASHTABLE_MALLOCERR|ハッシュ テーブルにメモリを割り当てられません。|  
|0xC0208258|-1071611304|DTS_E_TXAGG_HASHNODEHEAP_CREATEERR|ハッシュ ノードのヒープを作成するために、メモリを割り当てられません。|  
|0xC0208259|-1071611303|DTS_E_TXAGG_HASHNODEHEAP_MALLOCERR|ハッシュ ノード ヒープにメモリを割り当てられません。|  
|0xC020825A|-1071611302|DTS_E_TXAGG_CDNODEHEAP_CREATEERR|CountDistinct ノードのヒープを作成するために、メモリを割り当てられません。|  
|0xC020825B|-1071611301|DTS_E_TXAGG_CDNODEHEAP_MALLOCERR|CountDistinct ノード ヒープにメモリを割り当てられません。|  
|0xC020825C|-1071611300|DTS_E_TXAGG_CDCHAINHEAP_CREATEERR|CountDistinct チェーンのヒープを作成するために、メモリを割り当てられません。|  
|0xC020825D|-1071611299|DTS_E_TXAGG_CDHASHTABLE_CREATEERR|CountDistinct ハッシュ テーブルにメモリを割り当てられません。|  
|0xC020825E|-1071611298|DTS_E_TXAGG_CDWORKSPACE_MALLOCERR|CountDistinct ワークスペース バッファーの新しい行にメモリを割り当てられません。|  
|0xC020825F|-1071611297|DTS_E_TXAGG_CDWORKSPACE_CREATEERR|CountDistinct ワークスペース バッファーを作成できません。|  
|0xC0208260|-1071611296|DTS_E_TXAGG_CDCOLLASSEARRAY_MALLOCERR|CountDistinct 折りたたみ配列にメモリを割り当てられません。|  
|0xC0208261|-1071611295|DTS_E_TXAGG_CDCHAINHEAP_MALLOCERR|CountDistinct チェーンにメモリを割り当てられません。|  
|0xC0208262|-1071611294|DTS_E_TXCOPYMAP_MISMATCHED_COLUMN_METADATA|系列 ID %1!d! の列と系列 ID %2!d! の列のメタデータが一致していません。 copymap の出力列にマップされた入力列に、同じメタデータ (データ型、有効桁数、小数点以下桁数、長さ、またはコード ページ) がありません。|  
|0xC0208263|-1071611293|DTS_E_TXCOPYMAP_INCORRECT_OUTPUT_COLUMN_MAPPING|系列 ID "%1!d!" の出力列は 入力列に正しくマップされません。 出力列の CopyColumnId プロパティが正しくありません。|  
|0xC0208265|-1071611291|DTS_E_CANTGETBLOBDATA|列 "%1" の長い形式のデータを取得できませんでした。|  
|0xC0208266|-1071611290|DTS_E_CANTADDBLOBDATA|列の長い形式のデータを取得しましたが、データ フロー タスク バッファーに追加できません。|  
|0xC0208267|-1071611289|DTS_E_MCASTOUTPUTCOLUMNS|出力 "%1" (%2!d!) には出力列がありますが、マルチキャストの出力は列を宣言していません。 パッケージが破損しています。|  
|0xC0208273|-1071611277|DTS_E_UNABLETOGETLOCALIZEDRESOURCE|ローカライズされたリソース ID %1!d! を読み込めません。 RLL ファイルが存在するかどうかを確認してください。|  
|0xC0208274|-1071611276|DTS_E_DTPXMLEVENTSCACHEERR|イベント インターフェイスを取得できません。 XML に保存するためにデータ フロー モジュールに渡されたイベント インターフェイスが無効です。|  
|0xC0208275|-1071611275|DTS_E_DTPXMLPATHLOADERR|XML 読み込み中にパス オブジェクトを設定したときに、エラーが発生しました。|  
|0xC0208276|-1071611274|DTS_E_DTPXMLINPUTLOADERR|XML 読み込み中に入力オブジェクトを設定したときに、エラーが発生しました。|  
|0xC0208277|-1071611273|DTS_E_DTPXMLOUTPUTLOADERR|XML 読み込み中に出力オブジェクトを設定したときに、エラーが発生しました。|  
|0xC0208278|-1071611272|DTS_E_DTPXMLINPUTCOLUMNLOADERR|XML 読み込み中に入力列オブジェクトを設定したときに、エラーが発生しました。|  
|0xC0208279|-1071611271|DTS_E_DTPXMLOUTPUTCOLUMNLOADERR|XML 読み込み中に出力列オブジェクトを設定したときに、エラーが発生しました。|  
|0xC0208280|-1071611264|DTS_E_DTPXMLPROPERTYLOADERR|XML 読み込み中にプロパティ オブジェクトを設定したときに、エラーが発生しました。|  
|0xC0208281|-1071611263|DTS_E_DTPXMLCONNECTIONLOADERR|XML 読み込み中に接続オブジェクトを設定したときに、エラーが発生しました。|  
|0xC0208282|-1071611262|DTS_E_FG_MISSING_OUTPUT_COLUMNS|特殊変換に固有の列は存在しないか、正しくない型が含まれています。|  
|0xC0208283|-1071611261|DTS_E_FG_PREPARE_TABLES_AND_ACCESSORS|あいまいグループ化変換は、必要なテーブルおよびアクセサーの作成に失敗しました。|  
|0xC0208284|-1071611260|DTS_E_FG_COPY_INPUT|あいまいグループ化変換は、入力のコピーに失敗しました。|  
|0xC0208285|-1071611259|DTS_E_FG_GENERATE_GROUPS|あいまいグループ化変換は、グループの生成に失敗しました。|  
|0xC0208286|-1071611258|DTS_E_FG_LEADING_TRAILING|プロパティ '%1' の設定を適用しているときに、あいまいグループ化で予期しないエラーが発生しました。|  
|0xC0208287|-1071611257|DTS_E_FG_PICK_CANONICAL|あいまいグループ化変換は、データを標準化するときに使用するデータの正規行の選択に失敗しました。|  
|0xC0208288|-1071611256|DTS_E_FG_NOBLOBS|あいまいグループ化は、IMAGE、TEXT、または NTEXT 型の入力列をサポートしていません。|  
|0xC0208289|-1071611255|DTS_E_FG_FUZZY_MATCH_ON_NONSTRING|DT_STR 型または DT_WSTR 型ではない列 "%1" (%2!d!) にあいまい一致が指定されました。|  
|0xC020828A|-1071611254|DTS_E_FUZZYGROUPINGINTERNALPIPELINEERROR|あいまいグループ化変換のパイプライン エラーが発生し、エラー コード 0x%1!8.8X! が返されました: "%2"。|  
|0xC020828B|-1071611253|DTS_E_CODE_PAGE_NOT_SUPPORTED|出力列 "%2" (%3!d!) で指定されている コード ページ %1!d! はサポートされていません。  最初にこの列を DT_WSTR に変換する必要があります。変換を行うには、この列の前にデータ変換を挿入します。|  
|0xC0208294|-1071611244|DTS_E_SETEODFAILED|バッファーによる出力 "%1" (%2!d!) のデータの終了フラグを設定中にエラーが発生しました。|  
|0xC0208296|-1071611242|DTS_E_CANTCLONE|入力バッファーを複製できませんでした。 メモリが不足しているか、内部エラーが発生しました。|  
|0xC02082F9|-1071611143|DTS_E_TXCHARMAP_CANTKATAKANAHIRAGANA|列 "%1" で、カタカナ文字列とひらがな文字列を同時に生成するように要求しています。|  
|0xC02082FA|-1071611142|DTS_E_TXCHARMAP_CANTSIMPLECOMPLEX|列 "%1" で、簡体中国語と繁体中国語を同時に生成するように要求しています。|  
|0xC02082FB|-1071611141|DTS_E_TXCHARMAP_CANTFULLHALF|列 "%1" で、全角文字列と半角文字列の両方を生成する操作を要求しています。|  
|0xC02082FC|-1071611140|DTS_E_TXCHARMAP_CANTCHINAJAPAN|列 "%1" で、日本語文字列での操作と中国語文字列での操作を組み合わせています。|  
|0xC02082FD|-1071611139|DTS_E_TXCHARMAP_CANTCASECHINESE|列 "%1" で、中国語文字列の操作と、大文字および小文字の操作を組み合わせています。|  
|0xC02082FE|-1071611138|DTS_E_TXCHARMAP_CANTCASEJAPANESE|列 "%1" で、日本語文字列での操作と、大文字および小文字の操作を組み合わせています。|  
|0xC02082FF|-1071611137|DTS_E_TXCHARMAP_CANTBOTHCASE|列 "%1" で、この列が大文字と小文字の両方にマップされています。|  
|0xC0208300|-1071611136|DTS_E_TXCHARMAP_CANTLINGUISTIC|列 "%1" で、大文字と小文字以外のフラグと言語の文字種操作を組み合わせています。|  
|0xC0208301|-1071611135|DTS_E_TXCHARMAP_INVALIDMAPFLAGANDDATATYPE|列 "%1" のデータ型を指定どおりにマップできません。|  
|0xC0208302|-1071611134|DTS_E_TXFUZZYLOOKUP_UNSUPPORTED_MATCH_INDEX_VERSION|既存の一致インデックス "%2" のバージョン (%1) はサポートされていません。 予期していたバージョンは "%3" です。 このエラーは、インデックス メタデータに保存されているバージョンが現在のコードが構築されたときのバージョンと一致しない場合に発生します。 現在のバージョンのコードを使用してインデックスを再構築することで、エラーを修正してください。|  
|0xC0208303|-1071611133|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX|テーブル "%1" は、構築済みの有効な一致インデックスではないようです。 このエラーは、メタデータ レコードを指定された構築済みのインデックスから読み込めない場合に発生します。|  
|0xC0208304|-1071611132|DTS_E_TXFUZZYLOOKUP_UNABLE_TO_READ_MATCH_INDEX|指定された構築済みの一致インデックス "%1" を読み取れません。  OLEDB エラー コード: 0x%2!8.8X!。|  
|0xC0208305|-1071611131|DTS_E_TXFUZZYLOOKUP_NO_JOIN_COLUMNS|参照テーブル列への有効な結合が指定された入力列はありませんでした。  少なくとも 1 つの結合が、入力列プロパティ JoinToReferenceColumn および JoinType で定義されていることを確認してください。|  
|0xC0208306|-1071611130|DTS_E_TXFUZZYLOOKUP_INDEX_DOES_NOT_CONTAIN_COLUMN|指定された既存の一致インデックス "%1" は、もともと列 "%2" のあいまい一致情報を使用して構築されていませんでした。  この情報を含めるために、既存の一致インデックスを再構築する必要があります。 このエラーは、インデックスがあいまい結合列以外の列を使用して構築された場合に発生します。|  
|0xC0208307|-1071611129|DTS_E_TXFUZZYLOOKUP_IDENTIFIER_PROPERTY|プロパティ "%2" に指定された名前 "%1" は、有効な SQL 識別子名ではありません。 このエラーは、プロパティの名前が、有効な SQL 識別子名の仕様に準拠していない場合に発生します。|  
|0xC0208309|-1071611127|DTS_E_TXFUZZYLOOKUP_MINSIMILARITY_INVALID|あいまい参照変換の MinSimilarity しきい値プロパティには、0.0 以上かつ 1.0 未満の値を指定する必要があります。|  
|0xC020830A|-1071611126|DTS_E_TXFUZZYLOOKUP_INVALID_PROPERTY_VALUE|プロパティ "%2" の値 "%1" が無効です。|  
|0xC020830B|-1071611125|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_FUZZY_JOIN_DATATYPES|あいまい結合は DT_STR 型と DT_WSTR 型の文字列間でのみサポートされているので、入力列 "%1" と参照列 "%2" の間に指定されているあいまい参照は無効です。|  
|0xC020830C|-1071611124|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_EXACT_JOIN_DATATYPES|完全な参照列 "%1" と "%2" のデータ型が同じでないか、比較可能な文字列型ではありません。 完全結合は、列のデータ型が同一の場合、または DT_STR 型と DT_WSTR 型の組み合わせの場合にサポートされています。|  
|0xC020830D|-1071611123|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_COPYCOLUMN_DATATYPES|コピー列 "%1" と "%2" のデータ型が同じでないか、または普通に変換できる文字列型ではありません。 参照から出力へのコピーは、列のデータ型が同一の場合または DT_STR 型と DT_WSTR 型の組み合わせの場合にサポートされていますが、他のデータ型ではサポートされていません。このエラーは、このことが原因で発生します。|  
|0xC020830E|-1071611122|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_PASSTHRUCOLUMN_DATATYPES|パススルー列 "%1" と "%2" のデータ型が一致しません。 入力から出力へのパススルー列としてサポートされているのは、データ型が一致する列のみです。|  
|0xC020830F|-1071611121|DTS_E_TXFUZZYLOOKUP_UNABLETOLOCATEREFCOLUMN|参照列 "%1" が見つかりません。|  
|0xC0208311|-1071611119|DTS_E_TXFUZZYLOOKUP_OUTPUT_COLUMN_MUST_BE_PASSTHRU_COLUMN_OR_A_COPY_COLUMN|出力列には、CopyColumn プロパティまたは PassThruColumn プロパティのいずれか 1 つだけが指定されている必要があります。 このエラーは、CopyColumn プロパティおよび PassThruColumn プロパティのどちらにも空でない値が設定されていない場合、またはこれら両方のプロパティに空でない値が設定されている場合に発生します。|  
|0xC0208312|-1071611118|DTS_E_TXFUZZYLOOKUP_PASSTHRU_COLUMN_NOT_FOUND|出力列 '%3' でプロパティ '%2' に指定された変換元系列 ID '%1!d!' が 入力列のコレクションに見つかりませんでした。 このエラーは、出力列にパススルー列として指定された入力列 ID が入力のセットに見つからない場合に発生します。|  
|0xC0208313|-1071611117|DTS_E_TXFUZZYLOOKUP_INDEXED_COLUMN_NOT_FOUND_IN_REF_TABLE|構築済みのインデックス "%2" の列 "%1" が参照テーブルまたはクエリに見つかりませんでした。 このエラーは、参照テーブルのスキーマまたはクエリが、既存の一致インデックスの構築後に変更された場合に発生します。|  
|0xC0208314|-1071611116|DTS_E_TXFUZZYLOOKUP_TOKEN_TOO_LONG|コンポーネントで 2147483647 文字より大きいトークンが検出されました。|  
|0xC0208315|-1071611115|DTS_E_RAWMETADATAMISMATCHTYPE|出力ファイルを追加できません。 列 "%1" の名前は一致していますが、出力ファイルの列の型は %2 で、入力列の型は %3 です。 列のメタデータのデータ型が一致しません。|  
|0xC0208316|-1071611114|DTS_E_RAWMETADATAMISMATCHSIZE|出力ファイルを追加できません。 列 "%1" の名前は一致していますが、出力ファイルの列の最大長は %2!d! で、 入力列の最大長は %3!d! です。 列のメタデータの長さが一致しません。|  
|0xC0208317|-1071611113|DTS_E_RAWMETADATAMISMATCHCODEPAGE|出力ファイルを追加できません。 列 "%1" の名前は一致していますが、出力ファイルの列のコード ページは %2!d! で、 入力列のコード ページは %3!d! です。 指定された列のメタデータのコード ページが一致しません。|  
|0xC0208318|-1071611112|DTS_E_RAWMETADATAMISMATCHPRECISION|出力ファイルを追加できません。 列 "%1" の名前は一致していますが、出力ファイルの列の有効桁数は %2!d! で、 入力列の有効桁数は %3!d! です。 指定された列のメタデータの有効桁数が一致しません。|  
|0xC0208319|-1071611111|DTS_E_RAWMETADATAMISMATCHSCALE|出力ファイルを追加できません。 列 "%1" の名前は一致していますが、出力ファイルの列の小数点以下桁数は %2!d! で、 入力列の小数点以下桁数は %3!d! です。  指定された列のメタデータの小数点以下桁数が一致しません。|  
|0xC020831A|-1071611110|DTS_E_COULD_NOT_DETERMINE_DATASOURCE_DBMSNAME|"%1" の DBMS 名とバージョンを特定できません。 このエラーは、接続の IDBProperties によって、DBMS 名とバージョンを確認するのに必要な情報が返されなかった場合に発生します。|  
|0xC020831B|-1071611109|DTS_E_INCORRECT_SQL_SERVER_VERSION|"%1" の DBMS の種類またはバージョンは、サポートされていません。  Microsoft SQL Server Version 8.0 (2000) 以降への接続が必要です。 このエラーは、接続の IDBProperties から正しいバージョンが返されなかった場合に発生します。|  
|0xC020831D|-1071611107|DTS_E_CANTDELETEERRORCOLUMNS|%1 は特殊なエラー出力列なので、削除できません。|  
|0xC020831E|-1071611106|DTS_E_UNEXPECTEDCOLUMNDATATYPE|列 "%1" に指定されたデータ型が予期された型 "%2" ではありません。|  
|0xC020831F|-1071611105|DTS_E_INPUTCOLUMNNOTFOUND|出力列 "%3" でプロパティ "%2" によって参照されている入力列の系列 ID "%1" が入力列のコレクションに見つかりませんでした。|  
|0xC0208320|-1071611104|DTS_E_TXGROUPDUPS_INPUTCOLUMNNOTJOINED|出力列 "%3" でプロパティ "%2" によって参照されている入力列 "%1" には、プロパティ ToBeCleaned=True と有効な ExactFuzzy プロパティ値を指定する必要があります。|  
|0xC0208322|-1071611102|DTS_E_TXFUZZYLOOKUP_REF_TABLE_MISSING_IDENTITY_INDEX|参照テーブル '%1' の整数型の ID 列にクラスター化インデックスがありません。クラスター化インデックスは、プロパティ 'CopyRefTable' が False に設定されている場合に必要です。 CopyRefTable が False の場合、参照テーブルの整数型の ID 列にクラスター化インデックスが必要です。|  
|0xC0208323|-1071611101|DTS_E_TXFUZZYLOOKUP_REF_CONTAINS_NON_INTEGER_IDENT_COLUMN|参照テーブル '%1' には整数型ではない ID 列が含まれていますが、それはサポートされていません。 列 '%2' を含まないテーブルのビューを使用してください。  このエラーは、コピーが参照テーブルで作成されているときに、整数型の ID 列が追加されますが、テーブルごとに 1 つの ID 列しか保持できないことが原因で発生します。|  
|0xC0208324|-1071611100|DTS_E_TXFUZZY_MATCHCONTRIBUTION_AND_HIERARCHY_SPECIFIED|MatchContribution と階層情報の両方を同時に指定することはできません。 これらのプロパティはどちらもスコアに対する重み係数なので、許可されていません。|  
|0xC0208325|-1071611099|DTS_E_TXFUZZY_HIERARCHY_INCORRECT|階層内のレベルには一意の数字を指定する必要があります。 階層値の有効なレベルは 1 以上の整数です。 数値が小さくなるほど、階層の下位の列になります。 既定値は 0 で、列が階層の一部でないことを示します。 レベルが重なり合ったり、レベル間にギャップがあることは許可されません。|  
|0xC0208326|-1071611098|DTS_E_TXFUZZYGROUPING_INSUFFICIENT_FUZZY_JOIN_COLUMNS|あいまいグループ化の対象となる列が定義されませんでした。  列プロパティ ToBeCleaned=true および ExactFuzzy=2 が設定された入力列が少なくとも 1 つ必要です。|  
|0xC0208329|-1071611095|DTS_E_TXFUZZYLOOKUP_COLUMNINVALID|何らかの理由により、ID '%1!d!' の列 が有効ではありませんでした。|  
|0xC020832A|-1071611094|DTS_E_TXFUZZYLOOKUP_UNSUPPORTEDDATATYPE|列 '%1' のデータ型はサポートされていません。|  
|0xC020832C|-1071611092|DTS_E_TXFUZZYLOOKUP_OUTPUTLENGTHMISMATCH|出力列 '%1' の長さは、基になる列 '%2' の長さよりも短くなっています。|  
|0xC020832F|-1071611089|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFINPUTCOLUMNS|入力列は 1 つだけ存在する必要があります。|  
|0xC0208330|-1071611088|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFOUTPUTCOLUMNS|出力列は 2 つだけ存在する必要があります。|  
|0xC0208331|-1071611087|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFINPUTCOLUMN|入力列に指定できるデータ型は DT_WSTR または DT_NTEXT のみです。|  
|0xC0208332|-1071611086|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFOUTPUTCOLUMN|出力列 [%1!d!] にデータ型として設定できるのは、'%2' のみです。|  
|0xC0208333|-1071611085|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFREFERENCECOLUMN|参照列に指定できるデータ型は DT_STR または DT_WSTR のみです。|  
|0xC0208334|-1071611084|DTS_E_TERMEXTRACTION_UNABLETOLOCATEREFCOLUMN|参照列 '%1' を検索中にエラーが発生しました。|  
|0xC0208335|-1071611083|DTS_E_TERMEXTRACTION_INCORRECTTERMTYPE|変換の用語の種類には WordOnly、PhraseOnly、または WordPhrase のみを指定できます。|  
|0xC0208336|-1071611082|DTS_E_TERMEXTRACTION_INCORRECTFREQUENCYTHRESHOLD|頻度のしきい値の値には、'%1!d!' 以上を指定する必要があります。|  
|0xC0208337|-1071611081|DTS_E_TERMEXTRACTION_INCORRECTMAXLENOFTERM|用語の最大長の値には、'%1!d!' 以上を指定する必要があります。|  
|0xC0208338|-1071611080|DTS_E_TERMEXTRACTION_TOOFEWREFERENCECOLUMNS|用語抽出参照メタデータに含まれている列が少なすぎます。|  
|0xC0208339|-1071611079|DTS_E_TERMEXTRACTION_MALLOCERR_REFERENCECOLUMNINFO|メモリの割り当て中にエラーが発生しました。|  
|0xC020833A|-1071611078|DTS_E_TERMEXTRACTION_MAINWORKSPACE_CREATEERR|ワークスペース バッファーの作成中にエラーが発生しました。|  
|0xC020833B|-1071611077|DTS_E_TERMEXTRACTION_OLEDBERR_CREATEBINDING|バインドの作成中に OLEDB エラーが発生しました。|  
|0xC020833C|-1071611076|DTS_E_TERMEXTRACTION_OLEDBERR_GETIROWSET|行セットをフェッチ中に OLEDB エラーが発生しました。|  
|0xC020833D|-1071611075|DTS_E_TERMEXTRACTION_OLEDBERR_FILLBUFFER|内部キャッシュの設定中に OLEDB エラーが発生しました。|  
|0xC020833E|-1071611074|DTS_E_TERMEXTRACTION_PROCESSERR|行 %1!ld!、列 %2!ld! の用語を抽出中にエラーが発生しました。 返されたエラー コードは 0x%3!8.8X! です。 回避策として、入力からこの用語を削除してください。|  
|0xC020833F|-1071611073|DTS_E_TERMEXTRACTIONORLOOKUP_PROCESSERR_DEPOSITFULL|用語の候補数が制限の 4G を超えています。|  
|0xC0208340|-1071611072|DTS_E_TERMEXTRACTION_INVALIDOUTTERMTABLEORCOLUMN|除外用語に使用される参照テーブル、ビュー、または列が無効です。|  
|0xC0208341|-1071611071|DTS_E_TXFUZZYLOOKUP_STRINGCOLUMNTOOLONG|文字列型の列 '%1' の長さが 4,000 文字を超えています。  DT_STR から DT_WSTR に変換する必要があるため、切り捨てが発生します。  列幅を縮小するか、または DT_WSTR 型の列のみを使用してください。|  
|0xC0208342|-1071611070|DTS_E_TERMEXTRACTION_OUTTERMTABLEANDCOLUMNNOTSET|除外用語に使用される参照テーブル、ビュー、または列が設定されていません。|  
|0xC0208343|-1071611069|DTS_E_TERMLOOKUP_TOOFEWOUTPUTCOLUMNS|用語参照に含まれている出力列が少なすぎます。|  
|0xC0208344|-1071611068|DTS_E_TERMLOOKUP_INCORRECTDATATYPEOFREFERENCECOLUMN|参照列に指定できるデータ型は DT_STR または DT_WSTR のみです。|  
|0xC0208345|-1071611067|DTS_E_TERMLOOKUP_UNABLETOLOCATEREFCOLUMN|参照列 '%1' を検索中にエラーが発生しました。|  
|0xC0208346|-1071611066|DTS_E_TERMLOOKUP_TOOFEWREFERENCECOLUMNS|用語参照の参照メタデータに含まれている列が少なすぎます。|  
|0xC0208347|-1071611065|DTS_E_TERMEXTRACTIONORLOOKUP_TESTOFFSETERROR|単語の正規化中にエラーが発生しました。|  
|0xC0208348|-1071611064|DTS_E_TERMLOOKUP_MAINWORKSPACE_CREATEERR|ワークスペース バッファーの作成中にエラーが発生しました。|  
|0xC0208349|-1071611063|DTS_E_TERMLOOKUP_OLEDBERR_CREATEBINDING|バインドの作成中に OLEDB エラーが発生しました。|  
|0xC020834A|-1071611062|DTS_E_TERMLOOKUP_OLEDBERR_GETIROWSET|行セットをフェッチ中に OLEDB エラーが発生しました。|  
|0xC020834B|-1071611061|DTS_E_TERMLOOKUP_OLEDBERR_FILLBUFFER|内部キャッシュの設定中に OLEDB エラーが発生しました。|  
|0xC020834C|-1071611060|DTS_E_TERMLOOKUP_PROCESSERR|行 %1!ld!、列 %2!ld! の用語を参照中にエラーが発生しました。 返されたエラー コードは 0x%3!8.8X! です。 回避策として、入力からこの用語を削除してください。|  
|0xC020834D|-1071611059|DTS_E_TERMLOOKUP_TEXTIDINPUTCOLUMNNOTMAPPEDWITHOUTPUTCOLUMN|少なくとも 1 つのパススルー列が出力列にマップされません。|  
|0xC020834E|-1071611058|DTS_E_TERMLOOKUP_INCORRECTEXACTNUMBEROFTEXTCOLUMNS|1 つの参照列には入力列が 1 つだけマップされている必要があります。|  
|0xC020834F|-1071611057|DTS_E_TERMLOOKUP_TEXTINPUTCOLUMNHAVEINCORRECTDATATYPE|参照列にマップされている入力列に指定できるデータ型は、DT_NTXT または DT_WSTR のみです。|  
|0xC0208354|-1071611052|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX_NAME|参照テーブル名 "%1" は有効な SQL 識別子ではありません。 このエラーは、入力文字列からテーブル名を解析できない場合に発生します。 名前に含まれているスペースが引用符で囲まれていない可能性があります。 テーブル名が正しく引用符で囲まれていることを確認してください。|  
|0xC0208355|-1071611051|DTS_E_TERMEXTRACTION_TERMFILTERSTARTITERATIONERROR|用語フィルターの繰り返しの開始中にエラーが発生しました。|  
|0xC0208356|-1071611050|DTS_E_TERMEXTRACTION_EMPTYTERMRESULTERROR|用語のキャッシュに使用するバッファーの再要求中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC0208357|-1071611049|DTS_E_TERMEXTRACTION_STDLENGTHERROR|STL コンテナーから std::length_error が発生しました。|  
|0xC0208358|-1071611048|DTS_E_TERMLOOKUP_SAVEWORDWITHPUNCTERROR|句読点が含まれている単語の保存中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC0208359|-1071611047|DTS_E_TERMLOOKUP_ADDREFERENCETERM|%1!ld! 番目の参照用語を処理中にエラーが発生しました。 返されたエラー コードは 0x%2!8.8X! です。 回避策として、その参照用語を参照テーブルから削除してください。|  
|0xC020835A|-1071611046|DTS_E_TERMLOOKUP_SORREFERENCETERM|参照用語の並べ替え中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC020835B|-1071611045|DTS_E_TERMLOOKUP_COUNTTERM|用語の候補数をカウント中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC020835C|-1071611044|DTS_E_FUZZYLOOKUP_REFERENCECACHEFULL|あいまい参照によって、参照テーブル全体をメイン メモリに読み込めませんでした。これは、Exhaustive プロパティが有効なときに必要なことです。  システム メモリが不足していたか、参照テーブルを読み込むには十分でない制限が MaxMemoryUsage に指定されていました。  MaxMemoryUsage を 0 に設定するか、設定値を大幅に増やしてください。  または、Exhaustive プロパティを無効にしてください。|  
|0xC020835D|-1071611043|DTS_E_TERMLOOKUP_INITIALIZE|用語参照のエンジンの初期化中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC020835E|-1071611042|DTS_E_TERMLOOKUP_PROCESSSENTENCE|文の処理中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC020835F|-1071611041|DTS_E_TEXTMININGBASE_APPENDTOTEMPBUFFER|内部バッファーに文字列を追加中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC0208360|-1071611040|DTS_E_TERMEXTRACTION_SAVEPOSTAG|内部バッファーの品詞タグを保存中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC0208361|-1071611039|DTS_E_TERMEXTRACTION_COUNTTERM|用語の候補数をカウント中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC0208362|-1071611038|DTS_E_TERMEXTRACTION_INITPOSPROCESSOR|品詞プロセッサを初期化中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC0208363|-1071611037|DTS_E_TERMEXTRACTION_INITFSA|有限状態オートマトンの読み込み中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC0208364|-1071611036|DTS_E_TERMEXTRACTION_INITIALIZE|用語抽出のエンジンを初期化中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC0208365|-1071611035|DTS_E_TERMEXTRACTION_PROCESSSENTENCE|文の内部を処理中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC0208366|-1071611034|DTS_E_TERMEXTRACTION_INITPOSTAGVECTOR|品詞プロセッサを初期化中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC0208367|-1071611033|DTS_E_TERMEXTRACTION_SAVEPTRSTRING|内部バッファーに文字列を追加中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC0208368|-1071611032|DTS_E_TERMEXTRACTION_ADDWORDTODECODER|統計デコーダーへ単語を追加中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC0208369|-1071611031|DTS_E_TERMEXTRACTION_DECODE|文のデコード中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC020836A|-1071611030|DTS_E_TERMEXTRACTION_SETEXCLUDEDTERM|除外用語の設定中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC020836B|-1071611029|DTS_E_TERMEXTRACTION_PROCESSDOCUMENT|入力内のドキュメントを処理中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC020836C|-1071611028|DTS_E_TEXTMININGBASE_TESTPERIOD|ピリオドが頭字語に含まれているかどうかをテストしているときにエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC020836D|-1071611027|DTS_E_TERMLOOKUP_ENGINEADDREFERENCETERM|参照用語の設定中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC020836E|-1071611026|DTS_E_TERMLOOKUP_PROCESSDOCUMENT|入力内のドキュメントを処理中にエラーが発生しました。 返されたエラー コードは 0x%1!8.8X! です。|  
|0xC020836F|-1071611025|DTS_E_INVALIDBULKINSERTPROPERTYVALUE|プロパティ %1 の値は %2!d! ですが、許可されていません。  値には、%3!d! 以上の値を指定する必要があります。|  
|0xC0208370|-1071611024|DTS_E_INVALIDBULKINSERTFIRSTROWLASTROWVALUES|プロパティ %1 の値は %2!d! ですが、プロパティ %4 の値 %3!d! 以下の値である 必要があります。|  
|0xC0208371|-1071611023|DTS_E_FUZZYLOOKUPUNABLETODELETEEXISTINGMATCHINDEX|"%1" という名前の既存のあいまい一致インデックスを削除中にエラーが発生しました。 このテーブルはあいまい参照 (またはこのバージョンのあいまい参照) によって作成されなかったか、壊れているか、または別の問題がある可能性があります。 "%2" という名前のテーブルを手動で削除するか、MatchIndexName プロパティに別の名前を指定してください。|  
|0xC0208372|-1071611022|DTS_E_TERMEXTRACTION_INCORRECTSCORETYPE|変換のスコアの種類に設定できるのは、頻度または TFIDF のみです。|  
|0xC0208373|-1071611021|DTS_E_FUZZYLOOKUPREFTABLETOOBIG|指定された参照テーブルの行数が多すぎます。 あいまい参照は、10 億行未満の参照テーブルでのみ機能します。 参照テーブルで、より小さいビューを使用することを検討してください。|  
|0xC0208374|-1071611020|DTS_E_FUZZYLOOKUPUNABLETODETERMINEREFERENCETABLESIZE|参照テーブル '%1' のサイズを特定できません。  このオブジェクトがビューであり、テーブルではない可能性があります。  あいまい参照では、CopyReferentaceTable が False に設定されたビューをサポートしていません。  テーブルが存在し、CopyReferenceTable が True に設定されていることを確認してください。|  
|0xC0208377|-1071611017|DTS_E_XMLSRCOUTPUTCOLUMNDATATYPENOTSUPPORTED|%2 の SSIS データ フロー タスクのデータ型 "%1" は、%3 に対してはサポートされていません。|  
|0xC0208378|-1071611016|DTS_E_XMLSRCCANNOTFINDCOLUMNTOSETDATATYPE|ID が %2!d! の出力に ID が %1!d! の出力列のデータ型のプロパティを 設定できません。 出力または列が見つかりませんでした。|  
|0xC0208379|-1071611015|DTS_E_CUSTOMPROPERTYISREADONLY|%2 のカスタム プロパティ "%1" の値を変更できません。|  
|0xC020837A|-1071611014|DTS_E_OUTPUTCOLUMNHASNOERRORCOLUMN|エラー以外の出力の %1 には、エラー出力上に対応する出力列がありません。|  
|0xC020837B|-1071611013|DTS_E_ERRORCOLUMNHASNOOUTPUTCOLUMN|エラー出力の %1 には、エラー以外の出力上に対応する出力列がありません。|  
|0xC020837C|-1071611012|DTS_E_ERRORCOLUMNHASINCORRECTPROPERTIES|エラー出力の %1 には、対応するデータ ソース列のプロパティと一致しないプロパティがあります。|  
|0xC020837D|-1071611011|DTS_E_ADOSRCOUTPUTCOLUMNDATATYPECANNOTBECHANGED|DT_WSTR 列と DT_NTEXT 列を除き、%1 の出力列のデータ型は変更できません。|  
|0xC020837F|-1071611009|DTS_E_ADOSRCDATATYPEMISMATCH|"%1" のデータ型が変換元の列 "%3" のデータ型 "%2" と一致しません。|  
|0xC0208380|-1071611008|DTS_E_ADOSRCCOLUMNNOTINSCHEMAROWSET|%1 は、一致する変換元の列がスキーマにありません。|  
|0xC0208381|-1071611007|DTS_E_TERMLOOKUP_INVALIDREFERENCETERMTABLEORCOLUMN|参照用語に使用される参照テーブル/ビューまたは列が無効です。|  
|0xC0208382|-1071611006|DTS_E_TERMLOOKUP_REFERENCETERMTABLEANDCOLUMNNOTSET|参照用語に使用される参照テーブル/ビューまたは列が設定されていません。|  
|0xC0208383|-1071611005|DTS_E_COLUMNMAPPEDTOALREADYMAPPEDEXTERNALMETADATACOLUMN|%1 は ID %2!ld! の外部メタデータ列にマップされますが、既に別の列にマップされています。|  
|0xC0208384|-1071611004|DTS_E_TXFUZZYLOOKUP_TOOMANYPREFIXES|プロパティ '%2' に指定されている SQL オブジェクト名 '%1' には、最大数よりも多くのプレフィックスが含まれています。  最大数は 2 です。|  
|0xC0208385|-1071611003|DTS_E_MGDSRCSTATIC_OVERFLOW|値が大きすぎて、列に収まりませんでした。|  
|0xC0208386|-1071611002|DTS_E_DATAREADERDESTREADERISCLOSED|SSIS IDataReader は閉じています。|  
|0xC0208387|-1071611001|DTS_E_DATAREADERDESTREADERISATEND|SSIS IDataReader は結果セットの末尾に到達しました。|  
|0xC0208388|-1071611000|DTS_E_DATAREADERDESTINVALIDCOLUMNORDINAL|列の位置を表す序数が無効です。|  
|0xC0208389|-1071610999|DTS_E_DATAREADERDESTCANNOTCONVERT|%1 をデータ型 "%2" からデータ型 "%3" に変換できません。|  
|0xC020838A|-1071610998|DTS_E_DATAREADERDESTINVALIDCODEPAGE|%1 には、サポートされていないコード ページ %2!d! があります。|  
|0xC020838B|-1071610997|DTS_E_XMLSRCEXTERNALMETADATACOLUMNNOTINSCHEMA|%1 には、XML スキーマへのマッピングがありません。|  
|0xC020838D|-1071610995|DTS_E_TXTERMLOOKUP_MISMATCHED_COLUMN_METADATA|系列 ID %1!d! の列と系列 ID %2!d! の列のメタデータが一致していません。 出力列にマップされた入力列に、同じメタデータ (データ型、有効桁数、小数点以下桁数、長さ、またはコード ページ) がありません。|  
|0xC020838E|-1071610994|DTS_E_DATAREADERDESTREADERTIMEOUT|SSIS IDataReader は閉じています。 読み取りのタイムアウトの期限が切れています。|  
|0xC020838F|-1071610993|DTS_E_ADOSRCINVALIDSQLCOMMAND|指定された SQL コマンドの実行中にエラーが発生しました: "%1"。 %2|  
|0xC0208390|-1071610992|DTS_E_JOINTYPEDOESNTMATCHETI|入力列 '%1' に指定された JoinType プロパティは、一致インデックスが最初に作成されたときに、入力列に対応する参照テーブル列に指定された JoinType プロパティと異なります。  指定された JoinType で一致インデックスを再構築するか、または一致インデックスが作成されたときに使用される型と一致するように JoinType を変更してください。|  
|0xC0208392|-1071610990|DTS_E_SQLCEDESTDATATYPENOTSUPPORTED|列 "%2" のデータ型 "%1" は、%3 に対してはサポートされていません。|  
|0xC0208393|-1071610989|DTS_E_DATAREADERDESTDATATYPENOTSUPPORTED|"%2" のデータ型 "%1" は、%3 に対してはサポートされていません。|  
|0xC0208394|-1071610988|DTS_E_RECORDSETDESTDATATYPENOTSUPPORTED|%1 のデータ型は、%2 に対してはサポートされていません。|  
|0xC0208446|-1071610810|DTS_E_TXSCRIPTMIGRATIONCOULDNOTADDREFERENCE|%2 の移行中にプロジェクト参照 "%1" を追加できませんでした。 移行を手動で完了することが必要になる場合があります。|  
|0xC0208447|-1071610809|DTS_E_TXSCRIPTMIGRATIONMULTIPLEENTRYPOINTSFOUND|%2 の移行中に名前が "%1" のエントリ ポイントが複数見つかりました。 移行を手動で完了することが必要になる場合があります。|  
|0xC0208448|-1071610808|DTS_E_TXSCRIPTMIGRATIONNOENTRYPOINTFOUND|%1 の移行中にエントリ ポイントが見つかりませんでした。 移行を手動で完了することが必要になる場合があります。|  
|0xC020844B|-1071610805|DTS_E_ADODESTINSERTIONFAILURE|データの挿入中に例外が発生しました。プロバイダーから返されたメッセージは次のとおりです: %1|  
|0xC020844C|-1071610804|DTS_E_ADODESTCONNECTIONTYPENOTSUPPORTED|%1 からプロバイダー固定名を取得できませんでした。これは、現在、ADO NET 変換先コンポーネントでサポートされていません|  
|0xC020844D|-1071610803|DTS_E_ADODESTARGUMENTEXCEPTION|データ プロバイダーが変換先にデータを挿入中に引数例外が発生しました。 返されたメッセージは次のとおりです: %1|  
|0xC020844E|-1071610802|DTS_E_ADODESTWRONGBATCHSIZE|BatchSize プロパティには、負でない整数を指定してください|  
|0xC020844F|-1071610801|DTS_E_ADODESTERRORUPDATEROW|変換先のデータ ソースにこの行を送信中にエラーが発生しました。|  
|0xC0208450|-1071610800|DTS_E_ADODESTEXECUTEREADEREXCEPTION|tSQL コマンドを実行すると例外がスローされます。メッセージは次のとおりです: %1|  
|0xC0208451|-1071610799|DTS_E_ADODESTDATATYPENOTSUPPORTED|列 "%2" のデータ型 "%1" は、%3 に対してはサポートされていません。|  
|0xC0208452|-1071610798|DTS_E_ADODESTFAILEDTOACQUIRECONNECTION|ADO NET 変換先では、接続 %1 を取得できませんでした。 接続が壊れている可能性があります。|  
|0xC0208453|-1071610797|DTS_E_ADODESTNOTMANAGEDCONNECTION|指定した接続 %1 が管理されていません。ADO NET 変換先にマネージド接続を使用してください。|  
|0xC0208454|-1071610796|DTS_E_ADODESTNOERROROUTPUT|変換先コンポーネントにはエラー出力がありません。 コンポーネントが壊れている可能性があります。|  
|0xC0208455|-1071610795|DTS_E_ADODESTNOLINEAGEID|外部列 %2 に関連付けられている lineageID %1 は実行時に存在しません。|  
|0xC0208456|-1071610794|DTS_E_ADODESTEXTERNALCOLNOTEXIST|%1 はデータベースに存在しません。 削除または名前が変更された可能性があります。|  
|0xC0208457|-1071610793|DTS_E_ADODESTGETSCHEMATABLEFAILED|外部列のプロパティを取得できませんでした。 入力したテーブル名が存在しない可能性があります。または、テーブル オブジェクトに対して SELECT 権限がないため、接続を使用して列のプロパティの取得を試みましたが失敗しました。 エラー メッセージの詳細は次のとおりです: %1|  
|0xC0208458|-1071610792|DTS_E_ADODESTCOLUMNERRORDISPNOTSUPPORTED|入力列エラーの処理は、ADO NET 変換先コンポーネントでサポートされていません。|  
|0xC0208459|-1071610791|DTS_E_ADODESTCOLUMNTRUNDISPNOTSUPPORTED|入力列切り捨ての処理は、ADO NET 変換先コンポーネントでサポートされていません。|  
|0xC020845A|-1071610790|DTS_E_ADODESTINPUTTRUNDISPNOTSUPPORTED|入力切り捨て行の処理は、ADO NET 変換先コンポーネントでサポートされていません。|  
|0xC020845B|-1071610789|DTS_E_ADODESTTABLENAMEERROR|テーブル名またはビュー名が不適切です。 \n\t テーブル名を引用符で囲んでいる場合は、選択したデータ プロバイダーのプレフィックス %1 とサフィックス %2 を引用符に使用してください。 \n\t マルチパート名を使用している場合は、テーブル名を最大で 3 部構成にしてください。|  
|0xC0209001|-1071607807|DTS_E_FAILEDTOFINDCOLUMNINBUFFER|系列 ID %2!d! の列 "%1" が バッファーに見つかりませんでした。 バッファー マネージャーにより、エラー コード 0x%3!8.8X! が返されました。|  
|0xC0209002|-1071607806|DTS_E_FAILEDTOGETCOLUMNINFOFROMBUFFER|バッファーから列 "%1" (%2!d!) の情報を取得できませんでした。 返されたエラー コードは 0x%3!8.8X! です。|  
|0xC0209011|-1071607791|DTS_E_TXAGG_ARITHMETICOVERFLOW|"%1" の集計中に算術オーバーフローが発生しました。|  
|0xC0209012|-1071607790|DTS_E_FAILEDTOGETCOLINFO|バッファーから行 %1!ld!、列 %2!ld! の情報を 取得できませんでした。 返されたエラー コードは 0x%3!8.8X! です。|  
|0xC0209013|-1071607789|DTS_E_FAILEDTOSETCOLINFO|行 %1!ld!、列 %2!ld! の情報を バッファーに設定できませんでした。 返されたエラー コードは 0x%3!8.8X! です。|  
|0xC0209015|-1071607787|DTS_E_REQUIREDBUFFERISNOTAVAILBLE|必要なバッファーが使用できません。|  
|0xC0209016|-1071607786|DTS_E_FAILEDTOGETBUFFERBOUNDARYINFO|エラー コード 0x%1!8.8X! により、バッファーの境界情報を取得できませんでした。|  
|0xC0209017|-1071607785|DTS_E_FAILEDTOSETBUFFERENDOFROWSET|エラー コード 0x%1!8.8X! により、バッファーの行セットの末尾を設定できませんでした。|  
|0xC0209018|-1071607784|DTS_E_FAILEDTOGETDATAFORERROROUTPUTBUFFER|エラー出力バッファーのデータを取得できませんでした。|  
|0xC0209019|-1071607783|DTS_E_FAILEDTOREMOVEROWFROMBUFFER|エラー コード 0x%1!8.8X! により、バッファーから行を削除できませんでした。|  
|0xC020901B|-1071607781|DTS_E_FAILEDTOSETBUFFERERRORINFO|エラー コード 0x%1!8.8X! により、バッファーのエラー情報を設定できませんでした。|  
|0xC020901C|-1071607780|DTS_E_COLUMNSTATUSERROR|%2 の %1 にエラーがありました。 返された列の状態は "%3" でした。|  
|0xC020901D|-1071607779|DTS_E_TXLOOKUP_METADATAXMLCACHEERR|参照メタデータをキャッシュできません。|  
|0xC020901E|-1071607778|DTS_E_TXLOOKUP_ROWLOOKUPERROR|参照中に一致する行が見つかりませんでした。|  
|0xC020901F|-1071607777|DTS_E_INVALIDERRORDISPOSITION|%1 には無効なエラーまたは切り捨て行の処理があります。|  
|0xC0209022|-1071607774|DTS_E_FAILEDTODIRECTERRORROW|エラー コード 0x%1!8.8X! により、エラー出力への行の出力指定に失敗しました。|  
|0xC0209023|-1071607773|DTS_E_FAILEDTOPREPARECOLUMNSTATUSESFORINSERT|エラー コード 0x%1!8.8X! により、挿入用に列の状態を準備できませんでした。|  
|0xC0209024|-1071607772|DTS_E_FAILEDTOFINDCOLUMNBYLINEAGEID|エラー コード 0x%3!8.8X! により、 データ フロー タスク バッファーで系列 ID %2!d! の %1 を検索できませんでした。|  
|0xC0209025|-1071607771|DTS_E_FAILEDTOFINDNONSPECIALERRORCOLUMN|%1 に特殊なエラー列以外の列が見つかりませんでした。|  
|0xC0209029|-1071607767|DTS_E_INDUCEDTRANSFORMFAILUREONERROR|SSIS エラー コード DTS_E_INDUCEDTRANSFORMFAILUREONERROR。  エラー コード 0x%2!8.8X! により、"%1" が失敗しました。 "%3" のエラー行の処理により、エラーによる失敗が示されます。 ここに示されたコンポーネントのオブジェクトでエラーが発生しました。  このエラーの前に、エラーの詳細が記載されたエラー メッセージが報告されている可能性があります。|  
|0xC020902A|-1071607766|DTS_E_INDUCEDTRANSFORMFAILUREONTRUNCATION|"%1" が切り捨ての発生により失敗しました。"%2" の切り捨て行の処理により、切り捨てによる失敗が示されます。 ここに示されたコンポーネントのオブジェクトで切り捨てエラーが発生しました。|  
|0xC020902B|-1071607765|DTS_E_TXSPLITEXPRESSIONEVALUATEDTONULL|"%2" の式 "%1" は NULL と評価されましたが、"%3" ではブール型の結果が必要です。 出力でのエラー行の処理を変更して、これを無効な結果として処理する (エラーを無視する) か、この行をエラー出力にリダイレクトしてください (行のリダイレクト)。  条件分割式の結果は、ブール型にする必要があります。  式の結果が NULL の場合は、エラーになります。|  
|0xC020902C|-1071607764|DTS_E_TXSPLITSTATIC_EXPRESSIONEVALUATEDTONULL|式は NULL と評価されましたが、ブール型の結果が必要です。 出力でのエラー行の処理を変更して、これを無効な結果として処理する (エラーを無視する) か、この行をエラー出力にリダイレクトしてください (行のリダイレクト)。 条件分割式の結果は、ブール型にする必要があります。  式の結果が NULL の場合は、エラーになります。|  
|0xC020902D|-1071607763|DTS_E_UTF16BIGENDIANFORMATNOTSUPPORTED|UTF-16 Big Endian 形式のファイルはサポートされていません。  UTF-16 Little Endian 形式のみがサポートされています。|  
|0xC020902E|-1071607762|DTS_E_UTF8FORMATNOTSUPPORTEDASUNICODE|UTF-8 のファイル形式は Unicode としてサポートされていません。|  
|0xC020902F|-1071607761|DTS_E_DTPXMLCANTREADIDATTR|ID 属性を読み取れません。|  
|0xC020903E|-1071607746|DTS_E_TXLOOKUP_INDEXCOLUMNREUSED|キャッシュのインデックス列 %1 が複数の参照入力列によって参照されています。|  
|0xC020903F|-1071607745|DTS_E_TXLOOKUP_INDEXCOLUMNSMISMATCH|参照では、キャッシュ接続マネージャーのインデックス列の一部が参照されていません。 参照内で結合された列の数:  %1!d!。 インデックス列の数: %2!d!。|  
|0xC0209069|-1071607703|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|符号の不一致またはデータのオーバーフロー以外の原因により、データ値を変換できません。|  
|0xC020906A|-1071607702|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|データ値がスキーマの制約に違反しました。|  
|0xC020906B|-1071607701|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_TRUNCATED|データが切り捨てられました。|  
|0xC020906C|-1071607700|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SIGNMISMATCH|データ値は符号付きで、プロバイダーで使用された型は符号なしであったため、変換できませんでした。|  
|0xC020906D|-1071607699|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_DATAOVERFLOW|プロバイダーで使用された型ではデータ値がオーバーフローしたので、変換できませんでした。|  
|0xC020906E|-1071607698|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_UNAVAILABLE|状態を示す情報はありません。|  
|0xC020906F|-1071607697|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|ユーザーにこの列への正しい書き込み権限がありませんでした。|  
|0xC0209070|-1071607696|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|データ値が列の整合性制約に違反しました。|  
|0xC0209071|-1071607695|DTS_E_OLEDBSOURCEADAPTERSTATIC_UNAVAILABLE|状態を示す情報はありません。|  
|0xC0209072|-1071607694|DTS_E_OLEDBSOURCEADAPTERSTATIC_CANTCONVERTVALUE|符号の不一致またはデータのオーバーフロー以外の原因により、データ値を変換できません。|  
|0xC0209073|-1071607693|DTS_E_OLEDBSOURCEADAPTERSTATIC_TRUNCATED|データが切り捨てられました。|  
|0xC0209074|-1071607692|DTS_E_OLEDBSOURCEADAPTERSTATIC_SIGNMISMATCH|データ値は符号付きで、プロバイダーで使用された型は符号なしであったため、変換できませんでした。|  
|0xC0209075|-1071607691|DTS_E_OLEDBSOURCEADAPTERSTATIC_DATAOVERFLOW|プロバイダーで使用された型ではデータ値がオーバーフローしたので、変換できませんでした。|  
|0xC0209076|-1071607690|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|データ値がスキーマの制約に違反しました。|  
|0xC0209077|-1071607689|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|符号の不一致またはデータのオーバーフロー以外の原因により、データ値を変換できません。|  
|0xC0209078|-1071607688|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_TRUNCATED|データが切り捨てられました。|  
|0xC0209079|-1071607687|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SIGNMISMATCH|データ値は符号付きで、プロバイダーで使用された型は符号なしであったため、変換できませんでした。|  
|0xC020907A|-1071607686|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_DATAOVERFLOW|プロバイダーで使用された型ではデータ値がオーバーフローしたので、変換できませんでした。|  
|0xC020907B|-1071607685|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_UNAVAILABLE|状態を示す情報はありません。|  
|0xC020907C|-1071607684|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|ユーザーにこの列への正しい書き込み権限がありませんでした。|  
|0xC020907D|-1071607683|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|データ値が整合性制約に違反しています。|  
|0xC020907F|-1071607681|DTS_E_TXDATACONVERTSTATIC_CANTCONVERTVALUE|符号の不一致またはデータのオーバーフロー以外の原因により、データ値を変換できません。|  
|0xC0209080|-1071607680|DTS_E_TXDATACONVERTSTATIC_TRUNCATED|データが切り捨てられました。|  
|0xC0209081|-1071607679|DTS_E_TXDATACONVERTSTATIC_SIGNMISMATCH|データ値は符号付きで、プロバイダーで使用された型は符号なしであったため、変換できませんでした。|  
|0xC0209082|-1071607678|DTS_E_TXDATACONVERTSTATIC_DATAOVERFLOW|データ変換で使用された型ではデータ値がオーバーフローしたので、変換できませんでした。|  
|0xC0209083|-1071607677|DTS_E_FLATFILESOURCEADAPTERSTATIC_UNAVAILABLE|状態を示す情報はありません。|  
|0xC0209084|-1071607676|DTS_E_FLATFILESOURCEADAPTERSTATIC_CANTCONVERTVALUE|符号の不一致またはデータのオーバーフロー以外の原因により、データ値を変換できません。|  
|0xC0209085|-1071607675|DTS_E_FLATFILESOURCEADAPTERSTATIC_TRUNCATED|データが切り捨てられました。|  
|0xC0209086|-1071607674|DTS_E_FLATFILESOURCEADAPTERSTATIC_SIGNMISMATCH|データ値は符号付きで、フラット ファイル ソース アダプターで使用された型は符号なしであったため、変換できませんでした。|  
|0xC0209087|-1071607673|DTS_E_FLATFILESOURCEADAPTERSTATIC_DATAOVERFLOW|フラット ファイル ソース アダプターで使用された型ではデータ値がオーバーフローしたので、変換できませんでした。|  
|0xC020908E|-1071607666|DTS_E_TXDATACONVERTSTATIC_UNAVAILABLE|状態を示す情報はありません。|  
|0xC0209090|-1071607664|DTS_E_FILEOPENERR_FORREAD|エラー コード 0x%2!8.8X! により、読み取り用にファイル "%1" を開けませんでした。|  
|0xC0209091|-1071607663|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD|読み取り用にファイルを開けませんでした。|  
|0xC0209092|-1071607662|DTS_E_FILEOPENERR_FORWRITE|エラー コード 0x%2!8.8X! により、書き込み用にファイル "%1" を開けませんでした。|  
|0xC0209093|-1071607661|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE|書き込み用にファイルを開けませんでした。|  
|0xC0209094|-1071607660|DTS_E_TXFILEINSERTERSTATIC_INSERTERCANTREAD|ファイルから読み取れませんでした。|  
|0xC0209095|-1071607659|DTS_E_TXFILEEXTRACTORSTATIC_EXTRACTORCANTWRITE|ファイルに書き込めませんでした。|  
|0xC0209099|-1071607655|DTS_E_DTPXMLINVALIDPROPERTYARRAYTOOMANYVALUES|配列型のプロパティを解析中に見つかった配列要素が多すぎます。 elementCount は見つかった配列要素の数より小さくなっています。|  
|0xC020909A|-1071607654|DTS_E_DTPXMLINVALIDPROPERTYARRAYNOTENOUGHVALUES|配列型のプロパティを解析中に見つかった配列要素が少なすぎます。 elementCount は見つかった配列要素の数より大きくなっています。|  
|0xC020909E|-1071607650|DTS_E_FILEOPENERR_FORWRITE_FILENOTFOUND|書き込み用にファイル "%1" を開けませんでした。 ファイルが見つかりません。|  
|0xC020909F|-1071607649|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILENOTFOUND|書き込み用にファイルを開けませんでした。 ファイルが見つかりません。|  
|0xC02090A0|-1071607648|DTS_E_FILEOPENERR_FORWRITE_PATHNOTFOUND|書き込み用にファイル "%1" を開けませんでした。 パスが見つかりません。|  
|0xC02090A1|-1071607647|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_PATHNOTFOUND|書き込み用にファイルを開けませんでした。 パスが見つかりません。|  
|0xC02090A2|-1071607646|DTS_E_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|書き込み用にファイル "%1" を開けませんでした。 開いているファイルが多すぎます。|  
|0xC02090A3|-1071607645|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|書き込み用にファイルを開けませんでした。 開いているファイルが多すぎます。|  
|0xC02090A4|-1071607644|DTS_E_FILEOPENERR_FORWRITE_ACCESSDENIED|書き込み用にファイル "%1" を開けませんでした。 正しい権限がありません。|  
|0xC02090A5|-1071607643|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_ACCESSDENIED|書き込み用にファイルを開けませんでした。 正しい権限がありません。|  
|0xC02090A6|-1071607642|DTS_E_FILEOPENERR_FORWRITE_FILEEXISTS|書き込み用にファイル "%1" を開けませんでした。 ファイルが存在していて、上書きできません。 AllowAppend プロパティが False で、ForceTruncate プロパティも False に設定されている場合、ファイルが存在することが原因で、このエラーが発生します。|  
|0xC02090A7|-1071607641|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILEEXISTS|書き込み用にファイルを開けませんでした。 ファイルが既に存在していて、上書きできません。 AllowAppend プロパティおよび ForceTruncate プロパティが両方とも False に設定されている場合、ファイルが存在することが原因で、このエラーが発生します。|  
|0xC02090A8|-1071607640|DTS_E_INCORRECTCUSTOMPROPERTYVALUEFOROBJECT|%2 のカスタム プロパティ "%1" の値が正しくありません。|  
|0xC02090A9|-1071607639|DTS_E_COLUMNSHAVEINCOMPATIBLEMETADATA|列 "%1" と列 "%2" のメタデータには互換性がありません。|  
|0xC02090AD|-1071607635|DTS_E_FILEWRITEERR_DISKFULL|ディスクがいっぱいなので、書き込み用にファイル "%1" を開けませんでした。 このファイルを保存するには、ディスク領域が不足しています。|  
|0xC02090AE|-1071607634|DTS_E_TXFILEEXTRACTORSTATIC_FILEWRITEERR_DISKFULL|ディスクがいっぱいなので、書き込み用にファイルを開けませんでした。|  
|0xC02090B9|-1071607623|DTS_E_TXAGG_SORTKEYGENFAILED|エラー 0x%1!8.8X! により、並べ替えキーを生成できませんでした。 ComparisonFlags が有効になっているので、LCMapString を使用して並べ替えキーを生成できませんでした。|  
|0xC02090BA|-1071607622|DTS_E_TXCHARMAPLCMAPFAILED|文字列をマップする変換が失敗し、エラー 0x%1!8.8X! が返されました。 LCMapString が失敗しました。|  
|0xC02090BB|-1071607621|DTS_E_FILEOPENERR_FORREAD_FILENOTFOUND|読み取り用にファイル "%1" を開けませんでした。 ファイルが見つかりませんでした。|  
|0xC02090BC|-1071607620|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_FILENOTFOUND|読み取り用にファイルを開けませんでした。 ファイルが見つかりませんでした。|  
|0xC02090BD|-1071607619|DTS_E_FILEOPENERR_FORREAD_PATHNOTFOUND|読み取り用にファイル "%1" を開けませんでした。 パスが見つかりません。|  
|0xC02090BE|-1071607618|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_PATHNOTFOUND|読み取り用にファイルを開けませんでした。 パスが見つかりませんでした。|  
|0xC02090BF|-1071607617|DTS_E_FILEOPENERR_FORREAD_TOOMANYOPENFILES|読み取り用にファイル "%1" を開けませんでした。 開いているファイルが多すぎます。|  
|0xC02090C0|-1071607616|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_TOOMANYOPENFILES|読み取り用にファイルを開けませんでした。 開いているファイルが多すぎます。|  
|0xC02090C1|-1071607615|DTS_E_FILEOPENERR_FORREAD_ACCESSDENIED|読み取り用にファイル "%1" を開けませんでした。 アクセスが拒否されました。|  
|0xC02090C2|-1071607614|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_ACCESSDENIED|読み取り用にファイルを開けませんでした。 正しい権限がありません。|  
|0xC02090C3|-1071607613|DTS_E_INSERTERINVALIDBOM|ファイル "%1" のバイト順マーク (BOM) 値は 0x%2!4.4X! ですが、予期された値は 0x%3!4.4X! です。 このファイルに対して ExpectBOM プロパティが設定されていましたが、ファイルに BOM 値がないか、無効です。|  
|0xC02090C4|-1071607612|DTS_E_TXFILEINSERTERSTATIC_INSERTERINVALIDBOM|ファイルのバイト順マーク (BOM) 値が無効です。 このファイルに対して ExpectBOM プロパティが設定されていましたが、ファイルに BOM 値がないか、無効です。|  
|0xC02090C5|-1071607611|DTS_E_NOCOMPONENTATTACHED|%1 はコンポーネントにアタッチされていません。  コンポーネントをアタッチする必要があります。|  
|0xC02090C9|-1071607607|DTS_E_TXLOOKUP_INVALIDMAXMEMORYPROP|カスタム プロパティ %1 の値が正しくありません。  値には、%2!d! から %3!I64d! までの数値を指定する 必要があります。|  
|0xC02090CA|-1071607606|DTS_E_TXAGG_COMPFLAGS_BADAGGREGATIONTYPE|カスタム プロパティ "%1" を、この列で選択されている集計の種類に指定することはできません。 比較フラグのカスタム プロパティを指定できるのは、集計の種類がグループ化または個別のカウントに設定されている列だけです。|  
|0xC02090CB|-1071607605|DTS_E_TXAGG_COMPFLAGS_BADDATATYPE|比較フラグのカスタム プロパティ "%1" は、データ型が DT_STR または DT_WSTR の列にのみ指定できます。|  
|0xC02090CD|-1071607603|DTS_E_TXAGG_AGGREGATION_FAILURE|エラー コード 0x%2!8.8X! により、%1 を集計できませんでした。|  
|0xC02090CF|-1071607601|DTS_E_MAPPINGSETUPERROR|マッピングを設定中にエラーが発生しました。 %1|  
|0xC02090D0|-1071607600|DTS_E_XMLSRCUNABLETOREADXMLDATA|%1 は XML データを読み取れませんでした。|  
|0xC02090D1|-1071607599|DTS_E_XMLSRCUNABLETOGETXMLDATAVARIABLE|%1 は "%2" プロパティで指定された変数を取得できませんでした。|  
|0xC02090D2|-1071607598|DTS_E_NODATATABLEMATCHROWID|%1 に含まれている値 %2 の RowsetID がスキーマのデータ テーブルを参照していません。|  
|0xC02090D6|-1071607594|DTS_E_TXAGG_BADKEYSVALUE|プロパティ %1 は空にするか、または %2!u! から %3!u! までの数値を指定する 必要があります。 Keys プロパティまたは CountDistinctKeys プロパティに無効な値が指定されています。 このプロパティには、0 から ULONG_MAX までの数値を指定するか、プロパティ自体を設定しないでください。|  
|0xC02090D7|-1071607593|DTS_E_TXAGG_TOOMANYKEYS|集計コンポーネントにより、個別のキーの組み合わせが多数検出されました。 格納できる個別の値は %1!u! 個 以下です。 メイン ワークスペースに ULONG_MAX を超える個別のキー値があります。|  
|0xC02090D8|-1071607592|DTS_E_TXAGG_TOOMANYCOUNTDISTINCTVALUES|集計コンポーネントにより、個別のカウントの集計を計算中に、個別の値を多数検出しました。 格納できる個別の値は %1!u! 個 未満です。 個別のカウントの集計を計算中に、ULONG_MAX を超える個別の値が検出されました。|  
|0xC02090D9|-1071607591|DTS_E_FAILEDTOWRITETOTHEFILENAMECOLUMN|エラー コード 0x%1!8.8X! により、ファイル名列に書き込めませんでした。|  
|0xC02090DC|-1071607588|DTS_E_FAILEDTOFINDERRORCOLUMN|エラーが発生しましたが、エラー原因の列を特定できません。|  
|0xC02090E3|-1071607581|DTS_E_TXLOOKUP_FAILEDUPGRADE_BAD_VERSION|参照メタデータのバージョンを %1!d! から %2!d! に アップグレードできません。 参照変換は、PerformUpgrade() への呼び出しで、メタデータを既存のバージョン番号からアップグレードできませんでした。|  
|0xC02090E5|-1071607579|DTS_E_TERMEXTRACTIONORLOOKUP_NTEXTSPLITED|文の終了部分が見つかりませんでした。|  
|0xC02090E6|-1071607578|DTS_E_TERMEXTRACTION_EXCEED_MAXWORDNUM|入力テキストに長すぎる文があるので、用語抽出変換で入力テキストを処理できません。 対象の文は、複数の文に分割されます。|  
|0xC02090E7|-1071607577|DTS_E_XMLSRCFAILEDTOCREATEREADER|%1 は XML データを読み取れませんでした。 %2|  
|0xC02090F0|-1071607568|DTS_E_TXLOOKUP_REINITMETADATAFAILED|参照変換メソッド ReinitializeMetadata への呼び出しに失敗しました。|  
|0xC02090F1|-1071607567|DTS_E_TXLOOKUP_NOJOINS|参照変換では、参照列に結合された少なくとも 1 つの入力列が必要ですが、指定されていませんでした。 少なくとも 1 つの結合列を指定する必要があります。|  
|0xC02090F2|-1071607566|DTS_E_MANAGEDERR_BADFORMATSPECIFICATION|マネージド エラー インフラストラクチャによって通知されているメッセージ文字列に、正しくない書式が含まれています。 これは内部エラーです。|  
|0xC02090F3|-1071607565|DTS_E_MANAGEDERR_UNSUPPORTEDTYPE|マネージド エラー インフラストラクチャを使用してメッセージ文字列の書式を設定中に、サポートされていない書式であるバリアント型が見つかりました。 これは内部エラーです。|  
|0xC02090F5|-1071607563|DTS_E_DATAREADERSRCUNABLETOPROCESSDATA|%1 はデータを処理できませんでした。 %2|  
|0xC02090F6|-1071607562|DTS_E_XMLSRCEMPTYPROPERTY|%2 のプロパティ "%1" が空でした。|  
|0xC02090F7|-1071607561|DTS_E_XMLSRCINVALIDOUTPUTNAME|パス "%2" の XML テーブルに名前 "%1" の出力を作成しようとしましたが、この名前は無効なので作成できませんでした。|  
|0xC02090F8|-1071607560|DTS_E_MGDSRC_OVERFLOW|値が大きすぎて、%1 に収まりませんでした。|  
|0xC02090F9|-1071607559|DTS_E_DATAREADERDESTUNABLETOPROCESSDATA|%1 はデータを処理できませんでした。|  
|0xC02090FA|-1071607558|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONTRUNCATION|"%1" が切り捨ての発生により失敗しました。"%3" の "%2" の切り捨て行の処理により、切り捨てによる失敗が示されます。 ここに示されたコンポーネントのオブジェクトで切り捨てエラーが発生しました。|  
|0xC02090FB|-1071607557|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONERROR|エラー コード 0x%2!8.8X! により、"%1" が失敗しました。 "%4" の "%3" のエラー行の処理により、エラーによる失敗が示されます。 ここに示されたコンポーネントのオブジェクトでエラーが発生しました。|  
|0xC0209291|-1071607151|DTS_E_SQLCEDESTSTATIC_FAILEDTOSETVALUES|対象になる SQLCE で行に列の値を設定できませんでした。|  
|0xC0209292|-1071607150|DTS_E_SQLCEDESTSTATIC_FAILEDTOINSERT|対象になる SQLCE で行を挿入できませんでした。|  
|0xC0209293|-1071607149|DTS_E_TXFUZZYLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|列のメタデータを読み込み中に OLEDB エラーが発生しました。|  
|0xC0209294|-1071607148|DTS_E_TXFUZZYLOOKUP_TOOFEWREFERENCECOLUMNS|参照の参照メタデータに含まれている列が少なすぎます。|  
|0xC0209295|-1071607147|DTS_E_TXSCD_OLEDBERR_LOADCOLUMNMETADATA|列のメタデータを読み込み中に OLEDB エラーが発生しました。|  
|0xC0209296|-1071607146|DTS_E_TXSCD_TOOFEWREFERENCECOLUMNS|参照の参照メタデータに含まれている列が少なすぎます。|  
|0xC0209297|-1071607145|DTS_E_TXSCD_MALLOCERR_REFERENCECOLUMNINFO|メモリを割り当てられません。|  
|0xC0209298|-1071607144|DTS_E_TXSCD_MALLOCERR_BUFFCOL|メモリを割り当てられません。|  
|0xC0209299|-1071607143|DTS_E_TXSCD_MAINWORKSPACE_CREATEERR|ワークスペース バッファーを作成できません。|  
|0xC020929A|-1071607142|DTS_E_DTPXMLDOMCREATEERROR|XML DOM ドキュメントのインスタンスを作成できません。MSXML バイナリが正しくインストールおよび登録されていることを確認してください。|  
|0xC020929B|-1071607141|DTS_E_DTPXMLDOMLOADERROR|処理用にローカル DOM に XML データを読み込めません。|  
|0xC020929C|-1071607140|DTS_E_RSTDESTBADVARIABLETYPE|ランタイム変数 "%1" の型が正しくありません。 ランタイム変数の型は、Object である必要があります。|  
|0xC020929E|-1071607138|DTS_E_XMLDATAREADERMULTIPLEINLINEXMLSCHEMASNOTSUPPORTED|XML ソース アダプターは XML データを処理できませんでした。 インライン スキーマは複数使用できません。|  
|0xC020929F|-1071607137|DTS_E_XMLDATAREADERANYTYPENOTSUPPORTED|XML ソース アダプターは XML データを処理できませんでした。 要素のコンテンツは anyType として宣言できません。|  
|0xC02092A0|-1071607136|DTS_E_XMLDATAREADERGROUPREFNOTSUPPORTED|XML ソース アダプターは XML データを処理できませんでした。 要素内に、グループへの参照 (ref) を含めることはできません。|  
|0xC02092A1|-1071607135|DTS_E_XMLDATAREADERMIXEDCONTENTFORCOMPLEXTYPESNOTSUPPORTED|XML ソース アダプターは複合型の混合コンテンツ モデルをサポートしていません。|  
|0xC02092A2|-1071607134|DTS_E_XMLDATAREADERINLINESCHEMAFOUNDINSOURCEXML|XML ソース アダプターは XML データを処理できませんでした。 インライン スキーマはソース XML の最初の子ノードである必要があります。|  
|0xC02092A3|-1071607133|DTS_E_XMLDATAREADERNOINLINESCHEMAFOUND|XML ソース アダプターは XML データを処理できませんでした。 ソース XML にインライン スキーマはありませんが、"UseInlineSchema" プロパティが True に設定されています。|  
|0xC02092A4|-1071607132|DTS_E_CONNECTIONMANAGERTRANSACTEDANDRETAINEDINBULKINSERT|このコンポーネントでは、FastLoad または一括挿入を伴うトランザクション中に接続を保持する接続マネージャーを使用できません。|  
|0xC02092A5|-1071607131|DTS_E_OUTPUTREDIRECTINTRANSACTIONNOTALLOWED|%1 は、トランザクション内で接続を使用してエラーにリダイレクトするように設定できません。|  
|0xC02092A6|-1071607130|DTS_E_FOUNDORPHANEDEXTERNALMETADATACOLUMN|%1 には対応する入力列または出力列がありません。|  
|0xC02092A9|-1071607127|DTS_E_RAWDESTNOINPUTCOLUMNS|ファイルに書き込まれる列が選択されていません。|  
|0xC02092AA|-1071607126|DTS_E_RAWDESTBLOBDATATYPE|%1 のデータ型が無効です。 データ型が DT_IMAGE、DT_TEXT、および DT_NTEXT の列は、RAW ファイルに書き込めません。|  
|0xC02092AB|-1071607125|DTS_E_RAWDESTWRONGEXTERNALMETADATAUSAGE|このコンポーネントでは、外部メタデータ コレクションが正しく使用されていません。 既存のファイルを追加または切り捨てている場合、コンポーネントでは外部メタデータを使用する必要があります。 それ以外の場合、外部メタデータは必要ありません。|  
|0xC02092AC|-1071607124|DTS_E_RAWDESTMAPPEDINPUTCOLUMN|%1 は ID %2!d! の外部メタデータ列にマップされています。 書き込みオプションの値が [常に作成する] に設定されている場合、入力列を外部メタデータ列にマップする必要はありません。|  
|0xC02092AD|-1071607123|DTS_E_RAWFILECANTOPENFORMETADATA|メタデータを読み取るファイルを開けません。 ファイルが存在しない場合、およびコンポーネントで既に外部メタデータが定義されている場合、"ValidateExternalMetadata" プロパティを "false" に設定できます。ファイルは、実行時に作成されます。|  
|0xC02092AE|-1071607122|DTS_E_FAILEDTOACCESSLOBCOLUMN|エラー コード 0x%2!8.8X! により、データ ソース列 "%1" のデータ フロー バッファーから LOB データにアクセスできませんでした。|  
|0xC02092AF|-1071607121|DTS_E_XMLSRCUNABLETOPROCESSXMLDATA|%1 は XML データを処理できませんでした。 %2|  
|0xC02092B0|-1071607120|DTS_E_XMLSRCSTATIC_UNABLETOPROCESSXMLDATA|XML ソース アダプターは XML データを処理できませんでした。|  
|0xC02092B1|-1071607119|DTS_E_RAWINVALIDACCESSMODE|値 %1!d! は 有効なアクセス モードとして認識されません。|  
|0xC02092B2|-1071607118|DTS_E_INCOMPLETEDATASOURCECOLUMNFOUND|データ ソース列 "%1" の完全なメタデータ情報が使用できません。  列がデータ ソースで正しく定義されていることを確認してください。|  
|0xC02092B3|-1071607117|DTS_E_TXAUDIT_ONLYSTRINGLENGTHCHANGEALLOWED|[ユーザー名] 列、[パッケージ名] 列、[タスク名] 列、および [コンピューター名] 列の長さだけを変更できます。  他の監査列データ型情報は読み取り専用です。|  
|0xC02092B4|-1071607116|DTS_E_ROWSETUNAVAILABLE|この SQL コマンドに基づく行セットが、OLE DB プロバイダーによって返されませんでした。|  
|0xC02092B5|-1071607115|DTS_E_COMMITFAILED|コミットに失敗しました。|  
|0xC02092B6|-1071607114|DTS_E_USEBINARYFORMATREQUIRESANSIFILE|カスタム プロパティ "%1" (%2 上) は ANSI ファイルでのみ使用できます。|  
|0xC02092B7|-1071607113|DTS_E_USEBINARYFORMATREQUIRESBYTES|カスタム プロパティ "%1" (%2 上) は DT_BYTES でのみ使用できます。|  
|0xC0209302|-1071607038|DTS_E_OLEDB_NOPROVIDER_ERROR|SSIS エラー コード DTS_E_OLEDB_NOPROVIDER_ERROR。  要求された OLE DB プロバイダー %2 は登録されていません。 エラー コード:0x%1!8.8X!。|  
|0xC0209303|-1071607037|DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR|SSIS エラー コード DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR。  要求された OLE DB プロバイダー %2 は登録されていません。使用できる 64 ビット プロバイダーが存在しない可能性があります。  エラー コード:0x%1!8.8X!。|  
|0xC0209306|-1071607034|DTS_E_MULTICACHECOLMAPPINGS|キャッシュ列 "%1" が複数の列にマップされています。 重複する列マッピングを削除してください。|  
|0xC0209307|-1071607033|DTS_E_COLNOTMAPPEDTOCACHECOL|%1 は有効なキャッシュ列にマップされていません。|  
|0xC0209308|-1071607032|DTS_E_CACHECOLDATATYPEINCOMPAT|入力列 "%1" とキャッシュ列 "%2" は、データ型が一致しないため、マップすることができません。|  
|0xC0209309|-1071607031|DTS_E_INCORRECTINPUTCACHECOLCOUNT|入力列の数がキャッシュ列の数と一致しません。|  
|0xC020930A|-1071607030|DTS_E_INVALIDCACHEFILENAME|キャッシュ ファイル名が指定されていないか、無効です。 有効なキャッシュ ファイル名を指定してください。|  
|0xC020930B|-1071607029|DTS_E_CACHECOLINDEXPOSMISMATCH|列 "%1" のインデックス位置がキャッシュ接続マネージャーの列 "%2" のインデックス位置と異なります。|  
|0xC020930C|-1071607028|DTS_E_FAILEDTOLOADCACHE|ファイル "%1" からキャッシュを読み込むことができませんでした。|  
|0xC020930D|-1071607027|DTS_E_TXLOOKUP_REFCOLUMNISNOTINDEX|参照入力列 %1 はインデックス以外のキャッシュ列 %2 を参照します。|  
|0xC020930E|-1071607026|DTS_E_FAILEDTOGETCONNECTIONSTRING|接続文字列を取得できませんでした。|  
|0xC020930F|-1071607025|DTS_E_CACHECOLDATATYPEPROPINCOMPAT|入力列 "%1" とキャッシュ列 "%2" をマップできません。1 つ以上のデータ型のプロパティが一致していません。|  
|0xC0209311|-1071607023|DTS_E_CACHECOLUMNOTFOUND|キャッシュ列 "%1" がキャッシュに見つかりませんでした。|  
|0xC0209312|-1071607022|DTS_E_CACHECOLUMNMAPPINGFAILED|%1 をキャッシュ列にマップできませんでした。 hresult は 0x%2!8.8X! です。|  
|0xC0209313|-1071607021|DTS_E_CACHELOADEDFROMFILE|キャッシュは %2 によってファイルから読み込まれているため、%1 が書き込むことはできません。|  
|0xC0209314|-1071607020|DTS_E_CACHERELOADEDDIFFERENTFILES|キャッシュは既にファイル "%3" から読み込まれているため、%1 がファイル "%2" から読み込むことはできません。|  
|0xC0209316|-1071607018|DTS_E_OUTPUTNOTUSED|集計コンポーネントの出力 (ID %1!d!) が どのコンポーネントでも使用されていません。 この出力を削除するか、いずれかのコンポーネントの入力に関連付けてください。|  
|0xC0209317|-1071607017|DTS_E_CACHEFILEWRITEFAILED|%1 がファイル "%2" にキャッシュを書き込めませんでした。 hresult は 0x%3!8.8X! です。|  
|0xC0209318|-1071607016|DTS_E_XMLDATATYPECHANGED|要素 "%2" で、"%1" の XML スキーマ データ型情報が変更されています。  このコンポーネントのメタデータを再度初期化して、列マッピングを確認してください。|  
|0xC0209319|-1071607015|DTS_E_TXLOOKUP_UNUSEDINPUTCOLUMN|%1 は、結合またはコピーで使用されていません。 入力列の一覧から未使用の列を削除してください。|  
|0xC020931A|-1071607014|DTS_E_SORTSTACKOVERFLOW|入力バッファーの並べ替え中に、スタック オーバーフローによって並べ替えが失敗しました。  データ フロー タスクの DefaultBufferMaxRows プロパティを小さくしてください。|  
|0xC020F42A|-1071582166|DTS_E_OLEDB_OLDPROVIDER_ERROR|接続文字列の PROVIDER を %1 に変更することを検討するか、 https://www.microsoft.com/downloads にアクセスして %2 のサポートを探しインストールしてください。|  
|||DTS_E_INITTASKOBJECTFAILED|タスク オブジェクトを初期化できませんでした。タスク "%1!s!"、型 "%2!s!"。 エラー: 0x%3!8.8X! " %4!s!"。|  
|||DTS_E_GETRTINTERFACEFAILED|COM コンポーネント カテゴリ マネージャーを作成できませんでした。エラー: 0x%1!8.8X! "%2!s!"。|  
|||DTS_E_COMPONENTINITFAILED|エラー 0x%2!8.8X! " %3!s!" によって コンポーネント %1!s! の初期化に失敗しました 。|  
  
##  <a name="msgWarning"></a> 警告メッセージ  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の警告メッセージのシンボル名は、 **DTS_W_** で始まります。  
  
|16 進コード|10 進コード|シンボル名|[説明]|  
|----------------------|------------------|-------------------|-----------------|  
|0x80000036|-2147483594|DTS_W_COUNTDOWN|評価期間は あと %1!lu! 日間残っています。 評価期間が終了すると、パッケージを実行できなくなります。|  
|0x80010015|-2147418091|DTS_W_GENERICWARNING|警告が発生しました。 この警告の前に、より具体的な警告が発生しており、その警告で詳細が説明されています。|  
|0x80012010|-2147409904|DTS_W_FAILEDXMLDOCCREATION|XML ドキュメント オブジェクト インスタンスを作成できません。 MSXML がインストールされていて、正しく登録されていることを確認してください。|  
|0x80012011|-2147409903|DTS_W_FAILEDCONFIGLOAD|XML 構成ファイルを読み込めません。 XML 構成ファイルの形式が正しくないか、無効である可能性があります。|  
|0x80012012|-2147409902|DTS_W_CONFIGFILENAMEINVALID|構成ファイルの名前 "%1" が無効です。 構成ファイルの名前を確認してください。|  
|0x80012013|-2147409901|DTS_W_CONFIGFILEINVALID|構成ファイルは読み込まれましたが、無効です。 ファイルの形式が正しくありません。要素がないか、破損しています。|  
|0x80012014|-2147409900|DTS_W_CONFIGFILENOTFOUND|構成ファイル "%1" が見つかりません。 ディレクトリとファイル名を確認してください。|  
|0x80012015|-2147409899|DTS_W_CONFIGKEYNOTFOUND|構成レジストリ キー "%1" が見つかりませんでした。 構成エントリで使用できないレジストリ キーが指定されました。 レジストリにキーが存在することを確認してください。|  
|0x80012016|-2147409898|DTS_W_CONFIGTYPEINVALID|構成エントリに、無効な構成の種類が含まれていました。 有効な種類は DTSConfigurationType 列挙の一覧に記載されています。|  
|0x80012017|-2147409897|DTS_W_CANNOTFINDOBJECT|パッケージ パスで参照されたオブジェクト "%1" が見つかりません。 このエラーは、見つからないオブジェクトのパッケージ パスを解決しようとした場合に発生します。|  
|0x80012018|-2147409896|DTS_W_CONFIGFORMATINVALID_PACKAGEDELIMITER|構成エントリ "%1" は、パッケージ区切り記号で開始されていないため、形式が正しくありません。 パッケージ パスの先頭に "\package" を追加してください。|  
|0x80012019|-2147409895|DTS_W_CONFIGFORMATINVALID|構成エントリ "%1" の形式が正しくありませんでした。 このエラーは、区切り記号がないか、配列の区切り記号が無効であるなどの形式エラーが原因で発生する可能性があります。|  
|0x8001201A|-2147409894|DTS_W_NOPARENTVARIABLES|親変数のコレクションがなかったので、親変数 "%1" からの構成が行われませんでした。|  
|0x8001201B|-2147409893|DTS_W_CONFIGFILEFAILEDIMPORT|次の構成ファイルをインポート中にエラーが発生しました: "%1"。|  
|0x8001201C|-2147409892|DTS_W_PARENTVARIABLENOTFOUND|親変数がなかったので、親変数 "%1" からの構成が行われませんでした。 エラー コード:0x%2!8.8X!。|  
|0x8001201D|-2147409891|DTS_W_CONFIGFILEEMPTY|構成ファイルは空であり、構成エントリが含まれていませんでした。|  
|0x80012023|-2147409885|DTS_W_INVALIDCONFIGURATIONTYPE|構成 "%1" の構成の種類が無効です。 このエラーは、構成オブジェクトの種類プロパティを無効な構成の種類に設定しようとしたときに発生することがあります。|  
|0x80012025|-2147409883|DTS_W_REGISTRYCONFIGURATIONTYPENOTFOUND|レジストリ構成の構成の種類が、キー "%1" に見つかりませんでした。 レジストリ キーに ConfigType という値を追加し、"Variable"、"Property"、"ConnectionManager"、"LoggingProvider"、"ForEachEnumerator" のいずれかの文字列値を設定してください。|  
|0x80012026|-2147409882|DTS_W_REGISTRYCONFIGURATIONVALUENOTFOUND|レジストリ構成の構成値が、キー "%1" に見つかりませんでした。 種類が DWORD または文字列のレジストリ キーに Value という値を追加してください。|  
|0x80012028|-2147409880|DTS_W_PROCESSCONFIGURATIONFAILEDSET|プロセス構成は、パッケージ パス "%1" で対象を設定できませんでした。 このエラーは、対象になるプロパティまたは変数の設定に失敗したときに発生します。 対象になるプロパティまたは変数を確認してください。|  
|0x80012032|-2147409870|DTS_W_CONFIGUREDVALUESECTIONEMPTY|.ini ファイルから値を取得できませんでした。 ConfiguredValue セクションが空であるか、または存在しません: "%1"。|  
|0x80012033|-2147409869|DTS_W_CONFIGUREDTYPESECTIONEMPTY|.ini ファイルから値を取得できませんでした。 ConfiguredType セクションが空であるか、または存在しません: "%1"。|  
|0x80012034|-2147409868|DTS_W_PACKAGEPATHSECTIONEMPTY|.ini ファイルから値を取得できませんでした。 PackagePath セクションが空であるか、または存在しません: "%1"。|  
|0x80012035|-2147409867|DTS_W_CONFIGUREDVALUETYPE|.ini ファイルから値を取得できませんでした。 ConfiguredValueType セクションが空であるか、または存在しません: "%1"。|  
|0x80012051|-2147409839|DTS_W_SQLSERVERFAILEDIMPORT|構成が SQL Server から正常にインポートされませんでした: "%1"。|  
|0x80012052|-2147409838|DTS_W_INICONFIGURATIONPROBLEM|.ini 構成ファイルは、空白フィールドまたは見つからないフィールドがあるので無効です。|  
|0x80012054|-2147409836|DTS_W_NORECORDSFOUNDINTABLE|テーブル "%1" には構成用のレコードがありません。 このエラーは、構成用のレコードが存在しない SQL Server テーブルから構成を行った場合に発生します。|  
|0x80012055|-2147409835|DTS_W_DUPLICATECUSTOMEVENT|異なるカスタム イベントに同じ名前を使用しているエラーが発生しました。 カスタム イベント "%1" は、このコンテナーの異なる子によって別々に定義されました。 イベント ハンドラーの実行時にエラーが発生する可能性があります。|  
|0x80012057|-2147409833|DTS_W_CONFIGREADONLYVARIABLE|構成により、読み取り専用の変数を変更しようとしました。 変数はパッケージ パス "%1" にあります。|  
|0x80012058|-2147409832|DTS_W_CONFIGPROCESSCONFIGURATIONFAILED|パッケージの ProcessConfiguration を呼び出すことができませんでした。 構成により、パッケージ パス "%1" のプロパティを変更しようとしました。|  
|0x80012059|-2147409831|DTS_W_ONEORMORECONFIGLOADFAILED|パッケージの少なくとも 1 つの構成エントリを読み込めませんでした。 "%1" の構成エントリとそれ以前に発生した警告を確認して、読み込めなかった構成に関する説明を参照してください。|  
|0x8001205A|-2147409830|DTS_W_CONFIGNODEINVALID|構成ファイルの構成エントリ "%1" が無効であるか、変数を構成できませんでした。  エラー メッセージには問題のあるエントリ名が示されます。 ただし、名前がわからない場合もあります。|  
|0x80014058|-2147401640|DTS_W_FAILURENOTRESTARTABLE|このタスクまたはコンテナーが失敗しましたが、FailPackageOnFailure プロパティが False なのでパッケージの処理は続行されます。 この警告は、パッケージの SaveCheckpoints プロパティが True で、タスクまたはコンテナーが失敗した場合に通知されます。|  
|0x80017101|-2147389183|DTS_W_EMPTYPATH|パスが空です。|  
|0x80019002|-2147381246|DTS_W_MAXIMUMERRORCOUNTREACHED|SSIS 警告コード DTS_W_MAXIMUMERRORCOUNTREACHED。  Execution メソッドは成功しましたが、発生したエラーの数 (%1!d!) が最大許容値 (%2!d!) に達したため、処理が失敗しました。 これは、エラーの数が MaximumErrorCount で指定された数値に達した場合に発生します。 MaximumErrorCount を変更するか、エラーを解決してください。|  
|0x80019003|-2147381245|DTS_W_CONFIGENVVARNOTFOUND|構成の環境変数が見つかりませんでした。  環境変数: "%1"。 このエラーは、パッケージにより構成を設定するための環境変数が指定されていても、この変数を検出できなかった場合に発生します。 パッケージの構成コレクションを調べて、指定された環境変数が使用可能で有効であることを確認してください。|  
|0x80019316|-2147380458|DTS_W_CONNECTIONPROVIDERCHANGE|接続マネージャー "%1" のプロバイダー名が "%2" から "%3" に変更されました。|  
|0x80019317|-2147380457|DTS_W_READEXTMAPFAILED|アップグレード マッピング ファイルの読み取り中に例外が発生しました。 例外: "%1"。|  
|0x80019318|-2147380456|DTS_W_DUPLICATEMAPPINGKEY|ファイル "%1" に重複するマッピングがあります。 タグ: "%2"、キー: "%3"。|  
|0x80019319|-2147380455|DTS_W_IMPLICITUPGRADEMAPPING|拡張機能 "%1" は "%2" へ暗黙的にアップグレードされました。 この拡張機能のマッピングを UpgradeMappings ディレクトリに追加してください。|  
|0x8001931A|-2147380454|DTS_W_INVALIDEXTENSIONMAPPING|ファイル "%1" のマッピングは無効です。 値を NULL または空にすることはできません。 タグ: "%2"、キー: "%3"、値: "%4"。|  
|0x8001931C|-2147380452|DTS_W_ADOCONNECTIONDATATYPECOMPATCHANGE|ADO 型の接続マネージャー "%1" の DataTypeCompatibility プロパティは、旧バージョンとの互換性のために 80 に設定されました。|  
|0x8001C004|-2147368956|DTS_W_FILEENUMEMPTY|For Each File 列挙子が空です。 For Each File 列挙子が、ファイルのパターンに一致するファイルを見つけられなかったか、または指定されたディレクトリが空でした。|  
|0x8001F02F|-2147356625|DTS_W_COULDNOTRESOLVEPACKAGEPATH|パッケージ "%1" のオブジェクトへのパッケージ パスを解決できません。 パッケージ パスが有効であることを確認してください。|  
|0x8001F203|-2147356157|DTS_W_ITERATIONEXPRESSIONISNOTASSIGNMENT|反復式が代入式ではありません: "%1"。 このエラーは、通常 ForLoop の代入式の式が代入式ではない場合に発生します。|  
|0x8001F204|-2147356156|DTS_W_INITIALIZATIONEXPRESSIONISNOTASSIGNMENT|初期化式が代入式ではありません: "%1"。 このエラーは、通常 ForLoop の反復式の式が代入式ではない場合に発生します。|  
|0x8001F205|-2147356155|DTS_W_LOGPROVIDERNOTDEFINED|実行可能ファイル "%1" は正常に貼り付けられました。 ただし、この実行可能ファイルに関連付けられたログ プロバイダーがコレクション "LogProviders" に見つかりませんでした。  この実行可能ファイルは、ログ プロバイダー情報なしで貼り付けられました。|  
|0x8001F300|-2147355904|DTS_W_PACKAGEUPGRADED|パッケージのアップグレードに成功しました。|  
|0x8001F42B|-2147355605|DTS_W_LEGACYPROGID|"%1" ProgID は非推奨とされます。 代わりに、このコンポーネント "%2" の新しい ProgID を使用してください。|  
|0x80020918|-2147350248|DTS_W_FTPTASK_OPERATIONFAILURE|操作 "%1" に失敗しました。|  
|0x800283A5|-2147318875|DTS_W_MSMQTASK_USE_WEAK_ENCRYPTION|暗号化アルゴリズム "%1" には、弱い暗号が使われています。|  
|0x80029164|-2147315356|DTS_W_FSTASK_OPERATIONFAILURE|タスクが操作 "%1" を実行できませんでした。|  
|0x80029185|-2147315323|DTS_W_EXECPROCTASK_FILENOTINPATH|ファイル/プロセス "%1" がパス上にありません。|  
|0x800291C6|-2147315258|DTS_W_SENDMAILTASK_SUBJECT_MISSING|件名が空です。|  
|0x800291C7|-2147315257|DTS_W_SENDMAILTASK_ERROR_IN_TO_LINE|[宛先] 行に指定されたアドレスの形式が正しくありません。 "\@" 記号がないか、無効です。|  
|0x800291C8|-2147315256|DTS_W_SENDMAILTASK_AT_MISSING_IN_FROM|[差出人] 行に指定されたアドレスの形式が正しくありません。 "\@" 記号がないか、無効です。|  
|0x8002927A|-2147315078|DTS_W_XMLTASK_DIFFFAILURE|2 つの XML ドキュメントが異なっています。|  
|0x8002928C|-2147315060|DTS_W_XMLTASK_DTDVALIDATIONWARNING|DTD の検証には、XML ドキュメント内の DOCTYPE 行で定義されている DTD ファイルが使用されます。 プロパティ "%1" に割り当てられているものは使用されません。|  
|0x8002928D|-2147315059|DTS_W_XMLTASK_VALIDATIONFAILURE|タスクが "%1" を検証できませんでした。|  
|0x80029291|-2147315055|DTS_W_TRANSFERDBTASK_ACTIONSETTOCOPY|転送アクションの値が無効です。  コピーするように設定されています。|  
|0x80029292|-2147315054|DTS_W_TRANSFERDBTASK_METHODSETTOONLINE|転送方法の値が無効です。  オンライン転送に設定されています。|  
|0x8002F304|-2147290364|DTS_W_PROBLEMOCCURREDWITHFOLLOWINGMESSAGE|問題が次のメッセージで発生しました: "%1"。|  
|0x8002F322|-2147290334|DTS_W_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|エラー メッセージ "%1" は、既に転送先サーバーに存在します。|  
|0x8002F331|-2147290319|DTS_W_JOBSTASK_JOBEXISTSATDEST|ジョブ "%1" は、既に転送先サーバーに存在します。|  
|0x8002F332|-2147290318|DTS_W_JOBSTASK_SKIPPINGJOBEXISTSATDEST|ジョブ "%1" は転送先に既に存在するので、転送をスキップしています。|  
|0x8002F333|-2147290317|DTS_W_JOBSTASK_OVERWRITINGJOB|転送先のサーバーでジョブ "%1" を上書きしています。|  
|0x8002F339|-2147290311|DTS_W_LOGINSTASK_ENUMVALUEINCORRECT|プロパティ "FailIfExists" の保存された列挙値が変更され、無効になりました。 既定値にリセットしています。|  
|0x8002F343|-2147290301|DTS_W_LOGINSTASK_OVERWRITINGLOGINATDEST|転送先でログイン "%1" を上書きしています。|  
|0x8002F356|-2147290282|DTS_W_TRANSOBJECTSTASK_SPALREADYATDEST|ストアド プロシージャ "%1" は、既に転送先に存在します。|  
|0x8002F360|-2147290272|DTS_W_TRANSOBJECTSTASK_RULEALREADYATDEST|ルール "%1" は、既に転送先に存在します。|  
|0x8002F364|-2147290268|DTS_W_TRANSOBJECTSTASK_TABLEALREADYATDEST|テーブル "%1" は、既に転送先に存在します。|  
|0x8002F368|-2147290264|DTS_W_TRANSOBJECTSTASK_VIEWALREADYATDEST|ビュー "%1" は、既に転送先に存在します。|  
|0x8002F372|-2147290254|DTS_W_TRANSOBJECTSTASK_UDFALREADYATDEST|ユーザー定義関数 "%1" は、既に転送先に存在します。|  
|0x8002F376|-2147290250|DTS_W_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|既定値 "%1" は、既に転送先に存在します。|  
|0x8002F380|-2147290240|DTS_W_TRANSOBJECTSTASK_UDDTALREADYATDEST|ユーザー定義データ型 "%1" は、既に転送先に存在します。|  
|0x8002F384|-2147290236|DTS_W_TRANSOBJECTSTASK_PFALREADYATDEST|パーティション関数 "%1" は、既に転送先に存在します。|  
|0x8002F388|-2147290232|DTS_W_TRANSOBJECTSTASK_PSALREADYATDEST|パーティション構成 "%1" は、既に転送先に存在します。|  
|0x8002F391|-2147290223|DTS_W_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|スキーマ "%1" は、既に転送先に存在します。|  
|0x8002F396|-2147290218|DTS_W_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|SqlAssembly "%1" は、既に転送先に存在します。|  
|0x8002F400|-2147290112|DTS_W_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|ユーザー定義集計 "%1" は、既に転送先に存在します。|  
|0x8002F404|-2147290108|DTS_W_TRANSOBJECTSTASK_TYPEALREADYATDEST|ユーザー定義型 "%1" は、既に転送先に存在します。|  
|0x8002F408|-2147290104|DTS_W_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|XmlSchemaCollection "%1" は、既に転送先に存在します。|  
|0x8002F412|-2147290094|DTS_W_TRANSOBJECTSTASK_NOELEMENTSPECIFIEDTOTRANSFER|転送するように指定された要素はありません。|  
|0x8002F415|-2147290091|DTS_W_TRANSOBJECTSTASK_LOGINALREADYATDEST|ログイン "%1" は、既に転送先に存在します。|  
|0x8002F41A|-2147290086|DTS_W_TRANSOBJECTSTASK_USERALREADYATDEST|ユーザー "%1" は、既に転送先に存在します。|  
|0x80047007|-2147192825|DTS_W_NOLINEAGEVALIDATION|実行ツリーに循環参照が含まれているので、入力列の系列 ID を検証できません。|  
|0x80047034|-2147192780|DTS_W_EMPTYDATAFLOW|DataFlow タスクにはコンポーネントがありません。 コンポーネントを追加するか、タスクを削除してください。|  
|0x80047069|-2147192727|DTS_W_SORTEDOUTPUTHASNOSORTKEYPOSITIONS|%1 の IsSorted プロパティは True に設定されていますが、すべての出力列の SortKeyPositions が 0 に設定されています。|  
|0x8004706F|-2147192721|DTS_W_SOURCEREMOVED|データ フロー タスクの外部に表示されるデータがないので、基になる "%1" (%2!d!) は読み取られません。|  
|0x80047076|-2147192714|DTS_W_UNUSEDOUTPUTDATA|出力 "%3" (%4!d!) とコンポーネント "%5" (%6!d!) の出力列 "%1" (%2!d!) は、その後のデータ フロー タスクで使用されません。 この使用されない出力列を削除すると、データ フロー タスクのパフォーマンスが向上する可能性があります。|  
|0x800470AE|-2147192658|DTS_W_COMPONENTREMOVED|コンポーネント "%1" (%2!d!) は、出力が使用されておらず、入力に副作用がないか入力が他のコンポーネントの出力に接続されていないので、データ フロー タスクから削除されました。 このコンポーネントが必要な場合は、少なくとも 1 つの入力の HasSideEffects プロパティを True に設定するか、または出力を任意のオブジェクトに接続する必要があります。|  
|0x800470B0|-2147192656|DTS_W_NOWORKTODO|スレッドに行が渡されましたが、そのスレッドには実行する処理がありません。 レイアウトには切断された出力があります。 RunInOptimizedMode プロパティを True に設定したパイプラインは、実行時間が短く、この警告を解消できます。|  
|0x800470C8|-2147192632|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|%1 の外部列は、データ ソースの列と同期が取れていません。 %2|  
|0x800470C9|-2147192631|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSADDITION|外部列に列 "%1" を追加する必要があります。|  
|0x800470CA|-2147192630|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSUPDATE|外部列 "%1" を更新する必要があります。|  
|0x800470CB|-2147192629|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSREMOVAL|外部列から %1 を削除する必要があります。|  
|0x800470D8|-2147192616|DTS_W_EXPREVALPOTENTIALSTRINGTRUNCATION|式 "%1" の結果文字列は、最大文字数の %2!d! 文字を超えた場合に切り捨てられることが 超えています。 この式では、結果値が DT_WSTR 型の最大サイズを超える可能性があります。|  
|0x800470E9|-2147192599|DTS_W_COMPONENTLEAKPROCESSINPUT|%2 の入力 %1!d! に対する ProcessInput メソッドへの呼び出しで、 メソッドに渡されたバッファーへの参照が予期せず保持されました。 呼び出し前のそのバッファーの参照カウントは %3!d! で、 呼び出しが返された後に %4!d! に なりました。|  
|0x800470EB|-2147192597|DTS_W_EXPREVALUNREFERENCEDINPUTCOLUMN|"%2" の "%1" の使用法の種類は READONLY ですが、式によって参照されていません。 使用できる入力列の一覧からその列を削除するか、式でその列を参照してください。|  
|0x8004801E|-2147188706|DTS_W_COULDNOTFINDCURRENTVERSION|コンポーネント %2 の "%1" 値が見つかりません。 コンポーネントの CurrentVersion 値が見つかりません。 このエラーは、DTSInfo セクションに CurrentVersion 値を含むようにコンポーネントのレジストリ情報が設定されていない場合に発生します。 このメッセージは、コンポーネントが正しく登録されていない状態で、コンポーネントを開発していたり、コンポーネントをパッケージで使用しているときに表示されます。|  
|0x80049300|-2147183872|DTS_W_BUFFERGETTEMPFILENAME|バッファー マネージャーは一時ファイルの名前を取得できませんでした。|  
|0x80049301|-2147183871|DTS_W_UNUSABLETEMPORARYPATH|バッファー マネージャーはパス "%1" に一時ファイルを作成できませんでした。 このパスは一時保存域として見なされません。|  
|0x80049304|-2147183868|DTS_W_DF_PERFCOUNTERS_DISABLED|警告:パフォーマンス DLL と通信するためのグローバル共有メモリを開けなかったため、データ フロー パフォーマンス カウンターは使用できません。  解決するには、このパッケージを管理者として実行するか、システムのコンソールで実行してください。|  
|0x8020200F|-2145378289|DTS_W_PARTIALROWFOUNDATENDOFFILE|ファイルの末尾に不完全な行があります。|  
|0x8020202B|-2145378261|DTS_W_ENDOFFILEREACHWHILEREADINGHEADERROWS|ヘッダー行の読み取り中に、データ ファイルの末尾に到達しました。 ヘッダー行の区切り記号とスキップするヘッダー行数が正しいことを確認してください。|  
|0x80202066|-2145378202|DTS_W_CANTRETRIEVECODEPAGEFROMOLEDBPROVIDER|OLE DB プロバイダーから列コード ページ情報を取得できません。  コンポーネントで "%1" プロパティがサポートされている場合は、そのプロパティのコード ページを使用します。  現在の文字列のコード ページの値が正しくない場合は、プロパティの値を変更してください。  コンポーネントでこのプロパティがサポートされていない場合は、コンポーネントのロケール ID のコード ページを使用します。|  
|0x802020F7|-2145378057|DTS_W_TXSORTSORTISTHESAME|データは指定どおりに既に並べ替えられているので、変換を削除できます。|  
|0x8020400D|-2145370099|DTS_W_NOPIPELINEDATATYPEMAPPINGAVAILABLE|%1 から、データ フロー タスクのデータ型にマップできない外部のデータ型を参照しています。 データ フロー タスクのデータ型 DT_WSTR が代用されます。|  
|0x802070CC|-2145357620|DTS_W_STATICTRUNCATIONINEXPRESSION|式 "%1" では、常にデータの切り捨てが行われます。 この式には、静的な切り捨て (固定値の切り捨て) が含まれています。|  
|0x8020820C|-2145353204|DTS_W_UNMAPPEDINPUTCOLUMN|インデックス %3!d! にある ID %2!d! の 入力列 "%1" は マップ解除されています。 この列の系列 ID は 0 です。|  
|0x80208305|-2145352955|DTS_W_TXFUZZYLOOKUP_DELIMITERS_DONT_MATCH|指定された区切り記号が、既存の一致インデックス "%1" を構築するために使用された区切り記号と一致しません。 このエラーは、フィールドのトークン作成に使用された区切り記号が一致しない場合に発生します。 照合の動作や結果に未知の影響が出る可能性があります。|  
|0x80208308|-2145352952|DTS_W_TXFUZZYLOOKUP_MAXRESULTS_IS_ZERO|あいまい参照変換の MaxOutputMatchesPerInput プロパティは 0 です。 結果は生成されません。|  
|0x80208310|-2145352944|DTS_W_TXFUZZYLOOKUP_NO_FUZZY_JOIN_COLUMNS|JoinType 列のプロパティが Fuzzy に設定された、有効な入力列がありませんでした。  FuzzyLookup の代わりに参照変換を使用すると、完全結合のパフォーマンスが向上する可能性があります。|  
|0x8020831C|-2145352932|DTS_W_TXFUZZYLOOKUP_TIMESTAMPCAVEAT|参照列 "%1" が SQL timestamp 列になっている可能性があります。 あいまい一致インデックスが構築され、参照テーブルのコピーが作成されるときに、すべての参照テーブルのタイムスタンプにコピー時のテーブルの状態が反映されます。 CopyReferenceTable を False に設定している場合は、予期しない動作が発生することがあります。|  
|0x80208321|-2145352927|DTS_W_MATCHINDEXALREADYEXISTS|MatchIndexName に指定された名前 '%1' を持つテーブルが既に存在し、DropExistingMatchIndex が False に設定されています。  このテーブルが削除されるか、別の名前が指定されるか、または DropExistingMatchIndex が True に設定されない限り、変換の実行は失敗します。|  
|0x8020832B|-2145352917|DTS_W_TXFUZZYLOOKUP_JOINLENGTHMISMATCH|入力列 '%1' の長さは、比較対照の参照列 '%2' の長さと異なります。|  
|0x8020832D|-2145352915|DTS_W_TXFUZZYLOOKUP_CODEPAGE_MISMATCH|基になる DT_STR 列 "%1" と対象になる DT_STR 列 "%2" のコード ページが一致していないため、  予期しない結果が生じる可能性があります。|  
|0x8020832E|-2145352914|DTS_W_FUZZYLOOKUP_TOOMANYEXACTMATCHCOLUMNS|完全一致結合が 17 個以上あるため、パフォーマンスが最適でない可能性があります。 完全一致結合の数を減らして、パフォーマンスを向上させてください。 SQL Server には、各インデックスに保持できる列は 16 列までという制限があるので、すべての参照に反転されたインデックスが使用されます。|  
|0x80208350|-2145352880|DTS_W_FUZZYLOOKUP_MEMLIMITANDEXHAUSTIVESPECIFIED|Exhaustive オプションを使用すると、参照全体がメイン メモリに読み込まれます。  メモリ制限が MaxMemoryUsage プロパティに指定されているので、参照テーブル全体がこの制限内に収まらなかったり、実行時に一致操作が失敗する可能性があります。|  
|0x80208351|-2145352879|DTS_W_FUZZYLOOKUP_EXACTMATCHCOLUMNSEXCEEDBYTELIMIT|完全一致結合で指定した列の累積長が、インデックス キーの制限値である 900 バイトを超えました。  あいまい参照では、参照のパフォーマンスを向上させるため、完全一致列にインデックスが作成されますが、このインデックスの作成に失敗したり、一致する列の参照に別の低速な検索方法が使用される場合があります。 パフォーマンスを向上させる必要がある場合は、いくつかの完全一致の結合列を削除するか、完全一致列の可変長の最大値を小さくしてください。|  
|0x80208352|-2145352878|DTS_W_FUZZYLOOKUP_EXACTMATCHINDEXCREATIONFAILED|完全一致列にインデックスを作成できませんでした。 代替のあいまい参照方法に戻しています。|  
|0x80208353|-2145352877|DTS_W_FUZZYGROUPINGINTERNALPIPELINEWARNING|警告コード 0x%1!8.8X! により、次のあいまいグループ化の内部パイプライン警告が発生しました: "%2"。|  
|0x80208375|-2145352843|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTODEFAULT|%1 の最大長が外部のデータ型 %2 で指定されませんでした。 長さ %4!d! の SSIS データ フロー タスクのデータ型 "%3" が 使用されます。|  
|0x80208376|-2145352842|DTS_W_XMLSRCOUTPUTCOLUMNDATATYPEMAPPEDTOSTRING|%1 から、SSIS データ フロー タスクのデータ型にマップできない外部のデータ型 %2 を参照しています。  代わりに、長さ %3!d! の SSIS データ フロー タスクのデータ型 DT_WSTR が 使用されます。|  
|0x80208385|-2145352827|DTS_W_NOREDIRECTWITHATTACHEDERROROUTPUTS|エラー出力に行が送信されません。 エラー出力に行をリダイレクトするようにエラーまたは切り捨て処理を構成するか、エラー出力にアタッチされるデータ フロー変換または変換先を削除してください。|  
|0x80208386|-2145352826|DTS_W_REDIRECTWITHNOATTACHEDERROROUTPUTS|エラー出力に送信される行は失われます。 新しいデータ フロー変換または変換先を追加してエラー行を受け取るか、エラー出力への行のリダイレクトを停止するようにコンポーネントを再構成してください。|  
|0x80208391|-2145352815|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTOMAXIMUM|%1 (外部のデータ型 %2) に、XML スキーマで maxLength 制約 %3!d! が指定されています。これは最大許容列長の %4!d! を超えています。 長さ %6!d! の SSIS データ フロー タスクのデータ型 "%5" が 使用されます。|  
|0x802090E4|-2145349404|DTS_W_TXLOOKUP_DUPLICATE_KEYS|参照データをキャッシュしているときに、%1 により重複した参照キー値が検出されました。 このエラーはフル キャッシュ モードの場合にだけ発生する可能性があります。 重複したキーの値を削除するか、キャッシュ モードを PARTIAL または NO_CACHE に変更してください。|  
|0x802092A7|-2145348953|DTS_W_POTENTIALTRUNCATIONFROMDATAINSERTION|長さ %2!d! のデータ フロー列 "%1" から、長さ %4!d! のデータベース列 "%3" にデータを挿入することにより、 切り捨てが行われる可能性があります。|  
|0x802092A8|-2145348952|DTS_W_POTENTIALTRUNCATIONFROMDATARETRIEVAL|長さ %2!d! のデータベース列 "%1" から、長さ %4!d! のデータ フロー列 "%3" にデータを取得することにより、 切り捨てが行われる可能性があります。|  
|0x802092AA|-2145348950|DTS_W_ADODESTBATCHNOTSUPPORTEDFORERRORDISPOSITION|バッチ モードは、現在、エラー行の処理の使用時にサポートされていません。 BatchSize プロパティには 1 が設定されます。|  
|0x802092AB|-2145348949|DTS_W_ADODESTNOROWSINSERTED|行が変換先に正常に挿入されませんでした。 これは、列間のデータ型の不一致、または ADO.NET プロバイダーでサポートされていないデータ型の使用が原因である可能性があります。 このコンポーネントのエラー処理は "エラー コンポーネント" ではないため、ここではエラー メッセージが表示されません。エラー メッセージを表示するには、エラー処理を "エラー コンポーネント" に設定してください。|  
|0x802092AC|-2145348948|DTS_W_ADODESTPOTENTIALDATALOSS|データ型 "%2" の入力列 "%1" のデータをデータ型 "%4" の外部列 "%3" に挿入することにより、データが失われる可能性があります。 この操作を意図している場合、変換を行う別の方法として、ADO NET 変換先コンポーネントの前にデータ変換コンポーネントを使用するという方法もあります。|  
|0x802092AD|-2145348947|DTS_W_ADODESTEXTERNALCOLNOTMATCHSCHEMACOL|%1 はデータベース列と同期が取れていません。  最新の列には %2 があります。 必要に応じて、詳細エディターを使用し、使用できる変換先列を更新してください。|  
|0x802092AE|-2145348946|DTS_W_ADODESTEXTERNALCOLNOTEXIST|%1 はデータベースに存在しません。 削除または名前が変更された可能性があります。 必要に応じて、詳細エディターを使用し、使用できる変換先列を更新してください。|  
|0x802092AF|-2145348945|DTS_W_ADODESTNEWEXTCOL|%1 という名前の新しい列が外部データベース テーブルに追加されました。 必要に応じて、詳細エディターを使用し、使用できる変換先列を更新してください。|  
|0x8020930C|-2145348852|DTS_W_NOMATCHOUTPUTGETSNOROWS|不一致出力に送信される行はありません。 一致するエントリがない行を不一致出力にリダイレクトするように変換を構成するか、不一致出力にアタッチされるデータ フロー変換または変換先を削除してください。|  
|0x8020931B|-2145348837|DTS_W_ADODESTINVARIANTEXCEPTION|ADO.Net プロバイダーの列挙中に例外を受け取りました。 不変: "%1"。 例外メッセージは "%2" です。|  
|0xC020822C|-1071611348|DTS_W_UNMAPPEDOUTPUTCOLUMN|%1 はマップされている入力列がありません。|  
|0x930D|37645|DTS_W_EXTERNALTABLECOLSOUTOFSYNC|テーブル "%1" は変更されています。 このテーブルに新しい列が追加されている可能性があります。|  
  
##  <a name="msgInfo"></a> 情報メッセージ  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の情報メッセージのシンボル名は、 **DTS_I_** で始まります。  
  
|16 進コード|10 進コード|シンボル名|[説明]|  
|----------------------|------------------|-------------------|-----------------|  
|0x4001100A|1073811466|DTS_I_STARTINGTRANSACTION|このコンテナーの分散トランザクションを開始しています。|  
|0x4001100B|1073811467|DTS_I_COMMITTINGTRANSACTION|このコンテナーで開始された分散トランザクションをコミットしています。|  
|0x4001100C|1073811468|DTS_I_ABORTINGTRANSACTION|現在の分散トランザクションを中止しています。|  
|0x40013501|1073820929|DTS_I_GOTMUTEXFROMWAIT|ミューテックス "%1" が正常に取得されました。|  
|0x40013502|1073820930|DTS_I_RELEASEACQUIREDMUTEX|ミューテックス "%1" が正常に解放されました。|  
|0x40013503|1073820931|DTS_I_NEWMUTEXCREATED|ミューテックス "%1" が正常に作成されました。|  
|0x40015101|1073828097|DTS_I_DUMP_ON_ANY_ERR|エラー イベントに対してデバッグ ダンプ ファイルが生成されます。|  
|0x40015102|1073828098|DTS_I_DUMP_ON_CODES|次のイベント コードに対してデバッグ ダンプ ファイルが生成されます: "%1"|  
|0x40015103|1073828099|DTS_I_START_DUMP|イベント コード 0x%1!8.8X! により、デバッグ ダンプ ファイルがフォルダー "%2" に生成されました。|  
|0x40015104|1073828100|DTS_I_SSIS_INFO_DUMP|SSIS 情報ダンプ ファイル "%1" を作成しています。|  
|0x40015106|1073828102|DTS_I_FINISH_DUMP|デバッグ ダンプ ファイルが正常に作成されました。|  
|0x40016019|1073831961|DTS_I_PACKAGEMIGRATED|パッケージ形式がバージョン %1!d! から %2!d! に 移行されました。 移行による変更を保持するためにパッケージを保存する必要があります。|  
|0x4001601A|1073831962|DTS_I_SCRIPTSMIGRATED|パッケージのスクリプトが移行されました。 移行による変更を保持するためにパッケージを保存する必要があります。|  
|0x40016025|1073831973|DTS_I_FTPRECEIVEFILE|ファイル "%1" を受信しています。|  
|0x40016026|1073831974|DTS_I_FTPSENDFILE|ファイル "%1" を送信しています。|  
|0x40016027|1073831975|DTS_I_FTPFILEEXISTS|ファイル "%1" は既に存在します。|  
|0x40016028|1073831976|DTS_I_FTPERRORLOADINGMSG|内部エラーにより、追加のエラー情報を取得できません。|  
|0x40016036|1073831990|DTS_I_FTPDELETEFILE|ファイル "%1" の削除に失敗しました。 このエラーは、ファイルが存在しない場合、ファイル名の綴りが間違っている場合、またはファイルを削除する権限がない場合に発生することがあります。|  
|0x40016037|1073831991|DTS_I_CONFIGFROMREG|レジストリ キー "%1" を使用して、パッケージをレジストリ エントリから構成しようとしています。|  
|0x40016038|1073831992|DTS_I_CONFIGFROMENVVAR|パッケージを環境変数 "%1" から構成しようとしています。|  
|0x40016039|1073831993|DTS_I_CONFIGFROMINIFILE|パッケージを .INI ファイル "%1" から構成しようとしています。|  
|0x40016040|1073832000|DTS_I_CONFIGFROMSQLSERVER|構成文字列 "%1" を使用して、パッケージを SQL Server から構成しようとしています。|  
|0x40016041|1073832001|DTS_I_CONFIGFROMFILE|パッケージを XML ファイル "%1" から構成しようとしています。|  
|0x40016042|1073832002|DTS_I_CONFIGFROMPARENTVARIABLE|パッケージを親変数 "%1" から構成しようとしています。|  
|0x40016043|1073832003|DTS_I_ATTEMPTINGUPGRADEOFDTS|バージョン "%1" から "%2" に SSIS をアップグレードしようとしています。 パッケージは、ランタイムをアップグレードしようとしています。|  
|0x40016044|1073832004|DTS_I_ATTEMPTINGUPGRADEOFANEXTOBJ|"%1" をアップグレードしようとしています。 パッケージは、拡張可能なオブジェクトをアップグレードしようとしています。|  
|0x40016045|1073832005|DTS_I_SAVECHECKPOINTSTOFILE|パッケージは、実行中にチェックポイントをファイル "%1" に保存します。 パッケージは、チェックポイントを保存するように構成されています。|  
|0x40016046|1073832006|DTS_I_RESTARTFROMCHECKPOINTFILE|パッケージは、チェックポイント ファイル "%1" から再開されました。 パッケージは、チェックポイントから再開されるように構成されました。|  
|0x40016047|1073832007|DTS_I_CHECKPOINTSAVEDTOFILE|チェックポイント ファイル "%1" が更新され、このコンテナーの完了を記録しました。|  
|0x40016048|1073832008|DTS_I_CHECKPOINTFILEDELETED|パッケージが正常に完了した後、チェックポイント ファイル "%1" が削除されました。|  
|0x40016049|1073832009|DTS_I_CHECKPOINTSAVINGTOFILE|チェックポイント ファイル "%1" の更新を開始しています。|  
|0x40016051|1073832017|DTS_I_CHOSENMAXEXECUTABLES|システムの構成に基づいて、同時実行可能ファイルの最大数は %1!d! に設定されています。|  
|0x40016052|1073832018|DTS_I_MAXEXECUTABLES|同時実行可能ファイルの最大数は %1!d! に設定されています。|  
|0x40016053|1073832019|DTS_I_PACKAGESTART|パッケージ実行の開始です。|  
|0x40016054|1073832020|DTS_I_PACKAGEEND|パッケージ実行の終了です。|  
|0x40029161|1073910113|DTS_I_FSTASK_DIRECTORYDELETED|ディレクトリ "%1" は削除されました。|  
|0x40029162|1073910114|DTS_I_FSTASK_FILEDELETED|ファイルまたはディレクトリ "%1" は削除されました。|  
|0x400292A8|1073910440|DTS_I_TRANSFERDBTASK_OVERWRITEDB|転送先サーバー "%2" のデータベース "%1" を上書きしています。|  
|0x4002F304|1073935108|DTS_I_SOMETHINGHAPPENED|"%1"。|  
|0x4002F323|1073935139|DTS_I_ERRMSGTASK_SKIPPINGERRORMESSAGEALREADYEXISTS|エラー メッセージ "%1" は既に転送先サーバーに存在するので、このエラー メッセージをスキップしています。|  
|0x4002F326|1073935142|DTS_I_ERRMSGTASK_TRANSFEREDNERRORMESSAGES|"%1" 個のエラー メッセージが転送されました。|  
|0x4002F351|1073935185|DTS_I_STOREDPROCSTASKS_TRANSFEREDNSPS|このタスクで "%1" 個のストアド プロシージャが転送されました。|  
|0x4002F352|1073935186|DTS_I_TRANSOBJECTSTASK_TRANSFEREDNOBJECTS|"%1" 個のオブジェクトが転送されました。|  
|0x4002F358|1073935192|DTS_I_TRANSOBJECTSTASK_NOSPSTOTRANSFER|転送するストアド プロシージャはありません。|  
|0x4002F362|1073935202|DTS_I_TRANSOBJECTSTASK_NORULESTOTRANSFER|転送するルールはありません。|  
|0x4002F366|1073935206|DTS_I_TRANSOBJECTSTASK_NOTABLESTOTRANSFER|転送するテーブルはありません。|  
|0x4002F370|1073935216|DTS_I_TRANSOBJECTSTASK_NOVIEWSTOTRANSFER|転送するビューはありません。|  
|0x4002F374|1073935220|DTS_I_TRANSOBJECTSTASK_NOUDFSTOTRANSFER|転送するユーザー定義関数はありません。|  
|0x4002F378|1073935224|DTS_I_TRANSOBJECTSTASK_NODEFAULTSTOTRANSFER|転送する既定値はありません。|  
|0x4002F382|1073935234|DTS_I_TRANSOBJECTSTASK_NOUDDTSTOTRANSFER|転送するユーザー定義データ型はありません。|  
|0x4002F386|1073935238|DTS_I_TRANSOBJECTSTASK_NOPFSTOTRANSFER|転送するパーティション関数はありません。|  
|0x4002F390|1073935248|DTS_I_TRANSOBJECTSTASK_NOPSSTOTRANSFER|転送するパーティション構成はありません。|  
|0x4002F394|1073935252|DTS_I_TRANSOBJECTSTASK_NOSCHEMASTOTRANSFER|転送するスキーマはありません。|  
|0x4002F398|1073935256|DTS_I_TRANSOBJECTSTASK_NOSQLASSEMBLIESTOTRANSFER|転送する SqlAssemblies はありません。|  
|0x4002F402|1073935362|DTS_I_TRANSOBJECTSTASK_NOAGGREGATESTOTRANSFER|転送するユーザー定義集計はありません。|  
|0x4002F406|1073935366|DTS_I_TRANSOBJECTSTASK_NOTYPESTOTRANSFER|転送するユーザー定義型はありません。|  
|0x4002F410|1073935376|DTS_I_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONSTOTRANSFER|転送する XmlSchemaCollections はありません。|  
|0x4002F418|1073935384|DTS_I_TRANSOBJECTSTASK_NOLOGINSTOTRANSFER|転送するログインはありません。|  
|0x4002F41D|1073935389|DTS_I_TRANSOBJECTSTASK_NOUSERSTOTRANSFER|転送するユーザーはありません。|  
|0x4002F41E|1073935390|DTS_I_TRANSOBJECTSTASK_TRUNCATINGTABLE|テーブル "%1" を切り捨てています|  
|0x40043006|1074016262|DTS_I_EXECUTIONPHASE_PREPAREFOREXECUTE|実行フェーズの準備を開始しています。|  
|0x40043007|1074016263|DTS_I_EXECUTIONPHASE_PREEXECUTE|実行前フェーズを開始しています。|  
|0x40043008|1074016264|DTS_I_EXECUTIONPHASE_POSTEXECUTE|実行後フェーズを開始しています。|  
|0x40043009|1074016265|DTS_I_EXECUTIONPHASE_CLEANUP|クリーンアップ フェーズを開始しています。|  
|0x4004300A|1074016266|DTS_I_EXECUTIONPHASE_VALIDATE|検証フェーズを開始しています。|  
|0x4004300B|1074016267|DTS_I_ROWS_WRITTEN|"%1" により、%2!ld! 行が キャッシュされました。|  
|0x4004300C|1074016268|DTS_I_EXECUTIONPHASE_EXECUTE|実行フェーズを開始しています。|  
|0x4004800C|1074036748|DTS_I_CANTRELIEVEPRESSURE|バッファー マネージャーは、システムの仮想メモリが不足していることを検出しましたが、バッファーをスワップ アウトできませんでした。 %1!d! 個の バッファーが考慮され、%2!d! 個が ロックされました。 メモリの搭載量が不十分なのでパイプラインが十分なメモリを使用できないか、他のプロセスで消費されているか、ロックされているバッファーが多すぎます。|  
|0x4004800D|1074036749|DTS_I_CANTALLOCATEMEMORYPRESSURE|バッファー マネージャーは、%3!d! バイトのメモリ割り当て呼び出しに失敗しましたが、 バッファーをスワップ アウトしてメモリの負荷を下げることができませんでした。 %1!d! 個の バッファーが考慮され、%2!d! 個が ロックされました。 メモリの搭載量が不十分なのでパイプラインが十分なメモリを使用できないか、他のプロセスで消費されているか、ロックされているバッファーが多すぎます。|  
|0x4004800E|1074036750|DTS_I_ALLOCATEDDURINGMEMORYPRESSURE|メモリ不足が検出され、バッファーのスワップが繰り返し試行されて 失敗しましたが、バッファー マネージャーにより %1!d! バイト割り当てられました。|  
|0x400490F4|1074041076|DTS_I_TXLOOKUP_CACHE_PROGRESS|%1 により、%2!d! 行がキャッシュ キャッシュされました。|  
|0x400490F5|1074041077|DTS_I_TXLOOKUP_CACHE_FINAL|%1 により、合計 %2!d! 行が キャッシュされました。|  
|0x4020206D|1075847277|DTS_I_RAWSOURCENOCOLUMNS|生データ ソース アダプターでファイルを開きましたが、列がありませんでした。 アダプターではデータは生成されません。 これはファイルが破損しているか、ファイルに列がなくデータがないことを意味する可能性があります。|  
|0x402020DA|1075847386|DTS_I_OLEDBINFORMATIONALMESSAGE|OLE DB の情報メッセージがあります。|  
|0x40208327|1075872551|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_COLLATIONS_DONT_MATCH|入力列 "%1" の完全結合 FuzzyComparisonFlags が、参照テーブルの列 "%2" の既定の SQL 照合順序に一致するように設定すると、あいまい一致のパフォーマンスが向上する可能性があります。  また、FuzzyComparisonFlagsEx に、FuzzyComparisonFlags と重ならないフラグを設定する必要があります。|  
|0x40208328|1075872552|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_INDEX_MISSING|指定されたすべての完全一致列の参照テーブルでインデックスを作成すると、あいまい一致のパフォーマンスが向上する可能性があります。|  
|0x40208387|1075872647|DTS_I_DISPSNOTREVIEWED|エラー処理および切り捨て処理が確認されませんでした。 行をさらに転送する場合は、このコンポーネントがエラー出力に行をリダイレクトするように構成されていることを確認してください。|  
|0x402090DA|1075876058|DTS_I_TXAGG_WORKSPACE_REHASH|集計変換により、キーの組み合わせが %1!d! 個 検出されました。 キーの組み合わせの数が予期された数よりも多いので、データを再ハッシュする必要があります。 コンポーネントは、Keys、KeyScale、および AutoExtendFactor プロパティを調整することで、データを再ハッシュしない構成にすることができます。|  
|0x402090DB|1075876059|DTS_I_TXAGG_COUNTDISTINCT_REHASH|集計変換により、キーの組み合わせが %1!d! 個 %1!d! 個の個別の値が検出されました。 個別の値の数が予期された数よりも多いので、変換でデータが再ハッシュされます。 コンポーネントは、CountDistinctKeys、CountDistinctKeyScale、および AutoExtendFactor プロパティを調整することで、データを再ハッシュしない構成にすることができます。|  
|0x402090DC|1075876060|DTS_I_STARTPROCESSINGFILE|ファイル "%1" の処理が開始されました。|  
|0x402090DD|1075876061|DTS_I_FINISHPROCESSINGFILE|ファイル "%1" の処理が終了しました。|  
|0x402090DE|1075876062|DTS_I_TOTALDATAROWSPROCESSEDFORFILE|ファイル "%1" に対して処理されたデータ行の合計数は %2!I64d! です。|  
|0x402090DF|1075876063|DTS_I_FINALCOMMITSTARTED|"%1" にデータを挿入するための最後のコミットを開始しました。|  
|0x402090E0|1075876064|DTS_I_FINALCOMMITENDED|"%1" にデータを挿入するための最後のコミットが終了しました。|  
|0x402090E1|1075876065|DTS_I_BEGINHASHINGCACHE|%1!u! 行がキャッシュに追加されます。 システムはその行を処理しています。|  
|0x402090E2|1075876066|DTS_I_SUCCEEDEDHASHINGCACHE|%1 により、キャッシュ内で %2!u! 行を 処理しました。 処理時間は %3 秒でした。 キャッシュは %4!I64u! バイトのメモリを 使用しました。|  
|0x402090E3|1075876067|DTS_I_FAILEDHASHINGCACHE|%1 により、キャッシュ内の行を処理できませんでした。  処理時間は %2 秒でした。|  
|0x402090E4|1075876068|DTS_I_SUCCEEDEDPREPARINGCACHE|%1 により、キャッシュの準備に成功しました。 準備時間は %2 秒でした。|  
|0x40209314|1075876628|DTS_I_TXLOOKUP_PARTIALPERF|%1 は次の操作を実行しました: %2!I64u! 行の処理、 参照データベースへの %3!I64u! データベース コマンドの発行、部分的なキャッシュを使用した %4!I64u! 参照。|  
|0x40209315|1075876629|DTS_I_TXLOOKUP_PARTIALPERF2|%1 は次の操作を実行しました: %2!I64u! 行の処理、 参照データベースへの %3!I64u! データベース コマンドの発行、 部分的なキャッシュを使用した %4!I64u! 参照、 および初期の参照に一致するエントリがない行のキャッシュを使用した %5!I64u! 参照。|  
|0x40209316|1075876630|DTS_I_CACHEFILEWRITESTARTED|%1 により、ファイル "%2" にキャッシュを書き込んでいます。|  
|0x40209317|1075876631|DTS_I_CACHEFILEWRITESUCCEEDED|%1 により、ファイル "%2" にキャッシュを書き込みました。|  
|0x4020F42C|1075901484|DTS_I_OLEDBDESTZEROMAXCOMMITSIZE|OLE DB 変換先 "%1" の挿入コミット サイズの最大値プロパティは 0 に設定されています。 このプロパティの設定により、実行中のパッケージは応答を停止する可能性があります。 詳細については、[OLE DB 変換先エディター] ([接続マネージャー] ページ) の F1 ヘルプ トピックを参照してください。|  
  
##  <a name="msgGeneral"></a> 一般的なメッセージおよびイベント メッセージ  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のエラー メッセージのシンボル名は、 **DTS_MSG_** で始まります。  
  
|16 進コード|10 進コード|シンボル名|[説明]|  
|----------------------|------------------|-------------------|-----------------|  
|0x1|1|DTS_MSG_CATEGORY_SERVICE_CONTROL|関数が正しくありません。|  
|0x2|2|DTS_MSG_CATEGORY_RUNNING_PACKAGE_MANAGEMENT|指定されたファイルが見つかりません。|  
|0x100|256|DTS_MSG_SERVER_STARTING|Microsoft SSIS サービスを起動しています。<br /><br /> サーバーのバージョン %1|  
|0x101|257|DTS_MSG_SERVER_STARTED|Microsoft SSIS サービスが開始されました。<br /><br /> サーバーのバージョン %1|  
|0x102|258|DTS_MSG_SERVER_STOPPING|待ち操作がタイムアウトになりました。|  
|0x103|259|DTS_MSG_SERVER_STOPPED|データはこれ以上ありません。|  
|0x104|260|DTS_MSG_SERVER_START_FAILED|Microsoft SSIS サービスを開始できませんでした。<br /><br /> エラー: %1|  
|0x105|261|DTS_MSG_SERVER_STOP_ERROR|Microsoft SSIS サービスの停止中にエラーが発生しました。<br /><br /> エラー: %1|  
|0x110|272|DTS_MSG_SERVER_MISSING_CONFIG|Microsoft SSIS サービス構成ファイルが存在しません。<br /><br /> 既定の設定を使用して読み込んでいます。|  
|0x111|273|DTS_MSG_SERVER_BAD_CONFIG|Microsoft SSIS サービス構成ファイルが正しくありません。<br /><br /> 構成ファイルの読み取り中にエラーが発生しました: %1<br /><br /> 既定の設定を使用してサーバーを読み込んでいます。|  
|0x112|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|Microsoft SSIS サービス:<br /><br /> 構成ファイルを指定するレジストリ設定がありません。<br /><br /> 既定の構成ファイルを読み込もうとしています。|  
|0x150|336|DTS_MSG_SERVER_STOPPING_PACKAGE|Microsoft SSIS サービス: 実行中のパッケージを停止しています。<br /><br /> パッケージ インスタンス ID: %1<br /><br /> パッケージ ID: %2<br /><br /> パッケージ名: %3<br /><br /> パッケージの説明: %4<br /><br /> パッケージを起動したユーザー: %5。|  
|0x40013000|1073819648|DTS_MSG_PACKAGESTART|パッケージ "%1" が起動されました。|  
|0x40013001|1073819649|DTS_MSG_PACKAGESUCCESS|パッケージ "%1" が正常に完了しました。|  
|0x40013002|1073819650|DTS_MSG_PACKAGECANCEL|パッケージ "%1" は取り消されました。|  
|0x40013003|1073819651|DTS_MSG_PACKAGEFAILURE|パッケージ "%1" は失敗しました。|  
|0x40013004|1073819652|DTS_MSG_CANTDELAYLOADDLL|エラー %4 により、モジュール %1 は、DLL %2 を読み込んでエントリ ポイント %3 を呼び出すことができません。 製品では、この DLL を実行する必要がありますが、DLL がパスに見つかりませんでした。|  
|0x40013005|1073819653|DTS_MSG_CANTDELAYLOADDLLFUNCTION|エラー %4 により、モジュール %1 は DLL %2 を読み込みましたが、エントリ ポイント %3 を見つけることができません。 指定した DLL がパスに見つかりませんでした。製品では、この DLL を実行する必要があります。|  
|0x40103100|1074802944|DTS_MSG_EVENTLOGENTRY|イベント名: %1<br /><br /> メッセージ: %9<br /><br /> 演算子: %2<br /><br /> ソース名: %3<br /><br /> ソース ID: %4<br /><br /> 実行 ID: %5<br /><br /> 開始時刻: %6<br /><br /> 終了時刻: %7<br /><br /> データ コード: %8|  
|0x40103101|1074802945|DTS_MSG_EVENTLOGENTRY_PREEXECUTE|イベント名: %1<br /><br /> メッセージ: %9<br /><br /> 演算子: %2<br /><br /> ソース名: %3<br /><br /> ソース ID: %4<br /><br /> 実行 ID: %5<br /><br /> 開始時刻: %6<br /><br /> 終了時刻: %7<br /><br /> データ コード: %8|  
|0x40103102|1074802946|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|イベント名: %1<br /><br /> メッセージ: %9<br /><br /> 演算子: %2<br /><br /> ソース名: %3<br /><br /> ソース ID: %4<br /><br /> 実行 ID: %5<br /><br /> 開始時刻: %6<br /><br /> 終了時刻: %7<br /><br /> データ コード: %8|  
|0x40103103|1074802947|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|イベント名: %1<br /><br /> メッセージ: %9<br /><br /> 演算子: %2<br /><br /> ソース名: %3<br /><br /> ソース ID: %4<br /><br /> 実行 ID: %5<br /><br /> 開始時刻: %6<br /><br /> 終了時刻: %7<br /><br /> データ コード: %8|  
|0x40103104|1074802948|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|イベント名: %1<br /><br /> メッセージ: %9<br /><br /> 演算子: %2<br /><br /> ソース名: %3<br /><br /> ソース ID: %4<br /><br /> 実行 ID: %5<br /><br /> 開始時刻: %6<br /><br /> 終了時刻: %7<br /><br /> データ コード: %8|  
|0x40103105|1074802949|DTS_MSG_EVENTLOGENTRY_WARNING|イベント名: %1<br /><br /> メッセージ: %9<br /><br /> 演算子: %2<br /><br /> ソース名: %3<br /><br /> ソース ID: %4<br /><br /> 実行 ID: %5<br /><br /> 開始時刻: %6<br /><br /> 終了時刻: %7<br /><br /> データ コード: %8|  
|0x40103106|1074802950|DTS_MSG_EVENTLOGENTRY_ERROR|イベント名: %1<br /><br /> メッセージ: %9<br /><br /> 演算子: %2<br /><br /> ソース名: %3<br /><br /> ソース ID: %4<br /><br /> 実行 ID: %5<br /><br /> 開始時刻: %6<br /><br /> 終了時刻: %7<br /><br /> データ コード: %8|  
|0x40103107|1074802951|DTS_MSG_EVENTLOGENTRY_TASKFAILED|イベント名: %1<br /><br /> メッセージ: %9<br /><br /> 演算子: %2<br /><br /> ソース名: %3<br /><br /> ソース ID: %4<br /><br /> 実行 ID: %5<br /><br /> 開始時刻: %6<br /><br /> 終了時刻: %7<br /><br /> データ コード: %8|  
|0x40103108|1074802952|DTS_MSG_EVENTLOGENTRY_PROGRESS|イベント名: %1<br /><br /> メッセージ: %9<br /><br /> 演算子: %2<br /><br /> ソース名: %3<br /><br /> ソース ID: %4<br /><br /> 実行 ID: %5<br /><br /> 開始時刻: %6<br /><br /> 終了時刻: %7<br /><br /> データ コード: %8|  
|0x40103109|1074802953|DTS_MSG_EVENTLOGENTRY_EXECSTATCHANGE|イベント名: %1<br /><br /> メッセージ: %9<br /><br /> 演算子: %2<br /><br /> ソース名: %3<br /><br /> ソース ID: %4<br /><br /> 実行 ID: %5<br /><br /> 開始時刻: %6<br /><br /> 終了時刻: %7<br /><br /> データ コード: %8|  
|0x4010310A|1074802954|DTS_MSG_EVENTLOGENTRY_VARVALCHANGE|イベント名: %1<br /><br /> メッセージ: %9<br /><br /> 演算子: %2<br /><br /> ソース名: %3<br /><br /> ソース ID: %4<br /><br /> 実行 ID: %5<br /><br /> 開始時刻: %6<br /><br /> 終了時刻: %7<br /><br /> データ コード: %8|  
|0x4010310B|1074802955|DTS_MSG_EVENTLOGENTRY_CUSTOMEVENT|イベント名: %1<br /><br /> メッセージ: %9<br /><br /> 演算子: %2<br /><br /> ソース名: %3<br /><br /> ソース ID: %4<br /><br /> 実行 ID: %5<br /><br /> 開始時刻: %6<br /><br /> 終了時刻: %7<br /><br /> データ コード: %8|  
|0x4010310C|1074802956|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|イベント名: %1<br /><br /> メッセージ: %9<br /><br /> 演算子: %2<br /><br /> ソース名: %3<br /><br /> ソース ID: %4<br /><br /> 実行 ID: %5<br /><br /> 開始時刻: %6<br /><br /> 終了時刻: %7<br /><br /> データ コード: %8|  
|0x4010310D|1074802957|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|イベント名: %1<br /><br /> メッセージ: %9<br /><br /> 演算子: %2<br /><br /> ソース名: %3<br /><br /> ソース ID: %4<br /><br /> 実行 ID: %5<br /><br /> 開始時刻: %6<br /><br /> 終了時刻: %7<br /><br /> データ コード: %8|  
|0x4010310E|1074802958|DTS_MSG_EVENTLOGENTRY_INFORMATION|イベント名: %1<br /><br /> メッセージ: %9<br /><br /> 演算子: %2<br /><br /> ソース名: %3<br /><br /> ソース ID: %4<br /><br /> 実行 ID: %5<br /><br /> 開始時刻: %6<br /><br /> 終了時刻: %7<br /><br /> データ コード: %8|  
  
##  <a name="msgSuccess"></a> 成功時のメッセージ  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の成功時のメッセージのシンボル名は、 **DTS_S_** で始まります。  
  
|16 進コード|10 進コード|シンボル名|[説明]|  
|----------------------|------------------|-------------------|-----------------|  
|0x40003|262147|DTS_S_NULLDATA|値が NULL です。|  
|0x40005|262149|DTS_S_TRUNCATED|文字列値が切り捨てられました。 バッファーで列には長すぎる文字列を受け取ったため、バッファーにより文字列が切り捨てられました。|  
|0x200001|2097153|DTS_S_EXPREVALTRUNCATIONOCCURRED|式の評価中に切り捨てが発生しました。 評価中に切り捨てが発生しました。たとえば、中間手順のある時点で発生した可能性があります。|  
  
##  <a name="msgPipeline"></a> データ フロー コンポーネントのエラー メッセージ  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のエラー メッセージのシンボル名は、 **DTSBC_E_** で始まります。"BC" は、ほとんどの Microsoft データ フロー コンポーネントが派生しているネイティブ基本クラスであることを示します。  
  
|16 進コード|10 進コード|シンボル名|[説明]|  
|----------------------|------------------|-------------------|-----------------|  
|0xC8000002|-939524094|DTSBC_E_INCORRECTEXACTNUMBEROFTOTALOUTPUTS|出力とエラー出力の合計件数 %1!lu! が正しくありません。 正しくは、%2!lu! 件である必要があります。|  
|0xC8000003|-939524093|DTSBC_E_FAILEDTOGETOUTPUTBYINDEX|インデックス %1!lu! で出力を取得できません。|  
|0xC8000005|-939524091|DTSBC_E_INCORRECTEXACTNUMBEROFERROROUTPUTS|エラー出力の件数 %1!lu! が正しくありません。 正しくは、%2!lu! 件である必要があります。|  
|0xC8000006|-939524090|DTSBC_E_INVALIDVALIDATIONSTATUSVALUE|検証状態値 "%1!lu!" が正しくありません " でサポートされていないデータ型です。  値は DTSValidationStatus 列挙に見つかったいずれかの値である必要があります。|  
|0xC8000007|-939524089|DTSBC_E_INPUTHASNOOUTPUT|入力 "%1!lu!" には、 同期出力はありません。|  
|0xC8000008|-939524088|DTSBC_E_INPUTHASNOERROROUTPUT|入力 "%1!lu!" には、 同期エラー出力はありません。|  
|0xC8000009|-939524087|DTSBC_E_INVALIDHTPIVALUE|HowToProcessInput 値 %1!lu! が無効です。 この値は、HowToProcessInput 列挙のいずれかの値である必要があります。|  
|0xC800000A|-939524086|DTSBC_E_FAILEDTOGETCOLINFO|バッファーから行 "%1!ld!"、列 "%2!ld!" の情報を 取得できませんでした。  返されたエラー コードは 0x%3!8.8X! です。|  
|0xC800000B|-939524085|DTSBC_E_FAILEDTOSETCOLINFO|行 "%1!ld!"、列 "%2!ld!" の情報を バッファーに設定できませんでした。  返されたエラー コードは 0x%3!8.8X! です。|  
|0xC800000C|-939524084|DTSBC_E_INVALIDPROPERTY|プロパティ "%1" が無効です。|  
|0xC800000D|-939524083|DTSBC_E_PROPERTYNOTFOUND|プロパティ "%1" が見つかりませんでした。|  
|0xC8000010|-939524080|DTSBC_E_READONLYPROPERTY|値を読み取り専用プロパティ "%1" に割り当てるときにエラーが発生しました。|  
|0xC8000011|-939524079|DTSBC_E_CANTINSERTOUTPUTCOLUMN|%1 では出力列を挿入できません。|  
|0xC8000012|-939524078|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCH|出力列のメタデータは、関連付けられている入力列のメタデータと一致しません。  出力列のメタデータが更新されます。|  
|0xC8000013|-939524077|DTSBC_E_OUTPUTCOLUMNSMISSING|出力列に関連付けられていない入力列があります。 出力列が追加されます。|  
|0xC8000014|-939524076|DTSBC_E_TOOMANYOUTPUTCOLUMNS|入力列に関連付けられていない出力列があります。 出力列が削除されます。|  
|0xC8000015|-939524075|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCHUNMAP|出力列のメタデータは、関連付けられている入力列のメタデータと一致しません。  入力列はマップ解除されます。|  
|0xC8000016|-939524074|DTSBC_E_UNMAPINPUTCOLUMNS|出力列に関連付けられていない入力列があります。 入力列はマップ解除されます。|  
|0xC8000017|-939524073|DTSBC_E_MULTIPLEINCOLSTOOUTCOL|同じ入力で、入力列が関連付けられている出力列に対して、別の入力列が既に関連付けられています。|  
|0xC8000018|-939524072|DTSBC_E_CANTINSERTEXTERNALMETADATACOLUMN|%1 では外部メタデータ列を挿入できません。|  
  
  
