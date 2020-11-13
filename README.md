# React Template  

## Summary  

Setting up a boilerplate React App template from scratch using Webpack.  
This application supports the following by default:  
-   React
-   Redux
-   TypeScript
-   Sass

## Under the Hood  

### Babel  

Babel presets that allow browser compatibility to newer JavaScript, the React JSX and TypeScript.  
```javascript
//.babelrc
{
    "presets": [
        "@babel/preset-env",
        "@babel/preset-react",
        "@babel/preset-typescript"
    ]
}
```

### Loaders  

The babel loader will transpile the specified file types based on the preset configs set above.
```javascript
//babel-loader
{
    test: /\.(js|jsx|ts|tsx)$/,
    exclude: /nodule_modules/,
    use: 'babel-loader'
}
```

With the HtmlWebPackagePlugin, it will create a template index.html file in the output directory.
```javascript
//html-loader
{
    test: /\.html$/,
    use: 'html-loader'
}
```

The file loader will create our assets into the output directory.
```javascript
// file-loader
{
    test: /\.(png|jpe?g|gif)$/i,
    use: {
        loader: 'file-loader',
        options: {
            name: '[name].[hash].ext',
            outputPath: 'assets'
        }
    }
}
```
The sass loader and css-loader compiles the files into JavaScript while the plugin takes that and creates a css file in the output directory.
```javascript
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

//MiniCssExtractPlugin.loader, css-loader, sass-loader
{
    test: /\.s[ac]ss$/i,
    use: [
        MiniCssExtractPlugin.loader,
        'css-loader',
        'sass-loader'
    ]
}
```

### Plugins  

Configure and create the html and css files in the build process.
The build directory will delete everytime the script is ran.

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const webpack = require('webpack');
const CleanWebpackPlugin = require('clean-webpack-plugin');

plugins: [
        new HtmlWebpackPlugin({
            filename: 'index.html',
            template: './public/index.html',
            favicon: './public/assets/favicon.png'
        }),
        new MiniCssExtractPlugin({
            filename: 'main-[fullhash].css'
        }            
        ),
        new webpack.DefinePlugin({
            "process.env":{
                "NODE_ENV": JSON.stringify(process.env.NODE_ENV)
            }
        }),
        new CleanWebpackPlugin.CleanWebpackPlugin()
    ]
```

### Scripts  
    `npm start` - Starts a live development server port 3000
    `npm run dev` - Creates a development build
    `npm run build` - Creates a production build

### License  
The MIT License (MIT)

Copyright 2020 Chris Kim

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, ITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
