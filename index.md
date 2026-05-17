---
layout: default
title: 袋小路
---

# 袋小路

<style>
@import url('https://fonts.googleapis.com/css2?family=Potta+One&family=Yomogi&display=swap');

body {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    font-family: sans-serif;
    position: relative; /* 背景をこの幅の内部に配置するための基準 */
    overflow-wrap: break-word; /* 長いURLなどで横スクロールが発生して全体が左に寄るのを防ぐ */
    word-wrap: break-word;
}

/* 画像を完全に背面に置き、本文と重ねる */
.bg-wrapper {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    text-align: center;
    z-index: -1;
    pointer-events: none;
}

#header-image {
    max-width: 100%;
    height: 675px;
    width: 100%;
    object-fit: cover; /* 画像の縦横比を保ちつつ枠に収める */
    -webkit-mask-image: linear-gradient(to bottom, black 40%, transparent 100%);
    mask-image: linear-gradient(to bottom, black 40%, transparent 100%);
}

/* タイトルを少し下げて、画像と重ねた時にバランス良く見せる */
h1 {
    font-size: 4em;
    font-family: 'Potta One', sans-serif; /* タイトルにPotta Oneを適用 */
    margin-top: 40px;
    margin-bottom: 250px; /* 「袋小路」と「流れ」の間を大きく開ける */
    /* 文字が画像に埋もれないように白フチ（影）をつける */
    text-shadow: 0 0 10px white, 0 0 5px white;
}

h2 {
    font-family: 'Yomogi', sans-serif;
}
/* スマホ向けのレイアウト調整 (画面幅が600px以下の場合) */
@media screen and (max-width: 600px) {
    h1 {
        font-size: 2.5em; /* タイトルの文字を少し小さく */
        margin-top: 20px;
        margin-bottom: 120px; /* 画像とのバランスを見て余白を調整 */
    }

    #header-image {
        height: 350px; /* 画像の高さをスマホに合わせて低くする */
    }
    
    body {
        padding: 10px; /* 左右の余白を少し狭くして画面を広く使う */
    }
}
</style>

<div class="bg-wrapper">
    <img src="assets/images/Site_Image.png" alt="" id="header-image">
</div>

## 流れ

* 袋小路（ブログ） <https://blog.bagend.info>
    <p style="font-size: 0.85em; color: gray; margin-bottom: 0;">※ 各記事の要約は AI (Gemini) によって自動生成されています。</p>
    <ul id="blog-entries-list">
        <li>記事を読み込み中...</li>
    </ul>
* BagEnd（tumblr） <https://tumblr.bagend.info>

## 翻訳モノ

* Eloquent JavaScript  <https://www.bagend.info/eloquentJavaScript/>
* HOWTO-Customize-LogWatch <https://www.bagend.info/howto-customize-logwatch/>
* Growl Doc(JP) ~~http://dl.dropbox.com/u/2198478/GrowlForWindows/index.html~~
* Pythonicって何？ <https://www.bagend.info/what-is-pythonic_jp/>
* 個体群動態：翻訳 <http://nmori.blog91.fc2.com/blog-entry-448.html>

## 保管庫

* [サービス停止] twitterおみくじ ~~https://omikuji.bagend.info~~
* [サービス停止] ニコニコ動画ランキングデータ ~~http://nicorank.bagend.info~~
* [サービス停止]コミックダッシュ・新刊カレンダー  ~~https://blog.bagend.info/2011/11/blog-post_19.html~~
* [サービス停止] 郵便番号検索 ~~https://www.bagend.info/zipcode.html~~

<script>
document.addEventListener("DOMContentLoaded", function() {
    const url = "https://script.google.com/macros/s/AKfycbwb0GrerjXCfN3BzZPbBRx4RNdGaiic5lhNX024NYTmswS-Miz1MDEFcLgKq1zQQlB6/exec";
    const list = document.getElementById("blog-entries-list");
    
    fetch(url)
        .then(response => {
            if (!response.ok) throw new Error("Network response was not ok");
            return response.json();
        })
        .then(data => {
            if (data && data.status === "success" && data.items && data.items.length > 0) {
                list.innerHTML = "";
                data.items.forEach(item => {
                    const date = new Date(item.date);
                    const formattedDate = date.getFullYear() + "/" + 
                                        String(date.getMonth() + 1).padStart(2, '0') + "/" + 
                                        String(date.getDate()).padStart(2, '0');
                    const li = document.createElement("li");
                    
                    const a = document.createElement("a");
                    a.href = item.url;
                    a.textContent = item.title;
                    
                    const textNode = document.createTextNode(` (${formattedDate})`);
                    
                    const blockquote = document.createElement("blockquote");
                    blockquote.textContent = item.summary;
                    
                    li.appendChild(a);
                    li.appendChild(textNode);
                    li.appendChild(blockquote);
                    list.appendChild(li);
                });
            } else {
                list.innerHTML = "<li>最新記事が見つかりませんでした。</li>";
            }
        })
        .catch(error => {
            console.error("Error fetching blog entries:", error);
            list.innerHTML = "<li>最新記事の読み込みに失敗しました。時間をおいて再度お試しください。</li>";
        });
});
</script>
