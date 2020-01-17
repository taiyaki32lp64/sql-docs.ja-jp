---
title: ODBC コンポーネントのインストール |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC]
- installing ODBC components [ODBC], about installing
- ODBC [ODBC], component installation
ms.assetid: b7e48e9c-8912-4003-b4ef-30aa44de06a7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bf2ef856d8970bf60b3f1f329c57a2379eb528dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094019"
---
# <a name="installing-odbc-components"></a>ODBC コンポーネントのインストール
> [!NOTE]  
>  ODBC は Windows XP および Windows Server 2003 以降、Windows オペレーティング システムに含まれます。 Windows の以前のバージョンで ODBC を明示的にのみインストールしてください。  
  
 このセクションでは、ODBC コンポーネントをインストールおよび削除する方法について説明します。 ドライバー開発者は、常に、ODBC コンポーネント (ドライバー) をインストールするため、このセクションを参照している必要があります。 アプリケーション開発者は、自分のアプリケーションで ODBC コンポーネントが出荷されるは場合にのみ、このセクションを読む必要があります。 ODBC コンポーネントには、ドライバー マネージャー、ドライバー、翻訳者、インストーラー DLL、カーソル ライブラリ、および関連ファイルが含まれます。 このセクションの目的で、ODBC アプリケーションは、ODBC コンポーネントは考慮されません。  
  
> [!NOTE]  
>  このセクションでは、Microsoft Windows プラットフォームに固有です。 他のプラットフォームでの ODBC コンポーネントをインストールする方法は、プラットフォーム固有です。  
  
 ODBC コンポーネントはインストールされているし、ファイルのではなく、コンポーネントごとに削除します。 たとえば、トランスレーターは、それ自体とデータ ファイルの数、変換プログラムで構成され場合、これらのファイルがインストールされているし、グループとして削除いないをインストールし、ファイルの単位で削除します。 その理由は、システムでのみ完全なコンポーネントが存在するかどうかを確認することです。  
  
 インストールおよびコンポーネントを削除するためは、ODBC コンポーネントであるように、次が定義されました。  
  
-   **コア コンポーネント。** ドライバー マネージャー、カーソル ライブラリ、インストーラー DLL、およびその他のファイルのコア コンポーネントを構成してする必要がありますをインストールし、グループとして削除に関連します。  
  
-   **ドライバーです。** 各ドライバーは、個別のコンポーネントです。  
  
-   **翻訳者。** 各翻訳は、個別のコンポーネントです。  
  
 Unicode ODBC 3.5 以降をサポートすると、ODBC と OLE DB コンポーネントを使用するいくつかの考慮事項を指定する必要があります。 バージョン 1.1 の OLE DB Provider for ODBC は ODBC 3.0 内の特定の Unicode 仕様に作成されました。 ODBC 3.5 ではこれらの仕様が変更されたため、ODBC 3.5 を使用する場合は、バージョン 1.5 以降のプロバイダーを用意する必要以降になります。 このセクションでは、次のトピックを扱います。  
  
-   [インストール コンポーネント](../../../odbc/reference/install/installation-components.md)  
  
-   [使用状況のカウント](../../../odbc/reference/install/usage-counting.md)
