---
title: SQL Server 用 Microsoft Drivers for PHP に対する IIS の構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- configuring, Internet Information Services
ms.assetid: d2dc75d3-9bf7-481c-85f2-8b6310b21461
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 150addd664870e5441c888b6bc357f8fb4d92b20
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015162"
---
# <a name="configuring-iis-for-the-microsoft-drivers-for-php-for-sql-server"></a>SQL Server 用 Microsoft Drivers for PHP に対する IIS の構成
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

このトピックでは、PHP アプリケーションをホストするための IIS の構成に関連のある[インターネット インフォメーション サービス (IIS) Web サイト](https://www.iis.net/)上のリソースへのリンクを提供します。 ここに示すリソースは、IIS での FastCGI の使用に固有のものです。 FastCGI は、アプリケーション フレームワークの Common Gateway Interface (CGI) の実行可能ファイルが Web サーバーとやり取りできる標準プロトコルです。 FastCGI は、標準の CGI プロトコルとは異なり、CGI プロセスを複数の要求に再使用します。  
  
## <a name="tutorials"></a>チュートリアル  
次のリンクは、PHP 用の FastCGI の設定、および IIS 6.0 と IIS 7.0 での PHP アプリケーションのホストに関するチュートリアルに対するものです。  
  
-   [PHP での FastCGI](https://docs.microsoft.com/iis/web-hosting/web-server-for-shared-hosting/fastcgi-with-php)  
-   [IIS 7.0 で PHP アプリケーションをホストするための FastCGI の使用](https://docs.microsoft.com/iis/application-frameworks/install-and-configure-php-applications-on-iis/using-fastcgi-to-host-php-applications-on-iis)  
-   [IIS 6.0 で PHP アプリケーションをホストするための FastCGI の使用](https://docs.microsoft.com/iis/application-frameworks/install-and-configure-php-applications-on-iis/using-fastcgi-to-host-php-applications-on-iis-60)  
-   [Configuring FastCGI Extension for IIS 6.0 (IIS 6.0 用の FastCGI 拡張機能の構成)](https://docs.microsoft.com/iis/application-frameworks/install-and-configure-php-on-iis/configuring-the-fastcgi-extension-for-iis-60)  
  
## <a name="video-presentations"></a>ビデオ プレゼンテーション  
次のリンクは、PHP 用の FastCGI の設定、および IIS 7.0 機能を使用した PHP アプリケーションのホストに関するビデオ プレゼンテーションに対するものです。  
  
-   [Setting up FastCGI for PHP (PHP 用の FastCGI の設定)](https://docs.microsoft.com/iis/application-frameworks/running-php-applications-on-iis/set-up-fastcgi-for-php)  
-   [Partying with PHP on Microsoft Internet Information Services 7 (Microsoft インターネット インフォメーション サービス 7 での PHP とのパーティー)](https://docs.microsoft.com/iis/application-frameworks/running-php-applications-on-iis/mix08-partying-with-php-on-microsoft-internet-information-services-7-and-above)  
  
## <a name="support-resources"></a>サポート リソース  
次のフォーラムでは、IIS での FastCGI に対するコミュニティ サポートが提供されます。  
  
-   [FastCGI ハンドラー](https://forums.iis.net/1103.aspx)  
-   [IIS 7 - FastCGI モジュール](https://forums.iis.net/1104.aspx)  
  
## <a name="see-also"></a>参照  
[Microsoft Drivers for PHP for SQL Server の概要](../../connect/php/getting-started-with-the-php-sql-driver.md)

[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)

[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
  
