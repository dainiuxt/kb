# Scripts & Commands

Resize multiple graphic files from the command line:

```bash
sudo apt-get install imagemagick
mogrify -resize 640 *.jpg
```

Convert large jpg/png files into webp:

```bash
sudo apt-get install webp
cd /mywebapp/static/img/
mkdir webp        
for file in *.{jpg,png,jpeg}; do cwebp -q 60 ${file} -o webp/${file}.webp; done;
```
