# bash

[bashcrawl](https://gitlab.com/slackermedia/bashcrawl)

> Learn Linux commands by playing a simple text adventure.

## Scripts & Commands

[Writing a `bash` scripts like a pro](https://dev.to/unfor19/writing-bash-scripts-like-a-pro-part-1-styling-guide-4bin)

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

[Linux commands for optimizing web images](https://opensource.com/article/21/12/optimize-web-images-linux)
