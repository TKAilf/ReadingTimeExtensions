### 読了時間バッジの追加
このスクリプトは、指定したarticle要素のテキスト内容を解析して、読了時間のバッジを生成し、ページに追加します。

```javascript
// `article`要素をドキュメントから検索して取得します。
const article = document.querySelector("article");

if (article) {
  // article要素のテキスト内容を取得します。
  const text = article.textContent;
  
  // 単語をマッチさせるための正規表現を定義します。
  const wordMatchRegExp = /[^\s]+/g;

  // matchAllメソッドを使用して、textから全ての単語を検索します。
  const words = text.matchAll(wordMatchRegExp);

  // matchAllはイテレータを返すので、単語数を取得するために配列に変換します。
  const wordCount = [...words].length;

  // 読了時間を計算します。
  const readingTime = Math.round(wordCount / 200);

  // 読了時間を表示するための新しいp要素（バッジ）を作成します。
  const badge = document.createElement("p");
  
  // 作成したバッジにスタイルを適用するためにクラスを追加します。
  badge.classList.add("color-secondary-text", "type--caption");
  
  // バッジに表示するテキストを設定します。
  badge.textContent = `⏱️ ${readingTime} min read`;

  // article要素内の最初のh1要素を検索します。
  const heading = article.querySelector("h1");
  
  // article要素内のtime要素を検索し、その親要素を取得します。
  const date = article.querySelector("time")?.parentNode;
  
  // dateがnullまたはundefinedでない場合はdateを使用し、そうでない場合はheadingを使用して、バッジを適切な位置に挿入します。
  (date ?? heading).insertAdjacentElement("afterend", badge);
}
```

### 解説
* document.querySelector: ページ内の最初のarticle要素を取得します。マッチする要素がない場合はnullを返します。  
* 正規表現: 単語を検出するために、非空白文字にマッチする正規表現を使用します。  
* matchAll: 全てのマッチする単語を検索し、イテレータを返します。イテレータを配列に変換して単語数を計算します。  
* 読了時間: 1分あたり200単語を読むと仮定して読了時間を計算し、結果を四捨五入します。  
* バッジの生成と挿入: 読了時間を表示するバッジを生成し、適切な位置に挿入します。
