# Testing issues with file_get_contents in PhpUnit

I've recently been making some big changes to [Ticketlab](https://ticketlab.co.uk) and moving to a new domain (more on that later). 

This involved a major rebuild of the event pages in Laravel (the old event pages are using Code Igniter). This was done with special attention paid to SEO (rich snippets) and page speed.

To get enhanced page load, some of the CSS was inlined by creating a custom Blade directive added to the AppServiceProvider:

```
Blade::directive('embedStyles', function ($expression) {  
    return "<style><?php echo file_get_contents($expression); ?></style>";  
});
```

`file_get_contents` doesn't play nicely with PhpUnit for testing it would seem - the file structure is inaccessible when the tests are being run from the console.

In order to resolve this, I've made the directive code conditional on the environment:

```
Blade::directive('embedStyles', function ($expression) {  
    // if testing, file_get_contents doesn't work - and we don't need inline styles anyway  
    if (app()->environment('testing')) {  
        return "<style><?php echo $expression; ?></style>";  
    }  
  
    return "<style><?php echo file_get_contents($expression); ?></style>";  
});
```

An alternative (perhaps more prudent long-term) approach would be to create a service that executes `file_get_contents` but that could be mocked at test level... but I can revisit it if I run into this situation multiple times.