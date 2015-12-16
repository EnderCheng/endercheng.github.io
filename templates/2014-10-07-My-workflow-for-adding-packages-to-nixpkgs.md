---
layout: minimal_post
title: My workflow for adding packages to nixpkgs
published: true 
comments: true
introduction: I use NixOS, therefore it is necessary to know how to add packages to the main nixpkgs repository, locally or by pushing your changes.
---

Here I will be using the addition of [GEANT4](http://geant4.org/) to [nixpkgs](https://github.com/NixOS/nixpkgs) as an example.
First checkout the main repository:

    git clone https://github.com/NixOS/nixpkgs.git
    cd nixpkgs

$$\sum_{i=1}^n a_i=0$$
$$f(x)=x^{x^x}$$

{% highlight c %}
/* hello world demo */
#include <stdio.h>
int main(int argc, char **argv)
{
    printf("Hello, World!\n");
    return 0;
}
{% endhighlight %}

If you think you need to add a package, make sure you actually do first by searching for it in the repository:

    grep -Rsin geant pkgs/

Ok. It is not there, so the first thing we need to do is make a new branch, and add it in a sensible place.

    git branch geant4
    git checkout geant4

Lets choose `development/libraries/` and add a new category called `physics`, and a sub directory called `geant4`.

    mkdir -p pkgs/development/libraries/physics/geant4/

In this directory we will add our nix expression for GEANT4:

    touch pkgs/development/libraries/physics/geant4/default.nix

This expression will contain everything needed to build the software.
More on that in a later post.
Once you have made your changes you can test your expression by attempting to build the package:

    nix-build -A geant4

Or drop into a shell and play around:

    nix-shell -A geant4
    $> cd /tmp
    $> unpackPhase
    $> cd <source dir>
    $> cmakeConfigurePhase
    $> buildPhase
    $> exit

If it is all working as you expect, and the package builds correctly you can commit your changes:

    git add pkgs/development/libraries/physics/geant4/<files>
    git commit -m "Added geant4."

Finally, you can push this branch to your forked repository on github, and open a pull request:

    git push -u origin geant4

Here is the original [pull request for adding GEANT4 to nixpkgs](https://github.com/NixOS/nixpkgs/pull/3963).

