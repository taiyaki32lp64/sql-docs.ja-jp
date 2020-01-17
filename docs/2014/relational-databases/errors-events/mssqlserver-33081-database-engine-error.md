---
title: MSSQLSERVER_33081 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 33081 (Database Engine error)
ms.assetid: 839705e7-fa37-4c0d-9f3f-95a9eab98bcf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 913be11caa9a76ee012571e5ee4b275826668330
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62868586"
---
# <a name="mssqlserver33081"></a>MSSQLSERVER_33081
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|33081|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SEC_DLL_TRUST_VERIFICATION_FAILED|  
|メッセージ テキスト|Authenticode 署名またはファイル パスが無効なため、暗号プロバイダー '%.*ls' を読み込めませんでした。  前のメッセージでその他のエラーを確認してください。|  
  
## <a name="explanation"></a>説明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、エラー メッセージに表示されている暗号化サービス プロバイダーを読み込めませんでした。 このエラーの原因と考えられる Win API エラーがいくつかあります。 リング バッファーに、失敗した API の名前とその API によって返された Windows エラー コードが格納されています。 詳細情報を表示するには、次のクエリを使用して sys.dm_os_ring_buffers ビューにクエリを実行します。  
  
```  
SELECT * FROM sys.dm_os_ring_buffers   
WHERE ring_buffer_type = 'RING_BUFFER_SECURITY_ERROR';  
```  
  
## <a name="user-action"></a>ユーザーの操作  
 問題を調査するには、MSDN (https://msdn.microsoft.com/) で Windows エラー コードを検索します。 エラーを解決するか、詳細について [!INCLUDE[msCoName](../../includes/msconame-md.md)] CSS に問い合わせます。 CSS へのお問い合わせの際には、次の情報を収集してサポート スタッフにご提供ください。  
  
-   暗号化サービス プロバイダーの読み込み失敗に関するエラーを示すエラー ログ。  
  
-   次のステートメントからの出力。  
  
    ```  
    SELECT * FROM sys.dm_os_ring_buffers   
    WHERE ring_buffer_type = 'RING_BUFFER_SECURITY_ERROR';  
    ```  
  
> [!NOTE]  
>  リング バッファー情報は再起動時に失われる場合があるため、すばやく収集してください。  
  
  
