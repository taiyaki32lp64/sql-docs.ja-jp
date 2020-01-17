---
title: OLE DB Driver for SQL Server のインストール | Microsoft Docs
description: SQL Server 用 OLE DB ドライバーのインストールとアンインストール
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, uninstalling
- MSOLEDBSQL, installing
- MSOLEDBSQL, uninstalling
- Setup [OLE DB Driver for SQL Server]
- uninstalling OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], uninstalling OLE DB Driver for SQL Server
- installing OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, installing
- data access [OLE DB Driver for SQL Server], installing OLE DB Driver for SQL Server
- removing OLE DB Driver for SQL Server
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 08f33d84ee8c035e1e1d3818e2a036f96af2a280
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989311"
---
# <a name="installing-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server のインストール
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

SQL Server 用の OLE DB ドライバーをインストールするには、msoledbsql インストーラーが必要です。
インストーラーを実行し、適切な選択を行います。 SQL Server 用の OLE DB ドライバーは、以前のバージョンの Microsoft OLE DB プロバイダーとサイドバイサイドでインストールできます。

SQL Server ファイルの OLE DB ドライバー (msoledbsql、msoledbsqlr) は、に`%SYSTEMROOT%\system32\`インストールされます。 また、x64 msoledbsql は、32ビットバイナリをに`%SYSTEMROOT%\SysWOW64\`インストールします。

> [!NOTE]  
> SQL Server 用の OLE DB ドライバーの適切なレジストリ設定はすべて、インストールプロセスの一部として作成されます。  

SQL Server ヘッダーファイルとライブラリファイル (msoledbsql および msoledbsql) の OLE DB ドライバーは、に`%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`インストールされます。 また、x64 msoledbsql では、同じファイルがに`%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`インストールされます。  

Msoledbsql を使用して、SQL Server 用の OLE DB ドライバーを配布できます。 アプリケーションを展開するときに、SQL Server 用の OLE DB ドライバーをインストールすることが必要になる場合があります。 チェイナーとブートストラップのテクノロジを使用すると、ユーザーが 1 回のインストール手順に従うだけで複数のパッケージをまとめてインストールできるようになります。 詳細については、「[Visual Studio 2005 用のカスタム ブートストラップ パッケージの作成](https://go.microsoft.com/fwlink/?LinkId=115667)」および「[カスタムの必須コンポーネントの追加](https://go.microsoft.com/fwlink/?LinkId=115668)」をご覧ください。  
  
X64 msoledbsql では、SQL Server 用の OLE DB Driver の32ビットバージョンもインストールされます。 アプリケーションが開発されたプラットフォーム以外のプラットフォームを対象としている場合は、x64 および x86 用の msoledbsql のバージョンをダウンロードできます。

msoledbsql.msi を呼び出すと、既定ではクライアント コンポーネントだけがインストールされます。 クライアント コンポーネントは、OLE DB Driver for SQL Server を使用して開発されたアプリケーションの実行をサポートするファイルです。 SDK コンポーネントもインストールするには、コマンド ラインで `ADDLOCAL=All` を指定します。 例:  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>サイレント インストール  
 msiexec で /passive、/qn、/qb、または /qr オプションを指定する場合、IACCEPTMSOLEDBSQLLICENSETERMS=YES も指定して、使用許諾契約の条件に同意することを明示的に指定する必要があります。 このオプションは、すべて大文字で指定する必要があります。  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>依存関係として OLE DB Driver for SQL Server をインストールする  
すべての依存アプリケーションがアンインストールされるまで、SQL Server 用の OLE DB ドライバーをアンインストールしないことが重要です。 アプリケーションが SQL Server の OLE DB ドライバーに依存しているという警告をユーザーに提供するには、次のように MSI で APPGUID インストールオプションを使用します。  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

APPGUID に渡す値は、特定の製品コードです。 Microsoft インストーラーを使用してアプリケーションのセットアップ プログラムをバンドルするときは、製品コードを作成する必要があります。
APPGUID オプションでは、管理者特権でのコマンドプロンプトからインストーラーを実行する必要があります。

## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server を使用したアプリケーションの構築](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
