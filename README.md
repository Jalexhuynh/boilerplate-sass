# To Compile Local Sass Projects

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

# Responsive Images in HTML/CSS

## Density Switching
This is used for differences in resolution of the monitors, for example retina vs non-retina. 
Done by declaring 1x and 2x file versions of images in the srcset attribute. For example: 

```
<img srcset="img/logo-green-1x.png 1x, img/logo-green-2x.png 2x" 
        alt="Full logo"
        src="img/logo-green-2x.png">
```

Be sure to include the [src] attribute at the end for older browsers that do not support the [srcset] attribute!

5.  Art Direction
    - Used for swapping different images in case screen sizes call for the use of a different layout of image altogether. In this case, <picture> is used where <source> declares what image to use (even 1x/2x variations) at what screen size using CSS media queries. For example: 

    <picture class="footer__logo">
        <source srcset="img/logo-green-small-1x.png 1x, img/logo-green-small-2x.png 2x" 
                media="(max-width: 37.5em)">
        <img srcset="img/logo-green-1x.png 1x, img/logo-green-2x.png 2x" 
             alt="Full logo"
             src="img/logo-green-2x.png">
    </picture>

    Be sure to include the [src] attribute at the end for older browsers that do not support the [srcset] attribute!

6.  Resolution Switching
    - Used for swapping different images based on the size of the viewport window. For example:

    <img srcset="img/nat-1.jpg 300w, img/nat-1-large.jpg 1000w"
        sizes="(max-width: 900px) 20vw, (max-width: 600px) 30vw, 300px"
        alt="Photo 1"
        class="composition__photo composition__photo--1"
        src="img/nat-1-large.jpg">

    Reads as:
        - Use nat-1 at 300px window, and nat-1-large at 1000px window,
        - Size of the photo is about 20% viewport width at 900px, and 30% viewport width at 300px, then 300% at full screen.
        - Be sure to include the [src] attribute at the end for older browsers that do not support the [srcset] attribute!

=================================
DEVELOPMENT VS BUILD PROCESSES
=================================

* Use npm run [command] to activate commands.

1.  "watch:sass" 
    - Watches for changes in the main.scss file and then outputs a new style.css file.

2.  "devserver" 
    - Runs the live-server npm package.

3.  "start"
    - Runs both watch:sass and devserver in parallel using the npm-run-all package.

4.  "compile:sass" 
    - Uses node-sass to compile an initial style.comp.css file from main.scss.

5.  "concat:css"
    - Outputs style.concat.css by concatenating with all .css files listed after.

6.  "prefix:css"
    - Directs postcss-cli npm package to use the autoprefixer npm package to prefix style.concat.css with any needed for the "last 10 versions of all browsers."

7.  "compress:css" 
    - Uses node-sass to compress style.prefix.css to a style.min.css (or style.css if you prefer).

9.  "build:css"
    - Runs compilation, concatenation, prefixing, and compression all in sequence.

# Sass Boilerplate

This is a sample project using the [7-1 architecture pattern](http://sass-guidelin.es/#architecture) and sticking to [Sass Guidelines](http://sass-guidelin.es) writing conventions.

Each folder of this project has its own `README.md` file to explain the purpose and add extra information. Be sure to browse the repository to see how it works.

## Using the indented syntax

### Sass conversion

This boilerplate does not provide a `.sass` version as it would be painful to maintain both versions without an appropriate build process. However, it is very easy to convert this boilerplate to Sass indented syntax.

Clone it, head into the project and then run:

```
sass-convert -F scss -T sass -i -R ./  && find . -iname “*.scss” -exec bash -c 'mv "$0" “${0%\.scss}.sass"' {} \;
```

### Use with Node-sass

When using `node-sass` - in order to build that boilerplate, one needs to:

- install `node-sass` if not yet installed:

```bash
npm install -g node-sass
```

- run build command from command line:

```bash
node-sass stylesheets/main.scss dist/main.css
```
