---
title: SET EXCLUSIVE コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d1a37043d332b54d0d5c5ebb7b2ba9f3acce000
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071759"
---
# <a name="set-exclusive-command"></a>SET EXCLUSIVE コマンド
テーブルのファイルが、ネットワーク上で排他モードと共有の使用の開かれたかどうかを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>引数  
 ON  
 それを開いたユーザーのネットワーク上で開かれたテーブルへのアクセスを制限します。 テーブルに、ネットワーク上の他のユーザーにアクセスできません。 また、排他 ON の設定を行うと、その他のすべてのユーザー読み取り専用アクセス権を持つできなくなります。  
  
 OFF  
 ドライバーの既定値 (Visual FoxPro の既定値は、プライベート データ セッションのセッションのグローバル データと OFF ON は)。ネットワーク共有およびネットワーク上のすべてのユーザーが変更に開かれたテーブルを使用できます。  
  
## <a name="remarks"></a>コメント  
 排他的な設定の設定を変更する前に開かれたテーブルの状態は変更されません。 たとえば、設定排他 ON に設定を開くと、テーブル、排他的な設定は後で変更を OFF に、場合の表に、その排他使用状態が保持されます。  
  
## <a name="see-also"></a>関連項目  
 [ODBC Visual FoxPro セットアップ ダイアログ ボックス](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
