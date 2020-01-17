---
title: JDBC ドライバーの展開 | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 518f6bd2605d92857520f870b20edcd351771c54
ms.sourcegitcommit: 4fb6bc7c81a692a2df706df063d36afad42816af
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049833"
---
# <a name="deploying-the-jdbc-driver"></a>JDBC ドライバーの展開
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] に依存するアプリケーションを展開する場合、使用するアプリケーションと共に JDBC ドライバーを再配布する必要があります。 Windows オペレーティング システムのコンポーネントである Windows Data Access Component (Windows DAC) とは異なり、JDBC ドライバーは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のコンポーネントであると見なされます。  
  
 アプリケーションと共に JDBC ドライバーを展開する方法には 2 種類あります。 1 つは、JDBC ドライバーのファイルを、独自のカスタム インストール パッケージの一部として含める方法です。 2 つ目の方法では、Microsoft によって提供される JDBC インストール パッケージを使用します。これは、[デベロッパー センター内の Microsoft JDBC Driver for SQL Server](https://go.microsoft.com/fwlink/?LinkId=70166) に関するページからダウンロードできます。  
  
 以下のセクションでは、Windows および UNIX オペレーティング システム上で JDBC インストール パッケージを使用する方法について説明します。  
  
> [!NOTE]  
>  一般的な Java アプリケーションの展開については、Java の Web サイトを参照してください。  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>Windows システム上での JDBC ドライバーの展開  
 Windows オペレーティング システム上で JDBC ドライバーを展開する場合、実行可能な ZIP ファイル形式のインストール パッケージを使用する必要があります。これは通常、`sqljdbc_<version>_<language>.exe` という名前です。  
  
 実行可能な ZIP ファイルをサイレント実行するには、次のようにコマンド ライン上またはバッチ ファイル内で `/auto` コマンド ライン オプションを使用する必要があります。  
  
 `sqljdbc_<version>_<language>.exe /auto`  
  
> [!NOTE]  
>  `/auto` オプションを使用しても、ユーザーの画面上に WinZip ダイアログ ボックスは表示されるため、それは完全なサイレント インストールではありません。 ただし、このダイアログ ボックスで操作を行う必要はなく、解凍処理が完了するとダイアログ ボックスは閉じます。  
  
## <a name="deploying-the-driver-on-unix-systems"></a>UNIX システム上での JDBC ドライバーの展開 
 UNIX オペレーティング システム上で JDBC ドライバーを展開する場合、GZIP ファイル形式のインストール パッケージを使用する必要があります。これは通常、`sqljdbc_<version>_<language>.tar.gz` という名前です。  
  
 JDBC ドライバーをインストールする前に、gzip ユーティリティおよび tar ユーティリティの両方がユーザーのシステム上にインストールされ、これらのユーティリティの実行可能ファイルを含むフォルダーが PATH 環境変数に追加されていることを確認します。  
  
 zip 形式の tar ファイルをアンパックするには、ドライバーをアンパックするディレクトリに移動し、次のコマンドを入力します。  
  
 `gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
 tar ファイルをアンパックするには、ドライバーをインストールするディレクトリに tar ファイルを移動し、次のコマンドを入力します。  
  
 `tar -xf sqljdbc_<version>_<language>.tar`  

## <a name="legalities-of-driver-redistribution"></a>ドライバーの再配布の Legalities

JDBC Driver のバージョン6.0、6.2、6.4、および7.0 は再頒布可能です。 ライセンス契約の "_再頒布可能コード_" の条項をご確認ください。

JDBC Driver バージョン4.x は、古いバージョンと互換性のために残されています。 4\.x のサポートは2018より前に有効期限が切れました。

## <a name="see-also"></a>参照  
 [JDBC ドライバーの概要](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
