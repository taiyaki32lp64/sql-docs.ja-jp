---
title: 'ステップ 1: PHP 開発用に開発環境を構成する | Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0bce6022-00bd-45c6-9671-eaa9dfa395a8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc923e3f6e24290f7f2c869fa15dfa4305776452
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68014875"
---
# <a name="step-1-configure-environment-for-php-development"></a>手順 1: PHP 開発用の環境を構成する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]




* ここに記載されているように、使用する PHP ドライバーのバージョンを環境に応じて特定します。「 [Microsoft Drivers FOR PHP for SQL Server のシステム要件](../../connect/php/system-requirements-for-the-php-sql-driver.md)」を参照してください。
* 該当する PHP ドライバーをダウンロードしてインストールする: [MICROSOFT Php driver のダウンロード](https://www.microsoft.com/download/details.aspx?id=20098)  
* 該当する ODBC ドライバーをダウンロードしてインストールしてください。 [SQL Server 用 Odbc ドライバーのダウンロード](../../connect/odbc/download-odbc-driver-for-sql-server.md)  
* 特定のオペレーティングシステム用の PHP ドライバーと web サーバーを構成します。

### <a name="windows"></a>Windows  
  

* 「 [Microsoft Drivers FOR php for SQL Server の読み込み](../../connect/php/loading-the-php-sql-driver.md)」に記載されているように、php ドライバーの読み込みを構成します。 
* 次に示すように、IIS を構成して PHP アプリケーションをホストします。詳細については、 [Microsoft Drivers FOR php for SQL Server](../../connect/php/configuring-iis-for-php-sql-driver.md)を参照してください。

### <a name="linux-and-mac"></a>Linux と Mac


*   Php ドライバーの読み込みと php アプリケーションをホストするように web サーバーを構成する方法については、php [Linux および Mac ドライバーのインストール](../../connect/php/installation-tutorial-linux-mac.md)に関するチュートリアルを参照してください。
