# puppeteer-speech-to-text

```js(listen.js)
const puppeteer = require('puppeteer');

const htmlContent =
  '<!doctype html><html lang="uk"><head><meta charset="UTF-8" /><title>Web Speech API</title></head><body></body></html>';

const soundBeep =
  'data:audio/mpeg;base64,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';

export default {
  listenSync: async () => {
    return new Promise(async (resolve, reject) => {
      const browser = await puppeteer.launch({
        headless: 'new',
        ignoreDefaultArgs: ['--mute-audio'],
        args: [
          '--no-sandbox',
          '--enable-speech-dispatcher',
          '--enable-audio-service-sandbox',
          '--use-fake-ui-for-media-stream',
          '--autoplay-policy=no-user-gesture-required'
        ]
      });

      try {
        const page = await browser.newPage();

        await page.goto(`data:text/html,${htmlContent}`);

        const { transcript } = await page.evaluate(
          async ({ beep }) => {
            return new Promise((resolve, reject) => {
              const audio = new Audio(beep);
              audio.play();

              const recognition = new webkitSpeechRecognition();
              recognition.lang = 'uk-UA';
              recognition.continuous = false;

              recognition.onresult = event => {
                const [result] = event.results[event.results.length - 1];
                const { transcript } = result;
                resolve({ transcript });
              };

              recognition.onerror = event => {
                const { error } = event;
                resolve({ transcript: error });
              };

              recognition.onend = () => {
                resolve({ transcript: '' });
              };

              recognition.start();
            });
          },
          { beep: soundBeep }
        );

        await browser.close();

        resolve(transcript);
      } catch (err) {
        resolve({ transcript: 'Щось я тебе не зрозумів' });
      }
    });
  }
};
```

```js
import listen from './listen';

const output = await listen.listenSync();

console.log('result: ',output);
```
