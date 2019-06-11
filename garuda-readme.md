## Some tips when working with Slate

1. You can just follow the instructions on the official slate `README.md` to set up the project. Pretty simple to set up.
> TODO: If we are going to host on github as a fork, to add detailed instructions on how to clone and run the project locally.

2. To add more sections to the API, add a new `.md` (Markdown) file in the `/source/includes` directory. Remember to reference the file at the top of the `index.html.md` file, under `include`. The order in which you specify the files under `include` is the order that they will be added. Slate currently does not support nested include, i.e. adding a `include` in one of the "sub-files", so the order in which the files are included in `index.html.md` is important.

3. Code snippets are automatically added to the right column of the page. To add a code snippet in the middle column, you have to add a `<div class="center-column"></div>` before the snippet:

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

4. To ensure that the middle and right columns line up correctly in a readable manner, you need to add `<div></div>` after each section. 