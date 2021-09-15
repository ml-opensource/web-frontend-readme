# Ensuring Quality

We want to deliver high quality, so below we have elaborated on some sections that are good to pay extra attention to.

- [Design Accuracy](#design-accuracy)
- [Responsiveness to Viewport](#responsiveness-to-viewport)
- [Responsiveness to Content](#responsiveness-to-Content)
- [Components Behavior](#components-behavior)
- [External Dependencies](#external-dependencies)
- [External Dependencies](#SEO-/-HTML-semantics)

## Design Accuracy

It's important to ensure that the implemented look of the component is reflected accurately to the design. This is not just about it looking similar to the design but more about does it match the design in every little detail.

Most common properties that should be revised are:

- sizes (width, height, line height)
- colors
- font family
- font size
- font weight
- spacing (margin, padding)
- borders
- background
- list styling (ul, ol)
- number and date formats

Design accuracy should be checked on all supported browsers and platforms. That also involves making sure that the differences that come from platform and browser rendering capabilities are within an acceptable level of tolerance.

## Responsiveness to Viewport

In the case an application supports a responsive layout different viewports on all client devices should be reviewed and checked for design accuracy

## Responsiveness to Content

Every component that contains variable content is checked against multiple combinations of possible content states. Whether it would be most common case, minimal volume or maximum complexity - process assures flexibility of components and its reliability. Since change of component state usually impact the content with different look, additional text or indicators, it should be tested alongside other content variations.

List of tested aspects:

- component states
- normal
- hover
- click
- active
- switch
- success
- error
- tooltip
- text/number length
- text wrapping
- text/number align
- image align
- image floating
- content overflow and overlapping

The easiest way would be to prepare review of same component filled with diverse content or switched to certain states in form of dedicated list view. For that purpose we create and maintain component library dedicated to application - each change to component code can be immediately reviewed across different possible scenarios. If you cannot afford developing dedicated interface library just use inspector to manipulate component in tested case and observe how it responds to modification of content or styles.

Alternatively you could also utilize Storybook which is a open source tool used for working on UI components in isolation it works nicely with most major frontend frameworks like React, Vue and Angular etc.

## Components Behavior

Most of used components are implementations of proved interface patterns, and as such each of them often brings a number of component specific behaviors which should be tested.

Example list of components and their expected behaviors:

- navigation
- easy access
- scales with increasing number of items
- highlight current state
- list
- scales with increasing number of items
- distinguish root levels from sub levels
- table
- distinguish header from content
- properly formats and align different types of data
- fixed header
- does not conflict with rest of layout
- it's on the top level of all components (it's not covered - by any other UI component)
- always visible
- chart
- synchronized with related data set
- scales with increasing number of presented data
- labels are readable
- form fields
- error handling is supported
- label click focus corresponding inputs
- modals
- align and position itself within view
- can be accessed (it's not covered by any other UI component)
- in popup/blocking state it's not passable and requires action

This list is just an example. Fill it with patterns used in your app and extend for every UI element you think should appear here. Remember that this is not only a guide for testers - it's also part of specification for an interface.

## External Dependencies

In some cases, you might not find a package in the recommended list that solves your specific task, so as good rule of thumb, you can evaluate the package on these points:

- Is it still maintained?
  - JavaScript packages are notoriously famous for not being maintained, so they will quickly become outdated and possible contain dependencies that will have security vulnerabilities, so look out for that.
  - If the repo is **not** maintained, then possibly best to look for something else, otherwise consider if you have the time to fork it, update it and maybe even maintain it.
- How many stars/downloads?
  - If the library is popular, it usually means there are maintainers, and a community that can help with issues.
  - **PRO TIP:** You can use [npmtrends.com](https://www.npmtrends.com/) to check package downloads and stars, as well as compare it to a list of other packages.
- Browser support?
  - Some packages will be using experimental or modern JS features, which might not be supported for the browsers that your project needs, so make sure to check that before using it.
- What do you need from the library?
  - If it's a single method in a single file, it might be better to copy-paste the file/single method with attribution back to the repository. This ensures we don't pull in a large library that could introduce security vulnerabilities.

You might be in a situation where you are asking yourself, should we build it or use a package? Maybe you found a packages that solves 80-90% of the task, but the library doesn't support some small things. Start a discussion with the lead dev/head of and if necessary we can include the project manager and designer to see if it is possible to adjust the design slightly to better suit what is supported by the library, as it can save many hours of development.

Beside saving development hours, another reason behind selection a package, is that the project will most likely be easier to maintain as the package will have documentation and contributors keeping it up to date.

However, sometimes it can be better to build a custom solution to solve a specific task you are given, as you will be able to optimize and tweak it to your specific needs. If you are in doubt, then reach out to the local lead dev or head of.

## SEO / HTML Semantics

The benefit of writing semantic HTML stems from what should be the driving goal of any web page: the desire to communicate. By adding semantic tags to your document, you provide additional information about that document, which aids in communication. Specifically, semantic tags make it clear to the browser what the meaning of a page and its content is. That clarity is also communicated with search engines, ensuring that the right pages are delivered for the right queries.

Semantic HTML tags provide information about the contents of those tags that goes beyond just how they look on a page. Text that is enclosed in the `<code>` tag is immediately recognized by the browser as some type of coding language. Instead of trying to render that code, the browser understands that you are using that text as an example of the code for the purposes of an article or online tutorial.

### Meta data

Meta tags provide information about the webpage in the HTML of the document. This information is called "metadata" and while it is not displayed on the page itself, it can be read by search engines and web crawlers.

Search engines such as Google use metadata from meta tags to understand additional information about the webpage. They can use this information for ranking purposes, to display snippets in search results, and sometimes they can ignore meta tags.

### SEO Friendly Content

Generally it's important to have target keywords in web content, previously just having a keyword in a h1 tag was enough to get decent rankings, but now google and other search engines have become a lot smarter.

To make content SEO friendly having a mixture of links to reputable domains and a healthy mix of multimedia elements i.e. YouTube videos and images. All of these factors help make content on a website / app more SEO friendly.

### Html structure

We should be designing the site structure, URLs, and navigation in a logical way to make it easy to understand for humans and search engine robots.

Poor structure makes it harder for search engines to assess your site /app for rankings, and will likely affect the user’s experience as well.
