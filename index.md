---
title: About GRID
feature_text: |
  ## GRID: Geographic Reconnaissance for Infrastructure Detection
  An interface developed by UC San Diego Data Science students that detects San Diego Gas & Electric power poles through satellite imagery utilizing machine learning image recognition.
feature_image: "assets/cover_photo_1.jpg"
excerpt: "Alembic is a starting point for [Jekyll](https://jekyllrb.com/) projects. Rather than starting from scratch, this boilerplate is designed to get the ball rolling immediately. Install it, configure it, tweak it, push it."
---

Alembic is a starting point for [Jekyll](https://jekyllrb.com/) projects. Rather than starting from scratch, this boilerplate is designed to get rolling immediately. Install it, configure it, tweak it, push it.

## Introduction

Energy companies, like San Diego Gas & Electric, have the responsibility of ensuring that power is reliably and safely distributed. With Southern California being a historically fire prone region, it is even more essential that the utility company maintains its grid and minimizes the risk of fires caused by it's equipment. SDG&E alone has thousands of miles of power lines supplying energy to millions of customers in its service territory that spans the San Diego and southern Orange counties. This makes the task of monitoring and maintaining utility equipment imperative not only for consistent electrical delivery, but for the safety of human lives and property.

This project seeks to develop a tool using satellite imagery and object detection to assist in this task, providing SDG&E with up-to-date and accurate imagery of their equipment and allowing them to identify potential risks on or around the equipment and make informed decisions based on the state of their utilities.

### Fire Risk Posed By Electrical Utility Structures

- Available as a **theme gem** and **GitHub Pages** theme
- Clear and elegant design that can be used out of the box or as solid starting point
- Tested in all major browsers, including **IE and Edge**
- Built in **Service Worker** so it can work offline and on slow connections
- **Configurable colours** and typography in a single settings file
- Extensive set of **shortcodes** to include various elements; such as buttons, icons, figure images and more
- Solid **typographic framework** from [Sassline](https://sassline.com/)
- Configurable navigation via a single file
- Modular Jekyll components
- Post category support in the form of a single post index page grouped by category
- Built in live search using JavaScript
- **Contact form** built in using [Formspree](https://formspree.io/)
- Designed with **[Siteleaf](https://www.siteleaf.com/)** in mind
- Has 9 of the most popular networks as performant sharing buttons
- Has documentation

## Methodology

### Data Collection
In order to train an image recognition model that can identify electrical infrastructure from a satellite point of view, we collected image data of power line poles using the Google Static Maps API. This API is accessible and available for free up to a generous amount that is more than enough for the purpose of this project. With this, we were able to gather a significant number of images to use for our project. The API takes latitude and longitude coordinates as well as zoom to obtain the image data. The current training dataset consists of 101 satellite images around the San Diego area. Each image was then manually labeled using labeling tools, such as CVAT, and saved as a COCO json annotation file. When labeling, we made the decision to utilize the shadows of the poles as the primary identification point, so we ensure that the bounding boxes included not only the pole itself but also its visible shadow to improve the model’s detection ability.
### Model Training
The first model we used was Facebook’s DETR object detection model (DEtection TRansformer). This object detection framework, presented by Facebook AI at the European Conference on Computer Vision 2020 (ECCV), is simple but accurate, having efficient runtime performance. More information about this model can be found in their paper Carion et al. (2020). Using Facebook’s DETR model, we adapted it to incorporate our pole class, fine-tuning the model and training it with our image data. To train the model, the tagged image data was split into an 80/20 training and validation split and the model trained for 50 epochs. 

With further work, we plan to test other object detection models and compare their performances in identifying electric poles with the goal of identifying the most effective one. 
### Map Interface
For our user interface, we utilized Flask in order to create a website that would be able integrate our model with an interactive map. We embedded an interactive map using the Google Embed API, where users can navigate to any area and run our model in order to identify poles in the current view. Flask allowed us to integrate a script where PyTorch loaded our trained model and ran it on the current view.
![image](assets/interface_scrnshot.png "Map Interface Showing UCSD")

Here are a few examples of Alembic out in the wild being used in a variety of ways:

- [bawejakunal.github.io](https://bawejakunal.github.io/)
- [case2111.github.io](https://case2111.github.io/)
- [karateca.org](https://www.karateca.org/)

## Results

## Conclusion

### Quick setup

To give you a running start I've put together some starter kits that you can download, fork or even deploy immediately:

- ⚗️🍨 Vanilla Jekyll starter kit  
  [![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/daviddarnes/alembic-kit){:style="background: none"}
- ⚗️🌲 Forestry starter kit  
  [![Deploy to Forestry](https://assets.forestry.io/import-to-forestry.svg)](https://app.forestry.io/quick-start?repo=daviddarnes/alembic-forestry-kit&engine=jekyll){:style="background: none"}  
  [![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/daviddarnes/alembic-forestry-kit){:style="background: none"}
- ⚗️💠 Netlify CMS starter kit  
  [![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/daviddarnes/alembic-netlifycms-kit&stack=cms){:style="background: none"}

- ⚗️:octocat: GitHub Pages with remote theme kit  
  {% include button.html text="Download kit" link="https://github.com/daviddarnes/alembic-kit/archive/remote-theme.zip" color="#24292e" %}
- ⚗️🚀 Stackbit starter kit  
  [![Create with Stackbit](https://assets.stackbit.com/badge/create-with-stackbit.svg)](https://app.stackbit.com/create?theme=https://github.com/daviddarnes/alembic-stackbit-kit){:style="background: none"}

### As a Jekyll theme

1. Add `gem "alembic-jekyll-theme"` to your `Gemfile` to add the theme as a dependancy
2. Run the command `bundle install` in the root of project to install the theme and its dependancies
3. Add `theme: alembic-jekyll-theme` to your `_config.yml` file to set the site theme
4. Run `bundle exec jekyll serve` to build and serve your site
5. Done! Use the [configuration](#configuration) documentation and the example [`_config.yml`](https://github.com/daviddarnes/alembic/blob/master/_config.yml) file to set things like the navigation, contact form and social sharing buttons

### As a GitHub Pages remote theme

1. Add `gem "jekyll-remote-theme"` to your `Gemfile` to add the theme as a dependancy
2. Run the command `bundle install` in the root of project to install the jekyll remote theme gem as a dependancy
3. Add `jekyll-remote-theme` to the list of `plugins` in your `_config.yml` file
4. Add `remote_theme: daviddarnes/alembic@main` to your `_config.yml` file to set the site theme
5. Run `bundle exec jekyll serve` to build and serve your site
6. Done! Use the [configuration](#configuration) documentation and the example [`_config.yml`](https://github.com/daviddarnes/alembic/blob/master/_config.yml) file to set things like the navigation, contact form and social sharing buttons

### As a Boilerplate / Fork

_(deprecated, not recommended)_

1. [Fork the repo](https://github.com/daviddarnes/alembic#fork-destination-box)
2. Replace the `Gemfile` with one stating all the gems used in your project
3. Delete the following unnecessary files/folders: `.github`, `LICENSE`, `screenshot.png`, `CNAME` and `alembic-jekyll-theme.gemspec`
4. Run the command `bundle install` in the root of project to install the jekyll remote theme gem as a dependancy
5. Run `bundle exec jekyll serve` to build and serve your site
6. Done! Use the [configuration](#configuration) documentation and the example [`_config.yml`](https://github.com/daviddarnes/alembic/blob/master/_config.yml) file to set things like the navigation, contact form and social sharing buttons

## Customising

When using Alembic as a theme means you can take advantage of the file overriding method. This allows you to overwrite any file in this theme with your own custom file, by matching the file name and path. The most common example of this would be if you want to add your own styles or change the core style settings.

To add your own styles copy the [`styles.scss`](https://github.com/daviddarnes/alembic/blob/master/assets/styles.scss) into your own project with the same file path (`assets/styles.scss`). From there you can add your own styles, you can even optionally ignore the theme styles by removing the `@import "alembic";` line.

If you're looking to set your own colours and fonts you can overwrite them by matching the variable names from the [`_settings.scss`](https://github.com/daviddarnes/alembic/blob/master/_sass/_settings.scss) file in your own `styles.scss`, make sure to state them before the `@import "alembic";` line so they take effect. The settings are a mixture of custom variables and settings from [Sassline](https://medium.com/@jakegiltsoff/sassline-v2-0-e424b2881e7e) - follow the link to find out how to configure the typographic settings.
