# Svelte Filesystem Proof of concept

This is Quick POC of [an idea i had](https://twitter.com/swyx/status/1396005314227539968): what if you could edit Svelte components in place in the browser — using the File System Access API!

What if we didn't have to mentally map our source code rendered content? Just click on component, source pops up, we edit, save. **No IDE needed!**

> note: this idea works only in development - which makes sense if you think about it


https://user-images.githubusercontent.com/6764957/120790682-d9b7c400-c565-11eb-9580-740279005543.mp4


[see tweet responses](https://twitter.com/swyx/status/1400764771520040963)

## usage

```bash
npm install
npm run dev -- --open # localhost 
```

- Click `load` button to open `src/components/Comp.svelte` - you will have to navigate there yourself until [this PR lands](https://github.com/WICG/file-system-access/pull/287)
- try making edits the source
- then hit the `save` button
- see it hot reload thanks to Vite/SvelteKit. 

You now have a self-editing component!

## possible extensions

- mouseover components and cmd+click to open up their source (may have to choose from a list - use event bubbling to identify the list of components?)
- embed Monaco instance for better editing (like this https://github.com/sw-yx/svelte-zen-garden) - currently i only use `<pre contenteditable>` which is janky af

## notes on filesystem access api

its still too clunky - you HAVE to use `showOpenFilePicker` right now to load a file. 

Ideally we can just give a known filepath and construct the `FileSystemFileHandle` ourselves, but this is currently impossible. i've [opened an issue here](https://github.com/WICG/file-system-access/issues/301).

if it were, we could then instrument svelte's rollup/webpack loader to expose filepath info to every component so that we can figure out which component to open (or offer a menu of them) instead of having the user navigate to there.

- basic reading: https://web.dev/file-system-access/
- spec: https://wicg.github.io/file-system-access/#api-filpickeroptions-types
- key PR: https://github.com/WICG/file-system-access/pull/287
- potential polyfills
    - https://browser-fs-access.glitch.me/
    - https://github.com/jimmywarting/native-file-system-adapter/
