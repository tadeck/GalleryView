GalleryView - jQuery Content Gallery Plugin
Author: 		Jack Anderson

INSTRUCTIONS FOR USE
---------------------------------
1) Place galleryview-x.x folder somewhere in your website directory structure (you can rename this folder if desired)
2) Include script tags for the desired version of the script (uncompressed, packed) and for the included jQuery Times plugin file
3) Include a reference to the jquery.galleryview-x.x.css stylesheet in your document
4) Create an unordered list in your HTML with the content you wish to be displayed in your gallery (see below for more information on markup options
5) Edit the id of the first rule in jquery.galleryview-3.0.css to match the id given to your unordered list
6) Call the GalleryView plugin with the function call below:

	$('#id_of_list').galleryView()

	To override default option values, include them in JSON format in the call to the plugin, like so:
   
	$('#id_of_list').galleryView({
		gallery_width: 800,
		gallery_height: 600,
		frame_width: 120,
		frame_height: 90,
		pause_on_hover: true
	});
	
	Refer to the documentation URL listed above (or the uncompressed javascript) to see a full list of options, their effects on the plugin and their default values.
	


HTML MARKUP REQUIREMENTS
---------------------------------
Below, I will show you the markup required to produce various types of galleries. After the first example, 
I will exclude the UL wrapper and only show the HTML necessary for a single panel and/or frame.

1) 	Basic slideshow (no captions/overlay/HTML content)
		<ul id="gallery">
			<li><img src="../gv/path/to/image1.jpg" alt="image1" /></li>
			<li><img src="../gv/path/to/image2.jpg" alt="image2" /></li>
			<li><img src="../gv/path/to/image3.jpg" alt="image3" /></li>
			<li><img src="../gv/path/to/image4.jpg" alt="image4" /></li>
		</ul>
	
	This is the simplest gallery one can have. With all the defaul options set, the following actions occur within the plugin:
		- a copy of the image is created within a "panel" DIV
		- the filmstrip image is scaled and cropped to fit within the dimensions of the frame (set frame_scale to 'nocrop' to retain aspect ratio)
		- the panel image is scaled to fit within the gallery, but retains its own aspect ratio (set panel_scale to 'crop' to crop panel images)
	
	By default, the filmstrip will appear below the panels. The number of frames visible will be determined by the size of the panels. If there 
	is enough space in the gallery to fit all the filmstrip frames, the filmstrip will be centered within the gallery. If there are too many 
	frames, the additional frames will be hidden from view initially, appearing as the filmstrip slides to the left with each transition. Panel 
	and frame dimensions are set via plugin options, as is the location of the filmstrip. It can be set to appear below, above, or to either 
	side of the panels.
	
	To create a filmstrip-only gallery, no markup change is required, simply set the show_panels option to false. Alternatively, set 
	show_filmstrip to false for a panel-only gallery.
	
2)	Slideshow with frame captions

		<li><img src="../gv/path/to/image.jpg" alt="image" title="Pretty Picture" /></li>
		
	In this gallery, the title attribute of each image is used to create a caption under each frame. Note that GalleryView does not utilize 
	the alt attribute.
	
3)	Slideshow with panel overlays
	
		<li>
			<img src="../gv/path/to/image.jpg" alt="image" title="Pretty Picture" />
			<div class="gv-panel-overlay">
				<h3>Pretty Picture</h3>
				<p>Some more information about this photo, perhaps with a <a href="http://some.web.site" target="_blank">link</a> to another page.</p>
			</div>
		</li>
		
	For this gallery, the contents of the 'gv-panel-overlay' DIV will display on top of the panel image, its position determined by the 
	'overlay_position' option. The 'overlay_opacity' option controls how transparent the overlay is. The color and height of the overlays are 
	set in the included CSS file. A panel overlay can contain any HTML content desired, but it is preferable to stick to headings and paragraphs.
	
4)	Slideshow with HTML panel content

		<li>
			<img src="../gv/path/to/image.jpg" alt="image" title="Pretty Picture" />
			<div class="gv-panel-content">
				<h2>A News Article</h2>
				<p>Lorem ipsum dolor amet...</p>
				<p>More content...</p>
			</div>
		</li>
		
	When a 'gv-panel-content' DIV exists, the image provided is no longer used for the panel, but only the filmstrip. Any HTML content can 
	exist within a panel of this type, but it is important to remember that the panels do not scroll, and any overflow is hidden, so size 
	your panels appropriately with the panel_width and panel_height options.
	
	*NOTE* If you wish to have a gallery without filmstrips, it is not necessary to have any image outside your 'gv-panel-content' DIVs
	
	A useful implementation of this gallery type would be if you do not want to use the same image for the panel and filmstrip.  For 
	instance, if you want to use a specific portion of a large image for the filmstrip frame, you would create two images, one for your 
	panel and one for your filmstrip, then create the HTML as so:
	
		<li>
			<img src="../gv/path/to/thumbnail.jpg" alt="image" />
			<div class="gv-panel-content">
				<img src="../gv/path/to/full_size.jpg" alt="big image" />
			</div>
		</li>


CREATING/USING CUSTOM NAVIGATION THEMES
---------------------------------
GalleryView comes with four themes by default:
	- dark
	- light
	- ie6_dark
	- ie6_light
The dark themes contain dark navigation buttons and are best used in galleries with light backgrounds. The light themes contain light 
colored images and are best for galleries with dark backgrounds. The two ie6 themes use .GIF images instead of .PNG, so as to
ensure compatibility with older browsers that do not support alpha transparency.

To create your own navigation theme, first create the following images with the appropriate dimensions:
	- next.png (22x22)
	- prev.png (22x22)
	- panel-nav-next.png (42x42)
	- panel-nav-prev.png (42x42)

The images can be of any file type. Then, update the galleryView CSS file with the paths to your new navigation images.


That should hopefully be enough to get you started on the right track. Feel free to experiment and find me on twitter (@jackwanders) 
if you have any questions or comments. Enjoy!