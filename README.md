

# Problem from installing homebrew in user

If Gemfile included: Nokogiri, Mongoid or kaminari-mongoid (which might be dependency from some gems) otherwise may not have these errors.

## Why:

Because some of dependency files/gems were misplaced and not able to build

## Problem:

nokogiri ..'eof?': Is a directory

```

/Users/C79891A/.rbenv/versions/2.7.5/lib/ruby/gems/2.7.0/gems/nokogiri-1.12.5-x86_64-darwin/lib/nokogiri/xml/document.rb:372:in `eof?': Is a directory @ io_fillbuf - fd:14 /Users/C79891A/.rbenv/versions/2.7.5/share (Errno::EISDIR)


```
Example:

- An application that use both Nokogiri and Mongoid: [Jinda](https://github.com/kul1/jinda)
- Install Jinda in [simulated environment](#how-to-simulate-this-error:), then errors will appear as describled below


```
git clone https://github.com/kulprateep-experian/c269614.git
cd c269614
rails s

```
- if the environment setup as described below, rails app should run as expected in localhost:3000, otherwise it will have several errors when bundle to install needed gems below:


- Then please follow Problems/Solutions to fix those errors


---


## How to simulate this error:

- Mac OS, Big Sur 11.6.2
- No Admin previleges
- Use homebrew install in user directory

```

mkdir homebrew && curl -L https://github.com/Homebrew/brew/tarball/master |
tar xz --strip 1 -C homebrew

```

- Then add "export PATH=/Users/[username]/homebrew/bin:$PATH" to .zshrc

(for both zshrc or bash)


## Immediate errors: 

When bundle kaminari and kaminari-mongoid

```

mimemagic install error: "Could not find MIME type database in the following locations..."

```

## Solution:



First, create a file named freedesktop.org.xml.

Then copy the file [content](https://cgit.freedesktop.org/xdg/shared-mime-info/tree/freedesktop.org.xml.in?h=Release-1-9) found in this link and paste it into the file just created.

Finally, set the FREEDESKTOP_MIME_TYPES_PATH environment variable

Unix terminal:

```

export FREEDESKTOP_MIME_TYPES_PATH=/path/to/freedesktop.org.xml

```

## Problem (when kaminari-mongoid 1.0.1 build gem native extension)

```

Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

    current directory: /Users/C79891A/.rbenv/versions/2.6.9/lib/ruby/gems/2.6.0/gems/mimemagic-0.3.10/ext/mimemagic
/Users/C79891A/.rbenv/versions/2.6.9/bin/ruby -rrubygems /Users/C79891A/.rbenv/versions/2.6.9/lib/ruby/gems/2.6.0/gems/rake-13.0.6/exe/rake
RUBYARCHDIR\=/Users/C79891A/.rbenv/versions/2.6.9/lib/ruby/gems/2.6.0/extensions/x86_64-darwin-20/2.6.0/mimemagic-0.3.10
RUBYLIBDIR\=/Users/C79891A/.rbenv/versions/2.6.9/lib/ruby/gems/2.6.0/extensions/x86_64-darwin-20/2.6.0/mimemagic-0.3.10
rake aborted!
Could not find MIME type database in the following locations: ["/Users/C79891A/.rbenv/versions/2.6.9/freedesktop.org.xml",
"/usr/local/share/mime/packages/freedesktop.org.xml", "/opt/homebrew/share/mime/packages/freedesktop.org.xml",
"/opt/local/share/mime/packages/freedesktop.org.xml", "/usr/share/mime/packages/freedesktop.org.xml"]

Ensure you have either installed the shared-mime-info package for your distribution, or
obtain a version of freedesktop.org.xml and set FREEDESKTOP_MIME_TYPES_PATH to the location
of that file.

This gem might be installed as a dependency of some bigger package, such as rails, activestorage,
axlsx or cucumber. While most of these packages use the functionality of this gem, some gems have
included this gem by accident. Set USE_FREEDESKTOP_PLACEHOLDER=true if you are certain that you
do not need this gem, and wish to skip the inclusion of freedesktop.org.xml.

The FREEDESKTOP_PLACEHOLDER option is meant as a transitional feature, and will be deprecated in
the next release.


```

## Solution:

- Make sure:

    1. replace "C79891A" with your username

    2. replace "2.6.9" with proper version of ruby

    3. freedesktop.org.xml exist with it's [content](https://cgit.freedesktop.org/xdg/shared-mime-info/tree/freedesktop.org.xml.in?h=Release-1-9) 

    4. run below command:


```
    export FREEDESKTOP_MIME_TYPES_PATH=/Users/C79891A/.rbenv/versions/2.6.9/share/freedesktop.org.xml

```

- Install mememagic as instructed:

```
    gem install mimemagic

```

- Continue bundle or config command prior the error:


written by: prateep.kul@experian.com

