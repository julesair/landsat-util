Overview: What can landsat-util do?
====================================

Landsat-util has three main functions:

- **Search** for landsat tiles based on several search parameters.
- **Download** landsat images.
- **Image processing** and pan sharpening on landsat images.

These three functions have to be performed separately.

**Help**: Type ``landsat -h`` for detailed usage parameters.

Search
++++++

Search returns information about all landsat tiles that match your criteria.  This includes a link to an unprocessed preview of the tile.  The most important result is the tile's *sceneID*, which you will need to download the tile (see step 2 below).

Search for landsat tiles in a given geographical region, using any of the following:

- **Paths and rows**: If you know the paths and rows you want to search for.
- **Latidue and Longitude**: If you need the latitude and longitude of the point you want to search for.

Additionally filter your search using the following parameters:

- **Start and end dates** for when imagery was taken
- **Maximum percent cloud cover** (default is 20%)

**Examples of search**:

Search by path and row::

    $: landsat search --cloud 4 --start "january 1 2014" --end "january 10 2014" -p 009,045

Search by latitude and longitude::

    $: landsat search --lat 38.9004204 --lon -77.0237117


Download
++++++++

You can download tiles using their unique sceneID, which you get from landsat search.

Landsat-util will download a zip file that includes all the bands. You have the option of specifying the bands you want to down. In this case, landsat-util only downloads those bands if they are available online.

**Examples of download**:

Download images by their custom sceneID, which you get from landsat search::

    $: landsat download LC80090452014008LGN00

Download only band 4, 3 and 2 for a particular sceneID::

    $: landsat download LC80090452014008LGN00 --bands 432

Download multiple sceneIDs::

    $: landsat download LC80090452014008LGN00 LC80090452015008LGN00 LC80090452013008LGN00

Image processing
++++++++++++++++

You can process your downloaded tiles with our custom image processing algorithms.  In addition, you can choose to pansharpen your images and specify which bands to process.

**Examples of image processing**:

Process images that are already downloaded. Remember, the program accepts both zip files and unzipped folders::

    $: landsat process path/to/LC80090452014008LGN00.tar.bz

If unzipped::

    $: landsat process path/to/LC80090452014008LGN00

Specify bands 3, 5 and 1::

    $: landsat process path/to/LC80090452014008LGN00  --bands 351

Process *and* pansharpen a downloaded image::

    $: landsat process path/to/LC80090452014008LGN00.tar.bz --pansharpen
