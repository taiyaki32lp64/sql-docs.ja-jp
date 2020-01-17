---
title: データソースのレジストリエントリ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- data sources [ODBC], registry entries
- registry entries for data sources [ODBC], about registry entries
- data sources [ODBC], configuring
- registry entries for data sources [ODBC]
ms.assetid: 78aaa3d3-d081-4550-80e3-720c910d5996
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1fe76ba3926f2883e2518e255eddf0d567134f4d
ms.sourcegitcommit: 594cee116fa4ee321e1f5e5206f4a94d408f1576
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "70009354"
---
# <a name="registry-entries-for-data-sources"></a>データ ソースのレジストリ エントリ
> [!NOTE]  
>  Windows XP および windows Server 2003 以降では、ODBC は Windows オペレーティングシステムに含まれています。 ODBC は、以前のバージョンの Windows にのみ明示的にインストールする必要があります。  
  
 インストーラー DLL は、各データソースに関する情報をレジストリに保持します。 Microsoft Windows NT/Windows 2000 および Microsoft Windows 95/98 では、この情報はレジストリの次の2つのキーのいずれかの下のサブキーに格納されます。  

 ```console
 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\Odbc.ini  
 ```

 ```console
 HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini
 ```

 どのキーが使用されるかは、データソースが*システムデータソース*であるか、すべてのユーザーが利用できるか、または現在のユーザーのみが使用できる*ユーザーデータソース*であるかによって異なります。 システムデータソースは HKEY_LOCAL_MACHINE ツリーに格納され、ユーザーデータソースは HKEY_CURRENT_USER ツリーに格納されます。 それ以外の点では、システムデータソースとユーザーデータソースは同じです。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ODBC データ ソースのサブキー](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [データ ソースの仕様のサブキー](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [既定のサブキー](../../../odbc/reference/install/default-subkey.md)  
  
-   [ODBC のサブキー](../../../odbc/reference/install/odbc-subkey.md)
