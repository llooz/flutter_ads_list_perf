# flutter_ads_list_perf

This is a sample that uses `google_mobile_ads` to show MREC Ads inside a `ListView`.

It wraps the `AdWidget` in a custom widget with `AutomaticKeepAliveClientMixin` and `wantKeepAlive=true`.  
This way the Ad is kept alive while scrolling the content without rebuilding / reload hiccups.

It also uses
```dart
AdWidget.optOutOfVisibilityDetectorWorkaround = true;
```
because we use Flutter >= 3.7.0

## Why?

To demonstrate rendering performance issues from iPhone 12 onwards (tested on *iPhone 12, 12 Pro, 13 Pro, 14 Pro*).

While scrolling on an iPhone 12 Pro we see strange stuttering (vsync?) with some slow raster phase that causes the frame rate to be unstable around 53/55 fps and sometimes drops to 48 fps.

**The absurdity is that on iPhone 7 and iPhone 7 Plus the framerate is mostly stable with a lowrate of 58/59 fps (same on iPhone 11).**

## What to investigate?

We're using this use case with `google_mobile_ads` because it's a common use case that I also got in a production grade app.

But probably the issue isn't of `google_mobile_ads` but in the handling of `PlatformView`s and `WebView`s inside Flutter.