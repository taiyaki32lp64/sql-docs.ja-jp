---
title: サポートされていない Visual FoxPro コマンドと関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- FoxPro ODBC driver [ODBC], commands and functions
- functions [ODBC], Visual FoxPro
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro commands and functions
- FoxPro ODBC driver
ms.assetid: afdb6b7e-738d-42ca-8053-67ae50873ca6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db6aff35944b8811e79627c6076ab61e838edf3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912324"
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>サポートされていない Visual FoxPro コマンドと関数 (Visual FoxPro ODBC ドライバー)
次の表には、FoxPro コマンドとは、Visual FoxPro ODBC ドライバーではサポートされていませんが、Microsoft® Visual FoxPro® でサポートされている関数が一覧表示します。  
  
 ルール、トリガー、既定値にデータをやり取りするアプリケーション、またはストアド プロシージャは、これらの Visual FoxPro コマンドまたは関数を呼び出し、ドライバーはエラーを生成できます。  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>サポートされていない Visual FoxPro コマンドと関数  
  
||||  
|-|-|-|  
|# #UNDEF の DEFINE ...>|#IF... #ENDIF プリプロセッサ ディレクティブ|#IFDEF &#124; #IFNDEF|  
|#INCLUDE プリプロセッサ ディレクティブ|::スコープ解決演算子|! コマンド (実行を参照してください&#124;!。 コマンドを使用)|  
|? &#124; ?? Command|??? Command|\ &#124; \\\ コマンド|  
|@ ...ボックス コマンド|@ ...クラスのコマンド|@ ...クリア コマンド|  
|@ ...編集 - ボックスのコマンドを編集|@ ...コマンドを入力します。|@ ...GET|  
|@ ...メニュー コマンド|@ ...コマンド プロンプト|@ ...コマンドを言う|  
|@ ...スクロール コマンド|@ ...コマンドに||  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|コマンドをそのまま使用します。|ACLASS () 関数|メニュー コマンドをアクティブ化します。|  
|ポップアップのコマンドをアクティブ化します。|画面のコマンドをアクティブ化します。|ウィンドウのコマンドをアクティブ化します。|  
|ActivateCell メソッド|クラスのコマンドを追加します。|ADIR () 関数|  
|受けるフォントサーバの指定 () 関数|AINSTANCE () 関数|_ALIGNMENT システム メモリ変数|  
|AMEMBERS () 関数|ANSITOOEM () 関数|APRINTERS () 関数|  
|ASELOBJ () 関数|コマンドを支援します。||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|() 関数バー|BARCOUNT () 関数|BARPROMPT( ) Function|  
|_BEAUTIFY システム メモリ変数|システム メモリ変数のボックス (_b)|コマンドを参照します。|  
|_BROWSER システム メモリ変数|アプリのコマンドをビルドします。|ビルドの EXE コマンド|  
|ビルド プロジェクト コマンド|_BUILDER システム メモリ変数||  
  
## <a name="c"></a>c  
  
||||  
|-|-|-|  
|_CALCVALUE システム メモリ変数|_CLIPTEXT システム メモリ変数|_CONVERTER システム メモリ変数|  
|_CUROBJ システム メモリ変数|コマンドを呼び出す|コマンドをキャンセルします。|  
|CAPSLOCK () 関数|CD コマンド|変更コマンド|  
|CHDIR コマンド|CHRSAW () 関数|メモを閉じるコマンド|  
|CNTBAR () 関数|CNTPAD () 関数|COL () 関数|  
|コマンドをコンパイルします。|データベース コマンドをコンパイルします。|フォームのコマンドをコンパイルします。|  
|COMPOBJ () 関数|コンテナー オブジェクト|コントロール オブジェクト|  
|ファイルのコマンドをコピーします。|メモのコマンドをコピーします。|クラスのコマンドを作成します。|  
|CLASSLIB コマンドを作成します。|色の SET コマンドを作成します。|コマンドを作成します。|  
|接続コマンドを作成します。|データベース コマンドを作成します。|フォームのコマンドを作成します。|  
|コマンドを作成します。|ラベルのコマンドを作成します。|メニュー コマンドを作成します。|  
|プロジェクトのコマンドを作成します。|クエリ コマンドを作成します。|レポート コマンドを作成します。|  
|画面のコマンドを作成します。|SQL ビューのコマンドを作成します。|トリガーのコマンドを作成します。|  
|ビューのコマンドを作成します。|CREATEOBJECT () 関数|CURDIR () 関数|  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|_DBLCLICK システム メモリ変数|_DIARYDATE システム メモリ変数|DBSETPROP () 関数|  
|DDE 関数|メニュー コマンドを非アクティブ化します。|ポップアップのコマンドを非アクティブ化します。|  
|ウィンドウのコマンドを非アクティブ化します。|宣言の DLL コマンド|コマンドを宣言します。|  
|コマンド バーの定義します。|ボックスのコマンドを定義します。|クラスのコマンドを定義します。|  
|メニュー コマンドを定義します。|パッドのコマンドを定義します。|ポップアップ コマンドを定義します。|  
|ウィンドウのコマンドを定義します。|接続コマンドを削除します。|データベース コマンドを削除します。|  
|ファイルのコマンドを削除します。|DELETE トリガー コマンド|ビューのコマンドを削除します。|  
|DIR コマンド|ディレクトリのコマンド|表示コマンド|  
|接続コマンドの表示|データベース コマンドの表示|DLL コマンドの表示|  
|ファイルをコマンドの表示|表示メモリ コマンド|オブジェクトのコマンドの表示|  
|プロシージャのコマンドを表示|表示状態コマンド|構造体のコマンドを表示|  
|テーブルのコマンドを表示|ビューのコマンドを表示|コマンドをによって形成します。|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|コマンドを編集します。|エラー コマンド||  
|コマンドを消去します。|外部コマンド|[エクスポート] コマンド|  
|コマンドを取り出す|ページのコマンドを取り出す||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|_FOXDOC システム メモリ変数|_FOXGRAPH システム メモリ変数|FEOF () 関数|  
|FCLOSE () 関数|FCREATE () 関数|FGETS () 関数|  
|FERROR () 関数|FFLUSH () 関数|FKLABEL () 関数|  
|フィルター コマンド|FIND コマンド|FOPEN () 関数|  
|FKMAX () 関数|FONTMETRIC () 関数|FSEEK 定数 () 関数|  
|FPUTS () 関数|FREAD () 関数||  
|FWRITE () 関数|FCHSIZE () 関数||  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|_GENGRAPH システム メモリ変数|_GENMENU システム メモリ変数|_GENPD システム メモリ変数|  
|_GENSCRN システム メモリ変数|_GENXTAB システム メモリ変数|GETBAR () 関数|  
|GETCOLOR () 関数|GETDIR () 関数|GETEXPR コマンド|  
|GETFILE () 関数|GETFONT () 関数|GETOBJECT () 関数|  
|GETPAD () 関数|GETPICT () 関数|GETPRINTER () 関数|  
  
## <a name="h"></a>H  
  
||||  
|-|-|-|  
|コマンドのヘルプ|メニュー コマンドを非表示にします。|ポップアップのコマンドを非表示にします。|  
|ウィンドウのコマンドを非表示にします。|ホーム () 関数||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IMESTATUS () 関数|IMPORT コマンド|入力コマンド|  
|コマンドのインデックス|リンクキー () 関数|ISCOLOR () 関数|  
|コマンドを挿入します。|INSMODE () 関数||  
|ISMOUSE () 関数|システム メモリ変数の (_i)||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|結合 コマンド|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|キーボード コマンド|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|_LMARGIN システム メモリ変数|コマンドのラベル|LASTKEY () 関数|  
|LINENO () 関数|コマンドを一覧表示|接続の一覧表示コマンド|  
|読み込みコマンド|LOCFILE () 関数||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|MCOL () 関数|MD コマンド|メニュー コマンドを|  
|メモリ () 関数|メニュー コマンド|MKDIR コマンド|  
|メニュー () 関数|メッセージ ボックス () 関数|接続コマンドを変更します。|  
|クラスのコマンドを変更します。|コマンドのコマンドを変更します。|フォームのコマンドを変更します。|  
|データベース コマンドを変更します。|ファイルのコマンドを変更します。|メモのコマンドを変更します。|  
|[全般] コマンドを変更します。|コマンドのラベルを変更します。|プロジェクトのコマンドを変更します。|  
|メニュー コマンドを変更します。|プロシージャのコマンドを変更します。|画面のコマンドを変更します。|  
|クエリ コマンドを変更します。|レポート コマンドを変更します。|ウィンドウのコマンドを変更します。|  
|コマンドの構造を変更します。|コマンドの表示を変更します。|移動ウィンドウ コマンド|  
|マウス コマンド|移動 ポップアップ コマンド|MROW () 関数|  
|MRKBAR () 関数|MRKPAD () 関数||  
|MWINDOW () 関数|MDOWN () 関数||  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NUMLOCK () 関数|||  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|OBJNUM () 関数|OBJTOCLIENT () 関数|コマンド バーに|  
|OEMTOANSI () 関数|APLABOUT コマンド|ON EXIT メニュー コマンド|  
|エスケープ コマンド|終了バー コマンド|キー = コマンド|  
|ON EXIT パッド コマンド|ON EXIT ポップアップ コマンド|ON パッド コマンド|  
|キーのラベル コマンド|MACHELP コマンド|選択バー コマンド|  
|ページのコマンドで|READERROR コマンド|[選択] ポップアップ コマンドで|  
|メニュー コマンドを選択します|埋め込みコマンドを選択します||  
|シャット ダウン コマンド|持つ OBJVAR () 関数||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|_PADVANCE システム メモリ変数|_PAGENO システム メモリ変数|_PBPAGE システム メモリ変数|  
|_PCOLNO システム メモリ変数|_PCOPIES システム メモリ変数|_PDRIVER システム メモリ変数|  
|_PDSETUP システム メモリ変数|_PECODE システム メモリ変数|_PEJECT システム メモリ変数|  
|_PEPAGE システム メモリ変数|_PLENGTH システム メモリ変数|_PLINENO システム メモリ変数|  
|_PLOFFSET システム メモリ変数|_PPITCH システム メモリ変数|_PQUALITY システム メモリ変数|  
|_PRETEXT システム メモリ変数|_PSCODE システム メモリ変数|_PSPACING システム メモリ変数|  
|_PWAIT システム メモリ変数|PACK データベース コマンド|パッド () 関数|  
|PCOL () 関数|PEMSTATUS () 関数|再生マクロ コマンド|  
|ポップアップ キー コマンド|ポップアップ メニュー コマンド|POP ポップアップ コマンド|  
|ポップアップ () 関数|プリントしています.ENDPRINTJOB コマンド|PRINTSTATUS () 関数|  
|PRMBAR () 関数|PRMPAD () 関数|プロンプト () 関数|  
|PROW () 関数|PRTINFO () 関数|プッシュの主要なコマンド|  
|メニュー コマンドをプッシュします。|プッシュ ポップアップ コマンド|PUTFILE () 関数|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|コマンドを終了します。|||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|_RMARGIN システム メモリ変数|RD コマンド|READKEY () 関数|  
|コマンドを読み取り|メニュー コマンドを読み取り|リリース バー コマンド|  
|REFRESH() 関数|コマンドを再作成します。|リリース ライブラリ コマンド|  
|リリース CLASSLIB コマンド|リリース コマンド|リリース パッド コマンド|  
|リリース メニュー コマンド|モジュールのコマンドをリリース|リリースの WINDOWS のコマンド|  
|リリースのポップアップ コマンド|リリース PROCEDURE コマンド|コマンドの名前を変更します。|  
|クラスのコマンドを削除します。|クラスのコマンドの名前を変更します。|ビューのコマンドの名前を変更します。|  
|接続コマンドの名前を変更します。|TABLE コマンドの名前を変更します。|コマンドから復元します。|  
|レポート コマンド|REQUERY () 関数|ウィンドウのコマンドを復元します。|  
|マクロのコマンドを復元します。|画面のコマンドを復元します。|RGBSCHEME () 関数|  
|再開コマンド|RGB () 関数|実行&#124;! Command|  
|RMDIR コマンド|行 () 関数||  
|RUNSCRIPT コマンド|RDLEVEL () 関数||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|コマンドを保存します。|画面のコマンドを保存します。|コマンドへの保存します。|  
|WINDOWS のコマンドを保存します。|スキーム () 関数|SCOLS () 関数|  
|スクロール コマンド|_SCREEN システム メモリ変数|SET コマンド|  
|代替の SET コマンド|SET ANSI コマンド|SET APLABOUT コマンド|  
|セットの自動保存のコマンド|SET ベル コマンド|SET 点滅コマンド|  
|SET 境界線コマンド|SET BRSTATUS コマンド|SET CLASSLIB コマンド|  
|セットのクリア コマンド|セット時刻コマンド|色を設定するコマンドの|  
|スキームのコマンドの色を設定します。|SET 色セット コマンド|コマンドに色を設定します。|  
|互換性のあるコマンドのセット|セットの確認コマンド|コンソール コマンドのセット|  
|セット CPCOMPILE|セット CPDIALOG|通貨の SET コマンド|  
|SET CURSOR コマンド|SET DATASESSION コマンド|デバッグ コマンドのセット|  
|10 進数の SET コマンド|区切り記号の SET コマンド|SET 開発コマンド|  
|デバイス コマンドのセット|セットの表示コマンド|SET DOHISTORY コマンド|  
|SET ECHO コマンド|SET エスケープ コマンド|セットの形式のコマンド|  
|SET 関数コマンド|SET 見出しコマンド|SET ヘルプ コマンド|  
|SET HELPFILTER コマンド|SET 強度コマンド|SET KEY コマンド|  
|SET KEYCOMP コマンド|SET LOGERRORS コマンド|SET MACDESKTOP コマンド|  
|SET MACHELP コマンド|SET MACKEY コマンド|SET 余白コマンド|  
|コマンドのセットがマーク|コマンドにマークを設定します。|SET MEMOWIDTH コマンド|  
|メッセージの SET コマンド|マウスの SET コマンド|SET 走行距離計コマンド|  
|Oleobject クラスの SET コマンド|SET パレット コマンド|SET PDSETUP コマンド|  
|ポイントの設定コマンド|プリンターの SET コマンド|SET READBORDER コマンド|  
|REFRESH コマンドのセット|リソースの SET コマンド|安全性の SET コマンド|  
|SET スコアボード コマンド|SET 秒コマンド|区切り記号の SET コマンド|  
|SET SHADOWS コマンド|スキップする一連のコマンド|SET 領域コマンド|  
|セットの状態コマンド|ステータス バーのコマンドを設定します。|ステップ コマンドのセット|  
|SET スティッキー コマンド|SET SYSFORMATS コマンド|SET SYSMENU コマンド|  
|SET トーク コマンド|SET TEXTMERGE コマンド|SET TEXTMERGE 区切り記号のコマンド|  
|SET トピック コマンド|トピック ID の SET コマンド|SET TRBETWEEN コマンド|  
|SET TYPEAHEAD コマンド|セットの表示コマンド|メモのコマンドのセットのウィンドウ|  
|SET XCMDFILE コマンド|_SHELL システム メモリ変数|GET コマンドを表示します。|  
|表示するコマンドを取得します。|メニュー コマンドを表示します。|オブジェクトのコマンドを表示します。|  
|ポップアップの表示コマンド|ウィンドウのコマンドを表示します。|サイズのポップアップ コマンド|  
|サイズのウィンドウ コマンド|SKPBAR () 関数|SKPPAD () 関数|  
|SOUNDEX () 関数|_SPELLCHK システム メモリ変数|SQL 関数|  
|SROWS () 関数|_STARTUP システム メモリ変数|中断コマンド|  
|SYS(2011) 除く SYS() 関数|SYSMETRIC () 関数||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TABS システム メモリ変数|テキストの.ENDTEXT コマンド|[Txtwidth] () 関数|  
|変換 () 関数|_TRANSPORT システム メモリ変数||  
|コマンドの種類|_THROTTLE システム メモリ変数||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|更新 () 関数|コマンドを使用します。||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|データベース コマンドを検証します。|VARREAD () 関数|バージョン () 関数|  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|システム メモリ変数の (_w)|_WIZARD システム メモリ変数|WCHILD () 関数|  
|コマンドを待機します。|WBORDER () 関数|WFONT () 関数|  
|WCOLS () 関数|WEXIST () 関数|WLROW () 関数|  
|しています.ENDWITH コマンド|WLAST () 関数|WONTOP () 関数|  
|WMAXIMUM () 関数|WLCOL () 関数|WREAD () 関数|  
|WOUTPUT () 関数|WMINIMUM () 関数|WVISIBLE () 関数|  
|WPARENT () 関数|WTITLE () 関数||  
|WROWS () 関数|_WRAP システム メモリ変数||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|ズーム ウィンドウ コマンド|||
