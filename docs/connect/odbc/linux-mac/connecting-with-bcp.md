---
title: Bcp | を使用した接続Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bcp
ms.assetid: 3eca5717-e50f-40db-be16-a1cebbdfee70
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1dd80df3a0f7fabec7ae9ddc51b16cb4456c7970
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996620"
---
# <a name="connecting-with-bcp"></a>bcp による接続
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[bcp](https://go.microsoft.com/fwlink/?LinkID=190626) ユーティリティは、Linux および macOS では [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] にあります。 このページでは、の Windows バージョンとの`bcp`違いについて説明します。
  
- フィールド ターミネータはタブ ("\t") です。  
  
- 行ターミネータは改行 ("\n") です。  
  
- 拡張文字を含まない `bcp` フォーマット ファイルとデータ ファイルでは、文字モードが推奨される形式です。  
  
> [!NOTE]  
> コマンドライン引数のバックスラッシュ '\\' は、引用符で囲むか、エスケープする必要があります。 たとえば、ユーザー設定の行ターミネータとして改行を指定する場合、次のいずれかのメカニズムを使用する必要があります。  
>   
> -   -r\\\n  
> -   -r"\n"  
> -   -r'\n'  
  
次に、テーブルの行をテキスト ファイルにコピーする `bcp` コマンド呼び出しの例を示します。  
  
```  
bcp AdventureWorks2008R2.Person.Address out test.dat -Usa -Pxxxx -Sxxx.xxx.xxx.xxx  
```  
  
## <a name="available-options"></a>利用可能なオプション
現在のリリースでは、次の構文およびオプションを使用できます。  

[_データベース_ **.** ] _スキーマ_ **.** _テーブル_**in**_データ\_ファイル_ | **の出力** _データ\_ファイル_

- -a *packet_size*  
サーバーとの間で送信されるネットワーク パケットごとのバイト数を指定します。  
  
- -b *batch_size*  
一括インポートするデータの行数を指定します。  
  
- -c  
文字データ型を使用します。  
  
- -d *database_name*  
接続先のデータベースを指定します。  
  
- -d  
`bcp` -S オプションに渡された値が、データ ソース名 (DSN) として解釈されるようにします。 詳細については、「[Connecting with sqlcmd](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)」 (sqlcmd による接続) の「DSN Support in sqlcmd and bcp」 (sqlcmd および bcp の DSN サポート) を参照してください。  
  
- -e *error_file* `bcp` ユーティリティがファイルからデータベースに転送できなかった行を格納するエラー ファイルの完全パスを指定します。  
  
- -E  
ID 列に、インポートされたデータ ファイルの ID 値を使用します。  
  
- -f *format_file*  
フォーマット ファイルの完全パスを指定します。  
  
- -F *first_row*  
テーブルからエクスポートする最初の行、またはデータ ファイルからインポートする最初の行の番号を指定します。  
  
- -k  
一括コピー操作時、空の列には、挿入される列の既定値ではなく、NULL 値が保持されます。  
  
- -l  
ログインのタイムアウトを指定します。 \- l オプションでは、サーバーへの接続の試行時に、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] へのログインがタイムアウトするまでの秒数を指定します。 既定のログインタイムアウトは15秒です。 ログイン タイムアウトは、0 から 65,534 の数値にする必要があります。 指定した値が数値以外の場合、または範囲外の場合、`bcp` はエラー メッセージを生成します。 値が0の場合は、タイムアウトが無制限であることを示します。
  
- -L *last_row*  
テーブルからエクスポートする最後の行、またはデータ ファイルからインポートする最後の行の番号を指定します。  
  
- -m *max_errors*  
`bcp` 操作を取り消す前に発生することのできる構文エラーの最大数を指定します。  
  
- -n  
データのネイティブの (データベース) データ型を使用して一括コピー操作を実行します。  
  
- -P *password*  
ログイン ID のパスワードを指定します。  
  
- -Q  
`bcp` ユーティリティと [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスとの接続で、SET QUOTED_IDENTIFIERS ON ステートメントを実行します。  
  
- -r *row_terminator*  
行ターミネータを指定します。  
  
- -r  
通貨、日付、時刻のデータを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に一括コピーする場合に、クライアント コンピューターのロケール設定に定義された地域別設定が使用されます。  
  
- -S *server*  
接続先の[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンスの名前を指定します。または、-D が使用されている場合は、DSN を指定します。  
  
- -t *field_terminator*  
フィールド ターミネータを指定します。  
  
- -T  
`bcp` ユーティリティが信頼関係接続 (統合セキュリティ) を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続することを指定します。  
  
- -U *login_id*  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]への接続に使用されるログイン ID を指定します。  
  
- -V  
`bcp` ユーティリティ バージョン番号と著作権に関する情報を報告します。  
  
- -w  
Unicode 文字を使用して一括コピー操作を実行します。  
  
このリリースでは、Latin-1 および UTF-16 文字がサポートされています。  
  
## <a name="unavailable-options"></a>利用できないオプション
現在のリリースでは、次の構文とオプションは利用できません。  

- -c  
データ ファイル内のデータのコード ページを指定します。  
  
- -h *hint*  
データをテーブルまたはビューに一括インポートするときに使用するヒントを指定します。  
  
- -i *input_file*  
応答ファイルの名前を指定します。  
  
- -n  
文字ではないデータにはネイティブな (データベース) データ型を使用し、文字データには Unicode 文字を使用します。  
  
- -o *output_file*  
コマンド プロンプトからリダイレクトされた出力を受け取るファイル名を指定します。  
  
- -V (80 | 90 | 100)  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の以前のバージョンのデータ型を使用します。  
  
- -X  
フォーマットおよび -f format_file オプションと共に使用し、既定の XML ではないフォーマット ファイルの代わりに XML ベースのフォーマット ファイルを生成します。  
  
## <a name="see-also"></a>参照

[**sqlcmd** による接続](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)  
