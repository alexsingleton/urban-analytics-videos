# Urban Analytics practical videos

The short animated videos that open each practical in
[Urban Analytics and AI](https://alexsingleton.github.io/Urban_Analytics_101/),
served from <https://alexsingleton.github.io/urban-analytics-videos/>.

This repository only hosts them. The videos are made, and their source is kept, in
`alexsingleton/urban_analytics_video` (private).

## How it works

- Every file is an asset on the [`videos` release](../../releases/tag/videos); nothing
  is committed. For each episode there are three assets:
  - `<slug>.mp4`, the video
  - `<slug>.vtt`, its captions
  - `<slug>.jpg`, its poster
- `index.html` is a review page listing all of them.
- [`deploy.yml`](.github/workflows/deploy.yml) downloads the release into `site/` and
  publishes it with GitHub Pages.
- To replace a video, re-upload it under the same name and run the workflow. The URL
  doesn't change, and Pages caches files for 10 minutes.

Run `python video/scripts/publish.py [slug ...]` in the source repository. It stages
the episode's files under these names, uploads them with `--clobber`, and starts the
deploy.

## Embedding

```html
<video controls preload="metadata" crossorigin="anonymous"
       poster="https://alexsingleton.github.io/urban-analytics-videos/<slug>.jpg"
       style="width:100%;border-radius:8px">
  <source src="https://alexsingleton.github.io/urban-analytics-videos/<slug>.mp4" type="video/mp4">
  <track kind="captions" src="https://alexsingleton.github.io/urban-analytics-videos/<slug>.vtt"
         srclang="en" label="English" default>
</video>
```

The practicals site is on the same origin (`alexsingleton.github.io`), so the
captions load there anyway. `crossorigin="anonymous"`, together with Pages'
`Access-Control-Allow-Origin: *`, also lets them load in a local `quarto preview`
or on a custom domain.
