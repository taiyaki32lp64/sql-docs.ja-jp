---
title: 拡張性 API
titleSuffix: Azure Data Studio
description: Azure Data Studio 用の拡張 API について学習します
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 8a4ebe26cbbf768222c7b97b95fa7df238faded3
ms.sourcegitcommit: 56fb0b7750ad5967f5d8e43d87922dfa67b2deac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2019
ms.locfileid: "75001897"
---
# <a name="azure-data-studio-extensibility-apis"></a>Azure Data Studio 拡張 API

[!INCLUDE[name-sos](../includes/name-sos.md)] では、拡張機能を使用して、オブジェクト エクスプローラーなどの Azure Data Studio の他の部分とやりとりできる API を提供します。 これらの API は、[`src/sql/azdata.d.ts`](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/azdata.d.ts) ファイルから入手できます。以下で説明します。

## <a name="connection-management"></a>接続の管理
`azdata.connection`

### <a name="top-level-functions"></a>最上位の関数

- `getCurrentConnection(): Thenable<azdata.connection.Connection>` アクティブなエディターまたはオブジェクト エクスプローラーの選択に基づいて現在の接続を取得します。

- `getActiveConnections(): Thenable<azdata.connection.Connection[]>` アクティブなすべてのユーザーの接続のリストを取得します。 そのような接続がない場合は、空のリストを返します。

- `getCredentials(connectionId: string): Thenable<{ [name: string]: string }>` 接続に関連付けられている資格情報を含むディクショナリを取得します。 それ以外の場合、これらは `azdata.connection.Connection` オブジェクトの下のオプション ディクショナリの一部として返されますが、そのオブジェクトからは削除されます。 

### `Connection`
- `options: { [name: string]: string }` 接続オプションのディクショナリ
- `providerName: string` 接続プロバイダーの名前 (例: "MSSQL")
- `connectionId: string` 接続の一意識別子

### <a name="example-code"></a>コード例
```
> let connection = azdata.connection.getCurrentConnection();
connection: {
    providerName: 'MSSQL',
    connectionId: 'd97bb63a-466e-4ef0-ab6f-00cd44721dcc',
    options: {
        server: 'mairvine-sql-server',
        user: 'sa',
        authenticationType: 'sqlLogin',
        ...
    },
    ...
}
> let credentials = azdata.connection.getCredentials(connection.connectionId);
credentials: {
    password: 'abc123'
}

```

## <a name="object-explorer"></a>オブジェクト エクスプローラー

`azdata.objectexplorer`


### <a name="top-level-functions"></a>最上位の関数
- `getNode(connectionId: string, nodePath?: string): Thenable<azdata.objectexplorer.ObjectExplorerNode>` 指定された接続とパスに対応するオブジェクト エクスプローラー ノードを取得します。 パスが指定されていない場合は、指定された接続の最上位のノードが返されます。 指定されたパスにノードがない場合は、`undefined` が返されます。 注:オブジェクトの `nodePath` は、SQL ツール サービスのバックエンドによって生成されるため、手動では構成しにくいです。 将来の API の改善により、ノード (名前、型、スキーマなど) について指定したメタデータに基づいてノードを取得できるようになります。

- `getActiveConnectionNodes(): Thenable<azdata.objectexplorer.ObjectExplorerNode>` アクティブなオブジェクト エクスプローラーの接続ノードをすべて取得します。

- `findNodes(connectionId: string, type: string, schema: string, name: string, database: string, parentObjectNames: string[]): Thenable<azdata.objectexplorer.ObjectExplorerNode[]>` 指定されたメタデータに一致するオブジェクト エクスプローラー ノードをすべて検索します。 適用できない場合、`schema`、`database`、`parentObjectNames` の引数は `undefined` にする必要があります。 `parentObjectNames` は、目的のオブジェクトが下にある、オブジェクト エクスプローラーの最上位から最下位までのレベルで、データベース以外の親オブジェクトのリストです。 たとえば、接続 ID `connectionId` を使って、テーブル "schema1.table1" とデータベース "database1" に属している列 "column1" を検索している場合、`findNodes(connectionId, 'Column', undefined, 'column1', 'database1', ['schema1.table1'])` を呼び出します。 また、この API 呼び出しについては、[既定で Azure Data Studio でサポートされている型のリスト](https://github.com/Microsoft/azuredatastudio/wiki/Object-Explorer-types-supported-by-FindNodes-API)も参照してください。

### <a name="objectexplorernode"></a>ObjectExplorerNode
- `connectionId: string` ノードが存在する接続の ID

- `nodePath: string``getNode` 関数への呼び出しに使用されるノードのパス

- `nodeType: string` ノードの型を表す文字列

- `nodeSubType: string` ノードのサブタイプを表す文字列

- `nodeStatus: string` ノードの状態を表す文字列

- `label: string` オブジェクト エクスプローラーに表示されるノードのラベル

- `isLeaf: boolean` ノードがリーフ ノードのため、子がないかどうか

- `metadata: azdata.ObjectMetadata` このノードによって表されるオブジェクトを記述するメタデータ

- `errorMessage: string` ノードがエラー状態の場合に表示されるメッセージ

- `isExpanded(): Thenable<boolean>` 現在、ノードがオブジェクト エクスプローラーで展開されているかどうか

- `setExpandedState(expandedState: vscode.TreeItemCollapsibleState): Thenable<void>` ノードを展開するか、折りたたむかを設定します。 状態が None に設定されている場合、ノードは変更されません。

- `setSelected(selected: boolean, clearOtherSelections?: boolean): Thenable<void>` ノードが選択されているかどうかを設定します。 `clearOtherSelections` が True の場合は、新しい選択を行うときに他の選択をすべてクリアします。 False の場合は、既存の選択をすべてそのままにします。 `clearOtherSelections` は、`selected` が True の場合、既定で True に設定されます。`selected` が False の場合は、既定で False に設定されます。

- `getChildren(): Thenable<azdata.objectexplorer.ObjectExplorerNode[]>` このノードの子ノードをすべて取得します。 子が存在しない場合は、空のリストを返します。

- `getParent(): Thenable<azdata.objectexplorer.ObjectExplorerNode>` このノードの親ノードを取得します。 親が存在しない場合は、未定義を返します。

### <a name="example-code"></a>コード例

```cs
private async interactWithOENode(selectedNode: azdata.objectexplorer.ObjectExplorerNode): Promise<void> {
    let choices = ['Expand', 'Collapse', 'Select', 'Select (multi)', 'Deselect', 'Deselect (multi)'];
    if (selectedNode.isLeaf) {
        choices[0] += ' (is leaf)';
        choices[1] += ' (is leaf)';
    } else {
        let expanded = await selectedNode.isExpanded();
        if (expanded) {
            choices[0] += ' (is expanded)';
        } else {
            choices[1] += ' (is collapsed)';
        }
    }
    let parent = await selectedNode.getParent();
    if (parent) {
        choices.push('Get Parent');
    }
    let children = await selectedNode.getChildren();
    children.forEach(child => choices.push(child.label));
    let choice = await vscode.window.showQuickPick(choices);
    let nextNode: azdata.objectexplorer.ObjectExplorerNode = undefined;
    if (choice === choices[0]) {
        selectedNode.setExpandedState(vscode.TreeItemCollapsibleState.Expanded);
    } else if (choice === choices[1]) {
        selectedNode.setExpandedState(vscode.TreeItemCollapsibleState.Collapsed);
    } else if (choice === choices[2]) {
        selectedNode.setSelected(true);
    } else if (choice === choices[3]) {
        selectedNode.setSelected(true, false);
    } else if (choice === choices[4]) {
        selectedNode.setSelected(false);
    } else if (choice === choices[5]) {
        selectedNode.setSelected(false, true);
    } else if (choice === 'Get Parent') {
        nextNode = parent;
    } else {
        let childNode = children.find(child => child.label === choice);
        nextNode = childNode;
    }
    if (nextNode) {
        let updatedNode = await azdata.objectexplorer.getNode(nextNode.connectionId, nextNode.nodePath);
        this.interactWithOENode(updatedNode);
    }
}

vscode.commands.registerCommand('mssql.objectexplorer.interact', () => {
    azdata.objectexplorer.getActiveConnectionNodes().then(activeConnections => {
        vscode.window.showQuickPick(activeConnections.map(connection => connection.label + ' ' + connection.connectionId)).then(selection => {
            let selectedNode = activeConnections.find(connection => connection.label + ' ' + connection.connectionId === selection);
            this.interactWithOENode(selectedNode);
        });
    });
});
```

## <a name="proposed-apis"></a>提案された API

ダイアログ、ウィザード、ドキュメント タブなどの機能の中で、拡張機能でダイアログにカスタム UI を表示できるように、提案された API を追加しました。 その他のドキュメントについては、[提案された API 型ファイル](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/azdata.proposed.d.ts)を参照してください。しかし、これらの API はいつでも変更される可能性があることに注意してください。 これらの API の一部を使用する方法の例は、["sqlservices" のサンプル拡張機能](https://github.com/Microsoft/azuredatastudio/tree/master/samples/sqlservices)で見つけることができます。


