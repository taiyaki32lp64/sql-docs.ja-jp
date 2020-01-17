---
title: Linux と macOS での ODBC ドライバーによるデータ アクセスのトレース | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data access tracing
- tracing
ms.assetid: 3149173a-588e-47a0-9f50-edb8e9adf5e8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1fa39cd11f70a661de5c284e56f2ccc0f7a5777f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008824"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Linux と macOS での ODBC ドライバーによるデータ アクセスのトレース

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

MacOS と Linux の unixODBC Driver Manager は、ODBC API 呼び出しの開始と、ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の終了のトレースをサポートしています。

アプリケーションの ODBC 動作をトレースするには、 `odbcinst.ini`ファイルの`[ODBC]`セクションを編集して`Trace=Yes` 、 `TraceFile`トレース出力を格納するファイルのパスに値とを設定します。次に例を示します。

```ini
[ODBC]
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```

(またはその他`/dev/stdout`のデバイス名を使用して、永続的なファイルではなく、トレース出力を送信することもできます)。上記の設定では、アプリケーションが unixODBC Driver Manager を読み込むたびに、出力ファイルに対して実行したすべての ODBC API 呼び出しが記録されます。

アプリケーションのトレースが終了したら、 `Trace=Yes` `odbcinst.ini`ファイルからを削除して、トレースのパフォーマンスが低下しないようにし、不要なトレースファイルが削除されていることを確認します。

トレースは、`odbcinst.ini` 内のドライバーを使用するすべてのアプリケーションに適用されます。 すべてのアプリケーションをトレースしない (ユーザーごとの機密情報の公開を避けるためなど) 場合は、`ODBCSYSINI` 環境変数を使用して、プライベート `odbcinst.ini` の場所を指定することにより、個々のアプリケーション インスタンスをトレースできます。 例:

```bash
$ ODBCSYSINI=/home/myappuser myapp
```

この場合は、の`Trace=Yes` `[ODBC Driver 13 for SQL Server]` `/home/myappuser/odbcinst.ini`セクションにを追加できます。

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>ドライバーが使用している odbc.ini ファイルを特定する

Linux および macOS ODBC ドライバーは、使用`odbc.ini`されているものやファイルの`odbc.ini`パスを認識していません。 ただし、使用され`odbc.ini`ているファイルに関する情報は、unixODBC ツール`odbc_config`と`odbcinst`、unixODBC Driver Manager ドキュメントから入手できます。

たとえば、次のコマンドは、(他の情報と一緒に) システム DSN とユーザー DSN をそれぞれ格納するシステムおよびユーザーの `odbc.ini` ファイルの場所を出力します。

```
$ odbcinst -j
unixODBC 2.3.1
DRIVERS............: /etc/odbcinst.ini
SYSTEM DATA SOURCES: /etc/odbc.ini
FILE DATA SOURCES..: /etc/ODBCDataSources
USER DATA SOURCES..: /home/odbcuser/.odbc.ini`
SQLULEN Size.......: 8
SQLLEN Size........: 8
SQLSETPOSIROW Size.: 8
```

[UnixODBC のドキュメント](http://www.unixodbc.org/doc/UserManual/)では、ユーザーとシステムの dsn の違いについて説明します。 概要:

- ユーザー Dsn---は、特定のユーザーのみが使用できる Dsn です。 ユーザーは、独自のユーザー Dsn を使用して接続したり、追加、変更、および削除したりできます。 ユーザー Dsn は、ユーザーのホームディレクトリまたはそのサブディレクトリ内のファイルに格納されます。

- これらの Dsn---システム Dsn は、システム上のすべてのユーザーがそれらを使用して接続することができますが、システム管理者は追加、変更、および削除のみを行うことができます。 ユーザー dsn がシステム DSN と同じ名前のユーザー DSN を持っている場合、そのユーザーが接続するときにユーザー DSN が使用されます。

## <a name="see-also"></a>参照

- [プログラミング ガイドライン](../../../connect/odbc/linux-mac/programming-guidelines.md)
