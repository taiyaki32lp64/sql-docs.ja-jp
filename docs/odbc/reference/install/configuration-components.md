---
title: 構成コンポーネント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], configuring
ms.assetid: 0b68ff48-12e4-41aa-b9e2-b39ed5023ea7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 248a9e31b176444ad51cb3a62c7c5f12f1b7bde3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068584"
---
# <a name="configuration-components"></a>構成コンポーネント
> [!NOTE]  
>  ODBC は Windows XP および Windows Server 2003 以降、Windows オペレーティング システムに含まれます。 Windows の以前のバージョンで ODBC を明示的にのみインストールしてください。  
  
 データ ソースは、必要な Dll とトランスレーター セットアップ Dll のセットアップを有効にする呼び出しのドライバーのインストーラー DLL で構成されます。 インストーラー DLL は、コントロール パネルから直接呼び出されるまたは読み込まれと呼ばれる別のプログラムによって呼び出される、*管理プログラム*します。 次の図は、構成コンポーネント間の関係を示します。  
  
 ![構成コンポーネント間の関係](../../../odbc/reference/install/media/pr30.gif "pr30")  
  
 これらのコンポーネントの詳細については、このセクションの最後に、次のトピックを参照してください。  
  
-   [セットアップ プログラム](../../../odbc/reference/install/setup-program.md)  
  
-   [インストーラー DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [ドライバーのセットアップ DLL](../../../odbc/reference/install/driver-setup-dll.md)  
  
## <a name="see-also"></a>関連項目  
 [インストール コンポーネント](../../../odbc/reference/install/installation-components.md)
