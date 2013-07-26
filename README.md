# xcode_template.rb

A ruby script to automate the generation of iOS Object code to align with backend ruby-on-rails Model(s).

Original Source by [jTribe][jt] with detailed description [here][blogpost]

[jttwitter]: https://twitter.com/jtribeapps
[jt]: http://www.jtribe.com.au
[blogpost]: http://www.jtribe.com.au/2011/04/automating-data-exchange-between-your-rails-backend-and-an-iphone-app/

## Introduction

xcode_template.rb generates the necessary .h and .m files for specific Rails Models for iOS development. For any Rails model (as long as it is subclassed from ActiveRecord::Base) that you need to expose to Objective-C…

* it will create your Objective-C declaration file (.h), with all the instance variables and properties correctly declared
* it will create your Objective-C implementation file (.m), including a custom initializer that accepts a dictionary (which you will get from any good JSON parser) and convert that into an instance of your model class
* lastly, it will also create an extension to your Rails model by defining the as_json helper method. By default this method will ensure that all your model’s attributes are serialised when the to_json helper is called on the object, but because it explicitly names all the attributes and how they should be serialised, it gives you full control over what goes over the wire, and what doesn’t

## Usage

1. Copy xcode_template.rb into your models folder
2. Temporarily subclass from the XcodeTemplate class you just added by changing the line `class User < ActiveRecord::Base` to `class User < XcodeTemplate`
3. Launch Rails Console
	* ruby script/console (anything below Rails 3.0)
	* rails console
4. To generate the files for xcode for your model (User in this case), type
	`User.xcode`

Thats it.

Remember to change your model file back to `class User < ActiveRecord::Base`.

## Credits
Full credits to [jtribe][jt]: twitter [@jtribeapps][jttwitter]

