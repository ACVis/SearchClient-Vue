<template>
  <div class="about container mx-auto">
    <h1 class="mt-3 text-2xl font-semibold">Development Todo List and Self-Evaluation</h1>
    <pre class="align-left">
#TODOs#

[x] Setup basic config
[x] Create desktop prototype
[ ] Create mobile prototype
[x] Integrate endpoint
    [x] List results
    [x] Add pagination
[x] Flesh out styling

[ ] Review accessibility
[ ] Review basic security
[ ] Review performance

#Stretch Goals#

[x] Add sort
[ ] Highlight search term(s) in results
[ ] Clear/Refresh button
[ ] Click on Excerpt and have it unfold into bigger excerpt. Maybe scrollable?
[ ] Add first-search transition/animation

#Things I like#

-The color scheme
-Clear and simple layout
-The little animations are nice - small things.
-Overall, I think it's great; functional.

#Things I Would Improve#

-It's not easy to preview, due to the server's CORS settings, it has to be installed as a project
-The site needs the eye and feedback of more than one person
-Add ability to change number of results per page
-I could add the real reason logo
-Improve fonts
-I would finish my todos, especially as far as the Reviews. 
-The site is not really meant for mobile, but there's no reason it can't be.
-More sorting options
-Add filtering
-I'd consider adding a more impressive landing, with animations.
-Not sure I'm sold on the way I left aligned the results with the images. A "No Image" placeholder may have been better.
-The solution for result size is not bulletproof. The images height is tied to the text content height, which is tied to the length of text. 
I limit the length through truncation, but it's not perfect. When everything is long, there's ellipses everywhere. I'd probably have to style/layout 
differently or do more work on the css and structure.
-There's a lot of things I could do to make the project more developer friendly. 
    - Normally, I extract more things into utilities and common functionality and then centralize, organize, and reuse. 
    I did that some, but not as much as I'd like.
    - The css is made quickly, to just work. It's not as systematic and organized as I would like.
    However, I do think it is appropriate to the project length and scope.

-Alexander Caldwell
    </pre>
  </div>
</template>
