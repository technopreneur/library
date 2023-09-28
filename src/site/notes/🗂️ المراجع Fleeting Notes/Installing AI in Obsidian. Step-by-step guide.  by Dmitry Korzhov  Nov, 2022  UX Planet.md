---
{"dg-publish":true,"permalink":"/almraje-fleeting-notes/installing-ai-in-obsidian-step-by-step-guide-by-dmitry-korzhov-nov-2022-ux-planet/"}
---

I’ve written before about how comfortable I am with the OpenAI extension for working with text. But the problem was that this extension was only for Logseq.

![](https://miro.medium.com/max/1400/0*y8_Yrx99iSWUTGTK)

Photo by [DeepMind](https://unsplash.com/@deepmind?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

I found a solution and adapted it to Obsidian. Today I want to tell you how to install it quickly and start using it.

## What is GPT-3 extension?

Imagine you have a piece of text like the photo below.

![](https://miro.medium.com/max/1400/1*Z9GkQYU4SBQ3Ju8FqCyHYA.png)

And you want to cut yourself some work and do a squeeze of information from this text. You just click «Make summaries» and get this result.

![](https://miro.medium.com/max/1400/1*Gvml_PyaineQdJpTY8NIDw.png)

This is very useful, especially when it comes to the notes of some articles or books. I use it all the time. And the most important thing is the ease of use. I just set up a hotkey for it and the process happens in seconds.

## How do I set this up?

You need to install this plugin locally in your Obsidian.

Download all the files from my repository: [https://github.com/DmitryKorzhov/GPT-3\_summary](https://github.com/DmitryKorzhov/GPT-3_summary)

Then open the terminal and choose the path to this folder.

![](https://miro.medium.com/max/1400/1*_q1x2VJQjebRwAADkzKSEA.png)

Next you need to enter the 2 commands

-   *npm i*
-   *npm run dev*

![](https://miro.medium.com/max/1400/1*h_73WNRHEjqZQl8ZjhfiCA.png)

After that, you will have *main.js, style.css and manifest.json* in my repository folder. These 3 files must be manually placed in your plugins folder.

Open your Obisidan folder, press «cmd + shift + .» to see all hidden folders. Then go to the .obsidian folder and there the plugins folder. Create a new folder and move those 3 files I wrote above there. Be sure to check that you transferred *main.js*, and not *main.ts*.

Great, just a little bit left and everything will work. Next, open Obsidian and check if the new plugin appeared there.

If you did everything correctly, it showed up and requires an API code in the settings. To do this, go to this site: [https://beta.openai.com](https://beta.openai.com/) and register.

After registration, go to «View API keys», copy it and paste it into Obsidian.

![](https://miro.medium.com/max/1400/1*ZJv1OA9qVIyaT1BkwWlk6A.png)

Restart Obsidian, type a convenient hotkey to work with, and have fun.

![](https://miro.medium.com/max/1400/1*fOJ-yJ1qJzkA17XdHZ-aWA.png)

## Conclusions

You know how much I love to share and use tools that help improve efficiency and productivity. Using AI for word processing is an incredible advantage that we can’t just ignore. That’s why I decided to make this extension. Use it, enjoy it, and of course, like it!