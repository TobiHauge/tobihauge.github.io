---
layout: post
title:  "Being stupid is an art, and i excel at it."
date:   2025-05-02 10:53:41 +0200
categories: dumb shit
permalink: /stupid
---
Being stupid can manifest in many ways.  
And most of the time I would be against using the word stupid.
Just because you're bad at math(*I know you are*) doesn't mean you're stupid.

On the other hand ignoring good advice and common practice can be stupid. Something that also is stupid is writing som 4 billion if statements to check if a number is odd or even.  
Everybody knows that switch cases are minimally faster.  
So in the name of good optimisation the only good option is to write 4 billion cases.

**For optimisation!!!**

But for a start let's begin with making the 4 billion if statents. We have to know what we're optimising. Because I don't hate myself that much, I'm gonna make a script to write it for me, because let's be honest i only write at 48wpm, so it would take more time than I have to procrastinate my german exam.  
![48 words per minute](images/48wpm.png)  
Because I dont want to save to much time though I will be using python3, that way we'll still wast tons of time.
After thinking it thoroughly over, I have decided to keep these tests at 16bit, so only 65535 *sad*. My pc would kill if I did more.

{% highlight python %}
print("#include <stdio.h>")
print("int main() {")
print("int a;")
print('scanf("%d", &a);')
i = 0
while i < 2**16-1:
    print("if (a == "+str(i)+") {")
    if not i%2:
        print('printf("even");')
    else:
        print('printf("odd");')
    i += 1
    print("}")
print("}")
{% endhighlight %}

Now that gives us a nice 196611 lines long c file, ripe for compilation.  
Some keen eyed people may have noticed, "Wait doesn't the python script need to figure out which numbers are even and odd". *shh* it's using magic, like all optimised code.

Throwing our small c file through everyone favourite gcc gives us a nice executable, only thing left is to test it.  
And.  
It's suprisingly fast, well that wasn't supposed to happen. Now all the incoming optisation will seem pointless. No think about all the jobs those few microseconds will buy us.

Now to be fair this huge chunk of if statement can be optimised further, thats right the humble **else if** but worry not, that change won't be to hard.

With the code rewritten to implement else if statements we're ready to compile and gain huge optimisation benefits. Wait what, pitiful. Neither GCC nor MSVC can handle all this beautiful code. The only solution is to down scale again down to 8bit only 255 number. *Pitiful.*

{% highlight python %}
print("#include <stdio.h>")
print("int main() {")
print("int a;")
print('scanf("%d", &a);')
print('if (a == 0) {\nprintf("even");\n}')
i = 1
while i < 2**8:
    print("else if (a == "+str(i)+") {")
    if not i%2:
        print('printf("even");')
    else:
        print('printf("odd");')
    i += 1
    print("}")
print("}")
{% endhighlight %}

Now MSVC will finaly compile this file, sadly though this file only goes up to 255.  
As exepected this gile is still fast. Ofcourse it's also smaller, but still in theory it's more optimal.

Now we only have the last level of optimisation to go, the perfect c code **switch** statements.

{% highlight python %}
print("#include <stdio.h>")
print("int main() {")
print("int a;")
print('scanf("%d", &a);')
i = 0
print('switch(a) {')
while i < 2**8:
    print("case "+str(i)+":")
    if not i%2:
        print('printf("even");')
    else:
        print('printf("odd");')
    print("break;")
    i += 1
print("}")
print("}")
{% endhighlight %}

It's glorius, never has more beautiful c code graced MSVC(actually most code is better but bear with me). It's quick and optimal. Although theres no difference to the naked eye, it's hopefully miliseconds faster and thats all that matters. After this there is only one thing more optimal. The thing carrying the scripts all along, the modulo operator.

{% highlight c %}
#include <stdio.h>

int main() {
    int a;

    scanf("%d", &a);

    if (a%2 == 0) {
        printf("even");
    } else {
        printf("false");
    }
}
{% endhighlight %}

Free from the shackles of if statements this code will work on any number that your small processor can work with. Still somehow I prefer all the big un optimised messes that we've made, they feel deifferent, more beautiful in an ugly way.

Goodbye