#SamsonPHP CSS resource management module

## Module logic
Module hooks to [SamsonPHP/resource](https://github.com/samsonphp/resource)
CSS resources paths rewriting.

Module automatically rewrites CSS ```url(path/to/resource)``` from *module resource relative path*
 to *project root relative path*. For example we have next module structure:
 + src/MyModule/
 + www/
   + background.jpeg
   + list/
     + bullet.png
     + index.css

And contents of ```src/MyModule/www/list/index.css```:
```css
.list li {
    background-image: url("../background.jpeg"); // Module resource relative path 
}
.list li i {
    background-image: url("bullet.png"); // Module resource relative path
    background-position: 0% 50%;
}
```

After rewriting of this CSS rules we will get following changes:
```css
.list li {
    background-image: url("/resourcer/?p=src/MyModule/www/background.jpeg"); // Project root relative path 
}
.list li i {
    background-image: url("/resourcer/?p=src/MyModule/www/list/bullet.png"); // Project root relative path
    background-position: 0% 50%;
}
```

As you can see also special controller is prepended to resource path: ```/resourcer/?p=``` where ```p``` GET parameter
corresponds to *project root resource relative path*.

## Events
This module supports [SamsonPHP/event](https://github.com/samsonphp/event) eventing model for module
interoperation and this is a list of events that are fired within this module:
 * ```\samsonphp\css\CSS::E_BEFORE_HANDLER``` - Fires before CSS resource was processed
 * ```\samsonphp\css\CSS::E_AFTER_HANDLER``` - Fires after CSS resource was processed
