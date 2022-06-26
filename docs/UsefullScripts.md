# bash/shell

[bashcrawl](https://gitlab.com/slackermedia/bashcrawl)

> Learn Linux commands by playing a simple text adventure.

[Effective Shell](https://effective-shell.com/)

> This book is for anyone who is interested in computing, and wants to learn more about the exciting, but sometimes daunting world of The Shell. The shell is simple interface for working with computers and programs and learning some of its features can enormously increase your productivity as any computer user - whether a home user or hobbyist, programmer, data scientist, writer, administrator or other professional.
> 
> For the newcomer, you'll learn what a shell is, how to use it on your system, and then how to become more effective everyday by integrating the shell into your work. For the experienced professional, there is a wealth of detailed tips and tricks in each chapter that go into advanced topics and techniques to make you even more of a power user.


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
