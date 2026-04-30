# ER図（エンティティ関連図）

## 図

```mermaid
erDiagram

    BOARD {
        string id PK "ボードID（一意の識別子）"
        string title "ボードのタイトル"
        string createdAt "作成日時"
    }

    LIST {
        string id PK "リストID（一意の識別子）"
        string boardId FK "所属するボードのID"
        string title "リストのタイトル"
        int position "表示順（左から何番目か）"
        string createdAt "作成日時"
    }

    CARD {
        string id PK "カードID（一意の識別子）"
        string listId FK "所属するリストのID"
        string title "カードのタイトル（タスク名）"
        string memo "メモ（自由記述）"
        string dueDate "期日（例：2026-05-10）"
        int position "表示順（上から何番目か）"
        string createdAt "作成日時"
    }

    BOARD ||--o{ LIST : "1つのボードは複数のリストを持つ"
    LIST  ||--o{ CARD : "1つのリストは複数のカードを持つ"
```

---

## 用語の説明

| 用語 | 説明 |
|------|------|
| **PK**（Primary Key） | そのデータを一意に識別するID。他と絶対に重複しない |
| **FK**（Foreign Key） | 別のテーブルのIDを参照する項目。どこに所属するかを表す |
| **\|\|--o{** | 「1対多」の関係を表す記号。1つのボードに複数のリストが属する |

---

## 関係の説明

```
BOARD（ボード）
  └── LIST（リスト）　※ 1つのボードに複数のリストが属する
        └── CARD（カード）　※ 1つのリストに複数のカードが属する
```

- **BOARD → LIST**：1つのボードは0個以上のリストを持てる
- **LIST → CARD**：1つのリストは0個以上のカードを持てる
- カードは必ずどこか1つのリストに所属する
- リストは必ずどこか1つのボードに所属する
