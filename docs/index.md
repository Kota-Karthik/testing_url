# TechDocs Image Link Test (IDP-10939)
[img src="image.png"](https://youtube.com)
This page tests that image-wrapped links render and navigate correctly.
## Exact repro

[![Click here to see the playlist](image.png)](https://youtube.com)


## Test Case 1: Empty src image before content images

<!-- This simulates MkDocs theme elements that may have empty src attributes -->
<img src="" alt="placeholder-theme-icon" />

## Test Case 2: Regular image (should load after the empty-src above)

![Horizontal Rule](image.png)

## Test Case 3: Image wrapped in a link (the reported bug)

Clicking the image below should navigate to the linked URL:

<a href="https://youtube.com" target="_blank">
  <img src="image.png" alt="Click to open target page" />
</a>

## Test Case 4: Image wrapped in a link (Markdown syntax)

[![Alt text for linked image](image.png)](https://example.com/target-page)

## Test Case 5: Multiple images after empty src

These should all load correctly:

![Image A](image.png)

![Image B](image.png)

![Image C](image.png)

## Exact repro

[![Click here to see the playlist](./images/video_thumbnails/playlist_title_slide_with_play_button.png)](https://onyourside.sharepoint.com/sites/TechConsulting/Lists/Single%20Page%20App%20GP%20Videos/AllItems.aspx?referrer=OfficeHome%2EWeb&referrerScenario=StreamStartPage%2DRecommended&isDarkMode=false&viewid=e5a48e4b%2D39c2%2D4801%2D89b6%2D1005cdb92a96&playlistLayout=playback&itemId=2)

## Expected Results

| Test Case | Before Fix | After Fix |
|-----------|------------|-----------|
| 1 | Empty img, no visible effect | Same (expected) |
| 2 | Image does NOT load (no network request) | Image loads from TechDocs storage |
| 3 | Image does NOT load, link unclickable | Image loads, clicking navigates to example.com/target-page |
| 4 | Image does NOT load, link unclickable | Image loads, clicking navigates to example.com/target-page |
| 5 | None of the images load | All images load |

## How to Verify

1. Publish this page to TechDocs.
2. Ensure `image.png` exists in the same `docs/` directory as `index.md`.
3. Open the published TechDocs page in a browser.
4. Open **DevTools → Network**.
5. Verify that requests for `image.png` are made to the TechDocs static asset endpoint.
6. Verify that the images render correctly.
7. Verify that clicking the image in Test Case 3 opens `https://example.com/target-page` in a new tab.
8. Verify that clicking the image in Test Case 4 navigates to the same URL.
