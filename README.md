# About

Tailpages (Tailwind + Github Pages) is a Jekyll website template based on TailwindCSS, which can be hosted by Github for free. You can visit the demo site at [https://harrywang.me/](https://harrywang.me/).

Key features are:

- Minimalist design inspired by the [indigo template](https://github.com/sergiokopplin/indigo)
- Elegant typography via [TailwindCSS Typography plugin](https://tailwindcss.com/docs/typography-plugin) and [Inter font](https://rsms.me/inter/)
- Markdown support for content authoring (static pages and blogs)
- Code highlighting and styling via [highlight.js](https://highlightjs.org/) (see [code example](http://harrywang.me/tailpages/2022/02/07/code.html))
- Latex support via [MathJax](https://www.mathjax.org/) (see an [example](http://harrywang.me/tailpages/2022/02/09/latex.html))
- Table of Contents support via [jekyll-toc](https://github.com/allejo/jekyll-toc) (see an [example](http://harrywang.me/tailpages/toc))

### Tutorials
- No-code Tutorial: this tutorial shows how you can use Tailpages template to quickly setup your website and blogs without coding, which you can access at [medium](https://harrywang.medium.com/introducing-tailpages-tailwind-github-pages-89903c52d3ec) or [blog](https://harrywang.me/tailpages-tutorial-nocode).
- Technical Tutorial: this tutorial shows how to setup the development environment for Tailpages from scratch, which you can access at [medium](https://harrywang.medium.com/developing-tailpages-a-jekyll-template-based-on-tailwind-css-b8b51e60e25b) or [blog](https://harrywang.me/tailpages-tutorial-technical). 


Posts name format: yyyy-mm-dd-title.md

docker run -v $(pwd):/srv/jekyll -p 4000:4000 -it jekyll/jekyll jekyll build --watch



To enable typography plugin, inter font, and customizations by updating `tailwid.config.js` as follows:

```js
const defaultTheme = require('tailwindcss/defaultTheme')

module.exports = {
  content: [
    './**/*.html'
  ],
  darkMode: 'media',
  theme: {
    extend: {
      typography: {
        DEFAULT: {
          css: {
            pre: {
              padding: "0",
              color: "#1F2933",
              backgroundColor: "#F3F3F3"
            },
            code: {
              padding: "0.2em 0.4em",
              backgroundColor: "#F3F3F3",
              color: "#DD1144",
              fontWeight: "400",
              "border-radius": "0.25rem"
            },
            "code::before": false,
            "code::after": false,
            "blockquote p:first-of-type::before": false,
            "blockquote p:last-of-type::after": false,
          },
        },
      },
      fontFamily: {
        sans: ['Inter var', ...defaultTheme.fontFamily.sans],
      },
    },
  },

  variants: {
    extend: {},
  },
  plugins: [
    require('@tailwindcss/typography'),
  ],

}
```
