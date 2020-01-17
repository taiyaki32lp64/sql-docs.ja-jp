---
title: MSSQLSERVER_3169 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "3169"
helpviewer_keywords:
- 3169 (Database Engine error)
ms.assetid: 7d4dbed6-bb94-4908-bc03-2040a9cf63bc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 06a81eaa83b3420912494b61135790c4e8fabe29
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039292"
---
# <a name="mssqlserver3169"></a>MSSQLSERVER_3169
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|3169|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|NA|  
|メッセージ テキスト|データベースはバージョン %ls を実行中のサーバーにバックアップされました。 このバージョンは、このサーバー (バージョン %ls を実行) とは互換性がありません。 バックアップをサポートしているサーバーでデータベースを復元するか、またはこのサーバーと互換性のあるバックアップを使用してください。|  
  
## <a name="explanation"></a>説明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の一部の機能は、データベース ファイルの構造に影響を与えます。 データベースを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の別のインスタンスに復元する場合、ファイル形式が [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]の別のバージョンと互換性がない可能性があります。  
  
たとえば、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 以降のバージョンで vardecimal ストレージ形式を使用して、それよりも前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でデータベース ファイルを復元しようとすると、このエラーが発生することがあります。  
  
## <a name="user-action"></a>ユーザーの操作  
元のサーバーで実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンを判断します。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で、サーバーを右クリックして **[プロパティ]** をクリックするか、クエリ ウィンドウで「**SELECT @@VERSION** 」と入力します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の元のバージョンを使用してデータベースを開きます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで、元のデータベースで有効になっている機能を調べます。 データベースの復元先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンで使用できるように、これらの設定を修正します。  
  
