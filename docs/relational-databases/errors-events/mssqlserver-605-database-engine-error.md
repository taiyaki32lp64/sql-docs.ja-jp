---
title: MSSQLSERVER_605 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 605 (Database Engine error)
ms.assetid: d8d3a22e-1ff8-48a4-891f-4c8619437e24
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7657c18708e9b54c33f15142c57782da671037f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903931"
---
# <a name="mssqlserver605"></a>MSSQLSERVER_605
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|605|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|WRONGPAGE|  
|メッセージ テキスト|データベース %d の論理ページ %S_PGID のフェッチに失敗しました。 この論理ページは、アロケーション ユニット %I64d ではなく、%I64d に所属しています。|  
  
## <a name="explanation"></a>説明  
一般的に、このエラーは指定されたデータベース内のページまたはアロケーションの破損を意味しています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ページ リンケージをたどるか IAM (Index Allocation Map) を使用してテーブルに属するページを読み取る際に、破損が検出されます。 テーブルに割り当てられるすべてのページは、テーブルに関連付けられているいずれか 1 つのアロケーション ユニットに属している必要があります。 ページ ヘッダーに含まれるアロケーション ユニット ID が、テーブルに関連付けられているアロケーション ユニット ID と一致しない場合、この例外が発生します。 エラー メッセージの一覧で最初に示されるアロケーション ユニット ID はページ ヘッダー内の ID で、2 番目のアロケーション ユニットの値はテーブルに関連付けられている ID です。  
  
**データ破損エラー**  
  
重大度レベル 21 は、データ破損の可能性を示しています。 この原因としては、ページ チェーンの破損、IAM の破損、対象となるオブジェクトの [sys.objects](~/relational-databases/system-catalog-views/sys-objects-transact-sql.md) カタログ ビュー内に無効なエントリがあることなどが考えられます。 これらのエラーは多くの場合、ハードウェア エラーやディスク デバイスのドライバー エラーによって発生します。  
  
**一時的なエラー**  
  
重大度レベル 12 は、一時的なエラーの可能性を示しています。つまり、このエラーはキャッシュ内で発生するもので、ディスク上のデータの破損を示すものではありません。 一時的な 605 エラーは、以下の条件で発生することがあります。  
  
-   オペレーティング システムから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に、処理が途中であるにもかかわらず I/O 操作が完了したことが通知された場合。実際のデータの破損がない場合でも、エラー メッセージが表示されます。  
  
オプティマイザー ヒント NOLOCK を使用してクエリを実行しているか、トランザクション分離レベルを READ UNCOMMITTED に設定している場合。 NOLOCK または READ UNCOMMITTED を使用するクエリで、別のユーザーによる移動または変更が実行中であるデータを読み取ろうとすると、605 エラーが発生します。 一時的な 605 エラーかどうかを確認するには、後でクエリを再実行してください。 詳細については、サポート技術情報 [235880](https://support.microsoft.com/kb/235880/en-us) の「SQL Server で、オプティマイザー ヒント NOLOCK を指定してクエリを実行したり、分離レベルを READ UNCOMMITTED に設定したりすると、エラー 605 が表示される」を参照してください。  
  
一般的に、データ アクセス中にエラーが発生しても、後に続く DBCC CHECKDB 操作がエラーなしで完了した場合、605 エラーは一時的なエラーであったと考えられます。  
  
## <a name="user-action"></a>ユーザーの操作  
605 エラーが一時的なエラーでない場合、問題は深刻です。次の作業を行って修正する必要があります。  
  
1.  次のクエリを実行して、メッセージ内に指定されているアロケーション ユニットと関連付けられているテーブルを特定し、 `allocation_unit_id` をエラー メッセージ内に指定されているアロケーション ユニットと入れ替えます。  
  
    USE`database_name`;  
  
    GO  
  
    SELECT au.allocation_unit_id, OBJECT_NAME(p.object_id) AS table_name, fg.name AS filegroup_name,  
  
    au.type_desc AS allocation_type, au.data_pages, partition_number  
  
    FROM sys.allocation_units AS au  
  
    JOIN sys.partitions AS p ON au.container_id = p.partition_id  
  
    JOIN sys.filegroups AS fg ON fg.data_space_id = au.data_space_id  
  
    WHERE au.allocation_unit_id = `allocation_unit_id` OR au.allocation_unit_id = `allocation_unit_id`  
  
    ORDER BY au.allocation_unit_id;  
  
    GO  
  
2.  エラー メッセージ内に指定されている 2 番目のアロケーション ユニット ID と関連付けられているテーブルに対し、REPAIR 句なしで DBCC CHECKTABLE を実行します。  
  
3.  データベース全体における破損の全範囲を調べるには、できるだけ早く REPAIR 句なしで DBCC CHECKDB を実行します。  
  
4.  エラー ログで、605 エラーと共に頻繁に発生している他のエラーがないかどうかを確認し、Windows イベント ログで、システムまたはハードウェアに関連する問題がないか確認します。 ログに記録されているハードウェアに関する問題があれば、それを修正します。  
  
問題がハードウェアに関連するものでない場合は、次のいずれかの作業を実行します。  
  
1.  既知のクリーン バックアップを使用してデータベースを復元します。 破損したページだけを復元するには、ページ復元バックアップ機能を利用できます。  
  
2.  破損修復の手順 3. で実行した DBCC CHECKDB 操作で推奨された REPAIR 句と共に、DBCC CHECKDB を実行します。 いずれかの REPAIR 句を付けて DBCC CHECKDB を実行しても問題が解決しない場合は、購入元にお問い合わせください。 確認用に、DBCC CHECKDB からの出力を保存しておいてください。  
  
    > [!CAUTION]  
    > REPAIR 句を付けて DBCC CHECKDB を実行した場合にデータにどのような影響があるか確信がない場合は、ステートメントを実行する前に購入元にお問い合わせください。  
  
## <a name="see-also"></a>参照  
[DBCC CHECKTABLE &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checktable-transact-sql.md)  
  
