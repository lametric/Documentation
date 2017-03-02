.. cloud-icons
    
Icons
=====

+-------+-----------------------------------------------+
|URL    |/api/v2/icons                                  |
+-------+-----------------------------------------------+
|Method | GET                                           |
+-------+-----------------------------------------------+

Description
^^^^^^^^^^^^^^^^^^^^^
Returns the list of the icons available at http://developer.lametric.com/icons. Supports pagination and sorting.

Parameters
^^^^^^^^^^

==============  =====================================================================
Parameter       Description                                                           
==============  =====================================================================
``page``        Page number [0..n-1]                                                                   
``page_size``   Number of items per page [1..total_icon_count]                                           
``fields``      Comma separated field list to filter out fields that are not needed. 
``order``       [popular, newest, title]

                - "popular" instructs the server to return icons sorted by popularity
                - "newest" instructs the server to return icons sorted by the creation time
                - "title" instructs the server to return icons sorted by title.              
==============  =====================================================================

Response
^^^^^^^^
Returns list of icon object inside "data" object and pagination information in "meta" object.

**Meta Object**

====================  ================  ======================================================
Property              Type              Description                                           
====================  ================  ======================================================
``total_icon_count``  Integer           Total number of icons in database
``page``              Integer           Current page number
``page_size``         Integer           Page size (number of icons). Last page may have less
``page_count``        Integer           Total pages count
====================  ================  ======================================================

**Data Object**

Data object contains array of Icon objects.

**Icon Object**

=================  ================  ===========================================================================
Property           Type              Description                                           
=================  ================  ===========================================================================
``id``             Integer           Icon ID
``title``          String            Icon title
``code``           String            Code that can be used when sending icon to LaMetric.
``type``           Enum              Type of the image – picture or movie.

                                     - ``picture`` – static png image
                                     - ``movie`` – static or animated gif                    
-----------------  ----------------  ---------------------------------------------------------------------------                
``url``            String            Direct URL to download icon that has size of 8x8 pixels.									
									 
                                     .. image:: https://developer.lametric.com/content/apps/icon_thumbs/34.png
                                     .. image:: https://developer.lametric.com/content/apps/icon_thumbs/2867.gif
``thumb``          Object            Object that contains URLs to preview images.
                                     
                                     ``original`` (45px x 45px)
                                     
                                     - .. image:: https://developer.lametric.com/content/apps/icon_thumbs/34_icon_thumb.png 
                                     
                                     ``small`` (40px x 40px)

                                     - .. image:: https://developer.lametric.com/content/apps/icon_thumbs/34_icon_thumb_sm.png 
                                     
                                     ``large`` (99px x 99px)

                                     - .. image:: https://developer.lametric.com/content/apps/icon_thumbs/34_icon_thumb_lg.png 
                                     
                                     ``xlarge`` (150px x 149px)

                                     - .. image:: https://developer.lametric.com/content/apps/icon_thumbs/34_icon_thumb_big.png 
=================  ================  ===========================================================================

Examples
^^^^^^^^

**Request**
::

	GET https://developer.lametric.com/api/v2/icons


**Response**
::

	200 OK	

	{
	  "meta": {
	    "total_icon_count": 2676,
	    "page": 0,
	    "page_size": 2676,
	    "page_count": 1
	  },
	  "data": [
	    {
	      "id": 1,
	      "title": "Button Error",
	      "code": "a1",
	      "type": "movie",
	      "category": null,
	      "url": "https://developer.lametric.com/content/apps/icon_thumbs/1.gif",
	      "thumb": {
	        "original": "https://developer.lametric.com/content/apps/icon_thumbs/1_icon_thumb.gif",
	        "small": "https://developer.lametric.com/content/apps/icon_thumbs/1_icon_thumb_sm.png",
	        "large": "https://developer.lametric.com/content/apps/icon_thumbs/1_icon_thumb_lg.png",
	        "xlarge": "https://developer.lametric.com/content/apps/icon_thumbs/1_icon_thumb_big.png"
	      }
	    },
	    {
	      "id": 2,
	      "title": "Button Success",
	      "code": "i2",
	      "type": "picture",
	      "category": null,
	      "url": "https://developer.lametric.com/content/apps/icon_thumbs/2.png",
	      "thumb": {
	        "original": "https://developer.lametric.com/content/apps/icon_thumbs/2_icon_thumb.png",
	        "small": "https://developer.lametric.com/content/apps/icon_thumbs/2_icon_thumb_sm.png",
	        "large": "https://developer.lametric.com/content/apps/icon_thumbs/2_icon_thumb_lg.png",
	        "xlarge": "https://developer.lametric.com/content/apps/icon_thumbs/2_icon_thumb_big.png"
	      }
	    },
	    
	    // Result is truncated
	 ]
	}


**Request**
::

	GET https://developer.lametric.com/api/v2/icons?page=1&page_size=2&fields=id,title,url&order=newest

**Response**
::
	200 OK

	{
	  "meta": {
	    "total_icon_count": 2676,
	    "page": 1,
	    "page_size": 2,
	    "page_count": 1338
	  },
	  "data": [
	    {
	      "id": 2959,
	      "title": "JulienBreux - CPU",
	      "url": "https://developer.lametric.com/content/apps/icon_thumbs/2959.png"
	    },
	    {
	      "id": 2957,
	      "title": "JulienBreux - Memory",
	      "url": "https://developer.lametric.com/content/apps/icon_thumbs/2957.png"
	    }
	  ]
	}

----