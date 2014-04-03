Flickr field
=============

## Description

This is an add-on for the Advanced Custom Fields WordPress plugin that creates a list of all Flickr sets/galleries from a specific Flickr user.

**Contributors**:

* Paul Huisman	([paulhuisman.com](http://www.paulhuisman.com))

## Notice

- This add-on needs [ACF](http://www.advancedcustomfields.com/) 


## Installation

1. Download or clone the ACF Flickr Field repo to your plugin directory by downloading https://github.com/phuisman88/flickrfield/zipball/master or cloning: git clone git://github.com/phuisman88/flickrfield.git  
2. Enable the plugin in Wordpress.
3. Succes! You can now select a Flickr field when you create new custom fields.

## Usage Example (PHP)

	// Get the Flickr set data by using get_field
	$flickr_set = get_field('flickr_set');
	
	// Check if an set or gallery ID exists and if its not null
	if (!empty($flickr_set['id']) && $flickr_set['id'] != 0) {
		
		// Require phpFlickr
		require_once(dirname(__FILE__) . '/fields/flickr/phpFlickr.php');
		$f = new phpFlickr($flickr_set['api_key']);
		
		// Enable phpFlickr caching
		$f->enableCache("f", dirname(__FILE__) . '/fields/flickr/cache');
	
		$photos = $f->photosets_getPhotos($flickr_set['id']);
		foreach ($photos['photoset']['photo'] as $photo) {	
			echo '<a href="'. $f->buildPhotoURL($photo, 'large') .'"><img src="'. $f->buildPhotoURL($photo, 'square') .'"/></a>';
		}
			
		}
		
	}
	
