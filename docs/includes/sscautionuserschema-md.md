---
ms.openlocfilehash: 327fd6bac9bc1036a0dd07f7b955ee92cb7e40c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68223541"
---
  SQL Server 2005 からスキーマの動作が変更されました。 その結果、スキーマがデータベース ユーザーと同じであると想定しているコードでは、正しい結果が返されない場合があります。 以下の DDL ステートメントが使用されているデータベースでは、sysobjects などの古いカタログ ビューを使用してはいけません。CREATE SCHEMA、ALTER SCHEMA、DROP SCHEMA、CREATE USER、ALTER USER、DROP USER、CREATE ROLE、ALTER ROLE、DROP ROLE、CREATE APPROLE、ALTER APPROLE、DROP APPROLE、ALTER AUTHORIZATION。 そのようなデータベースでは、代わりに新しいカタログ ビューを使用してください。 新しいカタログ ビューでは、SQL Server 2005 で導入されたプリンシパルとスキーマの分離が考慮されます。 カタログ ビューの詳細については、「[カタログ ビュー &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/catalog-views-transact-sql.md)」を参照してください。
   