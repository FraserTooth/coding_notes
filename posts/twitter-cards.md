I recently tried sharing a post on Twitter about my website [Denki Carbon](https://denkicarbon.jp) and came up against...something terrifing...

(つ◉益◉)つ <img width="133" alt="image" src="https://user-images.githubusercontent.com/25011388/134919705-19cb5518-009f-4bbf-bcff-a4e2dea17111.png">

😱😱😱😱 𝕬𝖓 𝕰𝖒𝖕𝖙𝖞 𝕴𝖒𝖆𝖌𝖊 𝕭𝖔𝖝 😱😱😱😱  
Very Spooky 💀🎃👻 and it also looks kinda bad right?  

Now, I thought this would be an easy fix, but I just sunk like _**Threescore terrifying and nightmarish hours**_ into this _**dastardly experiment of my own invention**_ so I'm here to _**regale**_ to you my _**tale of woe and tragedy**_ so that _**YOU my child shall not befall such a fate as I**..._ so yeah _**lend me thine ears**_ etc. etc. Spooktober 💀🎃👻

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

Now, ok, I **could** just type that in and call it a day..._**BUT ALAS, my hubris!! Twas not to be!**_... because I'm a 𝒻𝒶𝓃𝒸𝓎 𝒹𝑒𝓋𝑒𝓁𝑜𝓅𝑒𝓇 and have multiple environments (Preview, Staging and Production) and a custom domain, all enabled using [Vercel](https://vercel.com/). Vercel makes it really easy, hosting is free for hobby projects and you get 𝒻𝒶𝓃𝒸𝓎 𝒻𝑒𝒶𝓉𝓊𝓇𝑒𝓈 like [Preview Deployments on every PR](https://vercel.com/docs/concepts/deployments/environments) without any setup. Very good, highly reccomended. But there was _**SIN! SIN in the garden of Eden!!!**_

![image](https://media.giphy.com/media/fnJQKWKn29NUGanUiA/giphy.gif?cid=ecf05e4767df5j77jig48e93rpv1pgko26q7smlvxwp8plsl&rid=giphy.gif&ct=g)

Ya see...Vercel generates a unique URL **for every deployment**. So even though you could just whack in your production domain, you wouldn't be able to test that this works in your Preview and Staging environments properly.

Online, the general suggestion is to add `"homepage": "https://www.yoururl.com",` to your `package.json` file and add `%PUBLIC_URL%` to the domain, like so:

```html
<meta name="twitter:image" content="%PUBLIC_URL%/thumbnail.png">
```

This allows `webpack` (assuming you're using it on your project, which you probably are) to jam in the URL during the build process. However this really doesn't work well with Vercel without a few additional steps. So here is the _**TERRIFYING AND UNNATURAL FRAKENSTEIN**_ of a hack I came up with...

1. Vercel exposes the current URL of the deployment in a Environment Variable called `VERCEL_URL`. This can be added into your build environment process by going to `https://vercel.com/<your-username>/<your-project>/settings/environment-variables` and clicking on "Automatically expose [System Environment Variables](https://vercel.com/docs/concepts/projects/environment-variables#system-environment-variables) →"

<img width="888" alt="image" src="https://user-images.githubusercontent.com/25011388/134925897-06789a13-2401-4c40-be2d-a4a99d5519d4.png">

2. Then, having done this, add the `%PUBLIC_URL%` to your twitter tag, like above.

3. Finally, add the following to your `build` script in `package.json` -> `PUBLIC_URL=https://$VERCEL_URL` so it might end up looking like this:

```json
"scripts": {
  ...
  "build": "PUBLIC_URL=https://$VERCEL_URL react-scripts build",
},
```

Utterly RANCID hack right? 😆 

![image](https://media.giphy.com/media/J2gHlRQQvFamqOWlJF/giphy-downsized-large.gif?cid=ecf05e47sy3lvpaqys9cl2w510czt0lkzov7cta941a7txko&rid=giphy-downsized-large.gif&ct=g)

This sets the `PUBLIC_URL` environment variable with the total generated vercel URL for ANY deployment, so something like `https://denki-carbon-qzjnakv9r-frasertooth.vercel.app/`. The `https://` at the start is needed because Vercel trims this off the start of their `VERCEL_URL`, which is odd but whatever 🤷. Finally, this all gets jammed by `webpack` into wherever you've used `%PUBLIC_URL%` in your code, so the final result in your built html will be:

```html
<meta name="twitter:image" content="https://denki-carbon-qzjnakv9r-frasertooth.vercel.app/thumbnail.png">
```

_**AND THUS our tale is at an end**_, Twitter reads the URL, scrapes the page and sees that nice full URL. Giving you a nice formatted card like this:
> ![image](https://user-images.githubusercontent.com/25011388/134927322-b3f90371-1475-453e-a599-3f72b70dc1b8.png)
> [Post](https://twitter.com/FraserTooth/status/1442322181275353091) - Follow me on Twitter [@FraserTooth](https://twitter.com/FraserTooth), nerdy takes ｇｕａｒａｎｔｅｅｄ

Naturally, there are nicer ways to do this, if your build system uses Node, you might do something like this:
```jsx
const vercelContentUrl = process.env.VERCEL_URL ? `https://${process.env.VERCEL_URL}` : '';

const twitterTag = (<meta name="twitter:image" content={`${vercelContentUrl}/thumbnail.png`} />)
```

The core point is: Twitter needs a full URL, but Vercel has a dynamic and random URL, use the `VERCEL_URL` environment variable as part of your build system to get it, even in Preview.

Hope that was useful ✌️ have a great week!

(Small note, Twitter caches pictures used for these cards for around a week, you can force them to rescrape the page using this tool they provide: https://cards-dev.twitter.com/validator)
