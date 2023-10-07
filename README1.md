## RUN GITHUB PAGE WITH JEKLLY IN DOCKER EVN NOTES


[BillRaymond/GitHub Pages Jekyll Dockerfile](https://gist.github.com/BillRaymond/db761d6b53dc4a237b095819d33c7332)


### Developing inside Visusal Code
#### Required plugins

1. Intstall Docker plugin
2. Install Docker Dev plugin

#### Build Docker 

1. get the DockerFile from 

    [BillRaymond/GitHub Pages Jekyll Dockerfile](https://gist.github.com/BillRaymond/db761d6b53dc4a237b095819d33c7332)

2. CRTL + SHIFT + p,  open folder in container

#### Install Jeklly in Docker

1. create file run-once.sh

2. CTRL + ` , open terminal

3. run run-once.sh

4. CRTL + SHIFT + p,  rebuild container 

5. config url in _config.yml
```
    zluo.github.io
```

6.  Run 
```
    bundle exec jekyll serve --livereload
```

6.  Look for the site at port 4000 
```
    http://127.0.0.1:4000/
```
