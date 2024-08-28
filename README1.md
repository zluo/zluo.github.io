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
    xxxx.github.io
```

6.  Run 
```
    bundle exec jekyll serve --livereload
```

6.  Look for the site at port 4000 
```
    http://127.0.0.1:4000/
```

7. Troubleshooting Permission Deny
```
cd /src/lab/github_pages/zluo.github.io
sudo rm -r _site
sudo rm -r .jelly_cache
```
### Jupyter Notebook Plugin

Jekyll Jupyter Notebook plugin adds Jupyter Notebook support to Jekyll. You can embed Jupyter Notebooks into your texts.

#### github: [Jekyll-juypter-notebook](https://github.com/red-data-tools/jekyll-jupyter-notebook)
   
#### Install

Add the following line to your site's Gemfile:
```ruby
gem "jekyll-jupyter-notebook"
```

Run the following command line to make the gem available:

```bash
% bundle install
```

Add the following line to your site's _config.yml:
```yaml
plugins:
  - jekyll-jupyter-notebook
```

Usage

Put a Jupyter Notebook (sample.ipynb) to the directory that has the target text (my-text.md) like the following:
```
.
|-- my-text.md
`-- sample.ipynb
```
Put the following tag into the target text:
```python
{% jupyter_notebook "sample.ipynb" %}
```

