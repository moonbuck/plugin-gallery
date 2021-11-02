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

Let’s look at the file and then I’ll explain how the keys are used.

```json
{
  "name": "Signed Art",
  "photo_width": 400,
  "link_class": "Custom Link Class",
  "img_class": "Custom Image Class",
  "video_class": "Custom Video Class",
  "link_style": "height:200px;flex-grow:1",
  "img_style": "max-height:100%;min-height:100%;object-fit:cover;vertical-align:bottom",
  "video_style": "max-height:100%;min-height:100%;object-fit:cover;vertical-align:bottom",
  "title_key": "title",
  "desc_key": "description",
  "src_key": "src",
  "width_key": "width",
  "height_key": "height",
  "thumb_src_key": "thumb",
  "desc_position_key": "desc-position",
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
<dd>This value will be used to set the `data-gallery` attributes within the glightbox API. The `.LinkTitle` of the page will be used when this value is absent.</dd>
<dt>photo\_width</dt>
<dd>Establishes a pixel width for requests running through the `https://micro.blog/photos/` API. The fetched image is intended to serve as a thumbnail.</dd>
<dt>link\_class</dt>
<dd> Custom class name to add to `<a>` tags. This value will be anchorized (dash-cased). </dd>
<dt>img\_class</dt>
<dd> Custom class name to add to `<img>` tags. This value will be anchorized (dash-cased). </dd>
<dt>video\_class</dt>
<dd>Custom class name to add to `<video>` tags. This value will be anchorized (dash-cased).</dd>
<dt>link\_style</dt>
<dd> Custom CSS style to be applied to `<a>` tags. </dd>
<dt>img\_style</dt>
<dd> Custom CSS style to be applied to `<img>` tags. </dd>
<dt>video\_style</dt>
<dd>Custom CSS style to be applied to `<video>` tags.</dd>
<dt>title\_key</dt>
<dd>The lookup key for slide title data to use in place of `title`.</dd>
<dt>desc\_key</dt>
<dd> The lookup key for slide description data to use in place of `description`.</dd>
<dt>src\_key</dt>
<dd> The lookup key for slide src data to use in place of `src`. </dd>
<dt>width\_key</dt>
<dd> The lookup key for slide width data to use in place of `width`. </dd>
<dt>height\_key</dt>
<dd> The lookup key for slide height data to use in place of `height`. </dd>
<dt>thumb\_src\_key</dt>
<dd> The lookup key for slide thumb source data to use in place of `thumb`. </dd>
<dt>desc\_position\_key</dt>
<dd> The lookup key for slide description position source data to use in place of `desc-position`. </dd>
<dt>description</dt>
<dd>This value holds the introductory for your gallery. Any markdown will be parsed before it hits the page.</dd>
<dt>slides</dt>
<dd>The array of all your slide JSON objects. The only entry required to create a slide is  `src`, which should point to your slide’s content.</dd>
</dl>
