# JavaScript - TinyMCE


#### Add to `Gemfile`:
```ruby
gem 'tinymce-rails' 
```


#### Add to `application.js`:
```js
//= require tinymce
```


#### Add to JavaScript:
```js

// Custom image buttons plugins
// ----------------------------------------------
tinymce.PluginManager.add('custom_image_buttons', function (editor) {

  editor.ui.registry.addMenuButton('image_dropdown', {
    icon: 'image',
    type: 'menubutton',
    fetch: function (callback) {
      callback([
        {
          type: 'menuitem',
          text: 'Upload',
          onAction: function () { editor.ui.registry.getAll().buttons.quickimage.onAction(); }
        },
        {
          type: 'menuitem',
          text: 'Select',
          onAction: function () {}
        },
        {
          type: 'menuitem',
          text: 'Paste URL',
          onAction: function () { editor.ui.registry.getAll().buttons.image.onAction(); }
        }
      ]);
    }
  });

  editor.ui.registry.addButton('image_paste', {
    icon: 'image',
    text: 'Paste URL',
    onAction: function () { editor.ui.registry.getAll().buttons.image.onAction(); }
  });

  editor.ui.registry.addButton('image_select', {
    icon: 'image',
    text: 'Select',
    onAction: function (_) {}
  });

  editor.ui.registry.addButton('image_upload', {
    icon: 'image',
    text: 'Upload',
    onAction: function () { editor.ui.registry.getAll().buttons.quickimage.onAction(); }
  });

});
// ----------------------------------------------


var options = {};

// Callback - init
// ----------------------------------------------
options['init_instance_callback'] = function (editor) {
  editor.on('Change', function (e) {});
};
// ----------------------------------------------

// General options
// ----------------------------------------------
options['selector']   = '.js-html-editor';
options['menubar']    = false; // Disable menubar above toolbar
options['min_height'] = 350;
options['max_height'] = 1000;
options['statusbar']  = true;

// Add custom styles
//options['content_css']   = ['/assets/tinymce.css'];
//options['content_style'] = 'a {text-decoration: none;';

// add skin
// options['skin_url'] = '/css/mytinymceskin'

options['plugins'] = [
  'quickbars', // required for Toolbar items: quickimage
  'wordcount', // adds word counter in the statusbar
  'fullscreen',
  'searchreplace',
  'lists',
  'link',
  'print',
  'image',
  'imagetools',
  'table',
  'charmap',
  'code', // edit as html
  'custom_image_buttons',
  'add_affiliate_btn'
];

//options['nonbreaking_force_tab']        = true;

options['quickbars_selection_toolbar'] = false; // disable floating bar when selecting text
options['table_tab_navigation']        = true;

// disable native right-click menu
options['contextmenu_never_use_native'] = true;
options['contextmenu']                  = false;

options['remove_trailing_brs'] = true;
options['keep_styles']         = false;
options['paste_as_text']       = false; // true = paste without formatting

options['custom_colors'] = true; // true = allow to use colorpicker to select any color
options['color_cols']    = 10;
options['color_map']     = [
  "000000", "Black",
  "993300", "Burnt orange",
  "333300", "Dark olive",
  "003300", "Dark green",
  "003366", "Dark azure",
  "000080", "Navy Blue",
  "333399", "Indigo",
  "333333", "Very dark gray",
  "800000", "Maroon",
  "FF6600", "Orange",
  "808000", "Olive",
  "008000", "Green",
  "008080", "Teal",
  "0000FF", "Blue",
  "666699", "Grayish blue",
  "808080", "Gray",
  "FF0000", "Red",
  "FF9900", "Amber",
  "99CC00", "Yellow green",
  "339966", "Sea green",
  "33CCCC", "Turquoise",
  "3366FF", "Royal blue",
  "800080", "Purple",
  "999999", "Medium gray",
  "FF00FF", "Magenta",
  "FFCC00", "Gold",
  "FFFF00", "Yellow",
  "00FF00", "Lime",
  "00FFFF", "Aqua",
  "00CCFF", "Sky blue",
  "993366", "Red violet",
  "FFFFFF", "White",
  "FF99CC", "Pink",
  "FFCC99", "Peach",
  "FFFF99", "Light yellow",
  "CCFFCC", "Pale green",
  "CCFFFF", "Pale cyan",
  "99CCFF", "Light sky blue",
  "CC99FF", "Plum"
];
//options['event_root'] = ''; // https://www.tiny.cloud/docs/configure/editor-appearance/#event_root
// ----------------------------------------------

// Font toolbar dropdown (toolbar item: 'fontselect')
// ----------------------------------------------
options['font_formats'] = [
  ['Andale Mono', 'andale mono,times'],
  ['Arial', 'arial,helvetica,sans-serif'],
  ['Arial Black', 'arial black,avant garde'],
  ['Book Antiqua', 'book antiqua,palatino'],
  ['Comic Sans MS', 'comic sans ms,sans-serif'],
  ['Courier New', 'courier new,courier'],
  ['Georgia', 'georgia,palatino'],
  ['Helvetica', 'helvetica'],
  ['Impact', 'impact,chicago'],
  ['Symbol', 'symbol'],
  ['Tahoma', 'tahoma,arial,helvetica,sans-serif'],
  ['Terminal', 'terminal,monaco'],
  ['Times New Roman', 'times new roman,times'],
  ['Trebuchet MS', 'trebuchet ms,geneva'],
  ['Verdana', 'verdana,geneva'],
  ['Webdings', 'webdings'],
  ['Wingdings', 'wingdings,zapf dingbats'],
  ['Roboto', 'roboto']
].map(function (x) { return (x[0] + '=' + x[1]) }).join(';');
// ----------------------------------------------

// Font size toolbar dropdown (toolbar item: 'fontsizeselect')
// ----------------------------------------------
options['fontsize_formats'] = '11px 12px 14px 16px 18px 24px 36px 48px';
// ----------------------------------------------

// Styles toolbar dropdown (toolbar item: 'styleselect')
// ----------------------------------------------
options['style_formats_merge'] = false;
options['style_formats']       = [
  {title: 'Heading 1', format: 'h1'},
  {title: 'Heading 2', format: 'h2'},
  {title: 'Heading 3', format: 'h3'},
  {title: 'Heading 4', format: 'h4'},
  {title: 'Heading 5', format: 'h5'},
  {title: 'Heading 6', format: 'h6'}
];
// ----------------------------------------------


// don't use '-' in class names. Only '_'
options['valid_classes'] = [
  'affiliate_link'
].join(' ');

// Toolbar
// ----------------------------------------------
options['toolbar'] = [
  [
    'fullscreen',
    'fontselect',
    'fontsizeselect',
    'styleselect',
    'forecolor backcolor',
    'outdent indent',
    'alignleft aligncenter alignright alignjustify',
    'print',
    'searchreplace',
    'code'
  ],
  [
    'undo redo',
    'bold italic underline',
    'strikethrough superscript subscript blockquote',
    'bullist numlist',
    'link charmap table',
    'image_dropdown',
    'image_upload image_select image_paste'
  ]
].map(function (x) { return x.join(' | '); });
// ----------------------------------------------

options['setup'] = function (editor) {};

tinyMCE.init(options);
```


#### Add custom btn:
Note: to show button add `affiliate_btn` to `options['toolbar']`
```js
tinymce.PluginManager.add('add_affiliate_btn', function (editor) {
  editor.ui.registry.addButton('affiliate_btn', {
    text: 'Affiliate',
    icon: 'link',
    onAction: function (_) {
      editor.windowManager.open({
        title: 'Dialog Title',
        body: {
          type: 'panel',
          items: [
            {type: 'input', name: 'title', label: 'Title'}
          ]
        },
        buttons: [
          {type: 'submit', text: 'submit'},
          {type: 'cancel', text: 'cancel'}
        ],
        onSubmit: function (e) {
          editor.focus();
          editor.selection.setContent('<span class="affiliate_link">' + e.getData().title + '</span>');
          tinymce.activeEditor.windowManager.close();
        }
      });
    }
  });
});

options['valid_classes'] = {
  'span': ['affiliate-link'].join(' ')
};

options['custom_elements'] = [
  'affiliate-link'
].join(',');
```
