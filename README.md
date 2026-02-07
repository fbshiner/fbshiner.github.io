# Guide to Adding to the Site

## Photos

### Adding
Images for each category are stored in src > lib > assets, with each category being stored in its respective folder (e.g. knitting photos are stored in src > lib > assets > knitting)

### Linking
For each category (located in `src/routes/{category}`), there exists a file `data.js`, with entries like
    {
        "slug": "slug_name", // name at the end of the url e.g. fbshiner.github.io/knitting/slug_name
        "title": "Image Title",
        "src": "name_of_image_in_assets.jpg", // could always be png or jpeg, etc.
        "description": "Description"
    },

You can add new images in that format anywhere in the `data.js` file, just make sure there is a , before the { and after the }. You can check 
src/routes/knitting/data.js for an example of how this data is formatted in sequence.

## Text

For text within the pictures' individual pages, you can add descriptions through the description field for images `data.js` (noted above). For writing text on the home page, you can edit the lines in between `<div class="page">` and the final `</div>` in `+page.svelte` (or anywhere on that file if you want to make a change to style, JavaScript, etc.). Similarly, for edits to the text of each category page (but not the titles of photos, which you can edit in the respective `data.js` files listed above) in the `+page.svelte` files in each of those category page's folders (e.g. `src/routes/music/+page.svelte`).

You can also always ask me if you get stuck and I can help!