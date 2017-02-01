## Firefox

#### Keyboard shortcuts
    Close tab: CTRL+W
    Close window: CTRL+Q
    Move focus to address bar: CTRL+L

#### about:config tweaks

###### Disable site notifications
    dom.webnotifications.enabled = false

###### Closing last tab closes window
    browser.tabs.closeWindowWithLastTab true

###### Enable 1080p video support:
    media.mediasource.enabled from = true
    media.mediasource.webm.enabled = true
    media.mediasource.mp4.enabled = true
    media.fragmented-mp4.use-blank-decoder = false
    media.fragmented-mp4.* = true
    media.mediasource.ignore_codecs = true

###### Stop sites from disabling right-click:
    dom.event.clipboardevents.enabled = false
