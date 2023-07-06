# Node.js CLI (Command Line Interface)

Node.js comes with a command-line interface, commonly referred to as the Node.js REPL (Read-Eval-Print-Loop). The REPL is an interactive environment that processes Node.js expressions. The environment gets its name from the way it reads input, evaluates the input, prints the result, and loops until closed. It's a quick way to test JavaScript and Node.js code.

### **1. Starting the REPL**

To start the REPL, open your terminal and type `node` without any arguments, then hit `Enter`. You should see a `>` prompt. Now you can start typing JavaScript code right in your terminal.

```bash
$ node
>
```

### **2. Using the REPL**

The REPL is interactive, which means you can type any JavaScript or Node.js command and see the result immediately. For example:

```bash
$ node
> 1 + 1
2
> console.log("Hello, Node.js!")
Hello, Node.js!
undefined
```

After you press `Enter`, the REPL evaluates the JavaScript expression and prints the result. `console.log()` returns `undefined`, which is why you see `undefined` after the message.

### **3. Exiting the REPL**

To exit the REPL, you can type `.exit` and hit `Enter`, or you can press `Ctrl + C` twice.

```bash
> .exit
$
```

### **4. Node.js Scripts from the CLI**

Apart from the REPL, you can use the CLI to run JavaScript files. If you have a file named `app.js`, you can run it using the `node` command followed by the filename:

```bash
$ node app.js
```

In summary, the Node.js CLI, whether it's used for the REPL or running scripts, is a powerful tool in your Node.js arsenal. It lets you execute JavaScript and Node.js code, test your functions, and run your scripts. The REPL, in particular, is a handy way to experiment with Node.js.
