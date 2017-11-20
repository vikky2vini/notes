## Firefox

#### Keyboard shortcuts
    Close tab: CTRL+W
    Close window: CTRL+Q
    Move focus to address bar: CTRL+L

#### Dark background and foreground fix for input boxes
    Create directory: ~/.mozilla/firefox/xxxxxxxx.default/chrome/userContent.css
    Add the following to that file:

    input:not(.urlbar-input):not(.textbox-input):not(.form-control):not([type='checkbox']):not([type='radio']), textarea, select {
        -moz-appearance: none !important;
        background-color: white;
        color: black;
    }

    #downloads-indicator-counter {
        color: white;
    }

    The following extension may fix it:
    https://addons.mozilla.org/en-US/firefox/addon/text-contrast-for-dark-themes/reviews/

#### about:config tweaks

###### Lower session store interval
    Update browser.sessionstore.interval to a larger number

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
