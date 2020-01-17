---
title: データ ソースの管理 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- deleting data sources [ODBC], ODBC data source administrator
- data sources [ODBC], ODBC data source administrator
- adding data sources [ODBC], ODBC data source administrator
- removing data sources [ODBC], ODBC data source administrator
- ODBC data source administrator [ODBC], data source management
ms.assetid: 67cc4945-4850-4eb4-8da6-b835ddaeca4c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9dc741321894ae69a9ffb59738576a01d47628f5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901664"
---
# <a name="managing-data-sources"></a>データ ソースの管理
ドライバーのセットアップ プログラムから ODBC ドライバーをインストールした後は、その 1 つまたは複数のデータ ソースを定義できます。 データ ソース名 (DSN) では、データの一意の説明を提供する必要があります。たとえば、*給与*または*Accounts Payable*します。 現在インストールされているすべてのドライバーに定義されているユーザーおよびシステム データ ソースが記載されて、**ユーザー DSN**または**システム DSN**のタブ、 **ODBC データ ソース アドミニストレーター** ダイアログ ボックス。 指定されたディレクトリにファイル データ ソースが記載されて、**ファイル DSN**  タブに表示されるディレクトリが入力されて、**ファイルの場所**ボックスに、**ファイル DSN**タブ。  
  
> [!NOTE]  
>  64 ビット プラットフォームでの 32 ビット ドライバーに接続するデータ ソースを管理するには、c:\windows\sysWOW64\odbcad32.exe を使用します。 64 ビット ドライバーに接続するデータ ソースを管理するには、c:\windows\system32\odbcad32.exe を使用します。 **管理ツール**64 ビットの Windows 8 オペレーティング システムでは、32 ビットと 64 ビットの両方のアイコンは**ODBC データ ソース アドミニストレーター**  ダイアログ ボックス。  
  
 場合は、64 ビット odbcad32.exe を使用して、構成や削除など、32 ビット ドライバーに接続する DSN**ドライバーは Microsoft Access (\*.mdb)** 、次のエラー メッセージが表示されます。  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 このエラーを解決するには、構成や削除、DSN を 32 ビット odbcad32.exe を使用します。  
  
 データ ソースは、特定の ODBC ドライバーをドライバーを通じてアクセスするデータに関連付けます。 たとえば、ODBC dBASE ドライバーを使用して、ハード ディスクまたはネットワーク ドライブ上の特定のディレクトリにある 1 つまたは複数の dBASE ファイルにアクセスするデータ ソースを作成する場合があります。 ODBC データ ソース アドミニストレーターを使用して、追加することができます、変更、次の表に示すように、データ ソースを削除およびします。  
  
|操作|説明|  
|------------|-----------------|  
|データ ソースの追加|ドライバーをドライバーを使用してアクセスするいくつかのデータに関連付けるそれぞれ複数のデータ ソースを追加することになります。 データ ソースごとに、そのデータ ソースを一意に識別する名前を付けます。 たとえば、顧客情報を含む dBASE ファイルを一連のデータ ソースを作成する場合は、データ ソース「顧客」を名前可能性があります。 アプリケーションは、通常ユーザーが選択のデータ ソース名を表示します。<br /><br /> ファイル データ ソースの追加は、ユーザーまたはシステム データ ソースを追加することが若干異なるです。 詳細については、ヘルプ ファイル、ODBC データ ソース アドミニストレーターを参照してください。|  
|データ ソースの変更|要件に応じて、する必要がありますをデータ ソースを再構成します。 オプションをリセットするをクリックして**構成**ドライバーのセットアップ ダイアログ ボックス。|  
|データ ソースの削除|クリックして**削除**データ ソースを選択した後。|  
  
 ファイル データ ソースの詳細については、次を参照してください。[を使用してファイル データ ソースの接続](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)または[SQLDriverConnect 関数](../../odbc/reference/syntax/sqldriverconnect-function.md)します。  
  
## <a name="see-also"></a>参照  
 [ODBC データ ソース アドミニストレーター](../../odbc/admin/odbc-data-source-administrator.md)
