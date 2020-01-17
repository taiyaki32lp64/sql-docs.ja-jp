---
title: レジストリ エントリ (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- registry keys [ODBC]
- Visual FoxPro ODBC driver [ODBC], registry entries
- keys [ODBC]
- FoxPro ODBC driver [ODBC], registry entries
ms.assetid: 1a63d92d-ca3a-46ae-911f-6788292c801e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 00a24ffca764c029b87470b7aa07d15f33b4c673
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996430"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>レジストリ エントリ (Visual FoxPro ODBC ドライバー)
Visual FoxPro ODBC ドライバーをインストールするときに、インストール プログラムは、Microsoft Visual FoxPro ドライバーと呼ばれる新しいキーを追加する、HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCInst.ini のレジストリ キーに、システムのレジストリを更新します。 そのキーの下では、次の表で説明されている値が追加されます。  
  
|値の名前|[値の型]|値|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|"YYN"|  
|Driver|REG_SZ|Vfpodbc.dll ファイルへのシステム パス|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns|REG_SZ|"*.dbf,\*.cdx,\*.fpt"|  
|FileUsage|REG_SZ|"1"|  
|セットアップ|REG_SZ|Vfpodbc.dll ファイルへのシステム パス|  
|SQLLevel|REG_SZ|"0"|  
  
 インストール プログラムには、"Visual FoxPro Files", システムの HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini キーへの既定の Visual FoxPro ドライバーを表すキーも追加します。 このキーの下では、インストール プログラムは、次の表で説明する値を追加します。  
  
|値の名前|[値の型]|[値]|  
|----------------|----------------|-----------|  
|Driver|REG_SZ|Vfpodbc.dll ファイルへのシステム パス|  
  
 Visual FoxPro ODBC データ ソース、ODBC の構成に追加するたびにデータ ソース名をその新しいキーが追加されます。 データ ソースの値に設定する値に対応して、 **ODBC Visual FoxPro セットアップ** ダイアログ ボックスで、次の表に記載されています。  
  
|値の名前 (キーワード)|[値の型]|値|  
|----------------------------|----------------|-----------|  
|[部単位で印刷]|REG_SQ|サポートされている照合順序|  
|説明|REG_SZ|データ ソースのユーザーの説明|  
|Driver||Vfpodbc.dll ファイルへのシステム パス|  
|[Exclusive]||はい、いいえ|  
|BackgroundFetch||はい、いいえ|  
|SourceDB|REG_SZ|パス。DBC ファイル|  
|[SourceType]|REG_SZ|"DBC"または"DBF"|  
  
 この情報を直接アクセスしないでください。レジストリのすべての管理には、追加、変更、またはデータ ソースを削除するときに ODBC 管理者によって、処理されます。  
  
 これらのキーワードと値の一部を使用するにはパラメーターとして、 [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) ODBC API 関数。
