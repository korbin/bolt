---
title: メッセージ・イベントのリスニング
lang: ja-jp
slug: message-listening
order: 1
---

<div class="section-content">
[アプリが受信権限を持っている](https://api.slack.com/messaging/retrieving#permissions)メッセージをリスニングするには、`message`型でないイベントを除外する`message()` メソッドを使用します。

`message()` は、パターンと一致しないメッセージを除外する、 `string` 型の `pattern` パラメーター (オプション) または `RegExp` オブジェクトを受け入れます。
</div>

```javascript
// 特定の文字列、この場合 👋絵文字を含むメッセージと一致
app.message(':wave:', async ({ message, say }) => {
  say(`Hello, <@${message.user}>`);
});
```

<details class="secondary-wrapper">
<summary class="section-head" markdown="0">
<h4 class="section-head">正規表現（RegExp） パターンの使用</h4>
</summary>

<div class="secondary-content" markdown="0">
文字列の代わりに 正規表現(RegExp) パターンを使用すると、照合の精度を高めることができます。

RegExp の一致結果はすべて `context.matches` に格納されます。
</div>

```javascript
app.message(/^(hi|hello|hey).*/, async ({ context, say }) => {
  // context.matches の内容が特定の正規表現と一致
  const greeting = context.matches[0];

  say(`${greeting}, how are you?`);
});
```

</details>
