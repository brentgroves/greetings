# greetings
<!-- https://go.dev/doc/tutorial/create-module -->
git@github.com:brentgroves/greetings.git
brentgroves/greetings

# publish
pushd ~/src/greetings
git clone git@github.com:brentgroves/greetings.git
https://go.dev/doc/modules/managing-dependencies#naming_module
go mod init brentgroves/greetings
The go mod init command creates a go.mod file to track your code's dependencies. So far, the file includes only the name of your module and the Go version your code supports. But as you add dependencies, the go.mod file will list the versions your code depends on. This keeps builds reproducible and gives you direct control over which module versions to use.
In your text editor, create a file in which to write your code and call it greetings.go.
Paste the following code into your greetings.go file and save the file.
package greetings

import "fmt"

// Hello returns a greeting for the named person.
func Hello(name string) string {
    // Return a greeting that embeds the name in a message.
    message := fmt.Sprintf("Hi, %v. Welcome!", name)
    return message
}

This is the first code for your module. It returns a greeting to any caller that asks for one. You'll write code that calls this function in the next step.

In this code, you:

Declare a greetings package to collect related functions.
Implement a Hello function to return the greeting.
This function takes a name parameter whose type is string. The function also returns a string. In Go, a function whose name starts with a capital letter can be called by a function not in the same package. This is known in Go as an exported name. For more about exported names, see Exported names in the Go tour.

Declare a message variable to hold your greeting.
In Go, the := operator is a shortcut for declaring and initializing a variable in one line (Go uses the value on the right to determine the variable's type). Taking the long way, you might have written this as:

var message string
message = fmt.Sprintf("Hi, %v. Welcome!", name)
Use the fmt package's Sprintf function to create a greeting message. The first argument is a format string, and Sprintf substitutes the name
parameter's value for the %v format verb. Inserting the value of the name parameter completes the greeting text.
Return the formatted greeting text to the caller.

https://go.dev/doc/tutorial/call-module-code

Call your code from another module
In the previous section, you created a greetings module. In this section, you'll write code to make calls to the Hello function in the module you just wrote. You'll write code you can execute as an application, and which calls code in the greetings module.

Note: This topic is part of a multi-part tutorial that begins with Create a Go module.
Create a hello directory for your Go module source code. This is where you'll write your caller.
After you create this directory, you should have both a hello and a greetings directory at the same level in the hierarchy, like so:
cd ~/src
git clone git@github.com:brentgroves/hello.git
cd hello
<home>/
 |-- greetings/
 |-- hello/
For example, if your command prompt is in the greetings directory, you could use the following commands:

Enable dependency tracking for the code you're about to write.
To enable dependency tracking for your code, run the go mod init command, giving it the name of the module your code will be in.

For the purposes of this tutorial, use example.com/hello for the module path.

$ go mod init brentgroves/hello
go: creating new go.mod: module brentgroves/hello
In your text editor, in the hello directory, create a file in which to write your code and call it hello.go.
Write code to call the Hello function, then print the function's return value.
To do that, paste the following code into hello.go.

package main

import (
    "fmt"

    "example.com/greetings"
)

func main() {
    // Get a greeting message and print it.
    message := greetings.Hello("Gladys")
    fmt.Println(message)
}
!!!!!!!!!!!!!!!!!!!!!!!!!
Next publish the greetings module and/or finish the tutorial
https://go.dev/doc/tutorial/call-module-code

go mod tidy
$ git commit -m "mymodule: changes for v0.1.0"
$ git tag v0.1.0
Push the new tag to the origin repository.

$ git push origin v0.1.0
Make the module available by running the go list command to prompt Go to update its index of modules with information about the module you’re publishing.
