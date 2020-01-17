---
title: MSSQLSERVER_21899 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21899 (Database Engine error)
ms.assetid: 32b87a7c-5380-4638-b147-dd78618f6625
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3bb511fcfc62d2175721b68cf0c8bf554f1b54b7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056594"
---
# <a name="mssqlserver21899"></a>MSSQLSERVER_21899
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|21899|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQLErrorNum21899|  
|メッセージ テキスト|元のパブリッシャー '%s' のサブスクライバーの sysserver エントリがあるかどうかを判断するために、リダイレクトされたパブリッシャー '%s' で実行したクエリが、エラー '%d'、エラー メッセージ '%s' で失敗しました。|  
  
## <a name="explanation"></a>説明  
**sp_validate_redirected_publisher** は、リモート サーバーでパブリッシャー データベースのサブスクリプション メタデータ テーブルにクエリを実行し、関連付けられているサブスクライバーを特定します。 このクエリが失敗すると、エラー 21899 が返されます。 検証のクエリでは、リダイレクトされたパブリッシャーのパブリッシュされたデータベースにアクセスする必要があります。 元のパブリッシャーに対して **sp_adddistpublisher** が呼び出されたときに指定されたログインに、リダイレクトされたパブリッシャーのパブリッシュされたデータベースにアクセスするための権限がない場合、エラー 21899 が返されます。  
  
## <a name="user-action"></a>ユーザーの操作  
示されたエラー メッセージを確認し、エラーの原因を特定して適切な修正措置を行います。  
  
