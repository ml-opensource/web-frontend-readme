# Performance

It is important to strive to develop a high performance website. This cannot be achieved with a single adjustment, but making sure that many factors are considered thoroughly during development.

## State / HTTP Request Management

### Loading State

When an app is in a state where a request is being make or there are some heavy calculations going on be sure to have some form of loading page

### Limit Request Spamming

Be sure to check that when a user triggers or a general an API request is being made i.e. user is submitting a form, that only 1 request gets sent and that the user can't keep clicking the submit button. A solution to this would be to have some form of property like `isLoading`.

### Debouncing API Requests

To make sure that not too many needless API requests are sent, it is generally a good idea to debounce your API requests as it limits the amount of times an event is called - no matter how many times the app or user fires the event. The request will only be fired after a specific amount of time has passed. You have two options: write your own debounce function, or utilize the debounce function in the [Lodash framework](https://lodash.com/), depending on how your project is structured.

Evaluated interface aspects:

- animations
- live updates
- data synchronization (timing)
- data-heavy views/lists/tables
- document rendering

Be careful especially when reviewing data-heavy lists or tables. When supporting low performance machines or mobile devices additional burden of re-rendering interface can make it unresponsive or even unusable.

## 3rd party technologies

Some applications require 3rd party technologies or extensions like Flash or Silverlight, whether they are used for core functionalities or fallback/polyfill for unavailable browser API. Tests should check if components based on those technologies are working properly when technology is installed in browser environment and if lack of such is gracefully handled by either fallback logic or proper message to the user.

## Code Splitting

Coming soon...

## Re-rendering (Memo / PureComponent)

Coming soon...

- Memo / PureComponent
- Why did I re-render?
- useMemo
- caching / local storage
- minify
- tree shaking
