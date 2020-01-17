---
title: ODBC Visual FoxPro セットアップ ダイアログ ボックス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], installing
- FoxPro ODBC driver [ODBC], installing
ms.assetid: de020197-7f53-4643-9cbf-b7887ba88de9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d9aa8954cd42ac715b3e6e67e0b0add69d07a570
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915660"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>ODBC Visual FoxPro セットアップ ダイアログ ボックス
**ODBC Visual FoxPro セットアップ**ダイアログ ボックスでは、Visual FoxPro データ ソースの変更を追加することができます。  
  
 ドライバーをダウンロードするには、次を参照してください。 [Visual FoxPro ODBC ドライバーのダウンロード サイト](https://go.microsoft.com/fwlink/?LinkId=121318)します。  
  
## <a name="dialog-box-options"></a>ダイアログ ボックスのオプション  
 **データ ソース名**  
 データ ソースを使用する名前を入力します。  
  
 **[説明]**  
 データ ソースの説明を入力します。  
  
 **データベースの種類**  
 データ ソースに接続データベースの種類を選択できます。  
  
 **Visual FoxPro データベース (します。DBC)**  
 Visual foxpro データ ソースを接続することを指定します。[データベース](../../odbc/microsoft/visual-foxpro-terminology.md)(.dbc ファイル) と、すべてのテーブルおよびデータベースのローカル ビュー。  
  
 **無料のテーブルのディレクトリ**  
 データ ソースのディレクトリに接続することを指定します。[テーブルを無料](../../odbc/microsoft/visual-foxpro-terminology.md)します。 すべて[データベース](../../odbc/microsoft/visual-foxpro-terminology.md)など、同じディレクトリ内のテーブルは ODBC カタログ関数によって無視されます[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)または[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)します。 テーブルにデータベースを経由して送信される SQL SELECT ステートメントを使用してアクセスできる[SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md)と[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)します。  
  
 **[パス]**  
 データベースまたはデータ ソースに接続する無料のテーブルのディレクトリの名前とパスが表示されます。  
  
 **[参照]**  
 システムとのデータベースまたはディレクトリのデータ ソースに接続するネットワークを検索できます。  
  
 **[オプション]**  
 Visual FoxPro ODBC ドライバーのオプションを設定できるように、ダイアログ ボックスを展開します。  
  
## <a name="driver"></a>Driver  
 **照合順序**  
 フィールドの並べ替えシーケンス。 既定の順序は、オペレーティング システムの言語バージョンでサポートされているシーケンスを反映します。 サポートされている照合順序の一覧は、次を参照してください。 [COLLATE 設定](../../odbc/microsoft/set-collate-command.md)します。  
  
 **[Exclusive]**  
 このチェック ボックスがオンの場合、データ ソースを使用してデータにアクセスするときにのみ、ドライバー、Visual FoxPro データベースが開きます。 他のユーザーは、データベースが排他的に開かれたときに、データベースまたはデータベース内のテーブル アクセスできません。 排他的に開かれているデータベース内のテーブルは、共有として開かれます。 排他的にテーブルを開くには、使用、[排他設定](../../odbc/microsoft/set-exclusive-command.md)コマンド。 このチェック ボックスが無効になっているときに**データベースの種類**に設定されている**無料テーブル ディレクトリ**します。  
  
 **Null**  
 ALTER TABLE と CREATE TABLE で作成される列が null 値を許容するかどうかを判断します。 Null に設定すると、ある場合、INSERT - SQL は INSERT - SQL に含まれていない任意の列に null 値を挿入しています.VALUE 句。 Null が OFF の場合は空白が挿入されます。 次のコードのように渡された接続文字列で、このオプションを制御することもできます。  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **削除**  
 削除済みとしてマークされている行が返されるかどうかを判断します。 次のコードのように渡された接続文字列で、このオプションを制御することもできます。  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **バック グラウンドでデータをフェッチします。**  
 レコードが (プログレッシブの取得)、バック グラウンドでフェッチされるかどうか、または、アプリケーションは、結果セット内のすべてのレコードがフェッチされるまでに待機を決定します。
