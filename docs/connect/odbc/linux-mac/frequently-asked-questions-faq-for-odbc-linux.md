---
title: ODBC Linux と macOS のよく寄せられる質問 (FAQ) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 65bfd6d2-c83d-4528-a5e1-a85b125a4f4a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cc31a8ae385f2dbb28db30b299377ab5b38058f9
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702776"
---
# <a name="frequently-asked-questions-faq-for-odbc-linux-and-macos"></a>ODBC Linux と macOS のよく寄せられる質問 (FAQ)
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

次に、ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] on Linux および macOS に関する質問に対する回答を示します。
  
## <a name="frequently-asked-questions"></a>よく寄せられる質問

**Linux または macOS 上の既存の ODBC アプリケーションは、どのようにドライバーと連動しますか?**  
他のドライバーを使用して Linux または macOS 上でコンパイルして実行している ODBC アプリケーションは、コンパイルして実行することができます。 
  
**このバージョンのドライバーがサポートしている [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] の機能はどれですか?**

ODBC Driver on Linux および macOS は、LocalDB を除く [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] のすべてのサーバー機能をサポートしています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]サポートされている機能の詳細については、「[プログラミングのガイドライン](../../../connect/odbc/linux-mac/programming-guidelines.md)」を参照してください。  
  
**ドライバーは Kerberos 認証をサポートしますか?**  
可能。 既存の Kerberos 環境を設定している場合は、 `Trusted_Connection=Yes` DSN または接続文字列オプションを使用してサーバーに接続できます。 詳細については、「[統合認証を使用する](../../../connect/odbc/linux-mac/using-integrated-authentication.md)」を参照してください。  
  
**アプリケーションではどの Unicode エンコードを使用すればよいですか?**  
SQL_CHAR データには UTF-8、SQL_WCHAR データには UTF-16 を使用してください。 システムのロケールとドライバーのバージョンによっては、いくつかのエンコーディングのいずれかで UTF-8 以外のデータがサポートされる場合もあります。 詳細については、「[プログラミングのガイドライン](../../../connect/odbc/linux-mac/programming-guidelines.md)」を参照してください。

**ドライバーの試用および評価のために、ダウンロードしてドライバーで実行できる ODBC サンプルはありますか?**

サンプルについては、「 [Use Existing MSDN C++ ODBC Samples for the ODBC Driver on Linux (Linux の ODBC ドライバーに既存の MSDN C++ ODBC サンプルを使用する)](https://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) 」を参照してください。 これは macOS ODBC ドライバーにも適用できます。 

**ODBC ドライバーは、Linux または macOS のオープンソースですか。**

いいえ。 Linux および macOS の ODBC ドライバーは、オープンソース製品ではありません。  

## <a name="see-also"></a>参照
[Linux および macOS に Microsoft ODBC Driver for SQL Server をインストールする](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
