---
title: MSSQLSERVER_8992 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8992 (Database Engine error)
ms.assetid: 68467e6a-09d8-478f-8bd9-3bb09453ada3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8ad75e136c4bef59f24b451b84f03e06d71a32ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62912546"
---
# <a name="mssqlserver8992"></a>MSSQLSERVER_8992
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|8992|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC3_CHECK_CATALOG|  
|メッセージ テキスト|チェック カタログ メッセージ エラー レベル レベル状態の状態:メッセージ。|  
  
## <a name="explanation"></a>説明  
 DBCC CHECKCATALOG または DBCC CHECKDB により、指定されたオブジェクトの不整合がシステム メタデータ テーブルで検出されました。 つまり、記録されたオブジェクト ID とエラー メッセージで指定されたオブジェクトの間に不整合があります。  
  
 このエラーは、システム メタデータに不整合が生じるような方法で 1 つ以上のシステム テーブルを手動で更新した場合に発生することがあります。 たとえば、ユーザーが他のテーブルにある関連する行 (**sysindexes** や **syscolumns** など) を削除せずに、**sysobjects** テーブルからオブジェクトを手動で削除した可能性があります。  
  
 このエラーは、SQL Server 2000 から SQL Server 2005 以降にアップグレードされたデータベースに対して DBCC CHECKDB を実行しているときに発生することがあります。 SQL Server 2000 では、DBCC CHECKDB に DBCC CHECKCATALOG 機能がありませんでした。そのため、SQL Server 2000 のデータベースに対して DBCC CHECKCATALOG を指定して実行しない限り、アップグレード前にこのエラーはキャッチされません。  
  
 エラー 8992 と共に、次のいずれかのエラーが表示される場合があります。  
  
 メッセージ 3851 - システム テーブル sys.%ls%ls に無効な行 (%ls) が見つかりました。  
  
 メッセージ 3852 - sys.%ls%ls の行 (%ls) と一致する行 (%ls) が sys.%ls%ls にありません。  
  
 3853 - sys.%ls%ls の行 (%ls) の属性 (%ls) には、sys.%ls%ls に一致する行 (%ls) がありません。  
  
 3854 - 属性 (%ls) (sys.%ls%ls の行 (%ls)) には、sys.%ls%ls に一致する行 (%ls) がありますが、無効です。  
  
 3855 - 属性 (%ls) が存在しますが、sys.%ls%ls の行 (%ls) がありません。  
  
 3856 - 属性 (%ls) が存在しますが、sys.%ls%ls の行 (%ls) では使用できません。  
  
 3857 - 属性 (%ls) が必要ですが、sys.%ls%ls の行 (%ls) にはありません。  
  
 3858 - sys.%ls%ls の行 (%ls) の属性 (%ls) には、無効な値が含まれています。  
  
## <a name="user-action"></a>ユーザーの操作  
  
### <a name="drop-and-re-create-the-specified-object"></a>指定されたオブジェクトを削除して再作成する  
 可能であれば、指定されたオブジェクトを削除して再作成します。 たとえば、オブジェクトがストアド プロシージャまたはユーザー定義型である場合、オブジェクトを再作成することで問題が解決する可能性があります。  
  
### <a name="restore-from-backup"></a>バックアップから復元する  
 問題がハードウェアに関するものではなく、また既知のクリーン バックアップがある場合は、そのバックアップを使用してデータベースを復元します。 この操作は、バックアップにメタデータ エラーが含まれていない場合にのみ実行できます。  
  
### <a name="export-the-data-to-a-new-database"></a>新しいデータベースにデータをエクスポートする  
 また、バックアップにメタデータの不整合が含まれている場合は、新しいデータベースを作成し、作成したデータベースに既存のデータベースのコンテンツをエクスポートする必要があります。  
  
### <a name="dbcc-checkdb-cannot-repair-this-error"></a>DBCC CHECKDB でこのエラーを修復できない  
 このエラーを修正することはできません。  バックアップからデータベースを復元できない場合は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] カスタマー サポート サービス (CSS) にご連絡ください。  
  
### <a name="do-not-manually-update-system-tables"></a>システム テーブルを手動で更新しない  
 システム テーブルは手動で更新しないでください。 SQL Server では、システム テーブルを手動で変更することはサポートされていません。 SQL Server データベース内のシステム テーブルを更新すると、2 つのイベント (イベント ID 17659 とイベント ID 3859) がログに記録されます。 詳細については、サポート技術情報の資料 2688307「SQL Server データベース内のシステム テーブルを更新するとイベント ID 17659 とイベント ID 3859 がログに記録される」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server データベース内のシステム テーブルを更新するとイベント ID 17659 とイベント ID 3859 がログに記録される](https://support.microsoft.com/kb/2688307/EN-US)  
  
  
