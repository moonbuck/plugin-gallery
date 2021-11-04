# plugin-gallery
A plugin for [Micro.blog](https://micro.blog "Micro.blog") that creates a page for housing an instance of a [GLightbox](https://biati-digital.github.io/glightbox/ "GLightbox") gallery. This plugin is dependent on [plugin-lightbox](https://github.com/moonbuck/plugin-lightbox "plugin-lightbox") as it utilizes its glightbox injection and shortcodes.

![](https://raw.githubusercontent.com/moonbuck/plugin-gallery/main/images/signed_art_gallery.jpeg)

Once installed, the generated page may be found at `[SCHEME]://[HOSTNAME]/gallery/`.

# Page Configuration

The file living at `content/gallery.md` specifies the front matter for the page.

```json
{
  "title": "Gallery",
  "description": "Gallery",
  "type": "gallery",
  "menu": {
    "main": {
      "name": "Gallery",
      "title": "Gallery",
      "identifier": "gallery",
      "url": "/gallery/",
      "weight": 105
    }
  }
}
```

You can customize this by editing the value for `description` to give the page an appropriate description. The value of `title` controls the page’s title. I played around with changing the value of `menu.main.name` and never noticed any difference. The value of `menu.main.title` controls the label used in the navigation menu. The value of `menu.main.weight` adjusts the order of the navigation item amongst other weighted items. The value of `menu.main.identifier` I believe may be of use within other Hugo partials.

If you are happy with page URL as described above, don’t touch `type` or `menu.main.url`. If you want to change the URL, this what you want to do:

1. Change the values of `type` and `menu.main.url` so that they contain the same replacement value (I believe the custom would be dashed for multiple words but I am not positive).
2. Edit the  location for the template at `layouts/gallery/single.html` by replacing `gallery` as the directory with the exact same value you replaced it with in step one. 

## Stylesheets

There is one stylesheet included. It lives at `static/assets/css/gallery.css` and looks like this:

```css
div.gallery {
  padding-top: 2em;
}

a.gallery-link {
  height: 30vh; 
  width: 20%; 
  flex-grow: 1;
}

img.gallery-image {
  max-height: 100%;
  min-height: 100%; 
  min-width: 100%; 
  object-fit: cover; 
  vertical-align: bottom;
}

video.gallery-video {
  margin-top: 0; 
  max-height: 100%; 
  min-height: 100%; 
  min-width: 100%; 
  object-fit: cover; 
  vertical-align: bottom;
}
```

These are the values I currently use on [my site](https://moondeer.blog/gallery/ "Gallery"). They utilize the classes that the `plugin-lightbox` automatically attaches in the `gallery` partial. You can change them or delete the file entirely if you are setting the style within the gallery data parameter (described below).

## Gallery Data Example

To make anything show up, you’re gonna need to feed the plugin some data. You can do this through the plugin parameter interface or by creating a new template (file) under the directory I specify below.

If you decide to utilize the plugin parameter interface:

![Plugin Parameter Interface](https://raw.githubusercontent.com/moonbuck/plugin-gallery/main/images/plugin_parameter.jpeg)

You will want to make sure you are pasting in a JSON object.

If, however, you choose to create a new file located at `data/plugin_gallery/gallery_data.ext` (where `ext` is replaced by the appropriate extension), the data file may be JSON, TOML, or YAML. This example will use JSON. So, to deploy it, I would want to create a new template at `data/plugin_gallery/gallery_data.json`.

Let’s look at an example file and then I’ll explain what all we can throw into it.

```json
{
  "name": "Signed Art",
  "photo_width": 400,
  "link_style": "height:200px;flex-grow:1",
  "img_style": "max-height:100%;min-height:100%;object-fit:cover;vertical-align:bottom",
  "video_style": "max-height:100%;min-height:100%;object-fit:cover;vertical-align:bottom",
  "description": "*An interactive grid of my signed digital art in the order I created them.*",
  "slides": [
    {"title": "American Fabric", 
     "src": "https://moondeer.blog/uploads/2021/80b124a294.jpg"},
    {"title": "Cold Race War", 
     "src": "https://moondeer.blog/uploads/2021/76c82b757c.jpg"},
    {"title": "Representation", 
     "src": "https://moondeer.blog/uploads/2021/95e03999ff.jpg"},
    {"title": "Josh", 
     "src": "https://moondeer.blog/uploads/2021/f706dce000.jpg"},
    {"title": "South Carolina Tokens", 
     "src": "https://moondeer.blog/uploads/2021/10c1206ccb.jpg"},
    {"title": "Fodder", 
     "src": "https://moondeer.blog/uploads/2021/7c1a92896a.jpg"},
    {"title": "Damn Good Dawg", 
     "src": "https://moondeer.blog/uploads/2021/f9ba3905ca.jpg"},
    {"title": "Murphy", 
     "src": "https://moondeer.blog/uploads/2021/f8b4727edc.jpg"},
    {"title": "Demography and The GOP", 
     "src": "https://moondeer.blog/uploads/2021/07f16097b2.jpg"},
    {"title": "Bubble Merger", 
     "src": "https://moondeer.blog/uploads/2021/57cccbe268.jpg"},
    {"title": "Euler Diagram", 
     "src": "https://moondeer.blog/uploads/2021/f1ed034c78.jpg"},
    {"title": "Follower's Count", 
     "src": "https://moondeer.blog/uploads/2021/2c5884abec.jpg"},
    {"title": "Shanti", 
     "src": "https://moondeer.blog/uploads/2021/869813b580.jpg"},
    {"title": "Obstacles", 
     "src": "https://moondeer.blog/uploads/2021/54a798a76b.jpg"},
    {"title": "Base Sculpting 101", 
     "src": "https://moondeer.blog/uploads/2021/e0c894684d.mov"},
    {"title": "Snake Oil", 
     "src": "https://moondeer.blog/uploads/2021/573e0c430d.jpg"},
    {"title": "Programming", 
     "src": "https://moondeer.blog/uploads/2021/69decd9ec3.jpg"},
    {"title": "House of Cards", 
     "src": "https://moondeer.blog/uploads/2021/57da10e35f.jpg"},
    {"title": "GOP Affiliations Deck", 
     "src": "https://moondeer.blog/uploads/2021/c27515570a.png"},
    {"title": "Thin Blue Line", 
     "src": "https://moondeer.blog/uploads/2021/51cd2fc27e.jpg"}
   ]
 }
```

## Valid Keys

<dl>
<dt>name</dt>
<dd>The name of the gallery. This is required.</dd>

<dt>wrap</dt>
<dd>Whether the gallery links should wrap or be constrained to a single row. Default is<code>true</code>.</dd>

<dt>div_class</dt>
<dd>Custom class to apply to the <code>div</code>. Default is<code>undefined</code>. 'gallery' is always applied.</dd>

<dt>div_style</dt>
<dd>Custom style to apply to the <code>div </code>in additon to the flex declaration and wrap specification. Default is<code>undefined</code>.</dd>

<dt>link_class</dt>
<dd>Custom class to apply to all anchor tags. Default is<code>undefined</code>. gallery-link and glightbox are always applied.</dd>

<dt>link_style</dt>
<dd>Custom style to apply to all anchor tags. Default is<code>undefined</code>.</dd>

<dt>desc_position</dt>
<dd>(<code>bottom</code>, <code>top</code>, <code>left</code>, <code>right</code>) Where all slides descriptions should be positioned. Default is <code>bottom</code>.</dd>

<dt>effect</dt>
<dd>(<code>zoom</code>, <code>fade</code>, <code>none</code>) The animation effect all slide should use. Default is <code>zoom</code>.</dd>

<dt>width</dt>
<dd>The custom width for all slides. Default is <code>900px</code>.</dd>

<dt>height</dt>
<dd>The custom height for all slides. Default is <code>506px</code>.</dd>

<dt>zoomable</dt>
<dd>Whether slides should be zoomable. Default is<code>true</code>.</dd>

<dt>draggable</dt>
<dd>Whether slides should be draggable. Default is<code>true</code>.</dd>

<dt>video_class</dt>
<dd>Custom class to apply to all <code>video</code> tags. Default is<code>undefined</code>. gallery-video is always applied.</dd>

<dt>video_style</dt>
<dd>Custom style to apply to all <code>video</code> tags. Default is<code>undefined</code>.</dd>

<dt>loop</dt>
<dd>Whether link videos should loop. Default is<code>true</code>.</dd>

<dt>autoplay</dt>
<dd>Whether link videos should be set to autoplay. Default is<code>true</code>.</dd>

<dt>preload</dt>
<dd>Value for link video <code>preload</code> attributes. This ignored when set to autoplay. Default is<code>undefined</code>.</dd>

<dt>img_class</dt>
<dd>Custom class to apply to all <code>img</code> tags. Default is<code>undefined</code>. gallery-image is always applied.</dd>

<dt>img_style</dt>
<dd>Custom style to apply to all <code>img</code> tags. Default is<code>undefined</code>.</dd>

<dt>photo_width</dt>
<dd>Specifies a pixel width for a thumbnail image to be fetched using the <code>https://micro.blog/photos/</code> API. Default is<code>undefined</code>.</dd>

<dt>slides</dt>
<dd>The array of slide data objects. The only requirement is to have an entry for at least one of <code>href</code> or <code>src</code>.
<dl>
<dt>href</dt>
<dd>The URL for the slide content. This is required unless a <code>src</code> parameter value has been provided.</dd>

<dt>src</dt>
<dd>The URL for the link content. This is required unless an <code>href</code> parameter value has been provided.</dd>

<dt>link_style</dt>
<dd>Custom style to apply to the anchor tag. Default is <code>undefined</code>.</dd>

<dt>gallery</dt>
<dd>The name of the slide's gallery. Default is <code>undefined</code>.</dd>

<dt>title</dt>
<dd>The slide's title. Default is <code>undefined</code>.</dd>

<dt>description</dt>
<dd>The slide's description. Default is <code>undefined</code>.</dd>

<dt>desc_position</dt>
<dd>(<code>bottom</code>, <code>top</code>, <code>left</code>, <code>right</code>) Where the slide's description should be positioned. Default is <code>bottom</code>.</dd>

<dt>type</dt>
<dd>(<code>image</code>, <code>video</code>, <code>inline</code>?, <code>iframe</code>?) The slide type. Default infers from source … and the last two options I'm not sure about.</dd>

<dt>effect</dt>
<dd>(<code>zoom</code>, <code>fade</code>, <code>none</code>) The animation effect the slide should use. Default is <code>zoom</code>.</dd>

<dt>width</dt>
<dd>The custom width for this slide. Default is <code>900px</code>.</dd>

<dt>height</dt>
<dd>The custom height for this slide. Default is <code>506px</code>.</dd>

<dt>zoomable</dt>
<dd>Whether this slide should be zoomable. Default is <code>true</code>.</dd>

<dt>draggable</dt>
<dd>Whether this slide should be draggable. Default is <code>true</code>.</dd>

<dt>sizes</dt>
<dd>Specifies image sizes for different page layouts. Default is<code>undefined</code>.</dd>

<dt>srcset</dt>
<dd>Specifies a list of image files to use in different situations. Default is<code>undefined</code>.</dd>

<dt>video_style</dt>
<dd>Custom style to apply to the <code>video tag</code>. Default is<code>undefined</code>.</dd>

<dt>loop</dt>
<dd>Whether the link video should loop. Default is<code>true</code>.</dd>

<dt>autoplay</dt>
<dd>Whether the link video should be set to autoplay. Default is<code>true</code>.</dd>

<dt>preload</dt>
<dd>Value for the link video's <code>preload</code> attribute. This ignored when set to <code>autoplay</code>. Default is<code>undefined</code>.</dd>

<dt>alt</dt>
<dd>Specifies an alternate text for an image. Default is<code>undefined</code>.</dd>

<dt>img_style</dt>
<dd>Custom style to apply to the <code>img</code> tag. Default is <code>undefined</code>.</dd>

<dt>photo_width</dt>
<dd>Specifies a pixel width for a thumbnail image to be fetched using the <code>https://micro.blog/photos/</code> API. Default is<code>undefined</code>.</dd>
</dl></dd>
</dl>