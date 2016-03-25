# Javascript Manifests

## Objectives

1. Create Javascript Manifest Files
2. Require Javascript Files in Manifests with Sprocket Directives
3. Include Javascript Manifest Files in Layouts
4. See a Manifest in Development vs Production

## Outline
Our previous lesson gave us a good overview of the Asset Pipeline. We touch briefly on manifest files and how they provide a central place to list the assets we want to load. Let's dive deeper into the JavaScript manifest file.

### Manifest Files
Manifest files have special characteristics about them that differentiate them from plain old JS files. If you open your JavaScript manifest, `app/assets/javascripts/application.js`, you will see that some of the lines start with `//=`. This is called a directive and it tells sprockets that this isn't a normal JS comment. 

### `require` directives

While there are a number of [different directives](https://github.com/rails/sprockets#sprockets-directives) available, let's learn about the one that is used to list the JS files we want to include in our application.  This directive, `require`, tells sprockets that the file we are specifying should be loaded. One thing to note is you don't have to put the file extension. If your file is `main.js` then you only need to type `//= require main``.

You may notice another directive in your manifest file. The `require_tree` directive tells sprockets to load all files in the given folder. By default, the manifest file has `//= require_tree .` which will include all JS files in the same folder that `application.js` is located. This makes adding new JS files into our application really easy but can cause problems. As your application grows, you may not want all of the JS loaded everywhere. For example, say you have two pages that have a similiar button. You want those two buttons to behave differently even though they look the same. If all JS is loaded all the time, then the browser will not know what JS should be applied to these buttons. In the end, it's generally better to control what JS is being loaded for each page.  Additionally, the files will be loaded in alphabetical order.  Often, external libraries will have a dependency on another JS file being loaded before it, and all your Javascript will error out if this load order is not honored.  Given that things load in alphabetical order it's unlikely things will magically be loaded in the right order.  Check the console in your browser to see if you are getting these types of errors and if so manually require each file in the order you need it to be loaded and get rid of `require tree`.

One last thing to remember, when you require something in your manifest file, the path you provide must be the asset path. If you have the file `comments.js` in the folder `/assets/javascripts/blog` you would need to use `//= require blog/comments` to include it in our manifest file.

### Loading a Manifest File in your layout

Now that we have our manifest file, we need to include it in our application. The only thing we need to do is use the javascript_include_tag in our application layout file.  This is just a rails helper that generates a script tag instructing the browser to load that JS file.

**File: app/views/layouts/application.html.slim**
```erb
<%= javascript_include_tag "application" %>
```

Sprockets will then take care of loading our manifest file and determining what assets to load. If we are in development mode, each asset will be loaded individually.

```html
<script src="assets/jquery.min.js" />
<script src="assets/bootstrap.min.js" />
<script src="assets/blogs.js" />
```

In production mode, all the assets will be combined into a single file.

```html
<script src="/assets/application-908e25f4bf641868d8683022a5b62f54.js" />
```

## Resources
- http://guides.rubyonrails.org/asset_pipeline.html



<p data-visibility='hidden'>View <a href='https://learn.co/lessons/javascript-manifests'>Javascript Manifests</a> on Learn.co and start learning to code for free.</p>
