I recently tried sharing a post on Twitter about my website [Denki Carbon](https://denkicarbon.jp) and came up against...something terrifing...

(つ◉益◉)つ <img width="133" alt="image" src="https://user-images.githubusercontent.com/25011388/134919705-19cb5518-009f-4bbf-bcff-a4e2dea17111.png">

😱😱😱😱 𝕬𝖓 𝕰𝖒𝖕𝖙𝖞 𝕴𝖒𝖆𝖌𝖊 𝕭𝖔𝖝 😱😱😱😱  
Very Spooky 💀🎃👻 and it also looks kinda bad right?  

Now, I thought this would be an easy fix, but I just sunk like _3** terrifying and nightmarish hours**_ into this _**dastardly experiment of my own invention**_ so I'm here to _**regale**_ to you my _**tale of woe and tragedy**_ so that _**YOU my child shall not befall such a fate as I**..._ so yeah _**lend me thine ears**_ etc. etc. Spooktober 💀🎃👻

![image](https://media.giphy.com/media/3ornjMatsZL3hRYltm/giphy.gif?cid=ecf05e47jw9i9uqooc8nuo4agbl5pdcj0ay3lo1qf3pbha95&rid=giphy.gif&ct=g)

So the core problem is that _**unbeknownst to the common man**_ that Twitter uses their own `<meta>` tag format for making these Twitter link cards. The basics are [here](https://developer.twitter.com/en/docs/twitter-for-websites/cards/guides/getting-started) but in general, you'll be wanting to stick something like the following inside your `<head>` tag of your `index.html` file.

```html
<!-- Twitter Tags -->
<meta name="twitter:title" content="デンキカーボン - Denki Carbon">
<meta name="twitter:description" content="日本の電力網がどれだけ炭素を使っているかを見ることができます。 See how much carbon the Japanese Electrical Grid is using.">
<meta name="twitter:image" content="/thumbnail.png">
<meta name="twitter:image:alt" content="Graph showing the carbon intensity of Japan">
<meta name="twitter:card" content="summary">
```

Naturally, we'll focus in on the `<meta name="twitter:image"...` tag, which sets the image. The `content` parameter here is saying that our image is named `thumbnail.png` and will be available on the "top level", or in "[Gen Z](https://www.theverge.com/22684730/students-file-folder-directory-structure-education-gen-z)" terms 😉, in the same folder as your `index.html` file. If you wanted to stick the image in a child folder, like one called `assets` then you'd change the content parameter to `content="assets/thumbnail.png"`.

_**BUT THIS MY CHILD IS ALL TOO SIMPLE!**_, the folder/location in your files doesn't really matter. **The core problem** with Twitter's image tag _**of which those dastardly FOOLS have concealed from the prying eyes of those who would challenge them**_ requires the WHOLE URL, in other words:

```html
<meta name="twitter:image" content="https://denkicarbon.jp/thumbnail.png">
```

Now, ok, I **could** just type that in and call it a day..._**BUT ALAS, my hubris!! Twas not to be!**_... because I'm a 𝒻𝒶𝓃𝒸𝓎 𝒹𝑒𝓋𝑒𝓁𝑜𝓅𝑒𝓇 and have multiple environments (Preview, Staging and Production) and a custom domain, all enabled using [Vercel](https://vercel.com/). Vercel makes it really easy, hosting is free for hobby projects and you get 𝒻𝒶𝓃𝒸𝓎 𝒻𝑒𝒶𝓉𝓊𝓇𝑒𝓈 like [Preview Deployments on every PR](https://vercel.com/docs/concepts/deployments/environments) without any setup. Very good, highly reccomended.

