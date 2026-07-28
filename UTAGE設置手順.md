# BOOSTER！応援共創ラボ カレンダー設置手順

公開ページ: https://uyaisin.github.io/booster-calendar/
ソース: `~/CC-booster/calendar-page/index.html`（リポジトリ `uyaisin/booster-calendar`）
対象カレンダー: `info.ooenfes@gmail.com`（すでに一般公開設定済み）

---

## 1. 公式LINE「BOOSTER！応援共創ラボ」のリッチメニュー

対象ボタンのアクションを「リンク（URL）」にして、以下を設定する。

```
https://uyaisin.github.io/booster-calendar/
```

- ボタンのラベル例: 「イベント予定」「開催スケジュール」
- LINE内蔵ブラウザで開かれた場合は、ページ上部に「ブラウザで開いてください」の案内が自動表示される（それ以外の環境では非表示）

## 2. 会員サイト《 BOOSTER！応援共創ラボ 》

### 方式A（推奨）: ページごと埋め込む

レッスン本文のHTMLブロックに貼る。カレンダー・追加ボタン・iCal URL がまとめて入る。

```html
<div style="max-width:800px;margin:0 auto;">
  <iframe src="https://uyaisin.github.io/booster-calendar/"
          style="width:100%;height:1500px;border:0;"
          title="イベントスケジュール" loading="lazy"></iframe>
</div>
```

### 方式B: 方式Aでiframeが消される場合

UTAGEのエディタがiframeをそぎ落とすことがある。その場合はボタンリンクに置き換える。

```html
<p style="text-align:center;">
  <a href="https://uyaisin.github.io/booster-calendar/" target="_blank" rel="noopener"
     style="display:inline-block;padding:14px 28px;border-radius:10px;
            background:#c8622f;color:#fff;text-decoration:none;font-weight:600;">
    イベントスケジュールを見る／カレンダーに追加する
  </a>
</p>
```

### 方式C: カレンダーだけを直接貼る場合

```html
<iframe src="https://calendar.google.com/calendar/embed?src=info.ooenfes%40gmail.com&ctz=Asia%2FTokyo&mode=AGENDA&showTitle=0&showPrint=0&showCalendars=0&showTz=0"
        style="width:100%;min-width:330px;height:600px;border:0;"
        title="イベントスケジュール" loading="lazy"></iframe>
```

---

## 会員が自分のカレンダーに追加する流れ

- **Googleカレンダー**: ページの「Googleカレンダーに追加する」を押す → 購読追加。以後こちらが予定を足せば全員に自動反映
- **iPhone / Outlook**: ページ下部の iCal URL を「照会するカレンダー」として登録

iCal URL:
```
https://calendar.google.com/calendar/ical/info.ooenfes%40gmail.com/public/basic.ics
```

---

## 運用メモ

- 予定の追加・変更は **Googleカレンダー側だけ** でよい。ページ・会員サイト・リッチメニューは触らなくても最新になる
- ページの文言・色を変えるときは `index.html` 末尾の `CONFIG` を編集 → `git add . && git commit -m "..." && git push`。反映まで1〜2分
- 一般公開カレンダーなので、URLを知れば誰でも全件見える。非公開にしたい予定は別カレンダーに入れる
- 【Aiport】の予定も同じカレンダーに入っているため、会員サイトにも表示される（2026-07-28時点で「そのままでOK」の判断）
- 追加した人のカレンダー一覧には `info.ooenfes@gmail.com` という名前で並ぶ（Gmail主カレンダーは名前変更不可。整えるなら専用カレンダーを新規作成して予定を移す）
