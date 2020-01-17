---
title: SET REPROCESS コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET REPROCESS command [ODBC]
ms.assetid: b0708757-b1d7-42f3-8988-787f2a806b8b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16f87c52b4149d62a8d57884216890b7421e8ef6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063620"
---
# <a name="set-reprocess-command"></a>SET REPROCESS コマンド
ロック失敗後のファイルまたはレコードのロックに長時間を時間に、または方法の数を指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>引数  
 *NAttempts*[秒]  
 時間数または失敗した最初の試行後に、レコードまたはファイルをロックしようとする秒数を指定します。 既定値は 0 になります。最大値は、32,000 します。  
  
 秒単位では、Visual FoxPro しようとするファイルをロックまたはの記録を指定します*nAttempts*秒。 場合にのみ使用が*nAttempts*が 0 より大きい。  
  
 たとえば場合、 *nAttempts* 30 は、Visual FoxPro がレコードをロックまたはファイルの最大 30 倍が試行されます。 秒 (設定を再処理を 30 秒も含めると、Visual FoxPro は継続的に最大で 30 秒間のレコードまたはファイルのロックを試行します。  
  
 ON ERROR ルーチンが有効になっていると、レコードまたはファイルをロックするためのコマンドによって試行が成功した場合は、ON ERROR ルーチンが実行されます。 ただし、関数は、ロックを試みると、ON ERROR ルーチンが実行されない場合は、関数、False を返します (します。F.)。  
  
 ON ERROR ルーチンが有効になっていない、コマンドが、レコードまたはファイルをロックしようとして、ロックを配置することはできません、エラーが生成されます。 関数は、ロックを配置しようとする場合、アラートが表示されていないし、関数は False を返します (します。F.)。  
  
 場合*nAttempts*は 0 (既定値) とコマンドまたはレコードまたはファイルをロックしようとする関数を発行して、Visual FoxPro が無期限にファイルをレコードをロックまたはしようとします。 レコードまたはファイルが待機中にロックの利用になるは、ロックが設定され、システム メッセージがクリアされます。 関数が、ロックを配置しようとすると、関数は True を返します (します。T.)。  
  
 場合は、ON ERROR ルーチンが有効では、レコードまたはファイルをロックしようとして、コマンド、ON ERROR ルーチンはレコードまたはファイルのロックを試みる他より優先されます。 ON ERROR ルーチンは、すぐに実行されます。 Visual FoxPro は、追加のレコードまたはファイルのロックを試行しませんし、システム メッセージは表示されません。  
  
 場合*nAttempts* 1 は、Visual FoxPro では、レコード ロック、またはファイルを無期限にしようとして、ON ERROR ルーチンが実行されません。  
  
 場合は、ロックがレコードをロックしようとしているファイルに別のユーザーが配置されている、ユーザーがロックを解放するまでを待つ必要があります。  
  
 自動  
 Visual FoxPro、レコードをロックまたはファイルを無期限にすることを指定します。 (-2 を再処理をセットは、同等のコマンドです)。  
  
## <a name="remarks"></a>コメント  
 レコードまたはファイルをロックする最初の試行が成功しない常にします。 多くの場合、レコードまたはファイルは、ネットワーク上の別のユーザーによってロックされています。 設定を再処理すると、Visual FoxPro の初回の試行が成功したときに、レコードまたはファイルをロックする追加の試行は、かどうかを判断します。 何回追加の試行が行われたまたは、どのくらいの時間の試行が行われますを指定できます。 ON ERROR ルーチンでは、試行の処理方法に失敗した場合のロックに影響します。
