BUILD_DIR=../app/images/tiles
ZOOMS=0 1 2 3 4 5 6
ZOOM_DIRS=$(patsubst %, $(BUILD_DIR)/%, $(ZOOMS))

all: $(ZOOM_DIRS)

# http://www.imagemagick.org/Usage/crop/#crop_tile
$(ZOOM_DIRS): $(BUILD_DIR)/%: squared-%.jpg
	mkdir -p $@
	convert $< -crop 256x256 -set filename:tile '%[fx:page.x/256]_%[fx:page.y/256]' +repage +adjoin $@/'foo_%[filename:tile].jpg'

D4.rgb.q95.jpg:
	wget https://s3.amazonaws.com/lsst-epo/testdata/D4.rgb.q95.jpg

squared-6.jpg: D4.rgb.q95.jpg
	convert D4.rgb.q95.jpg -crop 16384x16384+0+0 squared-6.jpg

squared-5.jpg: squared-6.jpg
	convert $< -resize 8192x8192 $@

squared-4.jpg: squared-5.jpg
	convert $< -resize 4096x4096 $@

squared-3.jpg: squared-4.jpg
	convert $< -resize 2048x2048 $@

squared-2.jpg: squared-3.jpg
	convert $< -resize 1024x1024 $@

squared-1.jpg: squared-2.jpg
	convert $< -resize 512x512 $@

squared-0.jpg: squared-1.jpg
	convert $< -resize 256x256 $@
