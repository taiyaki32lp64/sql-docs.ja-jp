---
title: Microsoft Drivers for PHP for SQL Server の概要 | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 66559249-34c0-409d-b919-9b5bf0c4c9ec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 25519d06df8b948d5cfc5d387029cf09beafc856
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936270"
---
# <a name="overview-of-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server の概要

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] は、Azure SQL Database を含む SQL Server 2005 以降のバージョンにデータ アクセスを提供する、PHP 拡張機能です。 拡張機能は、SQLSRV ドライバーとオブジェクト指向インターフェイスを備えたプロシージャインターフェイスを提供します。また、Express など、SQL Server のすべてのバージョンのデータにアクセスするための PDO_SQLSRV ドライバーと共に、SQL Server 2005 以降を使用します。 ドライバーのバージョン3.1 以降のサポートは SQL Server 2008 から始まります。 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] API には、Windows 認証、トランザクション、パラメーター バインディング、ストリーミング、メタデータ アクセス、およびエラー処理のサポートが含まれています。  
  
を使用[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]するには、PHP が実行されているのと同じコンピューターに、SQL Server Native Client または Microsoft ODBC ドライバーの正しいバージョンがインストールされている必要があります。  詳細については、「 [Microsoft Drivers FOR PHP for SQL Server のシステム要件](../../connect/php/system-requirements-for-the-php-sql-driver.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|---------|---------------|  
| ![ダウンロード-ダウン矢印-](../../ssdt/media/download.png)[SQL Server FOR PHP のドライバーをダウンロードするため](download-drivers-php-sql-server.md)の丸 | Microsoft Drivers for PHP for SQL Server をダウンロードするためのリンクです。 |
|[Microsoft Drivers for PHP for SQL Server リリース ノート](../../connect/php/release-notes-php-sql-driver.md)|バージョン 4.0、3.2、3.1、3.0、および 2.0 で追加された機能を示します。|  
|[Microsoft Drivers for PHP for SQL Server 向けのサポート リソース](../../connect/php/support-resources-for-the-php-sql-driver.md)|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]を使用するアプリケーションを開発するときに役立つリソースへのリンクを示します。|  
|[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)|このドキュメントのコード例を実行するときに役立つ情報を提供します。|  
| &nbsp; | &nbsp; |

## <a name="reference"></a>リファレンス

[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV ドライバー リファレンス](../../connect/php/pdo-sqlsrv-driver-reference.md)  
[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  

## <a name="see-also"></a>参照

[Microsoft Drivers for PHP for SQL Server の概要](../../connect/php/getting-started-with-the-php-sql-driver.md)

[SQL Server 用 Microsoft Drivers for PHP のためのプログラミング ガイド](../../connect/php/programming-guide-for-php-sql-driver.md)

[サンプル アプリケーション &#40;SQLSRV ドライバー&#41;](../../connect/php/example-application-sqlsrv-driver.md)
