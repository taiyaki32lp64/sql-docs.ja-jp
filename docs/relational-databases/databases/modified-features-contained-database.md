---
title: 変更された機能 (包含データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- contained database, modifications to DBs
ms.assetid: a2942509-39a2-4903-b504-ae80a300a9de
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3c85d6e423c63337be4d2eaf2f96c420a4f6ad33
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067342"
---
# <a name="modified-features-contained-database"></a>変更された機能 (包含データベース)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  次の機能は、部分的包含データベースでサポートされるように変更されました。 通常、機能の変更は、データベース境界を越えないように行われます。  
  
 詳細については、「 [包含データベース](../../relational-databases/databases/contained-databases.md)」を参照してください。  
  
## <a name="alter-database"></a>ALTER DATABASE  
  
### <a name="application-level"></a>アプリケーション レベル  
 ALTER DATABASE ステートメントを包含データベース内から使用する場合の構文は、非包含データベースに使用する構文と異なります。 この相違点には、データベースを超えてインスタンスにまで拡張されるステートメントの要素に関する制限が含まれます。 詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)」を参照してください。  
  
### <a name="instance-level"></a>インスタンス レベル  
 ALTER DATABASE ステートメントを包含データベース外で使用する場合の構文は、非包含データベースに使用する構文と異なります。 これらの変更を防ぐためには、データベースの境界を越えます。 詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)」を参照してください。  
  
## <a name="create-database"></a>CREATE DATABASE  
 CREATE DATABASE の構文は、包含データベースを使用する場合と非包含データベースを使用する場合とで異なります。 新しい構文の要件と許容値の詳細については、「[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)」を参照してください。  
  
## <a name="temporary-tables"></a>一時テーブル  
 包含データベース内でローカル一時テーブルを使用することはできますが、その動作は非包含データベース内のローカル一時テーブルの動作と異なります。 非包含データベースでは、一時テーブル データは **tempdb**の照合順序で照合されます。 包含データベースでは、一時テーブル データは包含データベースの照合順序で照合されます。  
  
 一時テーブルに関連付けられているすべてのメタデータ (テーブル名、列名、インデックスなど) には、カタログの照合順序が適用されます。  
  
 一時テーブル内では名前付き制約を使用できません。  
  
 一時テーブルでは、ユーザー定義型、XML スキーマ コレクション、またはユーザー定義関数を参照できません。  
  
## <a name="collation"></a>照合順序  
 非包含データベース モデルでは、3 種類の照合順序があります。データベースの照合、インスタンスの照合、および tempdb の照合です。 包含データベースでは、データベースの照合順序と新しいカタログの照合順序の 2 種類の照合順序のみが使用されます。 包含データベースの照合順序の詳細については、「 [包含データベースの照合順序](../../relational-databases/databases/contained-database-collations.md) 」を参照してください。  
  
## <a name="user-options"></a>ユーザー オプション  
 包含データベースを有効にする場合、 [のインスタンスに対して](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md) user options オプション [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を 0 に設定する必要があります。  
  
## <a name="see-also"></a>参照  
 [包含データベースの照合順序](../../relational-databases/databases/contained-database-collations.md)   
 [包含データベース](../../relational-databases/databases/contained-databases.md)  
  
  
