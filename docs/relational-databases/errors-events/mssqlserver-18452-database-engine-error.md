---
title: MSSQLSERVER_18452 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 18456 (Database Engine error)
- 18452 (Database Engine error)
ms.assetid: 21da332c-e81d-4dee-a9d2-95598911b3be
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 09f5703621f0904572da530744206a88de094cec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137107"
---
# <a name="mssqlserver18452"></a>MSSQLSERVER_18452
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|18452|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|LOGON_INVALID_CONNECT|  
|メッセージ テキスト|ユーザー '%.*ls' はログインできませんでした。 このログインは SQL Server ログインなので、Windows 認証では使用できません。%.\*ls|  
  
## <a name="explanation"></a>説明  
検証できない資格情報でユーザーがログインしようとしました。 次の原因が考えられます。  
  
-   ログインは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインですが、サーバーは Windows 認証のみを受け付けます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して接続しようとしていますが、使用しているログインが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に存在しません。  
  
-   ログインで Windows 認証を使用していますが、そのログインは認識できない Windows プリンシパルです。 認識できない Windows プリンシパルは、ログインを Windows で確認できないことを意味します。 これは、信頼されていないドメインからの Windows ログインである可能性があります。  
  
同様の問題によって、より広い意味のエラー 18456 が発生することがあります。  
  
## <a name="user-action"></a>ユーザーの操作  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して接続しようとしている場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が混合モード認証で構成されていることを確認します。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して接続しようとしている場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインが存在することを確認します。  
  
Windows 認証を使用して接続しようとしている場合は、正しいドメインに適切にログインしていることを確認します。  
  
