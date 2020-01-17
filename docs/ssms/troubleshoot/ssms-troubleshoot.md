---
title: SQL Server Management Studio (SSMS) のハングまたはクラッシュをトラブルシューティングする
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: dnethi
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.date: 09/18/2019
ms.openlocfilehash: 2bfe5606c55fd0f242650e5fffdb8cc20dc9f726
ms.sourcegitcommit: 183d622fff36a22b882309378892010be3bdcd52
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2019
ms.locfileid: "71127255"
---
# <a name="get-diagnostic-data-after-a-sql-server-management-studio-ssms-crash"></a>SQL Server Management Studio (SSMS) がクラッシュした後に診断データを取得する

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

## <a name="get-full-memory-dump-after-a-hang-or-crash"></a>ハングまたはクラッシュ後に完全メモリ ダンプを取得する

SQL Server Management Studio (SSMS) がハングまたはクラッシュしたときに、その完全メモリ ダンプを取得します。

SSMS のクラッシュまたはハングをトラブルシューティングするために診断情報を取得するには、以下の手順を行います。

1. [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx) をダウンロードします。

2. ダウンロードしたものをフォルダーに解凍します。

3. コマンド プロンプトを開き、次のコマンドを実行します。

    ```console
    <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    使用許諾契約書に同意するように求められた場合は、 *[同意する]* を選択します。

4. SSMS をまだ起動していない場合は起動します。

5. 問題を再現します。

6. ダンプ ファイルの書き込みに関する cmd プロンプトにテキストが表示されるはずです。書き込みが完了するまで待ちます。

7. 新しいフォルダーを作成し、そのフォルダーに書き込む *.dmp ファイルをコピーします。

8. 次のファイルを同じフォルダーにコピーします。

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. フォルダーを圧縮する

## <a name="get-full-memory-dump-for-an-outofmemoryexception"></a>OutOfMemoryException の完全メモリ ダンプを取得する

OutOfMemoryException がスローされるとき、SSMS の完全メモリ ダンプを取得する

あらゆる管理対象の例外について、完全メモリ ダンプを取得できます。

SSMS から OutOfMemoryException の問題を解決するための診断情報を取得するには、以下の手順を行います。

1. [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx) をダウンロードします。

2. ダウンロードしたものをフォルダーに解凍します。

3. コマンド プロンプトを開き、次のコマンドを実行します。

    ```console
    <PathToProcDumpFolder>\procdump.exe -e 1 -f System.OutOfMemoryException -ma -w ssms.exe
    ```

    使用許諾契約書に同意するように求められた場合は、 *[同意する]* を選択します。

4. SQL Server Management Studio をまだ起動していない場合は起動します。

5. 問題を再現します。

6. ダンプ ファイルの書き込みに関する cmd プロンプトにテキストが表示されるはずです。書き込みが完了するまで待ちます。

7. 新しいフォルダーを作成し、そのフォルダーに書き込む *.dmp ファイルをコピーします。

8. 次のファイルを同じフォルダーにコピーします。

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. フォルダーを圧縮します。
