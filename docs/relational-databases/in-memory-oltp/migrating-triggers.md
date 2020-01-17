---
title: トリガーの移行 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ad5385c5-5a50-40ca-a319-97d5606b8511
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4629b9f18cdf0b97b5a79cff0696973cb60f7c36
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050137"
---
# <a name="migrating-triggers"></a>トリガーの移行
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  このトピックでは、DDL トリガーとメモリ最適化テーブルについて説明します。  
  
 DML トリガーはメモリ最適化テーブルでサポートされていますが、FOR または AFTER トリガー イベントを使用する場合に限られます。 例については「 [FROM またはサブクエリを使用した UPDATE を実装する](../../relational-databases/in-memory-oltp/implementing-update-with-from-or-subqueries.md)」を参照して下さい。 
  
 LOGON トリガーとは、LOGON イベントで起動するように定義されたトリガーです。 LOGON トリガーは、メモリ最適化テーブルに影響しません。  
  
## <a name="ddl-triggers"></a>DDL トリガー  
 DDL トリガーとは、自らを定義しているデータベースまたはサーバーに対して CREATE、ALTER、DROP、GRANT、DENY、REVOKE、または UPDATE STATISTICS の各ステートメントを実行したときに起動するように定義されているトリガーです。  
  
 データベースまたはサーバーで、CREATE_TABLE イベントまたはこのイベントを含むイベント グループに対応する 1 つ以上の DDL トリガーが定義されている場合は、メモリ最適化テーブルを作成できません。 データベースまたはサーバーで、DROP_TABLE イベントまたはこのイベントを含むイベント グループに対応する 1 つ以上の DDL トリガーが定義されている場合は、メモリ最適化テーブルを削除できません。  
  
 CREATE_PROCEDURE、DROP_PROCEDURE、またはこれらのイベントを含むイベント グループに対応する 1 つ以上の DDL トリガーが存在している場合は、ネイティブ コンパイル ストアド プロシージャを作成できません。  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP への移行](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
