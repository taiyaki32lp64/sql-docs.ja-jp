---
title: MSSQLSERVER_3168 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3168 (Database Engine error)
ms.assetid: 991111d9-1eb3-43e9-9333-a75a775c3200
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 00538607fca244177541b20b96324c421a3746f9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039298"
---
# <a name="mssqlserver3168"></a>MSSQLSERVER_3168
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|3168|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|LDDB_SYSTEMWRONGVER|  
|メッセージ テキスト|デバイス %ls のシステム データベースのバックアップは復元できません。このバックアップを作成したサーバーのバージョン (%ls) とこのサーバーのバージョン (%ls) が異なります。|  
  
## <a name="explanation"></a>説明  
サーバーのビルドが最初のバックアップ実行時のビルドと異なる場合、システム データベース (**master**、**model**、**msdb**) のバックアップは復元できません。  
  
> [!NOTE]  
> Service Pack または修正プログラムのビルドをインストールすると、サーバーのビルド番号は変更されます。サーバーのビルドは常に増分です。  
  
### <a name="possible-causes"></a>考えられる原因  
システム データベースのデータベース スキーマが、サーバー ビルド間で変更されている可能性があります。 スキーマの変更によって一貫性が失われないようにするには、RESTORE ステートメントで、バックアップ ファイルのサーバー ビルド番号とバックアップを復元するサーバーのビルド番号を比較します。 ビルドが異なる場合、ステートメントでは 3168 のエラー メッセージが返され、復元操作は異常終了します。  
  
たとえば、次のような場合にこの問題が発生します。  
  
-   サーバー A のシステム データベースを、サーバー B で行ったバックアップから復元しようとしており、サーバー A とサーバー B でサーバー ビルドが異なる。 たとえば、サーバー A が最初のリリース バージョンのビルドで、サーバー B が Service Pack 1 (SP1) ビルドであるような場合です。  
  
-   同じサーバーで行ったバックアップからシステム データベースを復元しようとしており、 バックアップ時にサーバーでは別のビルドを実行していた (つまり、バックアップ後にサーバーがアップグレードされた)。  
  
## <a name="user-action"></a>ユーザーの操作  
この状況での復元プロセスはかなり複雑になるため、最後の手段としてのみ使用します。 詳細については、「[SQL Server の別のビルドにデータベースのシステム バックアップを復元することができません。](https://support.microsoft.com/kb/264474)」を参照してください。  
  
## <a name="see-also"></a>参照  
[システム データベースのバックアップと復元 &#40;SQL Server&#41;](~/relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
