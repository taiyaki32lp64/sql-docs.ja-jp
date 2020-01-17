---
title: 読み取り専用の状態 (Excel ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- read-only status for Excel driver [ODBC]
- Excel driver [ODBC], read-only status
ms.assetid: ef5d773b-4f8f-4005-b985-84b53d8e9f9b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 39f9d2e7ba40ba067659a86f45d2006c83594f3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988042"
---
# <a name="read-only-status-excel-driver"></a>読み取り専用の状態 (Excel ドライバー)
Microsoft Excel のドライバーを使用すると、データ ソースのテーブルは既定では、読み取り専用として開かれているし、一度に 1 つだけのユーザーが開くことが。 テーブルが読み取り専用の状態を持っていなくてただし、アプリケーション実行できます挿入と更新プログラムの Microsoft Excel のテーブル。  
  
 アプリケーションでは、Microsoft Excel のドライバーを介してデータを Microsoft Excel の名前を付けて保存コマンドを実行するとき、アプリケーションは新しいテーブルを作成し、新しいテーブルに保存するデータを挿入する必要があります。 挿入は、追加のテーブルがあります。 テーブルの他の操作は実行されませんを閉じてから再度開くまで。 テーブルが閉じられると、後続の挿入は実行されませんテーブルは読み取り専用のテーブルでは。  
  
 Microsoft Excel のドライバーを使用する場合は、値を更新することができますが、Microsoft Excel スプレッドシートに基づいているため、更新プログラムは、Microsoft Excel ドライバーで正式にサポートされていると見なされましていないテーブルから行を削除できません。
