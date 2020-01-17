---
title: SQL Server Management Studio (SSMS) の問題を解決する目的で完全メモリ ダンプを取得する
Description: 完全メモリ ダンプを収集することで、SSMS のハングやクラッシュの問題を解決する
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
ms.reviewer: dineth, sstein
ms.custom: ''
ms.date: 05/17/2019
ms.openlocfilehash: 95beb87d72295f4f5ea10b5bb33476d4d27af628
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266723"
---
# <a name="get-full-memory-dump"></a>完全メモリ ダンプの取得

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

この記事では、SQL Server Management Studio (SSMS) で発生するクラッシュやハングを解決する目的で診断情報を取得する方法について紹介します。

問題解決のために診断情報を取得するには、以下の手順を行います。

1. [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx) をダウンロードします。

2. ダウンロードしたものをフォルダーに解凍します。

3. コマンド プロンプトを開き (`cmd.exe` など)、次のコマンドを実行します。

    ```
    <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    使用許諾契約書に同意するように求められるので、 **[同意する]** を選択します。

4. SQL Server Management Studio (SSMS) をまだ起動していない場合は起動します。

5. 問題を再現します。

6. ダンプ ファイルの書き込みに関する cmd プロンプトにテキストが表示されるはずです。書き込みが完了するまで待ちます。

7. 新しいフォルダーを作成し、そのフォルダーに書き込む *.dmp ファイルをコピーします。

8. 次のファイルを同じフォルダーにコピーします。

    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. フォルダーを圧縮します。

## <a name="outofmemoryexception"></a>OutOfMemoryException

OutOfMemoryException (あらゆる管理対象例外) がスローされたら、SSMS の完全メモリ ダンプも取得できます。

SSMS から OutOfMemoryException の問題を解決するための診断情報を取得するには、以下の手順を行います。

1. [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx) をダウンロードします。

2. ダウンロードしたものをフォルダーに解凍します。

3. コマンド プロンプトを開き、次のコマンドを実行します。

    ```cmd
    <PathToProcDumpFolder>\procdump.exe -e 1 -f System.OutOfMemoryException -ma -w ssms.exe
    ```

    使用許諾契約書に同意するように求められるので、 **[同意する]** を選択します。

4. SQL Server Management Studio をまだ起動していない場合は起動します。

5. 問題を再現します。

6. ダンプ ファイルの書き込みに関する cmd プロンプトにテキストが表示されるはずです。書き込みが完了するまで待ちます。

7. 新しいフォルダーを作成し、そのフォルダーに書き込む *.dmp ファイルをコピーします。

8. 次のファイルを同じフォルダーにコピーします。

    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. フォルダーを圧縮します。

## <a name="share-the-information"></a>情報を共有する

1. SSMS チームと情報を共有するには、 https://aka.ms/sqlfeedback で問題を記録します。

2. さらに、ファイルを収集できる OneDrive (または同等のもの) に収集したメモリ ダンプ ファイルを共有します。

    > [!Important]
    > メモリ ダンプ ファイルには機密情報が含まれている場合があります。

## <a name="next-steps"></a>次の手順

[SQL Server Management Studio](../sql-server-management-studio-ssms.md)