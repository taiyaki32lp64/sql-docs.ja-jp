---
title: このバージョンの Driver for SQL Server の既知の問題 |Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c3508277502ad7e3eb3b0e7ff048301c8ed1efdd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008780"
---
# <a name="known-issues-in-this-version-of-the-driver"></a>このバージョンのドライバーの既知の問題

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

この記事では、Linux と macOS 上の Microsoft ODBC Driver 13、13.1、17 for SQL Server に関する既知の問題の一覧を示します。

その他の問題は、 [Microsoft ODBC ドライバー チームのブログ](https://blogs.msdn.com/b/sqlnativeclient/)に投稿されます。  

- Windows、Linux、および macOS では、私用領域 (PUA) またはエンド ユーザー定義文字 (EUDC) の文字を異なる方法で変換します。 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 内のサーバーで実行される変換では、Windows 変換ライブラリを使用します。 ドライバーでの変換では、Windows、Linux、または macOS 変換ライブラリを使用します。 各ライブラリは、これらの変換を実行するときに異なる結果を生成する可能性があります。 詳細については、「[エンド ユーザーによって定義されており、秘密の使用領域文字](/windows/desktop/Intl/end-user-defined-characters)」を参照してください。

- クライアント エンコードが UTF-8 の場合、ドライバー マネージャーは、UTF-8 から UTF-16 へ常に正しく変換するとは限りません。 現時点では、文字列内の 1 つ以上の文字が有効な UTF-8 文字でない場合、データの破損が発生します。 ASCII 文字は正しくマップされます。 SQLCHAR バージョンの ODBC API (たとえば、SQLDriverConnectA) を呼び出すときに、ドライバー マネージャーはこの変換を試行します。 SQLWCHAR バージョンの ODBC API (たとえば、SQLDriverConnectW) を呼び出す際には、ドライバー マネージャーはこの変換を試行しません。  

- **SQLBindParameter** の *ColumnSize* パラメーターは SQL 型の文字数を示し、*BufferLength* はアプリケーションのバッファー内のバイト数を示します。 ただし、SQL データ型が `varchar(n)` または `char(n)` で、アプリケーションがパラメーターを SQL_C_CHAR または SQL_C_VARCHAR としてバインドし、クライアントの文字エン コードが UTF-8 の場合は、*ColumnSize* の値がサーバー上のデータ型のサイズに揃っていても、ドライバーから "文字列データの右側が切り捨てられました" というエラーを受け取る可能性があります。 このエラーは、文字エンコード間の変換によってデータの長さが変更された場合に発生します。 たとえば、正しいアポストロフィ文字 (U+2019) が CP-1252 では半角の 0x92 としてエンコードされたが、UTF-8 では 3 バイトのシーケンス 0xe2 0x80 0x99 としてエンコードされた場合です。

たとえば、エンコードが UTF-8 の場合に、out パラメーターに対して **SQLBindParameter** の *BufferLength* と *ColumnSize* の両方に 1 を指定してから、(CP-1252 を使用して) サーバー上の `char(1)` 列に格納されている前の文字を取得しようとすると、ドライバーはこの文字を 3 バイトの UTF-8 エンコードに変換しようとしますが、結果は 1 バイトのバッファーに収まりません。 逆方向では、クライアントとサーバー上の異なるコード ページ間で変換を行う前に、ドライバーは *ColumnSize* を **SQLBindParameter** の *BufferLength* と比較します。 *ColumnSize* 1 が *BufferLength* (たとえば) 3 より小さいので、ドライバーはエラーを生成します。 このエラーを回避するには、変換後のデータの長さが、指定したバッファーまたは列に適合することを確認します。 `varchar(n)` 型では、*ColumnSize* を 8000 よりも大きくすることはできません。

## <a name="see-also"></a>参照  
[プログラミング ガイドライン](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[リリース ノート](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  

