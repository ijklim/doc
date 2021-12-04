# Webpack Guide

```sh
# Required packages
yarn add -D webpack webpack-cli
```

## Requirements for Javascripts

webpack.config.js
```
const path = require('path');

module.exports = {
  mode: 'development',
  entry: './src/index.js',
  output: {
    // Create file bundle.js in folder dist
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },
}
```

* To use the generated file: `<script src="bundle.js"></script>`

## Requirements for CSS

webpack.config.js
```
module.exports = {
  module: {
    rules: [
      {
        // Files ending .css will be served to style-loader, then css-loader
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
}
```

* Style file should be located: `src/style.css`

* To use in js file: `import './style.css';`

## Requirements for images

* Using webpack 5 built-in `Asset Modules`

webpack.config.js
```
module.exports = {
  module: {
    rules: [
      {
        test: /\.(png|svg|jpg|gif)$/i,
        type: 'asset/resource',         // Without this line, error: 'You may need an appropriate loader to handle this file type'
      },
    ],
  },
}