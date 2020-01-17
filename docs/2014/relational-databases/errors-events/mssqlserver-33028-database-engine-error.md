---
title: MSSQLSERVER_33028 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 33028 (Database Engine error)
ms.assetid: c5cec0e4-0bcd-4907-826f-e7d835cfcb37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 89f02cfd7ab2116528adb82d6e98023c912c6437
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62868665"
---
# <a name="mssqlserver33028"></a>MSSQLSERVER_33028
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|33028|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SEC_CRYPTOPROV_CANTOPENSESSION|  
|メッセージ テキスト|%S_MSG '%.*ls' のセッションを開くことができません。 プロバイダー エラー コード: %d。|  
  
## <a name="explanation"></a>説明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、エラー メッセージに表示されている暗号化サービス プロバイダーを開くことができませんでした。 暗号化サービス プロバイダーは、表示されているエラー コードを返しました。 エラーの詳細については、暗号化サービス プロバイダーに問い合わせる必要があります。  
  
|エラー コード|説明|  
|----------------|-----------------|  
|0|正常終了しました。 エラーなし。|  
|1|失敗しました。 未定義のエラーまたは予期しないエラーが発生しました。 追加情報は入手できません。|  
|2|バッファーが不足しています。 暗号化サービス プロバイダー用の領域を割り当てることができませんでした。|  
|3|サポートされていません。 問題となる暗号化サービス プロバイダーが、このリリースではサポートされていません。 別の暗号化サービス プロバイダーを選択してください。|  
|4|検出されませんでした。 指定した暗号化サービス プロバイダーが存在しないか、ファイルにアクセスする承認を得ていません。|  
|5|承認エラーです。 資格情報の作成時に指定したパスワードまたはユーザー名が正しくないか、 資格情報が存在しない可能性があります。|  
|6|引数が無効です。 暗号化サービス プロバイダーに無効な引数が渡されました。|  
  
## <a name="user-action"></a>ユーザーの操作  
 エラーを解決するか、暗号化サービス プロバイダーに詳細を問い合わせてください。  
  
  
