# Lab Report 2: Servers and Bugs

## Part 1: `StringServer`

This is the code I used to implement the server:
<img width="1025" alt="image" src="lab2-screenshot3.png">

This is my first screenshot of the server running:
<img width="1025" alt="image" src="lab2-screenshot1.png">

Here, `StringServerHandler`'s `handleRequest` method is called. Its only relevant argument is the URL
`https://localhost:4000/add-message?s=This is the first message`, since it uses the URL to determine
what it needs to add to the meesage, and its only relevant field is `message`, since it uses it in order 
to keep track of what the output should be. `StringServerHandler` also changes `message` by appending to
it the message passed to the function through the URL `"This is the first message"`, followed by a new
line.

This is my second screenshot of the server running:
<img width="1025" alt="image" src="lab2-screenshot2.png">

Once again, `StringServerHandler`'s `handleRequest` method is called. Its only relevant argument is
the URL `https://localhost:4000/add-message?s=And this is the second message, appearing a line below the first`,
and its only relevant field is `message`. Both are relevant for the same reasons that they were relevant for
the first screenshot. Here, `StringServerHandler` also appends the message in the URL `"And this is the second message, 
appearing a line below the first"`, followed by a new line, to `message`. However, `message` was initially empty
in the first screenshot, in this screenshot, it is not empty, as it already contains the message from earlier.

