---
title: MSSQLSERVER_50000 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 50000 [SQL Server Native Client setup error]
ms.assetid: 5426d87a-d5d9-4984-b211-b07d69e834a2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 741420467a50aff6cdd0486c91dbf69224b160e7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62761623"
---
# <a name="mssqlserver50000"></a>MSSQLSERVER_50000
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|製品バージョン|11.0|  
|イベント ID|50000|  
|イベント ソース|SETUP|  
|コンポーネント|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client|  
|シンボル名||  
|メッセージ テキスト|ファイル '%.*ls' の読み取り中にネットワーク エラーが発生しました。|  
  
## <a name="explanation"></a>説明  
 名前が sqlncli.msi から変更された MSI ファイルを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client がインストールされているコンピューターで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client をインストール (または更新) しようとしました。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、既存のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client をアンインストールします。 このエラーを防ぐには、sqlncli.msi 以外の名前の MSI ファイルから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client をインストールしないようにします。  
  
## <a name="internal-only"></a>内部使用のみ  
  
