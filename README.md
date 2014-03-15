mruby-iOS
=========

build_config.rb to cross-compile mruby for iOS applications. 

    # cd to your mruby src path
    cd ~/Downloads/mruby-1.0.0
    
    # Compile mrbuy with this build_config.rb
    MRUBY_CONFIG=(PATH_TO_CLONED_REPO)/build_config.rb ./minirake
    
    # Navigate to built libraries
    cd build
    
This should have generated build/iphone-sim, build/iphone-armv7 and build/iphone-armv7s directories. 
Copy the required libmruby.a from ./build/iphone-*/lib paths to your projects and enjoy. 
You only need build/iphone-sim/lib/libmruby.a if you're using the iOS simulator, don't forget 
to copy the headers from include/ path as well

RubyMotion
----------

To use mruby in a RubyMotion project, do the following:

1) Build mruby as explained above

2) Create a new directory `vendor/mruby` in your RubyMotion project

3) Copy `libmruby.a` from `build/iphone-sim/lib/libmruby.a` to the `vendor/mruby` directory

4) Copy everything inside `include/` dir to you `vendor/mruby` directory as well

5) Add the following line to your RubyMotion Rakefile
    
    app.vendor_project('vendor/mruby', :static)
    
6) Use mruby in your application. For example use this in your app_delegate.rb:

    mrb = Pointer.new(:object)
    mrb[0] = mrb_open()
    mrb_load_string(mrb[0], "class TestClass; end")
    puts mrb_class_defined(mrb[0], "TestClass") # Should output 1 in the console

7) Run `rake` and look at the console

