I recently came across the need to style a child component based on the hover state of the parent component. 

At John Lewis, I work on the Product Listing Page (PLP), and we're experimenting with adding an image carousel to product listings to enrich search results.

Carousels are extremely fiddly beasts, and I've built a few over the years in various technologies including Flash and jQuery (because they were cool once, you know). For this one, we're using React and CSS snap-scroll.

Snap-scroll is a quite recent addition to the styling arsenal. It was created to solve this exact problem: if you have a number of images or full-width containers (slides, if you will), you can users to scroll between them but for scrolling to stop on any given slide. You can buy do this on the x or y axis (which gives the opportunity for some simple TikTok style scroll implementations if you're inclined) and the snapping can be set to either `mandatory` to always snap exactly on the nearest slide edge or `proximity` where the snapping only happens if you're close enough, but doesn't otherwise interfere with natural scrolling.

So, within our carousel we wanted to show some navigation buttons to go to the next and previous slides. This is triggered on hovering the product card, which ideally we can do in CSS quite simply: 
```
.ProductCard:hover .Carousel-button {
  display: block;
}
```

In React however, our Carousel is a child component of the ProductCard, so trying to add this style to our parent won't work, as it has no way to know the final compiled class name of the buttons in the carousel (React converts class names and appends characters to them to ensure they're unique, which means)