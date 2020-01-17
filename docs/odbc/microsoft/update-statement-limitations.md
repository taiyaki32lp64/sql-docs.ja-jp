---
title: UPDATE ステートメントの制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1cc8cf58d4e4d826dc4b152e395dedbea395a095
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088204"
---
# <a name="update-statement-limitations"></a>UPDATE ステートメントの制限事項
テーブルを更新する Paradox ドライバーの場合、テーブルに一意のインデックス (Paradox 主キー) ことが必要です。 Borland データベース エンジンを実装することがなく Paradox ドライバーを使用する場合、Paradox テーブルを更新することはできません。  
  
 テキストのドライバーによってサポートされていません。  
  
 Microsoft Excel のドライバーを使用する場合、値を更新することができますが、Microsoft Excel スプレッドシートに基づくテーブルから行を削除できません。 その結果、UPDATE ステートメントでは、Microsoft Excel のドライバーで正式にサポートはありません。 INSERT ステートメントのみがサポートされていると見なされます。
