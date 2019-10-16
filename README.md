# froala-oembed [![npm](https://img.shields.io/npm/v/froala-oembed.svg)](https://www.npmjs.com/package/froala-oembed) [![license](https://img.shields.io/npm/l/froala-oembed.svg)](LICENSE.md)

A simple plugin for [Froala WYSIWYG Editor](https://www.froala.com/wysiwyg-editor/) that allows users to insert and customise a wide variety of external Web content.

## Prerequisites

This plugin requires Froala Editor >= 2.0.0 - it was developed under 2.7.5.

## Installing

Add `froala-oembed` to your package.json:
```bash
npm install --save froala-oembed
# or
yarn add froala-oembed
```

Then load the files froala-oembed.js and froala-oembed.css on your page:
```html
<!-- anywhere on the page -->
<link rel="stylesheet" src="/node_modules/froala-oembed/froala-oembed.css" />

<!-- after loading froala core -->
<script src="/node_modules/froala-oembed/froala-oembed.js"></script>
```

In your Froala configuration, add the `oembed` plugin to the list of enabled plugins. Then you can add `insertOembed` to any of the toolbars, or `oembed` to the Quick Insert buttons, or both:
```javascript
const froalaConfig = {
  pluginsEnabled: ['image', 'video', 'oembed', ...],
  toolbarButtons: ['insertOembed', '|', 'insertVideo', ...],
  quickInsertButtons: ['oembed', 'video', ...],
  ...
};
```

## Configuration

froala-oembed supports a variety of configuration options, several of which work just like core plugins' options. Here are the recognised options:

### `oembedEditButtons`

**Type:** `[String]`
**Default:** `['oembedReplace', 'oembedRemove']`

The buttons that appear in the edit-oEmbed popup when an existing oEmbed widget is selected. Adding different buttons to this list is unlikely to work well, but you may remove unwanted buttons without any trouble.

### `oembedEmbedFactory`

**Type:** `String -> Promise ($Element|String)`
**Default:** `src => Promise.resolve($('<iframe>').attr({src}))`

Perhaps the most important option, the embed factory is a function that froala-oembed will use to display oEmbedded content. The URL of the content will be passed in, and a promise for that content's embeddable form should be returned. Either a string of HTML or a jQuery element may be returned, whichever is easier for the factory to produce.

As you can see, the default implementation is simply to generate an `<iframe>` with no special behaviour. This works for some sites, but many sites refuse to be displayed in an `<iframe>` and so won't work. Therefore, we recommend you override the factory with one of your own that's a lot smarter - for example, here at Coassemble we use an embed factory that calls [Iframely](https://iframely.com/) and fetches HTML from its API.

### `oembedInsertButtons`

**Type:** `[String]`
**Default:** `['oembedBack']`

The buttons that appear in the insert-oEmbed popup when the oEmbed button is clicked in a toolbar. These buttons function like tabs, toggling between the different possible ways to insert an audio clip. Again, adding new buttons is unlikely to work well, but you may remove unwanted ones.

### `oembedMove`

**Type:** `Boolean`
**Default:** `true`

Allows changing the position of oEmbed widgets in the content by dragging them.

### `oembedSplitHTML`

**Type:** `Boolean`
**Default:** `false`

Allows a new oEmbed widget to split apart existing HTML when it is inserted. Not recommended.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/coassemble/froala-oembed/tags). 

## Authors

* **Danielle McLean** - [00dani](https://github.com/00dani)

See also the list of [contributors](https://github.com/coassemble/froala-oembed/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.
