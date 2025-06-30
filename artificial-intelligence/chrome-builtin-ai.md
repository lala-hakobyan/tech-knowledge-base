# Chrome Built-in AI
- **Built-in AI** is one form of client-side AI which brings models to the browser, protecting sensitive data and improving latency. **Client-side AI** inference occurs on-device, which can be incredibly powerful alongside any existing server-side setup.
- Google is developing **web platform APIs** and browser features designed to work with AI models, expert models and large language models (LLMs), built in the browser. This includes **Gemini Nano**, the most efficient version of the Gemini family of LLMs, designed to run locally on most modern desktop and laptop computers. With built-in AI, your website or web application can perform AI-powered tasks, without needing to deploy, manage, or self-host AI models.

## Built-in AI APIs
There are several built-in AI APIs available at different stages of development. 
Some are in Chrome stable, others are available to all developers in origin trials, and some are only available to Early Preview Program (EPP) participants.
You can check availability of different APIS in [Built-in AI APIs Official Documentation](https://developer.chrome.com/docs/ai/built-in-apis).   
Below you can find the list of APIs along with their official documentation with code snippets to try:
- [**Translator API**](https://developer.chrome.com/docs/ai/translator-api)  
  Use the Translator API in Chrome to translate text with AI models provided in the browser.
- [**Language Detector API**](https://developer.chrome.com/docs/ai/language-detection)  
  Use Language Detector API to determine what language is used in the given text before translating text from one language to another.
- [**Summarizer API**](https://developer.chrome.com/docs/ai/summarizer-api)  
  The Summarizer API can be used to generate different types of summaries in varied lengths and formats, such as sentences, paragraphs, bullet point lists, and more. This API may be useful in the following scenarios:
  - Summarizing the key points of an article or a chat conversation. 
  - Suggesting titles and headings for articles. 
  - Creating a concise and informative summary of a lengthy text. 
  - Generating a teaser for a book based on a book review.
- [**Writer API**](https://developer.chrome.com/docs/ai/writer-api)  
  The Writer API helps you create new content that conforms to a specified writing task. The Writer API and the Rewriter API are part of the [Writing Assistance APIs proposal](https://github.com/webmachinelearning/writing-assistance-apis). 
  These partner APIs can help you improve content created by users.
  The Writer API can be used to write new content, based on your initial idea and optional context. This could be used to:
  - Support users write any kind of content, like reviews, blog posts, or emails. 
  - Help users write better support requests. 
  - Draft an introduction for a series of work samples, to better capture certain skills.
- [**Rewriter API**](https://developer.chrome.com/docs/ai/rewriter-api)  
  The Rewriter API helps you revise and restructure text. This API and the Writer API are part of the [Writing Assistance APIs proposal](https://github.com/webmachinelearning/writing-assistance-apis). 
  These APIs can help you improve content created by users.
  The Rewriter API can be used to refine existing text by making it longer or shorter, or changing the tone. For example, you could:
  - Rewrite a short email so that it sounds more polite and formal. 
  - Suggest edits to customer reviews to help other customers understand the feedback or remove toxicity. 
  - Format content to meet the expectations of certain audiences.
- [**Prompt API**](https://developer.chrome.com/docs/ai/prompt-api)  
  With the Prompt API, you can send natural language requests to Gemini Nano in the browser.
  There are many ways you can use the Prompt API. In a web application or website, you can create:
  - AI-powered search: Answer questions based on the content of a web page. 
  - Personalized news feeds: Build a feed that dynamically classifies articles with categories and allow for users to filter for that content.
- **Proofreader API** 
  The Proofreader API is available from Chrome 139 Canary for local experimentation Early Preview Program participants. With this API, you can provide interactive proofreading for your users in your web application or Chrome Extension.
  the Proofreader API can be used for any of the following use cases:
  - Correct a document the user is editing in their browser. 
  - Help your customers send grammatically correct chat messages. 
  - Edit comments on a blog post or forum. 
  - Provide corrections in note-taking applications.

## Hardware Requirements
The Language Detector and Translator APIs work on desktop only in Chrome. 
The Prompt API, Summarizer API, Writer API, and Rewriter API work in Chrome when the following conditions are met:
- Operating system: Windows 10 or 11; macOS 13+ (Ventura and onwards); or Linux. Chrome for Android, iOS, and ChromeOS are not yet supported by our APIs backed by Gemini Nano.
- Storage: At least 22 GB on the volume that contains your Chrome profile.
- GPU: Strictly more than 4 GB of VRAM.
- Network: Unlimited data or an unmetered connection.

## Getting started
Best way to get started is to [install Chrome Canary](https://www.google.com/chrome/canary/) and join [the early preview program](https://developer.chrome.com/docs/ai/join-epp) in order to leverage Chrome built-in APIs full capabilities.
Below are steps to enable and test Chrome Built-in APIs:
- [Download Chrome Canary](https://www.google.com/chrome/canary/) and install it.
- Open **`chrome://flags`** to enable necessary flags:
  - `#optimization-guide-on-device-model` (Set to `"Enabled BypassPerfRequirement"` or `"Enabled"`)
  - `#prompt-api-for-gemini-nano` (Set to `"Enabled"`)
  - Look also for other related flags and enable them, like `#summarization-api-for-gemini-nano`, `#rewriter-api-for-gemini-nano`, `#writer-api-for-gemini-nano`, etc.
- Restart Canary: After changing flags, relaunch Chrome Canary. 
- Check Components: Go to `chrome://components` and look for `Optimization Guide On Device Model.`. If it doesn't appear, wait for some time - sometimes it takes a bit more time for the component to appear and for the browser to download it. You may also relaunch your browser or restart your PC and check again. Ensure it has a version number (e.g., 2024.x.x.x).
  If it doesn't, click "Check for update" to try and force the model download. This can take some time and requires a stable internet connection.
- Check `chrome://components` to make sure the model is downloaded. Check the status of the model and check for updates.
- Open browser console and test if AI APIs are enabled. In the Chrome Canary console:
  - Run `await LanguageModel.availability()` to verify the runtime is `'available'`.
  - Run `window.ai` to make sure that prompt API model is fully downloaded and capable. If it is `undefined`, it means Gemini Nano was not fully installed and capable to work on your machine.
  While in this case you can use simple text base prompt API and other AI APIs functionalities, you may not be able to use image and audio related heavy features.
  In this case, check [Hardware Requirements](#hardware-requirements) listed above to make sure they are fully met in your device.


## Documentation & References
- [Official Google Documentation for Built-in APIs](https://developer.chrome.com/docs/ai/built-in-apis)
- [The Early Preview Program for Google Built-in AI APIs](https://developer.chrome.com/docs/ai/join-epp)
  - [Public Discussion Mailing List](https://groups.google.com/a/chromium.org/g/chrome-ai-dev-preview-discuss?pli=1)
  - [Google Developer Community on Discord](https://discord.com/invite/zzj2ywFx8B)
- [Official Collection of Client-side AI Demos](https://github.com/GoogleChromeLabs/web-ai-demos)
- [Built-in AI Apis Demo by Thomas Steiner](https://local-first-conf-rocks.glitch.me/)
- **AI Right in the Browser with Chrome’s Built-in AI APIs** - Presentation by [Thomas Steiner](https://www.linkedin.com/in/thomassteinerlinkedin/) at JSNation, June 2025. 
  - [Google docs presentation](https://docs.google.com/presentation/d/1E1d8yOi0tsRQ8n5rVXOfBNl6X74GvzgldJXyycoHpHE/edit?slide=id.g35d8303de8b_1_4#slide=id.g35d8303de8b_1_4)
  - [Project demo](https://tomayac.github.io/prompt-api-sqlite/)
- **Practical Web AI: Built-In, Browser Based, Brilliant** - Presentation by [Phil Nash](https://www.linkedin.com/in/philnash/) at JSNation, June 2025. 

