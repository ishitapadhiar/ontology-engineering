---
---

# Site Development Instructions

This page contains technical documentation useful for developing your project site.

The site is built using Jekyll, which primarily uses Markdown along with the Liquid template language.
Helpful documentation on Jekyll development can be found [here](https://jekyllrb.com).

If you have questions or are experiencing difficulties, please contact Sam:
stoufs2 at rpi dot edu or Shruthi: chari at rpi dot edu

## Project Repo Maintenance and Site Setup Instructions

When you are trying to add to the website template that you have setup for your individual projects, please follow these steps:

1. Each project has a dedicated github branch, which is titled . Note, the is a placeholder that you need to replace with your actual project name.
2. Please only checkout this branch onto your machine using "git checkout "
3. All your project files are under the oe2020/ folder. This will be your project repository, a folder that you will upload all your artefacts, and use for website rendering as well.
4. We have setup website templates for each of your projects, that are accessible at project specific URLS of the form: http://--rpi-ontology-engineering.netlify.app/
5. When you are editing the website for your assignments, you can edit the .md files that we have created for you in your project repositories.
6. Images can be added to the images/ folder in your project repository.
7. Files can be added to the files/ folder in your project repository.
8. We have examples on how you can embed files and images for preview on your project website. Please try and use these templates we have provided for you.

Also, the navigation bar of your project page is filled out by us, and if you want to edit this (e.g.:, to add options), please consult with course TA, Shruthi: charis@rpi.edu or Sam Stouffer, stoufs2@rpi.edu
Finally, should you have any questions: please check the course instructions page at: https://master--rpi-ontology-engineering.netlify.app/.

We have further instructions, on the technical implementation of this infrastructure below. Please read through for your understanding. 

## Preview a branch site on Netlify

The primary course site is hosted on GitHub Pages and is automatically built from the master branch.
The projects, however, cannot be hosted on GitHub Pages, which only allows hosting of a single branch.
Because of this, we will be hosting the branches using Netlify, a free cloud hosting service.

All branches of the GitHub repository will be built and hosted on Netlify at a url dependent upon the branch name.

The url for your branch will be https://*branch-name*--rpi-ontology-engineering.netlify.app/
where *branch-name* is the name of your branch.

Netlify will rebuild the site from your branch whenever you push new commits to the GitHub repo.
Allow several minutes for Netlify to rebuild the site from your changes.

## Preview a branch site on your own machine

Optionally, you can preview changes to your branch site without the hassle of pushing up a commit and waiting for Netlify
by building and serving the site on your own machine.

Follow the instructions [here](https://jekyllrb.com/docs/).
Skip the steps where you create a new site and change directory (just make sure you are in the `ontology-engineering` root directory when executing commands.)

## Ontology Hygiene

Every time you push commits to your branch, a continuous integration job will run ontology hygiene checks on your branch.
These checks will examine the ontologies in the repository and report errors if the ontologies do not conform to certain best practices.

The checks will pick up ontologies in files with extensions `.rdf`, `.ttl`, or `.jsonld`.
These files can be anywhere in the repository.

Resources in your ontology that do not contain `twc` in the namespace will not be checked.
This is done to prevent checking of imported ontologies.
*All of the resources for ontologies you develop must contain `twc` in the namespace.*

If the hygiene checks find errors in your ontologies, then the CI job will fail.
This will update the status of your latest commit to indicate that it did not pass checks.
*When submitting assignments, your ontologies must pass all hygiene checks.*

You can view details about the hygiene test runs on the project [CircleCI page](https://app.circleci.com/pipelines/github/tetherless-world/ontology-engineering).


## Nav Menu

The nav menu contains both static and configurable items.
The static items are specified in the html template in `_layouts/default.html`.
Course year specific items are configured via YAML files.

Each course year will have its own directory in `_data/years` e.g. the fall 2020 course is in `_data/years/2020`.
Each year specified in this way will be rendered as a nav link on the main menu.
Within the year directory is a `year.yml` file that contains the nav label and relative path for that course year.  Example `_data/years/2020/year.yml`:
```yaml
name: OE 2020
path: oe2020
```
{% assign main_nav_capt = "The main nav menu using example config" %}
![{{ main_nav_capt }}](main_nav_example.png)
<br>
*{{ main_nav_capt }}*

Also within the year directory is a `projects` directory containing a YAML file for each project of that year.
The YAML files in this directory will be used to populate a sub-menu of the year's projects that is visible when the user is on that year's page.
The sub-menu for the most recent year will be visible by default if the user is not on a year page.

Project YAML files are similar to the `year.yml` file in that they contain `name` and `path` fields to specify the nav label and relative path respectively.
In this case, the `path` is relative to the project's year.
Additionally there is a `pages` list that dictates the contents of the nav menu for the project page.
Each element of the `pages` list contains a `name` field and a `path` field, which is relative to the project page.

Example `_data/years/2020/projects/project1.yml`:
```yaml
name: Project One
path: project1
pages:
  - name: Sub Page
    path: sub_page
  - name: Other Page
    path: other_page
```

{% assign proj_nav_capt = "The project one page nav menu using example config" %}
![{{ proj_nav_capt }}](project_nav_example.png)
<br>
*{{ proj_nav_capt }}*