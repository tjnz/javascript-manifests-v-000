# Javascript Manifests

## Objectives

1. Create Javascript Manifest Files
2. Require Javascript Files in Manifests with Sprocket Directives
3. Include Javascript Manifest Files in Layouts
4. See a Manifest in Development vs Production

## Outline

### Manifest Files

There are two things that make a JS file in app/assets a manifest file as opposed to actual JS code.

1. You load it into a main layout via javascript_include_tag

2. You use the magic "sprocket" directives that are valid JS comments that look like:

//=

### `require` directives

Let's learn about the directives available to you to require files into a manifest.

https://github.com/rails/sprockets#sprockets-directives

The most common one is require and in fact we recommend explicitly loading asset dependencies using only require. require_tree and the such can lead to weird issues with load order and dependencies.

Remember that when you require something the path you provide must be the asset path, as though accessed via /assets

### Loading a Manifest File in your layout

Nothing special here, when you say javascript_include_tag it will see if it's a manifest an act accordingly loading all the dependencies or it will simply create a script tag for the single JS file.

When you see javascript_include_tag application you think 1 file was loaded but actually many were.

Show the student that there is a script tag for each file in the manifest.

Show how to debug manifest files that require files that can't be found.

#### Manifests in Production

Show what a concatenated manifest looks like in production.
