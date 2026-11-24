# BandScoreSplit  

> [!IMPORTANT]
> **本工具已停止維護，請改用 [audiveris-bandscore](https://github.com/hibikiwtnb/audiveris-bandscore) 的 `skill/tools/extract_parts.py`。**
>
> 新工具用 Audiveris 讀出的版面直接從原始掃描裁出各聲部分譜，不辨識音符，因此 OMR 的音符錯誤不會進入分譜。它會自動找出每個樂器在每行譜表的位置，一次替每個樂器輸出一份 A4 PDF，不必再手動逐段拉裁剪框、逐頁拼接圖檔；聲部名稱取自樂譜結構而不是 OCR；可選加上和弦符號或主唱歌詞。用法見 [skill/README.md 的「圖片式分譜」](https://github.com/hibikiwtnb/audiveris-bandscore/blob/bandscore/skill/README.md#圖片式分譜)。執行前需先依 [skill/SKILL.md](https://github.com/hibikiwtnb/audiveris-bandscore/blob/bandscore/skill/SKILL.md) 用 Audiveris 跑過該曲。
>
> **本ツールはメンテナンスを終了しました。[audiveris-bandscore](https://github.com/hibikiwtnb/audiveris-bandscore) の `skill/tools/extract_parts.py` をご利用ください。** Audiveris が読み取ったレイアウトを使って元のスキャン画像から各パートを自動で切り出し、楽器ごとに A4 PDF を出力します。音符は認識しないため OMR の誤認識がパート譜に入らず、トリミング枠の手動調整やページの貼り合わせも不要です。コード記号やボーカル譜の追加も選べます。使い方は [skill/README.md](https://github.com/hibikiwtnb/audiveris-bandscore/blob/bandscore/skill/README.md#圖片式分譜) を参照してください（事前に [skill/SKILL.md](https://github.com/hibikiwtnb/audiveris-bandscore/blob/bandscore/skill/SKILL.md) に従って Audiveris で処理しておく必要があります）。
>
> **This tool is no longer maintained.** Use `skill/tools/extract_parts.py` in [audiveris-bandscore](https://github.com/hibikiwtnb/audiveris-bandscore) instead: it reads the Audiveris layout and automatically cuts one A4 PDF per instrument from the original scan, without recognizing notes, so OMR note errors cannot reach the parts. It needs no manual trim boxes or page assembly, takes part names from the score structure rather than OCR, and can optionally add chord symbols or the vocal staff. See the [image parts section of skill/README.md](https://github.com/hibikiwtnb/audiveris-bandscore/blob/bandscore/skill/README.md#圖片式分譜) for usage; the score must first be processed through Audiveris as described in [skill/SKILL.md](https://github.com/hibikiwtnb/audiveris-bandscore/blob/bandscore/skill/SKILL.md).

BandScoreSplit is a tool for dividing band scores(Or orchestra score, etc.) into parts scores. that is built with HTML5 Canvas. only use for image(JPG,PNG) or PDF files. Files will not be sent to the server, all processing is completed locally. (OCR function needs to go through HTTP server, or use the Online demo)  

BandScoreSplitは画像形式のバンドスコア(またはオーケストラスコアなど)をパート譜に抽出するためのツールです。HTML5のCanvasを使用して構築したものです。処理できるのは画像（JPG,PNG）とPDF。処理するファイルはサーバーに転送されることはありません、全部処理はローカルで完結します。(OCR機能を使用するにはHTTPサーバ経由か、下方のOnline demoのリンクから使用してください)  

BandScoreSplit是使用HTML5 Canvas構建的用於將樂譜（樂團樂譜等）劃分為單獨樂器的樂譜的工具，僅用於圖像（JPG，PNG）或PDF文件，文件不會發送到服務器，所有處理在本地完成。(OCR功能需要構建網頁伺服器，或使用下方的線上鏡像)  

## Tutorial:  
https://www.youtube.com/watch?v=J3RbeaMzhDM

## Online demo:  
+ English https://kitami.github.io/BandScoreSplit/main_en.html  
+ 日本語版 https://kitami.github.io/BandScoreSplit/main.html  
+ 中文版 https://kitami.github.io/BandScoreSplit/main_cn.html  

## What can it do  
1.Automatically identify staff border  
2.Automatically corrects the tilt of scanned images  
3.After trimming once, perform the same trimming process (at the relative position to the staff border,or Part name position) on other images  
4.Automatically output image when page is full  
5.OCR the instrument name on left   

できること:  
1.自動的に譜表の外枠を特定  
2.スキャンした画像の傾きを自動補正  
3.一度トリミングした後、他の画像に対して同じ位置(外枠に対する相対位置、または楽器名の位置)のトリミング処理を行う  
4.ページがいっぱいになったら自動的に画像を出力する  
5.ガイド線左側の楽器名に対してOCR（文字認識）を行う  

主要功能:  
1.自動識別譜表邊界  
2.自動校正掃描圖像的傾斜  
3.修剪一次後，在其他圖像上執行相同的修剪過程（根據到上側邊界的相對位置，或使用樂器名的位置）  
4.頁面填滿時自動輸出圖像  
5.處理左側有樂器名稱的樂譜時，可以使用OCR(光學文字識別)功能定位譜表位置  

## Using module or sources  
利用しているモジュール/使用的模組
+ [wellflat/Line Segment Detector(LSD) module (MIT License)](https://github.com/wellflat/imageprocessing-labs/tree/master/cv/lsd)
+ [naptha/tesseract.js](https://github.com/naptha/tesseract.js)
+ [mozilla/pdf.js](https://github.com/mozilla/pdf.js)

## Using Guide  
1.Load an image or PDF file by selecting a file button.  
2.adding a trim box, and adjust the position and height, or use the Part Name OCR.  
3.The results will be displayed in the output-area.  

batch processing  
click "Batch start" button. 

使い方:  
1.ファイル選択で画像ファイルを読み込ませる  
2.トリミング枠を追加して、位置と縦幅を調整する、または楽器名OCRを使う  
3.結果は右側のエリアに表示される  
  
自動化処理  
「処理開始」ボタンをクリックする  

使用方法:  
1.選擇一個或多個圖像文件  
2.按下「追加」按鈕用來追加剪切框，調節左上角的參數以及按住拖動剪切框到想要剪切的譜表的位置，或使用樂器名OCR  
3.剪切結果會在右側輸出圖像區域表示  
  
自動化處理  
點擊「處理開始」按鈕  

## Questions  
質問  
File an issue:
+ https://github.com/Kitami/BandScoreSplit/issues/new

Follow twitter: @KitamiHibiki
+ https://twitter.com/KitamiHibiki
