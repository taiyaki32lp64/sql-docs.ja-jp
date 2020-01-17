---
title: セットアップ プログラム |Microsoft Docs
ms.custom: ''
ms.date: 08/31/2016
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
ms.assetid: 9cc5d75d-b293-41e5-927c-10f4af2e7af1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc79bb5d12b53938e3e2ef1c531fd03b0002ed78
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093831"
---
# <a name="setup-program"></a>セットアップ プログラム
> **注:** 以降では、Windows XP および Windows Server 2003、 **ODBC が Windows オペレーティング システムに含まれる**します。 Windows の以前のバージョンで ODBC を明示的にのみインストールしてください。  
  
 ユーザーは、セットアップ プロセスを開始するセットアップ プログラムを実行します。 セットアップ プログラムは、アプリケーションまたはドライバーの開発者によって書き込まれます。 ODBC コンポーネントをインストールするだけでなく、その他のソフトウェアをインストールできます。 たとえば、アプリケーション開発者は、ODBC コンポーネントをインストールして、そのアプリケーションをインストールする、同じセットアップ プログラムを使用可能性があります。  
  
 開発者プログラムを作成して、セットアップ最初から Microsoft® Windows® SDK セットアップ ユーティリティまたはその他のベンダーからのセットアップ ソフトウェアを使用しています。 これにより、開発者は、セットアップ プログラムのルック アンド フィールを完全に制御します。 ODBC アプリケーションなど、追加のソフトウェアをインストールするセットアップ プログラムを記述できます。 Windows SDK のセットアップ ユーティリティの詳細については、Windows SDK のドキュメントを参照してください。  
  
 インストールがどの程度実際には、セットアップ プログラムによっては、呼び出しインストーラー DLL で関数に依存します。 インストーラー DLL には、個々 の ODBC コンポーネントをインストールする機能が含まれています。 セットアップ プログラムを呼び出すだけです**SQLInstallDriverManager**、 **SQLInstallDriverEx**、または**SQLInstallTranslatorEx**インストーラーのパスを取得するための DLL で、コンポーネントがインストールされていると、コンポーネントに関する情報をレジストリに追加するディレクトリ。 これらの関数がファイルを実際にコピーしないでください。セットアップ プログラムは情報を使用してこれらの関数の引数。  
  
 インストーラー DLL には、ODBC コンポーネントを削除する関数も含まれています。 セットアップ プログラムの呼び出し**SQLRemoveDriverManager**、 **SQLRemoveDriver**、または**SQLRemoveTranslator**内インストーラー コンポーネントの使用状況をデクリメントする DLL の数、レジストリと、コンポーネントの新しい使用率カウントを 0 になる場合、コンポーネントのすべての情報をレジストリから削除します。 これらの関数が、コンポーネントのファイルを実際に削除しないでください。セットアップ プログラムがこれには新しいの使用状況カウントが 0 に達する場合。
