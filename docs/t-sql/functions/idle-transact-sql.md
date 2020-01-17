---
title: '@@IDLE (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@IDLE_TSQL'
- '@@IDLE'
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], idle
- ticks [SQL Server]
- '@@IDLE function'
- status information [SQL Server], idle time
- idle time [SQL Server]
ms.assetid: 8f49c62a-8da5-4afd-a5eb-4df8ef8be755
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 272af8e89dfdf313e24017edd615401bc2a35362
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097464"
---
# <a name="x40x40idle-transact-sql"></a>&#x40;&#x40;IDLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が最後に起動してからアイドル状態になっていた時間を返します。 結果は CPU 時間の増分 ("ティック") で返され、これはすべての CPU 時間を累積したものです。したがって、実際の経過時間を超える場合があります。 マイクロ秒に変換するには、@@TIMETICKS を乗算します。  
  
> [!NOTE]  
>  @@CPU_BUSY または @@IO_BUSY で返される時間が、約 49 日分の累積 CPU 時間を超えた場合は、演算オーバーフロー警告が表示されます。 その場合、@@CPU_BUSY@@IO_BUSY、および @@IDLE の各変数は正確ではありません。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
@@IDLE  
```  
  
## <a name="return-types"></a>戻り値の型  
 **整数 (integer)**  
  
## <a name="remarks"></a>Remarks  
 いくつか含むレポートを表示する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 実行の統計情報 **sp_monitor**です。  
  
## <a name="examples"></a>使用例  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動時から現在までのアイドル時間をミリ秒単位で返します。 値をマイクロ秒に変換するときに演算オーバーフローが発生しないようにするため、この例では値の 1 つを `float` 型に変換しています。  
  
```  
SELECT @@IDLE * CAST(@@TIMETICKS AS float) AS 'Idle microseconds',  
   GETDATE() AS 'as of';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
I  
Idle microseconds  as of                   
----------------- ----------------------  
8199934           12/5/2006 10:23:00 AM   
```  
  
## <a name="see-also"></a>参照  
 [@@CPU_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/cpu-busy-transact-sql.md)   
 [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [@@IO_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/io-busy-transact-sql.md)   
 [システム統計関数 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
