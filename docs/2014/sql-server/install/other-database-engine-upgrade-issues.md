---
title: その他のデータベース エンジンのアップグレード問題 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], upgrading
ms.assetid: 78a1d8e8-fa97-476f-8777-84617d145340
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f247f9addde6baa949f3260d7a9d9f86ce0c5bff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093699"
---
# <a name="other-database-engine-upgrade-issues"></a>データベース エンジンのアップグレードに関するその他の問題
  アップグレードに関する次の問題は、現在のバージョンのアップグレード アドバイザーでは検出されません。 一覧表示されている問題を確認し、使用するシステムへの影響を判断してください。  
  
## <a name="multiple-database-engine-deprecated-features"></a>データベース エンジンの複数の非推奨の機能  
 次に示す [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントまたはオプションは非推奨とされます：  
  
-   BACKUP LOG の NO_LOG オプションと TRUNCATE_ONLY オプション  
  
-   BACKUP TRANSACTION  
  
-   RESTORE TRANSACTION  
  
-   DUMP  
  
-   LOAD  
  
-   DBCC CONCURRENCYVIOLATION  
  
-   sp_addalias  
  
-   sp_addgroup  
  
-   sp_changegroup  
  
-   sp_dropgroup  
  
-   sp_helpgroup  
  
-   syssegments  
  
 VIA プロトコルの使用による[!INCLUDE[ssDE](../../includes/ssde-md.md)]への接続は、非推奨とされます。  
  
## <a name="new-data-types"></a>新しいデータ型  
 次の型がシステム型として予約されます。 アップグレードする前、またはアップグレードした後に、競合する既存のユーザー定義型の名前を変更してください。  
  
-   Geography  
  
-   Geometry  
  
-   Datetime2  
  
-   HierarchyID  
  
## <a name="target-table-of-the-output-into-clause-cannot-have-any-defined-triggers"></a>定義済みのトリガーを使用できなくなった OUTPUT INTO 句の対象テーブル  
 OUTPUT INTO テーブルに有効なトリガーがある場合は、ターゲット テーブルはサポートされていません。  
  
## <a name="compile-time-error-for-udfs-when-the-target-of-an-output-into-clause-is-a-table"></a>OUTPUT INTO 句の対象がテーブルである場合に発生する UDF のコンパイル時エラー  
 ユーザー定義関数 (UDF) は、データベースの状態を変更するアクションの実行には使用できません。 たとえば、テーブル変数以外のオブジェクトに対して、UDF で DDL (CREATE、ALTER、DROP) または DML (INSERT、UPDATE、DELETE) アクションを実行することはできません。  
  
## <a name="merge-is-a-reserved-keyword"></a>予約済みキーワードになった MERGE  
 MERGE は完全に予約されたキーワードになりました。 アプリケーションでは、MERGE という名前のオブジェクト (テーブルや列など) を使用できなくなりました。  
  
## <a name="rename-cdc-schema"></a>CDC スキーマの名前の変更  
 CDC というスキーマ名が存在します。 このスキーマ名が使用されている場合にすることはできません**Change Data Capture**データベースが有効になっています。  
  
 有効にする前に、CDC スキーマを削除する必要があります**Change Data Capture**データベース。 この手順は、アップグレードの前でも後でも実行できます。 スキーマを削除するには、次の手順を実行します。  
  
1.  ALTER SCHEMA を使用して、CDC スキーマから新しいスキーマ名にオブジェクトを転送します。  
  
2.  新しいスキーマ内のオブジェクトに対する権限を確認します。  
  
3.  アプリケーションに必要な変更を加えます。  
  
4.  DROP SCHEMA を使用して CDC スキーマを削除します。  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)  
  
  
