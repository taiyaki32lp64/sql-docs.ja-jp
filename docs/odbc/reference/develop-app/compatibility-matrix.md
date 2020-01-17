---
title: 互換性対応表 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application compatibility issues [ODBC]
- application upgrades [ODBC], compatibility matrix
- upgrading applications [ODBC], compatibility matrix
ms.assetid: 0690b463-15a1-48fa-9d0b-9cc9e5bf7fc6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 273633532b9b9247ea7aa12fe90bfcc3c6f6bb81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083274"
---
# <a name="compatibility-matrix"></a>互換性マトリックス
次の表では、アプリケーションとドライバーのこのセクションでは以前に定義した型の互換性について説明します。  
  
|アプリケーションの種類<br /><br /> およびバージョン|32 ビット ODBC<br /><br /> *2.x*ドライバー|ODBC *3.x*<br /><br /> ドライバー●どらいば○|ODBC 3.8 ドライバー|ISO と開いているグループ準拠のドライバー|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|16 ビット アプリケーションで任意のバージョン|互換性のあります。|互換性のあります。|互換性のあります。|互換性のあります。|  
|純粋な*2.x*アプリケーション|互換性のあります。|互換性のあります。|互換性のあります。|いない互換性のある [3]|  
|純粋な*2.x*アプリケーションを再コンパイル|互換性のあります。|互換性のある [1]|互換性のある [1]|いない互換性のある [3]|  
|純粋な*2.x* Unicode アプリケーション|互換性のあります。|互換性のある [1]|互換性のある [1]|いない互換性のある [3]|  
|純粋なグループと ISO 準拠のアプリケーション|互換性がありません。|互換性のある [2]|互換性のある [2]|互換性のある [2]|  
|純粋な 3.0 アプリケーション|互換性がありません。|互換性のあります。|互換性のあります。|いない互換性のある [4]|  
|純粋な 3.5 アプリケーション|互換性がありません。|互換性のあります。|互換性のあります。|いない互換性のある [4]|  
|純粋な 3.8 (またはそれ以降) のアプリケーション|いない互換性のある [5]|いない互換性のある [5]|互換性のあります。|いない互換性のある [4]|  
|置き換えられたアプリケーション|互換性のあります。|互換性のあります。|互換性のあります。|いない互換性のある [3]|  
  
 [1] で、アプリケーションでは、(Unicode アプリケーションの場合) は、UNICODE のオプションを使用して ODBC 3.5 (またはそれ以降) のヘッダーを使用して再コンパイルする必要がありますに 0x0250 ODBCVER を設定する必要があります。  
  
 [2] で、アプリケーションは、ODBC 3.5 (またはそれ以降) のヘッダーを使用してコンパイルし、リンク、ODBC ドライバー マネージャーでする必要があります。 ページ ヘッダー フラグ ODBC_STD 設定することもあります。  
  
 [3] この構成は、ODBC の機能があるために動作しないことができます可能性のある*2.x*ブックマークなど、標準ではないです。  
  
 [4] この構成は、ODBC の機能があるために動作しないことができます可能性のある*3.x*ブックマークなど、標準ではないです。  
  
 [ODBC 3.8 の特定のドライバーなど、ODBC 2.x または 3.x のドライバーが含まれていない機能があるためにが、5] この構成に失敗する可能性があることができます[ODBC における C データ型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)します。  
  
## <a name="driver-manager-compatibility"></a>ドライバー マネージャーの互換性  
 ODBC 3.0 アプリケーションをすべてのドライバー マネージャーのバージョンで動作する必要がありますには、起動時に、次を実行する必要があります。  
  
-   環境ハンドルを割り当てます。  
  
-   SQL_OV_ODBC3_80 を SQL_ATTR_ODBC_VERSION 環境属性を設定します。 ドライバー マネージャーでは、SQL_ERROR が返された場合、ドライバー マネージャーは 3.8 より古いです。 ドライバー マネージャーに対応する、必要に応じてを SQL_OV_ODBC3 または SQL_OV_ODBC2、SQL_ATTR_ODBC_VERSION をリセットします。  
  
-   接続ハンドルを割り当てます。  
  
-   接続を作成します。  
  
-   SQLGetInfo SQL_DRIVER_ODBC_VER ドライバーのバージョンを判断するを呼び出します。 ドライバーは、ODBC 3.8 ドライバー、ドライバー固有の C 型を使用することができます。 それ以外の場合、ドライバー固有の C データ型を使用しないでください。  
  
 なお、再コンパイルされた ODBC 3.x アプリケーション SQL_OV_ODBC3_80 を SQL_ATTR_ODBC_VERSION に指定することがなくドライバー固有の C 型以外の ODBC 3.8 機能を使用できます。 ODBC 3.x の機能を使用して、再コンパイルされた ODBC 2.x アプリケーションに似ています。  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>SQLCancelHandle を使用して、アプリケーションと互換性のあるすべてのドライバー マネージャーで  
 [SQLCancelHandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)はサポートされていない Windows 7 より前にリリースされたドライバー マネージャーでアプリケーションを読み込めません以前のバージョンの Windows で呼び出す場合**SQLCancelHandle**直接します。 ドライバー マネージャーのすべてのバージョンを使用して、使用する**SQLCancelHandle** Windows の新しいバージョンでは、アプリケーションを呼び出す必要があります**SQLCancelHandle**を使用して直接**LoadLibrary**と**GetProcAddress します。**  
  
## <a name="see-also"></a>関連項目  
 [ODBC 3.8 の新機能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
