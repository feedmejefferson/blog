---
layout: post
author: dscheffy
title: Fun with Data
custom_css: pca-scatter
date: 2018-02-17 11:54 +0700
categories: data
---

The site's been up and running for almost a month now, and those of you actually paying attention may have noticed that nothing much has really changed (aside from us adding some more pictures to the random wheel of food).

So what have we been up to in the interim? Well, aside from leaving India, getting settled in Thailand and taking some Thai massage courses, mostly I've just been playing around with the data that we've started to collect. 

We have a separate [project on github](https://github.com/feedmejefferson/feedme-data) just for keeping track of our data science/analytics work. It's not particularly well organized at the moment -- there are a few R scripts and notebooks just sitting around in the root folder that I put together to parse and analyze the site's access logs. I'd like to find an easy way to publish the output of some of those notebooks here as blog posts, but I'd also like to create a separate section with automatically update dashboard statistics. Work for another day. 

## Food Similarity

The last thing that I did work on the week before last (before we took a break to focus on our Thai massage classes) was an interactive graph that lets me (and anybody else) visualize the output of my [collaborative filtering work](https://github.com/feedmejefferson/feedme-data/blob/master/pca.Rmd). Basically I've been trying out some different approaches to map out food similarity based on who clicks on what when. 

One approach projects every image of food onto a multidimensional space. The problem with multidimensional spaces is that we have a hard time _seeing_ them -- particularly on a two dimensional screen. 

The graph below at least makes it quick and easy for me to select and look at two of those dimensions at a time. 

<div id="pca-scatter"></div>
<script src="https://d3js.org/d3.v3.min.js"></script>
<script src="/blog/scripts/pca-scatter.js"></script>

The scatter plot defaults to the first two dimensions that principal component analisys found to be the greatest dimensions of differentiation. If two points are close together on this plot, they're probably more similar than two points that are far apart. 

The problem is, they're just points -- it would be really nice if you could see the image that each point refers to. If you hover over any point, you should see a thumbnail for the image that it refers to show up to the right of the plot. 

While two points may look close together on this projection, you have to remember that these are not just points in a two dimensional space -- if you rotate the projection by 90 degrees, you may find that those two points that looked close are actually far apart. That's where the `X1` through `X10` links come into play -- click on one and you'll see the scatter plot rotate from the old dimension that was displayed on that axis to the new one that you've selected. 

## New Images and Food Popularity

Aside from the interactive dimension selector, I've tried to communicate two additional sets of information with size and color. We've added new images over time (and removed some old ones). We don't expect that to stop any time soon (or ever), so it would be nice to see which of the points in the scatter plot are newer and haven't been shown as frequently (because it means we have less feedback information for them).

It would also be nice to see at a glance if there's any obvious relation between the various dimensions and overall food popularity -- which foods get clicked more and which get clicked less. The size of each point is based on the number of times that image has been chosen (relative to the number of times it was shown). I've also included `S` (shown), `C` (clicked) and `U` (unclicked) as dimensions that you can select on each of the axes.

It's not necessarily the most polished user interface, but it was a learning experience for me (getting to know [D3.js](https://d3js.org/) has been on my todo list for a few years now) and it makes it a little easier to show what I've been doing!

## Next Steps

We have another week of Thai massage classes to go, so don't expect to see much of a change before then, but my next priority is to incorporate some of this back into the site itself. 

Right now, the images that we show are still completely random (or to be more technical, selected uniformly randomly from the full pool of available images each time).

I'm not ready yet to implement and deploy a fully dynamic model that tries to use the food map to progressively show you images that you think are more likely what you want, but I would like to add some automated dynamic feedback into the site. In particular, it would be nice to prioritize images that haven't been shown as much so that newer images would quickly catch up to older images. It's a simple enough feature that would force us to implement a basic data feedback pipeline.

We'll just have to see what we can get done in the few days between finishing our massage classes and leaving Thailand. 