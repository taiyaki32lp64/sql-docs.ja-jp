---
title: Installing the Driver Manager (ODBC Driver for SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Driver Manager, installing
ms.assetid: 7c4b6fb4-f45a-4973-adb9-a4d83f0a2a7a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6fc46627dcbd10e4fc64a8520412105475e9c0a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008795"
---
# <a name="installing-the-driver-manager"></a>ドライバー マネージャーのインストール
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

この記事では、SQL Server on Linux と macOS の Microsoft ODBC ドライバーのすべてのバージョンで使用するための unixODBC ドライバー マネージャーをインストールする手順を説明します。  

> [!IMPORTANT]  
> unixODBC ドライバー マネージャーをインストールする前に、お使いのコンピューターにインストールされているドライバー マネージャー パッケージを削除します。 unixODBC ドライバー マネージャーをインストールすると、既存のドライバー マネージャーのエラーが発生する可能性があります。  

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-13-131-and-17"></a>Microsoft ODBC Driver 13、13.1、17 のドライバー マネージャーのインストール
ドライバー マネージャーの依存関係が自動的に解決、パッケージ管理システムで次の手順で Microsoft ODBC Driver 13、13.1、または 17 for Linux または macOS 上の SQL Server をインストールするときに[Microsoft ODBC Driver をインストールします。Linux または macOS 上の SQL Server の](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)します。 

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 for SQL Server のドライバー マネージャーのインストール  

(SUSE と Red Hat Linux のみ)

**インストール スクリプトを使用する**  
  
> [!IMPORTANT]  
> 次の手順では、Red Hat Linux 用のインストール ファイル `msodbcsql-11.0.2270.0.tar.gz` を参照しています。 Preview for SUSE Linux をインストールする場合のファイル名は `msodbcsql-11.0.2260.0.tar.gz` です。  

ドライバー マネージャーをインストールには:  
  
1.  ルートのアクセス許可があることを確認します。  
  
2.  [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC ドライバーのダウンロードで `msodbcsql-11.0.2270.0.tar.gz` という名前のファイルを配置したディレクトリに移動します。 使用している Linux のバージョンに対応する \*.tar.gz ファイルがあることを確認します。 ファイルを解凍するには、コマンド **tar xvzf msodbcsql-11.0.2270.0.tar.gz** を実行します。  

3.  `msodbcsql-11.0.2270.0` ディレクトリに移動すると、ディレクトリ内に `build_dm.sh` というファイルがあることを確認できます。 実行することができます`build_dm.sh`unixODBC ドライバー マネージャーをインストールします。

4.  使用可能なオプションの一覧を表示するには、コマンド **./build_dm.sh --help** を実行します。  
  
5.  インストールの準備ができたら、コマンド **./build_dm.sh** を実行します (お使いのコンピューターが FTP 経由で外部のサイトにアクセスできる場合)。

お使いのコンピューターが FTP 経由で外部のサイトにアクセスできない場合は、`unixODBC-2.3.0.tar.gz` を取得します。 `unixODBC-2.3.0.tar.gz` は [http://www.unixodbc.org](http://www.unixodbc.org/) から取得できます。ページの左側にある **[ダウンロード]** リンクをクリックして、ダウンロード ページに移動します。 適切なリンクをクリックして、unixODBC-2.3.0 (unixODBC-2.3.1 ではなく) をダウンロードします。 unixODBC-2.3.1 は、[!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の今回のリリースではサポートされていません。 UnixODBC ドライバー マネージャーのインストールを開始するには、次のコマンドを実行します。 **./build_dm.sh --download-url=file://unixODBC-2.3.0.tar.gz**します。  

6.  **YES** を入力してファイルの解凍を続行します。 プロセスのこの部分は完了までに最大 5 分かかります。  

7.  スクリプトの実行が停止したら、画面の指示に従って unixODBC ドライバー マネージャーをインストールします。

これで、ドライバーをインストールする準備ができました。 詳細については、次を参照してください。 [Linux と macOS での SQL Server 用 Microsoft ODBC Driver をインストールする](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)します。  

**手動インストール**

インストール スクリプトが完了できない場合は、ユーザーが適切なドライバー マネージャーを構成して作成します。

1.  インストールされている古いバージョンの unixODBC (unixODBC 2.2.11 など) を削除します。 Red Hat Enterprise Linux 5 または 6 では、コマンド **yum remove unixODBC** を実行します。 On SUSE Linux Enterprise、 **zypper 削除 unixODBC**します。  
  
2.  [http://www.unixodbc.org](http://www.unixodbc.org/) に移動します。ページの左側にある **[ダウンロード]** リンクをクリックして、ダウンロード ページに移動します。 適切なリンクをクリックして、ファイル unixODBC-2.3.0.tar.gz をコンピューターに保存します。 UnixODBC-2.3.1 は、[!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の今回のリリースではサポートされていません。  
  
3.  Linux コンピューター上のコマンドを実行します: **tar xvzf unixodbc-2.3.0.tar.gz**します。  
  
4.  unixODBC-2.3.0 ディレクトリに変更します。  
  
5.  コマンド プロンプトでコマンドを実行します: **CPPFLAGS ="-DSIZEOF_LONG_INT = 8"** します。  
  
6.  コマンド プロンプトでコマンドを実行します:**export CPPFLAGS**します。  
  
7.  コマンド プロンプトでコマンドを実行します: **"./configure --prefix=/usr --libdir=/usr/lib64 --sysconfdir=/etc --enable-gui=no --enable-drivers=no --enable-iconv --with-iconv-char-enc=UTF8 --with-iconv-ucode-enc=UTF16LE"** .  
  
8.  (root としてログインして) コマンド プロンプトでコマンド **make** を実行します。  
  
9. (root としてログインして) コマンド プロンプトでコマンド **make install** を実行します。  

これで、ドライバーをインストールする準備ができました。 詳細については、次を参照してください。 [Linux と macOS での SQL Server 用 Microsoft ODBC Driver をインストールする](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)します。  
  
## <a name="see-also"></a>参照
[Linux および macOS に Microsoft ODBC Driver for SQL Server をインストールする](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

[このバージョンのドライバーの既知の問題](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[リリース ノート](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)
