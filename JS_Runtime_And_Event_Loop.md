# JavaScript at runtime

Unlike other programming languages, JavaScript is a **single-threaded** langauge at runtime.
It means, when you open a website in the browser, it uses a single JavaScript execution thread. That thread is responsible to handle everything, like scrolling the web page, printing something on the web page, listen to DOM events (*like when the user clicks a button*), and doing other things. 

That means the code execution will be done one piece at a time. Since code execution is done sequentially, any code that takes a long time to execute will block anything that needs to be executed after that.

You can see that in action using below eternal `while` loop.

```javascript
while(true){}
```

Any code after the above statement won’t be executed as the while loop will loop infinitely until system is out of resources. This can also happen in an infinitely **recursive function call**.

Thanks to modern browsers, as not all open browser tabs rely on single JavaScript thread. Instead, they use separate JavaScript thread **per tab** or **per domain**. 

That will only freeze the current tab where that code was executed but other tabs will function normally. 

To visualize, how JavaScript executes a program, we need to understand JavaScript runtime and different components that play a part in it. So lets write a simple JavaScript program to visualize this.

<script src="https://gist.github.com/thatisuday/7d2432656da8d66e3226e3bb75d963f1.js"></script>

