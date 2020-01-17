---
title: '[SQL スクリプトの生成] (レプリケーション オブジェクト) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.generatesqlscript.f1
helpviewer_keywords:
- Generate SQL Script dialog box
ms.assetid: b7ccc34e-1c22-44b8-8eb5-f6423af3164e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2585452ee31c911ea6e288effc3e5e91fff88a64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721269"
---
# <a name="generate-sql-script-replication-objects"></a>[SQL スクリプトの生成] (レプリケーション オブジェクト)
  レプリケーション スクリプトには、パブリケーションやサブスクリプションなど、スクリプト化されたレプリケーション コンポーネントを実装するために必要な [!INCLUDE[tsql](../../includes/tsql-md.md)] システム ストアド プロシージャが含まれます。 トポロジ内のすべてのレプリケーション コンポーンネントは、ディザスター リカバリー計画の一部としてスクリプト化され、スクリプトはタスクの繰り返しの自動化にも使用することができます。 レプリケーションでは、レプリケーション オブジェクトをスクリプト化するための次の 2 つのダイアログ ボックスが用意されています。  
  
-   **[SQL スクリプトの生成]** ダイアログ ボックスは、 **msCoName** の [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]フォルダーと、すべてのサブ フォルダーのショートカット メニューから利用可能です。 このダイアログ ボックスを使用して、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス上のすべてのレプリケーション オブジェクトのスクリプトを作成できます。  
  
-   **[SQL スクリプトの生成 \<ObjectName>]** ダイアログ ボックスは、パブリケーションおよびサブスクリプションのショートカット メニューから利用可能です。 このダイアログ ボックスを使用して、個々のオブジェクトのスクリプトを作成できます。  
  
 これらのダイアログ ボックスでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の単一のインスタンスにオブジェクトのスクリプトを作成します。ダイアログ ボックスは、他のインスタンスに接続して関連するオブジェクトのスクリプトを作成することはありません。  
  
## <a name="generate-sql-script-options"></a>[SQL スクリプトの生成] ダイアログ ボックスのオプション  
 **[ディストリビューターのプロパティ]**  
 ディストリビューターの有効化または無効化、ディストリビューターに関連付けられたパブリッシャーの追加または削除、およびディストリビューション データベースの作成または削除を行うため、ストアド プロシージャのスクリプトを作成します。  
  
 **[次のデータ ソースのパブリケーション]**  
 パブリッシュの有効化または無効化と、パブリケーション、アーティクル、プッシュ サブスクリプション、およびレプリケーション ジョブの作成または削除を行うため、ストアド プロシージャのスクリプトを作成します。  
  
 **[次のデータ ソース内のサブスクリプション]**  
 プル サブスクリプションとレプリケーション ジョブの作成または削除を行うため、ストアド プロシージャのスクリプトを作成します。  
  
 **[コンポーネントを作成または有効にする]** と **[コンポーネントを削除または無効にする]**  
 スクリプトにレプリケーション オブジェクトの作成または削除を行うコマンドを含めるかどうかを指定します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、コンポーネントの有効化と無効化を行うために、ダイアログ ボックスを使用してスクリプト セットを作成することを推奨します。  
  
 **[レプリケーション ジョブ]**  
 ストアド プロシージャの呼び出しに加えて、レプリケーション ジョブのスクリプトを作成します。 このオプションは、ディストリビューターからスクリプトを作成する場合にのみ利用可能です。  
  
 レプリケーション ストアド プロシージャは実行時に必要なジョブを作成します。そのため、このオプションを選択する必要はありません。 ただし、作成したジョブを記録しておくと、個々のジョブを再作成する必要が生じた場合に役に立ちます。  
  
## <a name="generate-sql-script-objectname-options"></a>[SQL スクリプトの生成 \<ObjectName>] ダイアログ ボックスのオプション  
 **[コンポーネントを作成または有効にする]** と **[コンポーネントを削除または無効にする]**  
 スクリプトにレプリケーション オブジェクトの作成または削除を行うコマンドを含めるかどうかを指定します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、コンポーネントの有効化と無効化を行うために、ダイアログ ボックスを使用してスクリプト セットを作成することを推奨します。  
  
 **[レプリケーション ジョブ]**  
 このオプションは、 **[SQL スクリプトの生成]** ダイアログ ボックスからのみ利用可能です。  
  
## <a name="see-also"></a>参照  
 [レプリケーションのスクリプト作成](scripting-replication.md)  
  
  
