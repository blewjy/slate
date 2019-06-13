## How to work with this repo

We will use this repo only for development. This means that this repo will not be hosted as a github-page or a website made available to the public. Instead, after making changes to this repo, you should build the slate website and then copy the generated source files into the plex-web-api repo, then use those generated source files to display on github-pages.

> TODO: this dev repo should be hosted in bitbucket ideally. then garuda developers will pull this repo from bitbucket onto their local, and also pull a copy of the plex-web-api from github onto their local. they will make whatever changes they need in this repo, and then we should provide a script that helps to copy the built files into plex-web-api folder on their local. running `jekyll serve` on the plex-web-api repo should then show the updated changes.

### Instructions

1. Clone this repo on to your local machine. Then you can just follow the instructions on the official slate `README.md` to set up the project. Pretty simple to set up.
> TODO: More detailed instructions please.

2. To add more sections to the API, add a new `.md` (Markdown) file in the `/source/includes` directory. Remember to reference the file at the top of the `index.html.md` file, under `include`. The order in which you specify the files under `include` is the order that they will be added. Slate currently does not support nested include, i.e. adding a `include` in one of the "sub-files", so the order in which the files are included in `index.html.md` is important.

3. To edit **content only**, you should only edit the markdown files in `/source/includes` and the main `index.html.md` file. The rest of the files do not modify content in any way.

4. If you wish to change the looks of the website, or mess around with the javascript, they are all located in `/layouts`, `/stylesheets`, and `/javascript`.

5. Once you are done making the changes, check if they look ok on your localhost first. 

```shell
bundle exec middleman server
```

This should serve the website on `localhost:4567`.

6. Once everything looks ok, build the project to generate the web source files.

```shell
bundle exec middleman build --clean
```

Running this command creates a `build` folder that contains all the source files that you will need to generate the static website. These files simply have to be copied over to plex-web-api and it should be able to display what you need.
> TOOD: write a script for this maybe?

## Some tips for working with Slate

1. Code snippets are automatically added to the right column of the page. To add a code snippet in the middle column, you have to add a `<div class="center-column"></div>` before the snippet:

```
<div class="center-column"></div>
```json
{
    "first_name": "John",
    "last_name": "Smith"
}
```
```
  
This was referenced from (this issue)[https://github.com/lord/slate/issues/855]. This is done in `flight_plans.md`.

2. To ensure that the middle and right columns line up correctly in a readable manner, you need to add `<div></div>` after each section. 