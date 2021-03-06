# React Project Bolierplate

## Features

- Image Loading
- Redux
  - `redux-thunk`
- React Router
- Sass supported
- Code Splitting
  - Create a Component, `import` it in `/pages/index.js` using `withSplitting()`
- Environment Variables
- Webpack Dev Server
- Storybook for React
- Github Page Deployment
- Other optimizations for build

## Index

### `public`
- `index.html` for initial entry point to users
- `/assets` for all static resources used in this web page

### `src`
- `/components` for presentational unit components
  - `/base` for large components
  - `/common` for minimal component unit
    - `Component.js`
    - `Component.css`
    - `Component.stories.js`
    - `Component.test.js`
    - `index.js`
- `/containers` for container components
- `/pages` for page per each routings
  - `/common` for functional pages
  - All routings indexed in `App.js`
  - Code Splitting enabled
- `/utils` for utility functions
- `/redux` for redux store and reducers settings in Ducks pattern
- `/config` for environment variables setting and Webpack config files
  - put your `.env` file in `/config/env` directory

## Prerequisite

1. Run `npm install` to provide required npm modules
2. Go to `/config/env` and make `.env` file for your project

### `.env`

You can inject your custom environment variables in your project.

The `.env` file should be located in `/config/env` directory.

The project will inject `{ __NOT_USED__: undefined }` environment variable object as a default. You don't necessarily have to use `.env` file.

## How to build

1. Run `npm run build`
2. Use a build output from `/build` directory

## How to run `webpack-dev-server`

1. Run `npm run dev`
2. Visit `http://localhost:3000` (Automatically opens)

## How to run **Storybook**

1. Run `npm run storybook`
2. Visit Storybook UI (Automatically opens)

## How to deploy via Github Page

1. Add following values in `.env` file (`/config/env/.env`):

```
# .env
REPO_NAME=<GITHUB_REPOSITORY_NAME>
REPO_URL=https://<GITHUB_ID>.github.io/<GITHUB_REPOSITORY_NAME>
```

2. Run `npm run gh-pages`
3. Include the output `/docs` in the `master` branch of your project
4. `git push origin master`
5. Go to your repository page, navigate into [Settings → GitHub Pages → Source], and choose **`master branch /docs folder`**.

## Update Report

### v1.4.4 (2020-01-10)
- `webpack.config.js`
  - used `path` module consistently to support non-POSIX path

### v1.4.3 (2020-01-02)
- added support for multi-routing for Github Page Deployment
- added html templates for Github Page Deployment
- fixed typo and added modification in README.md

### v1.4.2 (2020-01-02)
- added Webpack config files
  - `webpack.config.dev.js` for development only
  - added HMR and Sourcemap options
- modified npm scripts along with new Webpack config files

### v1.4.1 (2020-01-02)
- added Github Page deployment script and settings
  - Currently for only a single routing page

### v1.4 (2020-01-01)
- added custom Environment Variables settings
  - added warning message if `.env` is not provided or empty when webpack builds
- separated Webpack config files in `/config` directory
- updated module (html-webpack-plugin)

### v1.3 (2019-12-27)
- added Sass support
  - added `webpack.config.js` for Storybook config 
- changed `.css` to `.scss`

### v1.2.3 (2019-12-11)
- added build option for production build

### v1.2.2 (2019-11-22)
- added `url-loader` and support for image loading from server's directory

### v1.2.1 (2019-11-21)
- added tips for using react-router's `withRouter()` HoC.

### v1.2 (2019-11-15)
- added `/templates` directory: general purpose template components
  - example: `<Article />` component
- bugfix when using `react-router` with `wds`
- added example for `react-router`
- added **Tips** section:
  - relevant tips

### v1.1 (2019-11-14)
- added comments with core logic explanations
- added `redux-thunk`, loaders for style
- added **Storybook** features

### v1.0.1 (2019-11-11)
- added `redux` basic sample codes
- changed directory structures

### v1.0.0 (2019-11-9)
Initial boilerplate checkout

## Appendix

### If you want to use images in pages

You can simply load static images which are uploaded in web server's directory by using specific URI indicating the resources.

```js
<img src="assets/images/BlueMountains.jpg" />
```

Files have to be located in `public/assets` directory, and the URI should include prefix of `assets/`. Subdirectories are able to customized. See `webpack.config.js` for more detailed configurations.

### Tips for using React Router

#### Webpack Dev Server

As Webpack Dev Server(WDS) does not serve `index.html` for routes except `/` as default config, we should set relevant configuration.

```js
// webpack.config.js
module.exports = {
  output: {
    publicPath: '/'
  },

  // ...
  devServer: {
    histroyApiFallback: true
  }
}
```

You should set `publicPath` property to `/`, so that the WDS can understand real root (/) even when you are on subroutes. [See this article](https://stackoverflow.com/a/50179280/9341051).

#### Storybook

If your component use `withRouter()` HoC and use relevant props within itself(i.e. `history.push()`), that component has to be wrapped with `<Router />`. You can use `<MemoryRouter />` to mock the routing environment.

```js
// Component.stories.js
import { MemoryRouter } from 'react-router'

storiesOf('MainButton', module)
  .addDecorator(story => <MemoryRouter initialEntries={['/']}>{story()}</MemoryRouter>)
  .add('default', () => (
      <ComponentWithRouter />
    )
  )
```

### Deployment on Github Pages

If you have a repository on Github and want to deploy your static web page via Github Page, the site will have a URL like below:

```
https://<USERNAME>.github.io/<REPO_NAME>
```

When your `index.html` (쓰다 말았다!) (https://github.com/rafrex/spa-github-pages)
