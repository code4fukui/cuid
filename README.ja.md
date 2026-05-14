# cuid2

水平スケーリングとパフォーマンスに最適化された、セキュアで衝突耐性のあるID。次世代のUUID。

## 特徴

-   **セキュア:** 次のIDを推測することは事実上不可能です。Cuid2は複数の独立したエントロピー源を使用し、セキュリティ監査済みのNIST標準の暗号論的に安全なハッシュアルゴリズム（SHA3-512）でそれらをハッシュ化します。
-   **衝突耐性:** 同じIDが2回生成される可能性は極めて低いです。1回の衝突が発生する確率が50%になるには、およそ400京（4 × 10¹⁸）個のIDを生成する必要があります。
-   **水平スケーラブル:** 調整なしで複数のマシン上でIDを生成できます。
-   **オフライン対応:** ネットワーク接続なしでIDを生成できます。
-   **URLや名前に使いやすい:** 特殊文字を含みません。
-   **高速で便利:** 非同期操作はなく、ライブラリはgzip圧縮で5KB未満です。

## インストール

```bash
npm install @paralleldrive/cuid2
```

## 使い方

```javascript
import { createId } from "@paralleldrive/cuid2";

const id = createId();
// 'tz4a98xxat96iws9zmbrgj3a'
```

## API

### `init(options)`

独自の乱数生成器、長さ、またはホストフィンガープリントを提供することで、ID生成をカスタマイズできます。

```javascript
import { init } from "@paralleldrive/cuid2";

// カスタムID生成器の作成
const createId = init({
  // 0から1の範囲の値を返すカスタム乱数関数
  random: Math.random,
  // IDの長さ
  length: 10,
  // ホスト環境のカスタムフィンガープリント
  fingerprint: "a-custom-host-fingerprint",
});

const customId = createId(); // 例: 'wjfazn7qnd'
```

### `isCuid(id)`

文字列が有効なCuidかどうかを確認します。

```javascript
import { createId, isCuid } from "@paralleldrive/cuid2";

console.log(
  isCuid(createId()), // true
  isCuid("not a cuid") // false
);
```

## 乱数性と分布

Cuid2は、一様でランダムな分布を持つIDを生成するように設計されています。これはセキュリティと衝突耐性において重要です。同梱のデモアプリケーションは、生成されたIDのセグメントをキャンバス上のピクセル座標にマッピングすることでこの特性を視覚化しており、結果として識別可能なパターンのないホワイトノイズのような画像が生成されます。

## ライセンス

MIT License — 詳細は [LICENSE](LICENSE) を参照してください。
