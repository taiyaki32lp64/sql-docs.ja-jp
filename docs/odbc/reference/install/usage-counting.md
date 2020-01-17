---
title: 使用状況のカウント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- usage counts [ODBC]
- file usage counts [ODBC]
- installing ODBC components [ODBC], usage counts
- subkeys [ODBC], usage counts
ms.assetid: 0678aee9-8256-463c-89dd-77b1a0dfdd60
author: MightyPen
ms.author: genemi
ms.openlocfilehash: edf9976dd3e5d890b46919808e896a8e81a0cd93
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093791"
---
# <a name="usage-counting"></a>使用状況のカウント
> [!NOTE]  
>  ODBC は Windows XP および Windows Server 2003 以降、Windows オペレーティング システムに含まれます。 Windows の以前のバージョンで ODBC を明示的にのみインストールしてください。  
  
 各コンポーネントのレジストリでの使用状況カウントが 2 つの型が保持されます。 コンポーネントの使用率カウントと省略可能なファイル使用状況カウントが 1 つまたは複数です。 コンポーネントの使用率カウントは、インストーラー DLL レジストリ エントリを維持します。 ODBC Core、ドライバー、およびトランスレーターのサブキーの下の UsageCount 値で格納されます。 UsageCount 値との詳細については、これらのサブキーはの形式の場合、次を参照してください。 [ODBC コンポーネントのレジストリ エントリ](../../../odbc/reference/install/registry-entries-for-odbc-components.md)します。  
  
 コンポーネントが最初にインストールされたときに、インストーラー DLL のサブキーを作成し、設定 UsageCount 値のデータをそのサブキーを 1 にします。 コンポーネントを再度インストールをインストーラー DLL は、使用率カウントをインクリメントします。 コンポーネントが削除されると、インストーラー DLL、使用状況カウントをデクリメントします。 使用率カウントを 0 になる場合、インストーラーの DLL は、コンポーネントのサブキーを削除します。  
  
> [!CAUTION]  
>  アプリケーション削除しないでください物理的にドライバー マネージャーのファイル コンポーネントの使用率カウントとファイルの使用率カウントに達すると 0 です。  
  
 使用率カウントをインクリメントまたはデクリメントではなくファイルの使用状況カウントまたは特定できるときにファイルをする必要があります実際にするコピーとして削除します。 これは、機能は、ODBC コンポーネントとそのため、ODBC コンポーネント内のファイル共有しできますインストールまたは削除さまざまなアプリケーションであるため重要です。 アプリケーションは、コンポーネントの使用率カウントとファイルの使用率カウントが 0 になる場合、ドライバーおよび translator のファイルを削除できます。 ドライバー マネージャーのファイルは、should not、ただし、これらのファイルは、ファイルの使用率カウントはインクリメントされませんが、他のアプリケーションで使用できるため、両方のコンポーネントの使用率カウントとファイルの使用率カウントを 0 に到達したときに削除します。  
  
> [!NOTE]  
>  ファイルの使用状況のカウントは、オプションで Microsoft® WindowsNT®/windows 2000 です。  
  
 ファイル使用状況カウントは、呼び出された後、セットアップ プログラムによって維持**SQLInstallDriverManager**、 **SQLInstallDriverEx**、 **SQLInstallTranslatorEx**、 **SQLRemoveDriverManager**、 **SQLRemoveDriver**、または**SQLRemoveTranslator**します。  
  
 コンポーネントが最初にインストールされたときに、セットアップ プログラムまたはインストーラー DLL を作成しますファイルごとに次のキーの値が既にシステムにそのコンポーネントに。  
  
> [!NOTE]  
>  HKEY_LOCAL_MACHINE  
>   
>  ソフトウェア  
>   
>  Microsoft  
>   
>  Windows  
>   
>  CurrentVersion  
>   
>  SharedDlls  
  
 これらの値のデータを 1 に設定し、ファイル システムにコピーします。 コンポーネントを再度インストールとセットアップ プログラムまたは DLL のインストーラーには、使用状況カウントが増加します。 コンポーネントが削除されると、セットアップ プログラムまたはインストーラー DLL のデクリメント、使用率をカウントします。 任意の使用率カウントを 0 になる場合、セットアップ プログラムまたは DLL のインストーラー ファイルの値を削除し、コンポーネントが、ドライバーまたは翻訳者の場合は、ファイルを削除します。 ドライバー マネージャーのファイルを削除しない必要があります。  
  
 ファイルの使用状況カウントの値の形式は、次の表に示します。  
  
|名前|データ型|data|  
|----------|---------------|----------|  
|*完全なパス*|REG_DWORD|*count*|  
  
 たとえば、Informix 用のドライバーが、Infrmx32.dll および Infrmx32.hlp ファイルを使用するとし、このドライバーが 2 回インストールされているとします。 Informix ドライバーの SharedDlls サブキーの値には、次のようになります。  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
