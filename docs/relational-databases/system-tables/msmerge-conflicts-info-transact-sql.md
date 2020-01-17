---
title: MSmerge_conflicts_info (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_conflicts_info_TSQL
- MSmerge_conflicts_info
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflicts_info system table
ms.assetid: 6b76ae96-737a-4000-a6b6-fcc8772c2af4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7629bff37fb33080f8057fc1799437fff182882f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044803"
---
# <a name="msmerge_conflicts_info-transact-sql"></a>MSmerge_conflicts_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_conflicts_info**テーブルはマージ パブリケーションに対するサブスクリプションを同期するときに発生する競合を追跡します。 競合行のデータが格納されている、 [MSmerge_conflict_publication_article](../../relational-databases/system-tables/msmerge-conflict-publication-article-transact-sql.md)テーブル アーティクルの競合が発生しました。 このテーブルは、パブリケーション データベースでパブリッシャーとサブスクライバー側でサブスクリプション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|パブリッシュされたテーブルのニックネームです。|  
|**rowguid**|**uniqueidentifier**|競合している行の識別子です。|  
|**origin_datasource**|**nvarchar (255)**|競合している変更が発生したデータベースの名前です。|  
|**conflict_type**|**int**|型が発生した競合のできる、次のいずれか。<br /><br /> **1** = 更新の競合。行レベルで競合が検出されています。<br /><br /> **2** = 列更新の競合。列レベルで検出された競合します。<br /><br /> **3** = update 削除が優先される競合。削除が優先されます。<br /><br /> **4** = update Wins 削除の競合。競合を避けるに削除された rowguid が、このテーブルに記録されます。<br /><br /> **5** = 挿入のアップロードに失敗しました。パブリッシャーでサブスクライバーからの挿入を適用できませんでした。<br /><br /> **6** = 挿入のダウンロードに失敗しました。サブスクライバーでパブリッシャーからの挿入を適用できませんでした。<br /><br /> **7** = 削除のアップロードに失敗しました。サブスクライバーでの削除をパブリッシャーにアップロードされませんでした。<br /><br /> **8** = 削除のダウンロードに失敗しました。パブリッシャーでの削除がサブスクライバーにダウンロードできませんでした。<br /><br /> **9** = アップロードを更新できませんでした。サブスクライバーで更新プログラムをパブリッシャー側で適用されませんでした。<br /><br /> **10** = 更新のダウンロードに失敗しました。パブリッシャーでの更新をサブスクライバーに適用されませんでした。<br /><br /> **11**解像度を =<br /><br /> **12** = 論理レコードの更新の Wins の削除。競合を避ける削除された論理レコードは、このテーブルに記録されます。<br /><br /> **13** = 論理レコード競合挿入の更新。更新プログラムを論理レコードの競合を挿入します。<br /><br /> **14** = 論理レコードの削除が優先される更新競合。競合を避ける更新された論理レコードは、このテーブルに記録されます。|  
|**reason_code**|**int**|状況依存のエラー コード。 この列で使用される値では、更新-更新と更新、削除の競合の場合と同じ、 **conflict_type**します。 ただし、失敗した変更の競合の理由コードはエラーは、変更を適用することから、マージ エージェントです。 たとえば、マージ エージェントは、主キー違反のため、サブスクライバーで挿入を適用することはできない場合、ログに記録、 **conflict_type** 6 (「挿入のダウンロードに失敗しました」) の**reason_code** 2672 がある、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]主キー違反の内部エラー メッセージ。"%Ls 制約の違反 ' %. * ls'。 オブジェクトが重複するキーを挿入できません ' % です。\*ls'"。|  
|**reason_text**|**nvarchar(720)**|状況依存エラーの説明。|  
|**pubid**|**uniqueidentifier**|パブリケーションの識別子。|  
|**MSrepl_create_time**|**datetime**|競合が発生した時刻。|  
|**origin_datasource_id**|**uniqueidentifier**|競合する変更が発生したデータベースの識別子。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
