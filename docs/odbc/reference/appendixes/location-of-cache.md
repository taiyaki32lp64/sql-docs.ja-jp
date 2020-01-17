---
title: キャッシュの場所 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 240d6162-4da6-4b1f-96c7-f379f4ecb16f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a925b66b0d09a9beb32e4441d62bc4fa9296313
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990739"
---
# <a name="location-of-cache"></a>キャッシュの場所
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 カーソル ライブラリでは、メモリ内および Windows® 一時ファイル内のデータをキャッシュします。 これにより、カーソル ライブラリを使用可能なディスク領域によってのみ処理できる結果セットのサイズが制限されます。 一時ファイルは、カーソル ライブラリのキャッシュの末尾に挿入された場合、セグメントの境界と重複するデータをキャッシュするときに使用されます。 代わりに、キャッシュされたデータは、キャッシュ内のデータの最後に保存されたブロックの代わりに追加されます。 最後に保存されたデータ ブロックは、一時ファイルに保存されます。 など、電源が失敗すると、カーソル ライブラリが異常終了した場合は、Windows の一時ファイル、ディスクのままにできます。 これらの名前は ~ CTT*nnnn*.tmp とは、現在のディレクトリに作成します。  
  
> [!NOTE]  
>  カーソル ライブラリの Microsoft® WindowsNT®/windows 2000 しようとすると、現在のディレクトリに一時ファイルにデータをキャッシュから読み取り専用の共有またはコンパクト_ディスク (Microsoft Foundation Class ライブラリ サンプルの場合) など、アプリケーションの実行中に SQLSTATEHY000 (一般的なエラー-できませんファイル バッファーを作成する) が返されます。
