# BOOSTER！応援共創ラボ カレンダー設置手順

公開ページ: https://uyaisin.github.io/booster-calendar/
ソース: `~/CC-booster/calendar-page/index.html`（リポジトリ `uyaisin/booster-calendar`）
対象カレンダー: `info.ooenfes@gmail.com`（すでに一般公開設定済み）

---

## 1. 公式LINE「BOOSTER！応援共創ラボ」のリッチメニュー ← 2026-07-28 設定済み

UTAGE アカウント `vGr95bNjxbaq`（BOOSTER！応援共創ラボ）＞ LINE リッチメニュー

| 項目 | 内容 |
|---|---|
| 管理名 | BOOSTER 3ボタン（FB／会員サイト／イベントスケジュール） |
| token | `oA9OPdPFWsZ7` |
| 状態 | **デフォルト**（2026-07-28に2ボタン版から切替） |
| 画像 | `richmenu-booster-2500x843.jpg`（2500×843／428KB／JPG） |
| レイアウト | レイアウト1（2行×3列＝6エリア） |
| 開閉ボタン文言 | `FB・会員サイト・予定`（**14文字以内が上限**。超えると保存でエラー） |

エリア割り当て（列ごとに同じURLを2つ入れて、ボタン全体をタップ可能にしている）:

| エリア | URL |
|---|---|
| 1・4（左＝専用Facebookグループ） | `https://www.facebook.com/groups/900730145498503` |
| 2・5（中＝会員サイト） | `https://info.ooen-booster.com/members/94TOLagXD3lw/login` |
| 3・6（右＝イベントスケジュール） | `https://uyaisin.github.io/booster-calendar/` |

- 旧「BOOSTER 2ボタン（FB／会員サイト）」（token `BUvSeMQTLAzP`）は消さずに残してある。**戻したい時はそちらを「デフォルトにする」に変えるだけ**
- LINE内蔵ブラウザで開かれた場合は、カレンダーページ上部に「ブラウザで開いてください」の案内が自動表示される（それ以外の環境では非表示）

### 画像アップロードの注意（実地でハマった点）

- LINEの仕様は **2500×843 または 2500×1686／1MB以下のJPG or PNG**。元のPNG（2162×727・1.7MB）はそのままでは通らない。`sips -z 843 2500` でリサイズ →`sips -s format jpeg -s formatOptions 80` でJPEG化して428KBに収めた
- Chrome MCP の `file_upload` はセッション共有ファイルしか受け付けず今回は使えなかった。**画像をGitHub Pagesに置いて、ページ内JSで `fetch`→`File`→`DataTransfer`→`input.files` に流し込む方法で成功**（同じ場面ではこの手が使える）

## 2. 会員サイト《 BOOSTER！応援共創ラボ 》 ← 2026-07-28 設置済み

サイト `94TOLagXD3lw` ＞ コース「【はじめに】Boosterの歩き方」（`Hrc9moMmRPfv`）＞ レッスン「イベントスケジュール」（`fqsZUi2R3SZG`・**公開・即時開放**）

- 種類は **コンテンツエディター** を使用。要素「**カスタムHTML**」に下記を入れている
- **リッチテキストではiframeが除去される**（CKEditorが消す）ので、埋め込みたい場合はカスタムHTML一択

```html
<div style="max-width:800px;margin:0 auto;">
  <iframe src="https://uyaisin.github.io/booster-calendar/"
          style="width:100%;height:1500px;border:0;"
          title="イベントスケジュール" loading="lazy"></iframe>
  <p style="text-align:center;font-size:14px;">
    <a href="https://uyaisin.github.io/booster-calendar/" target="_blank" rel="noopener">▶︎ カレンダーが表示されない場合はこちらから開く</a>
  </p>
</div>
```

### 参考: カレンダーだけを直接貼る場合

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
