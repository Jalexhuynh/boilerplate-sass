# Sass Boilerplate

This is a sample project using the [7-1 architecture pattern](http://sass-guidelin.es/#architecture) and sticking to [Sass Guidelines](http://sass-guidelin.es) writing conventions.

Each folder of this project has its own `README.md` file to explain the purpose and add extra information. Be sure to browse the repository to see how it works.

## To Compile Local Sass Projects

### Installing node sass.

This installs the node package `node-sass` which compiles sass code. `--save-dev` identifies this package as a developer tool that was used, but is not needed explicitly by the project overall.

``` 
npm install node-sass --save-dev
```

### Compiling Sass

Added `-w` to tell compile:sass to keep watching the `main.scss file for changes, and recompile a new `style.css` file after each save. This user-inputed script will run `node-sass` and take the input file `sass/main.scss` and output it in `css/style.css`.
    
Can be launched via `npm run compile:sass`.

```
"compile:sass": "node-sass sass/main.scss css/style.css -w"
```


### Installing live-server *ONLY ONCE!*

Globally installs `live-server` to your computer. This allows the browser to refresh on file changes within the current directory. Might need to override the password settings on a macbook with: `sudo npm install live-server -g`

```
npm install live-server -g
```

## Scrips in package.JSON for handling dev/production processes.

Use `npm run [command]` to activate commands.

### Development Process
`"watch:sass": "node-sass sass/main.scss css/style.css -w"`
Watches for changes in the main.scss file and then outputs a new style.css file.

`"devserver": "live-server"`
Runs the live-server npm package.

`"start": "npm-run-all --parallel devserver watch:sass"`
Runs both watch:sass and devserver in parallel using the npm-run-all package.

### Production Process
`"compile:sass": "node-sass sass/main.scss css/style.comp.css"`
Uses node-sass to compile an initial style.comp.css file from main.scss.

`"concat:css": "concat -o css/style.concat.css css/icon-font.css css/style.comp.css"`
Outputs style.concat.css by concatenating with all .css files listed after.

`"prefix:css": "postcss --use autoprefixer -b 'last 10 versions' css/style.concat.css -o css/style.prefix.css"`
Directs postcss-cli npm package to use the autoprefixer npm package to prefix style.concat.css with any needed for the "last 10 versions of all browsers."

`"compress:css": "node-sass css/style.prefix.css css/style.css --output-style compressed"`
Uses node-sass to compress style.prefix.css to a style.min.css (or style.css if you prefer).

`"build:css": "npm-run-all compile:sass concat:css prefix:css compress:css"`
Runs compilation, concatenation, prefixing, and compression all in sequence.

## Responsive Images in HTML/CSS

### 1. Density Switching

This is used for differences in resolution of the monitors, for example retina vs non-retina. 
Done by declaring 1x and 2x file versions of images in the srcset attribute. For example: 

```
<img srcset="img/path-1x 1x, img/path-2x 2x" 
        alt="Full logo"
        src="img/path">
```

Be sure to include the `src` attribute at the end for older browsers that do not support the `srcset` attribute.

### 2. Art Direction

Used for swapping different images in case screen sizes call for the use of a different layout of image altogether. In this case, `<picture>` is used where `<source>` declares what image to use (even 1x/2x variations) at what screen size using CSS media queries. For example: 

```
<picture class="footer__logo">     
    <source srcset="img/path-1x 1x, img/path-2x 2x" 
             media="(max-width: 37.5em)">
    <img srcset="img/path-1x 1x, img/path-2x 2x" 
            alt="Full logo"  
            src="img/path.png">
</picture>
```
Be sure to include the `src` attribute at the end for older browsers that do not support the `srcset` attribute!

### 3. Resolution Switching

Used for swapping different images based on the size of the viewport window. For example:

```
<img srcset="img/path-small 300w, img/path-large 1000w"
    sizes="(max-width: 900px) 20vw, (max-width: 600px) 30vw, 300px"
      alt="Photo 1"
    class="composition__photo composition__photo--1"
      src="img/path-large">
```

Reads as:
- Use path-small at 300px window, and path-large at 1000px window,
- Size of the photo is about 20% viewport width at 900px, and 30% viewport width at 300px, then 300% at full screen.
- Be sure to include the `src` attribute at the end for older browsers that do not support the `srcset` attribute!
