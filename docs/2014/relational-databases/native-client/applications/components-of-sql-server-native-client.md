---
title: SQL Server Native Client のコンポーネント |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 329ffa78471ead02b1431a41d898cfc43ca65684
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213511"
---
# <a name="components-of-sql-server-native-client"></a>SQL Server Native Client のコンポーネント
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client には、次のコンポーネントが含まれています。  
  
|コンポーネント|説明|  
|---------------|-----------------|  
|sqlncli11.dll|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client のすべての機能を含む DLL (ダイナミック リンク ライブラリ) ファイル。 このファイルには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーと [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーが含まれます。|  
|sqlnclir11.rll|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ライブラリに付随するリソース ファイル。|  
|s10ch_sqlncli.chm|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーまたは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ ソースを作成する方法について記載している、データ ソース ウィザードのヘルプ ファイル。|  
|sqlncli.h|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client を使用する場合に必要となる、新しいすべての定義を含む [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ヘッダー ファイル。 このヘッダー ファイルは、odbcss.h ヘッダー ファイルと sqloledb.h ヘッダー ファイルの両方に置き換わるものです。 **注:** Sqlncli.h と odbcss.h を同じプログラムで、を参照することはできませんが、sqloledb.h を最初に定義されている限り、sqlncli.h と sqloledb.h を同じプログラム内で参照できます。|  
|sqlncli11.lib|直接の呼び出しに必要なライブラリ ファイル、 **bcp**ユーティリティ関数の一部である、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバー。 **注:** プログラミング コードで sqlncli11.lib ファイルを参照する場合は、sqlncli11.dll ファイルがシステム パス、およびを行うユーザーのシステム パスであることを確認する必要があります。 アプリケーションを使用します。|  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client を使用したアプリケーションのビルド](building-applications-with-sql-server-native-client.md)  
  
  
