# ptlinked-plugin

PTLINKED is a digital health / physical therapy company focused on creating engaging digital content and solutions that improve the musculoskeletal health, fitness, and wellness of populations globally, while also equipping providers with innovative tools that enable them to deliver convenient, accessible, and affordable care.

PTLINKED has developed a proprietary library of digital exercise content including over 3,000 HD rendered exercise animations and hundreds of pre-designed exercise programs packaged by a team of licensed physical therapists and certified strength & conditioning specialists. The PTLINKED exercise library is consistently reviewed by our clinical content team and updated regularly to ensure it is supported by the best available evidence-based research and meets the needs of our customers.

The PTLINKED plugin is a jQuery plugin that will integrate seamlessly into any website to create a fully functional interface for accessing the PTLINKED pre-designed exercise program library. The plugin requires a valid API Key and content license agreement from PTLINKED.

## Table of contents

- [Main](#main)
- [Getting started](#getting-started)
- [Options](#options)
- [Methods](#methods)
- [Callbacks](#callbacks)
- [Browser support](#browser-support)
- [Versioning](#versioning)


## Main

```text
dist/
├── ptlinked_plugin.css
├── ptlinked_plugin.min.css         (compressed)
├── jquery-ptlinked_plugin.js        
└── jquery-ptlinked_plugin.min.js   (compressed)
```

## Getting Started

### Installation

To install the plugin you will need to define the GitHub repository URL in the composer.json file. Below is an example:

```shell

"repositories": [
	{
		"type": "vcs",

		"url": "https://github.com/ptlinked/ptlinked-plugin"

	}
]

```

```shell
php composer require ptlinked/ptlinked-plugin
```

Includes:

```html
<script src="/path/to/jquery.js"></script><!-- jQuery is required -->

<script src="/path/to/jquery-ui.js"></script><!-- jQuery is required -->

<script src="/path/to/ptlinked-plugin/dist/jquery-ptlinked_plugin.min.js"></script><!-- jQuery PTLINKED Plugin is required -->

<link  href="/path/to/ptlinked-plugin/dist/ptlinked_plugin.min.css" rel="stylesheet"><!-- Plugin default stylesheet is required -->
```

The latest stable release of the plugin is also hosted on the PTLINKED CDN.

```html
<script src="https://0e7822f9ecb8551cd298-03053818a8848e389259d1c57ba1747f.ssl.cf2.rackcdn.com/jquery-ptlinked_plugin.min.js"></script>

<link  href="https://0e7822f9ecb8551cd298-03053818a8848e389259d1c57ba1747f.ssl.cf2.rackcdn.com/ptlinked_plugin.min.css" rel="stylesheet">
```

### Usage

#### Syntax

```js
new ptlinkedLibrary( element[, options] )
```

- **element**
	- Type: `HTMLDivElement`
	- The target DIV for the PTLINKED Plugin

- **options**
	- Type: `Object`
	- The plugin options object allowing you to control certain aspects of the plugin. Check out the available [options](#options) for the plugin.

#### Example

```html
<!-- Create a containing DIV that will be used to initialize the plugin -->

<div id="ptlinked--application_container" class="ptlinked--application_container">

</div>
```

```js
// Initialize the plugin
var ptlinked_plugin = $("#ptlinked--application_container").ptlinkedLibrary({

	api_key: {assigned_api_key},

	api_root_url: 'https://api-{deployment_name}.ptlinked.com',

	app_root_url: 'https://{web_site_url}/{page_plugin_is_installed_on}',

	user_uid: '{unique_user_identifier}',

	user_type: '{physician || patient || support || other}',

	header_element_class: 'site-header,site-nav-wrapper',

	save_favorites: '{true || false}',

	secure_messaging: '{true || false}',

	training_mode: '{true || false}',

	debug_mode: '{true || false}',

	dialog_box_type: '{jquery || hook}'

}) ;
```

#### Notes

- A valid **API Key** must be provided on initialization. The API Key is provided by PTLINKED.

- The base URI for the PTLINKED API **must be supplied** as an option during initialization of the plugin. PTLINKED will provide this along with the API Key.

- The URL of the web page that the plugin will be initialized on must be specified during the plugin initialization.

- If you are integrating with user capabilities (saving favorites, prescribing programs, tracking) you will need to initialize the plugin with a unique identifier (uid) and a label for the type of user (i.e. physician, patient).

[⬆ back to top](#table-of-contents)

## Options

You may set the PTLINKED Plugin options with `new ptlinkedLibrary(element, options)`.
If you want to change the global default options, You may use `$el.ptlinkedLibrary(option, key, value)`.

### api_key (required)

- Type: `String`
- Default: `''`

A valid API Key must be provided during initialization of the plugin. The API Key is a hash string generated by PTLINKED. This API Key is **essential** for this plugin to work as it will provide authorization to use the PTLINKED API in order to request and receive the PTLINKED exercise program content.

### api_root_url  (required)

- Type: `string`
- Default: `'https://api-{deployment_name}.ptlinked.com'`

The base (root) URI for the PTLINKED API **must be supplied** as an option during initialization of the plugin. PTLINKED will provide this along with the API Key.

### app_root_url (required)

- Type: `string`
- Default: `''`

The URL of the web page that the plugin will be initialized on must be specified during the plugin initialization. The purpose of this URL is to display a direct link to exercise programs within your website or application, typically found on the printed handouts.

### user_uid (required)

- Type: `string`
- Default: 0

This option allows you to specify a unique user identifier for the currently logged in user. This option supports both an integer or string value, as long as its unique to each specific user.


### user_type (required)

- Type: `string`
- Default: `'patient'`

This option will allow you to specify the type of user who is using the plugin. The purpose of this is to allow functionality control over certain aspects of the plugin based on the type of user using it. For example, a user type **Physician** will need the ability to **Send** exercise programs to their patients. Whereas a user type **patient** will not need that functionality.

### video_bg

- Type: `string`
- Default: `white`

This option will tell the plugin which background color version of the exercise videos to use. The default is **white** with the ability to set as either **blue** or **grey**.

### header_element_class (required)

- Type: `string`
- Default: `'site-header'`

This option allows you to define the web page header wrapper class name. The header, in this situation, refers to the visual HTML header at the top of the webpage (i.e. logo and primary menu header bar). This option is **essential** because the plugin uses the header wrapper element to calculate the plugin content display wrapper height. Without specifying this, there will be issues with the vertical scrollbar within the library content area. If the webpage header has multiple header elements that are not wrapped under one DOM element, you can specify multiple class names by seperating them with a coma (i.e. 'primary-site-header,secondary-site-header').

### viewer_header_element_class

- Type: `string`
- Default: `'viewer--header'`

This option is for the exercise program viewer overlay. You should not need to change this value unless you're using a custom HTML/CSS for the viewer overlay.

### viewer_thumb_scroller_class

- Type: `string`
- Default: `'viewer--header_bar'`

As with the previous option, this should not be changed. It is used to calculate the scroll area height for the exercise program viewer overlay.

### dialog_box_type

- Type: `string`
- Default: `'jquery'`
- Options:
	- `'jquery'`: Use jQuery UI dialog boxes. When using this option, the plugin iteself will trigger the jQuery dialog box.
	- `'hook'`: Setting this value will not trigger any dialog box from within the plugin. Instead, it will trigger a callback function `onShowDialog` with a data object containing the title, content, and button configuration. This will allow you to hook the dialog box calls and display anytype of dialog box framework/component your site or application is using.

### save_favorites

- Type: `boolean`
- Default: `false`
- Options:
	- `true`: Enable the **Save to Favorites** button on the exercise program viewer. For this option to work, `user_uid` and `user_type` must be set during initialization.
	- `false`: Disabled the **Save to Favorites** button on the exercise program viewer.

### secure_messaging

- Type: `boolean`
- Default: `false`
- Options:
	- `true`: Enable the **Send Exercise Program** button on the exercise program viewer. For this option to work, `user_uid` and `user_type` must be set during initialization.
	- `false`: Disabled the **Send Exercise Program** button on the exercise program viewer.

### training_mode

- Type: `boolean`
- Default: `false`
- Options:
	- `true`: When this option is enabled, the plugin will provide all functionality, however, no user specific data will be committed to the database. This includes **Saved to Favorites**, **Usage Tracking**, **Sending Exercise Programs**. This mode is intended to help train new users with the need to clear the data afterwards.
	- `false`: Turn training mode off, so any modified data will be committed to the database.

### debug_mode

- Type: `boolean`
- Default: `false`
- Options:
	- `true`: When this option is enabled, debug information will be outputted to the browser console. This should only be enabled in sandbox enviornments, prior to production launch.
	- `false`: This will disable the console output for the plugin.


[⬆ back to top](#table-of-contents)

## Methods

### destroy()

Usage:

```js
$('#el').ptlinkedLibrary('destroy') ;
```
Destroy the PTLINKED Plugin and remove the instance from the element.

### option()

Usage:

```js
$('#el').ptlinkedLibrary('option', 'key') ; // Get OPTION value

$('#el').ptlinkedLibrary('option', 'key', 'value') ; // Set OPTION value
```

Get/Set a plugin option after initialization.

## Callbacks

### onInit()

This callback is triggered when the PTLINKED Plugin has been initialized and loaded successfully.

```js
ptlinked_app = $("#ptlinked--application_container").ptlinkedLibrary({

	onInit: function(){

		console.log( "Plugin has been initialized" ) ;

	}

});
```

### onSendProgram( data )

This callback is triggered when a user clicks the **Send** button on the exercise viewer. A data object is passed to the registered callback function providing details on the exercise program being sent.

```js
ptlinked_app = $("#ptlinked--application_container").ptlinkedLibrary({

	onSendProgram: function( data ){

		console.log( "User wants to send this exercise program." ) ;
		console.log( "Title of the Exercise Program: " + data["exercise_program_title"] ) ;
		console.log( "Direct Link to Exercise Program: " + data["exercise_program_link"] ) ;			

	}

});
```

### onPrintProgram( data )

This callback is triggered when a user clicks the **Print** button on the exercise viewer. A data object is passed to the registered callback function providing details on the exercise program being printed.

```js
ptlinked_app = $("#ptlinked--application_container").ptlinkedLibrary({

	onPrintProgram: function( data ){

		console.log( "User wants to print this exercise program." ) ;
		console.log( "Title of the Exercise Program: " + data["exercise_program_title"] ) ;		
		console.log( "Direct Link to Exercise Program: " + data["exercise_program_link"] ) ;		
		console.log( "User UID: " + data["user_id"] ) ;

	}

});
```

### onSaveProgram( data )

This callback is triggered when a user clicks the **Save** button on the exercise viewer. A data object is passed to the registered callback function providing details on the exercise program being saved.

```js
ptlinked_app = $("#ptlinked--application_container").ptlinkedLibrary({

	onSaveProgram: function( data ){

		console.log( "User wants to save this exercise program." ) ;
		console.log( "Title of the Exercise Program: " + data["exercise_program_title"] ) ;		
		console.log( "Direct Link to Exercise Program: " + data["exercise_program_link"] ) ;		
		console.log( "User UID: " + data["user_id"] ) ;

	}

});
```

### onViewExerciseProgram( data )

This callback is triggered when a user clicks an exercise program card to view the program. A data object is passed to the registered callback function providing details on the exercise program being viewed.

```js
ptlinked_app = $("#ptlinked--application_container").ptlinkedLibrary({

	onViewExerciseProgram: function( data ){

		console.log( "User wants to view this exercise program." ) ;
		console.log( "Title of the Exercise Program: " + data["title"] ) ;		
		console.log( "Direct Link to Exercise Program: " + data["url"] ) ;		
		console.log( "User UID: " + data["user_id"] ) ;

	}

});
```

### onShowDialog( data )

This callback is triggered when the **dialog_box_type** is set to **hook** and the display of a dialog box is required by the plugin. A data object is passed to the registered callback function providing details on how to display the dialog box.

```js
ptlinked_app = $("#ptlinked--application_container").ptlinkedLibrary({

	onShowDialog: function( data ){

		console.log( "Display a dialog box to the user" ) ;
		console.log( "Title of the dialog box: " + data["title"] ) ;		
		console.log( "Body/Message of the dialog box: " + data["content"] ) ;		
		console.log( "Confirmation Button: " + data["confirmation_btn"] ) ;
		console.log( "Callback if user confirms: " + data["confirmation_callbackn"] ) ;

	}

});
```

[⬆ back to top](#table-of-contents)

## Browser support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Opera (latest)
- Edge (latest)
- Internet Explorer 11+
- iOS & Android

[⬆ back to top](#table-of-contents)

## Versioning

Maintained under the [Semantic Versioning guidelines](https://semver.org/).

[⬆ back to top](#table-of-contents)