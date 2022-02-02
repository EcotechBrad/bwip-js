//copied fron ZlibPNG and modified to return an ImageData Object
function DrawingImageData(opts) {
    var image_buffer, image_width, image_height;
    // Provide our specializations for the builtin drawing
    var drawing = DrawingBuiltin(opts);
    drawing.image = image;
    drawing.end = end;
    return drawing;

    // Called by DrawingBuiltin.init() to get the RGBA image data for rendering.
    function image(width, height) {
        // PNG RGBA buffers are prefixed with a one-byte filter type
        image_buffer = Buffer.alloc ? Buffer.alloc(width * height * 4) :
            new Buffer(width * height * 4);
        image_width = width;
        image_height = height;
        console.log(image_height);
        console.log(image_width);
        // Set background 
        if (/^[0-9a-fA-F]{6}$/.test('' + opts.backgroundcolor)) {
            var rgb = opts.backgroundcolor;
            fillRGB(parseInt(rgb.substr(0, 2), 16),
                parseInt(rgb.substr(2, 2), 16),
                parseInt(rgb.substr(4, 2), 16));
        }
        return { buffer: image_buffer };
    }

    function fillRGB(r, g, b) {
        var color = ((r << 24) | (g << 16) | (b << 8) | 0xff) >>> 0;

        // This is made complex by the filter byte that prefixes each row...
        var len = image_width * 4 + 1;
        var row = Buffer.alloc ? Buffer.alloc(len) : new Buffer(len);
        for (var i = 1; i < len; i += 4) {
            row.writeUInt32BE(color, i);
        }
        image_buffer.fill(row);
    }

    function end() {
        return new ImageData(new Uint8ClampedArray(image_buffer), image_width, image_height)
    }
}
