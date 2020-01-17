---
title: JDBC ドライバーのデータ型についてMicrosoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7802328d-4d23-4775-9573-4169b127d258
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a8daea8b477be13dd7b267a17ddf5f960868f579
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027272"
---
# <a name="understanding-the-jdbc-driver-data-types"></a>JDBC ドライバーのデータ型について

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をデータベースとして使用する Java アプリケーション内での、JDBC の基本データ型と高度なデータ型の使用をサポートします。  
  
JDBC の型システムは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型と Java 言語の型やオブジェクトとの間の変換を仲介します。 JDBC の型は、SQL-92 および SQL-99 の型をモデルにしています。 JDBC ドライバーは、JDBC 仕様を満たし、予測可能性と柔軟性の適切なバランスを維持できるように設計されています。  
  
このセクションのトピックでは、基本型および高度な型の使用方法と、データ型を他のデータ型に変換する方法について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
| トピック                                                                                                                                            | [説明]                                                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [基本データ型の使用](../../connect/jdbc/using-basic-data-types.md)                                                                           | JDBC の基本データ型について説明します。 これには、結果セット、パラメーター化クエリ、およびストアド プロシージャを使用してデータ型を操作する方法の例が含まれます。                                                                                                        |
| [java.sql.Time の値をサーバーに送信する方法の構成](../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md) | JDBC Driver での日付の生成方法について説明します。                                                                                                                                                                                                                       |
| [高度なデータ型の使用](../../connect/jdbc/using-advanced-data-types.md)                                                                     | JDBC の高度なデータ型について説明します。                                                                                                                                                                                                                              |
| [データ型の違いについて](../../connect/jdbc/understanding-data-type-differences.md)                                                 | JDBC ドライバーのさまざまなデータ型の違いについて説明します。                                                                                                                                                                                                    |
| [データ型変換について](../../connect/jdbc/understanding-data-type-conversions.md)                                                 | getter メソッドおよび setter メソッドを使用するときに、データ型の変換を処理する方法について説明します。                                                                                                                                                                                  |
| [各国語文字セットのサポート](../../connect/jdbc/national-character-set-support.md)                                                           | National Character Set の型のサポートについて説明します。                                                                                                                                                                                                          |
| [XML データのサポート](../../connect/jdbc/supporting-xml-data.md)                                                                                 | SQLXML インターフェイスについて説明します。 **SQLXML** Java データ型を使用して、リレーショナル データベースから XML データを読み取ったり、リレーショナル データベースに XML データを書き込んだりする方法についても説明します。                                                                                                             |
| [ラッパーとインターフェイス](../../connect/jdbc/wrappers-and-interfaces.md)                                                                         | アプリケーション サーバーがクラスのプロキシを作成することを可能にする、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 固有のメソッドと定数を持つインターフェイスについて説明します。また、`java.sql.Wrapper` インターフェイスのサポートについても説明します。 |
  
## <a name="see-also"></a>参照

[JDBC ドライバーの概要](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
