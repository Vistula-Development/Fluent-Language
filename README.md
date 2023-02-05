![Fluent Logo (if you see this, something is very wrong.)](https://raw.githubusercontent.com/Vistula-Development/Fluent-Language/main/FLUENT%20LOGO.png)

Fluent is a programming language I am making because I want a programming language in this specific syntax. It's basically just a fucking combination of a bunch of features and will probably be buggy af.

# Example Fluent Code
```java
package com.example.fluentexample;

class FluentExample {
  
   entry Main(str[] args) {
      [[ 
         Combines all the strings in the args list            
         with the delimiter being a space 
      ]]
      str combinedArgs = args.combine(" ");

      [F-Strings, inspired by Python.]
      output(f"Args are {combinedArgs}");

      if(combinedArgs.contains("hello")) {
         output("You put hello in the arguments.", end="") [ Prints, but with no new line afterwards ]
         output("Thats so nice of you.") [Prints with normal settings]
         
      } else {
        output("You didn't put Hello, that's mean...")
      }

   }
   
   func SetMode(int mode) {
       switch(mode) {
	      case 1:
		    output("Set mode to Mode 1.")
		  case 2:
		    output("Set mode to Mode 2.")
		  case 3:
		    output("Set mode to Mode 3.")
		  otherwise: [ It is none of the above ]
			output("Mode should be 1 - 3.")
	   }
   }
   
   func LoopAmount(int times) {
      int counter = 0;
	  while (times != counter) {
	  	counter++;
	    output(f"{counter}/{times}")
	  }
   }
   
   func LoopAmount(int times, int interrupt) {
      int counter = 0;
	  while (times != counter) {
	  	counter++;
	    output(f"{counter}/{times}")
		if (counter == interrupt) {
			break [ Leaves the loop ]
		}
	  }
   }
   
   [[
	This function can be ran like:
	LoopAmount(100, 80, 30, 20) (ignores 80, 30 and 20)
	LoopAmount(100, 20) (ignores 20)
	LoopAmount(100) (Ignores none of them)
	
	... means the parameter is a list, but can be put as if it is multiple parameters
	Similar to Java.
   ]]
   
   func LoopAmount(int times, int... ignored) {
      int counter = 0;
	  while (times != counter) {
	  	 counter++;
	  	if (counter in ignored) { [[ Counter is in the ignored int list ]]
			continue [ Ignores this index ]
		}
	    output(f"{counter}/{times}")
	  }
   }
}

```

It will be converted to C# to become like this:
```c#
using System;
using System.Linq;
using System.Text;

namespace com.example.fluentexample
{
    class FluentExample
    {
        static void Main(string[] args)
        {
            // Combines all the strings in the args list with the delimiter being a space
            string combinedArgs = string.Join(" ", args);

            // F-Strings, inspired by Python
            Console.WriteLine($"Args are {combinedArgs}");

            if (combinedArgs.Contains("hello"))
            {
                Console.Write("You put hello in the arguments."); // Prints, but with no new line afterwards
                Console.WriteLine("That's so nice of you."); // Prints with normal settings
            }
            else
            {
                Console.WriteLine("You didn't put Hello, that's mean...");
            }
        }

        static void SetMode(int mode)
        {
            switch (mode)
            {
                case 1:
                    Console.WriteLine("Set mode to Mode 1.");
                    break;
                case 2:
                    Console.WriteLine("Set mode to Mode 2.");
                    break;
                case 3:
                    Console.WriteLine("Set mode to Mode 3.");
                    break;
                default: // It is none of the above
                    Console.WriteLine("Mode should be 1 - 3.");
                    break;
            }
        }

        static void LoopAmount(int times)
        {
            int counter = 0;
            while (times != counter)
            {
                counter++;
                Console.WriteLine($"{counter}/{times}");
            }
        }

        static void LoopAmount(int times, int interrupt)
        {
            int counter = 0;
            while (times != counter)
            {
                counter++;
                Console.WriteLine($"{counter}/{times}");
                if (counter == interrupt)
                {
                    break; // Leaves the loop
                }
            }
        }

        static void LoopAmount(int times, params int[] ignored)
        {
            int counter = 0;
            while (times != counter)
            {
                counter++;
                if (ignored.Contains(counter)) // Counter is in the ignored int list
                {
                    continue; // Ignores this index
                }
                Console.WriteLine($"{counter}/{times}");
            }
        }
    }
}
```
