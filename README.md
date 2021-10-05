# nodejs-chromium-debugger-console
Simple stdin/stdout javascript-console for remotely executing js in chromium-based browsers.

# Installation

    git clone https://github.com/jetibest/nodejs-chromium-debugger-console

# Usage

Run Chromium-based browser with remote debugger option enabled:

    chromium-browser --remote-debugging-port=9222 "https://github.com/jetibest/nodejs-chromium-debugger-console/"

Then, run the console for a given page by the first argument which is the target URL.
Any opened tab or window or iframe has its own target, the target for the console must be specified.
However, iframes of the same host/domain in the same tab/window probably have the same target.
Only the first target that matches the given target URL is chosen.
The given target URL may end with an asterisk wildcard, exclusively to match any URL that starts with the given string.

    > nodejs/chromium-debugger-console/chromium-debugger-console "https://github.com/jetibest/*"
    alert('Remote Debugger says hello to: ' + window.location.href);
    { result: { type: 'undefined' } }

This will show an alert in the browser, with: "Remote Debugger says hello to: https://github.com/jetibest/nodejs-chromium-debugger-console/".
Any javascript expressions are available, such as history.back(), to control the page navigation, etc.

Every newline is sent to the page as a separate expression, which will always return at least one result.

Type `.exit`, `exit`, `quit`, or `q` to exit the console.
