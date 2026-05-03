---
layout: default
title: 袋小路
---

# 袋小路

## 流れ

* 袋小路（ブログ） <https://blog.bagend.info>
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
