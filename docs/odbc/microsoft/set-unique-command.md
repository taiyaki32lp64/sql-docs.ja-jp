---
title: SET UNIQUE コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET UNIQUE command [ODBC]
ms.assetid: 1f69e31e-4599-47cc-ac89-b86fba8703c5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 29598ed97cba8be04a0c08727cffc40e663becba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063615"
---
# <a name="set-unique-command"></a>SET UNIQUE コマンド
インデックス ファイルで、重複するインデックス キー値を持つレコードが保持されるかどうかを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>引数  
 ON  
 重複するインデックス キーの値を持つ任意のレコードは、インデックス ファイルに含まれないことを指定します。 インデックス ファイルには、元のインデックス キー値を持つ最初のレコードのみが含まれます。  
  
 OFF  
 (既定値。) インデックス ファイルに重複するインデックス キー値を持つレコードが含まれることを指定します。  
  
## <a name="remarks"></a>コメント  
 インデックス ファイルでは、インデックスの再作成を発行するときに、設定の一意の設定が保持されます。 詳細については、次を参照してください。[インデックス](../../odbc/microsoft/index-command.md)します。
