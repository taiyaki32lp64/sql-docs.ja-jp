---
title: SQL Server 用 Microsoft Drivers for PHP を読み込む | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e3c6614425cf8796bd7ec462a62f9410b9ca5857
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936380"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>SQL Server 用 Microsoft Drivers for PHP を読み込む
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このトピックでは、[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] を PHP プロセス領域に読み込む手順について説明します。  
  
プラットフォーム用に作成されたドライバーは、 [Microsoft drivers FOR PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github プロジェクトページからダウンロードできます。 各インストールパッケージには、スレッド化および非スレッド化されたバリアント形式の SQLSRV および PDO_SQLSRV ドライバーファイルが含まれています。 Windows では、32ビットおよび64ビットのバリアントでも使用できます。 各パッケージに含まれるドライバーファイルの一覧については[、「Microsoft Drivers FOR PHP for SQL Server のシステム要件](../../connect/php/system-requirements-for-the-php-sql-driver.md)」を参照してください。 ドライバーファイルは、php 環境の PHP のバージョン、アーキテクチャ、および threadedness と一致している必要があります。

Linux と macOS では、[インストールチュートリアル](../../connect/php/installation-tutorial-linux-mac.md)に記載されているように、ドライバーを PECL を使用してインストールすることもできます。

PHP のビルド時またはを使用`phpize`して、ソースからドライバーをビルドすることもできます。 ソースからドライバーをビルドする場合は、(Linux と macOS の場合) または (Windows `--enable-sqlsrv=static --with-pdo_sqlsrv=static` `./configure`の場合) をコマンドに追加して、共有拡張機能として`--enable-sqlsrv=static --with-pdo-sqlsrv=static`ビルドするのではなく、PHP に静的にビルドするオプションがあります。PHP のビルド。 Php ビルドシステムと`phpize`の詳細については、php の[ドキュメント](http://php.net/manual/install.php)を参照してください。
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>ドライバー ファイルを拡張機能ディレクトリに移動する  
ドライバーファイルは、PHP ランタイムが検出できるディレクトリに配置する必要があります。 既定の PHP 拡張機能ディレクトリにドライバーファイルを配置するのが最も簡単です。既定のディレクトリを`php -i | sls extension_dir`検索するに`php -i | grep extension_dir`は、Windows で実行するか、Linux/macOS で実行します。 既定の拡張機能ディレクトリを使用していない場合は、 **extension_dir**オプションを使用して、php 構成ファイル (php.ini) でディレクトリを指定します。 たとえば、Windows で、ドライバーファイルを`c:\php\ext`ディレクトリに配置している場合は、次の行を php.ini に追加します。
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>PHP の起動時にドライバーを読み込む  
PHP の起動時に SQLSRV ドライバーを読み込むには、まずドライバー ファイルを拡張機能ディレクトリに移動します。 その後、次の操作を行います。  
  
1.  **SQLSRV**ドライバーを有効にするには、次の行を拡張機能セクションに追加して**php.ini**を変更し、必要に応じてファイル名を変更します。  
  
    Windows の場合: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    Linux では、ディストリビューション用に事前に作成されたバイナリをダウンロードしている場合は、次のようになります。 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    ソースまたは PECL から SQLSRV バイナリをコンパイルした場合、代わりに sqlsrv.so という名前が付けられます。
    ```
    extension=sqlsrv.so
    ```
  
2.  **PDO_SQLSRV**ドライバーを有効にするには、PHP Data OBJECTS (PDO) 拡張機能が、組み込みの拡張機能として、または動的に読み込まれた拡張機能として使用可能である必要があります。

    Windows では、ビルド済みの PHP バイナリに組み込みの PDO が付属しているため、php.ini を変更して読み込む必要はありません。 ただし、ソースから PHP をコンパイルし、ビルドする別の PDO 拡張機能を指定した場合は、と`php_pdo.dll`いう名前が付けられ、拡張ディレクトリにコピーして、php.ini に次の行を追加する必要があります。  
    ```
    extension=php_pdo.dll  
    ```
    Linux では、システムのパッケージマネージャーを使用して PHP をインストールした場合、PDO は pdo.so という名前の動的に読み込まれた拡張機能としてインストールされる可能性があります。 PDO_SQLSRV 拡張機能の前に PDO 拡張機能を読み込む必要があります。読み込まない場合、読み込みは失敗します。 通常、拡張機能は個別の .ini ファイルを使用して読み込まれ、これらのファイルは php.ini の後に読み取られます。 したがって、pdo.so が独自の .ini ファイルを介して読み込まれる場合は、PDO の後に PDO_SQLSRV ドライバーを読み込む別のファイルが必要になります。 

    拡張機能固有の .ini ファイルが配置されているディレクトリを確認する`php --ini`には、を実行し`Scan for additional .ini files in:`、の下に表示されているディレクトリをメモします。 Pdo.so を読み込むファイルを見つけます。このファイルの先頭には、10 ~ 10 のような番号が付けられます。 数字のプレフィックスは、.ini ファイルの読み込み順序を示します。数値のプレフィックスを持たないファイルはアルファベット順に読み込まれます。 30-pdo_sqlsrv という名前の PDO_SQLSRV ドライバーファイル (pdo のプレフィックスが付いている値より大きい任意の数) または PDO_SQLSRV (pdo のプレフィックスが数字でない場合) のいずれかを読み込むファイルを作成し、次の行をそのファイルに追加して、filename をとして変更します。対応  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    SQLSRV の場合と同様に、ソースまたは PECL から PDO_SQLSRV バイナリをコンパイルした場合は、代わりに PDO_SQLSRV という名前が付けられます。
    ```
    extension=pdo_sqlsrv.so
    ```
    他の .ini ファイルが格納されているディレクトリにこのファイルをコピーします。 

    組み込みの PDO サポートを使用してソースから PHP をコンパイルした場合は、別の .ini ファイルは必要ありません。また、上記の適切な行を php.ini に追加することもできます。
  
3.  Web サーバーを再起動します。  
  
> [!NOTE]  
> ドライバーが正常に読み込まれたかどうかを判断するために、[phpinfo()](https://php.net/manual/en/function.phpinfo.php) を呼び出すスクリプトを実行します。  
  
**php.ini** ディレクティブの詳細については、[コア php.ini ディレクティブ](https://php.net/manual/en/ini.core.php)に関するページを参照してください。  
  
## <a name="see-also"></a>参照  
[Microsoft Drivers for PHP for SQL Server の概要](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Microsoft SQL Server 用 Drivers for PHP のシステム要件](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV ドライバー API リファレンス](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
