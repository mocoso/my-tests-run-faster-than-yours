<!SLIDE >
# How?

<!SLIDE >
# Forks

Creating copies of processes

<!SLIDE >
# Speculative execution

> "...do work _before_ it is known whether that work will be needed at
> all, so as to prevent a delay that would have to be incurred by doing
> the work _after_ it is known whether it is needed"

<!SLIDE >

# Zeus

Written by Burke Libbey of Shopify

Manages pool of slaves which have preloaded parts of your app and
speculatively replaces them when your code changes.

(demo)

.notes show zeus start

<!SLIDE >
# Preloading

    @@@ ruby
    class Zeus::Rails < Zeus::Plan
      ...
      def default_bundle
        Bundler.require(:default)
      end

      def development_environment
        Bundler.require(:development)
        ::Rails.env = ENV['RAILS_ENV'] = "development"
        require APP_PATH
        ::Rails.application.require_environment!
      end
      ...
    end

<!SLIDE >

# Keeping fresh

Slaves are replaced when any ruby file they have loaded is changed 

.notes Monkey patches Kernel#load and YAML#load\_file and reports back to master which watches these files

<!SLIDE >
# More than just testing

    @@@ sh
    $ zeus console
    $ zeus rake
    $ zeus server
    ... 

<!SLIDE bullets >
# Requirements

* Large ruby application
* Ruby 1.9.3

<!SLIDE >
# How do I get the goodness?

Inside your rails project directory:

    @@@ sh
    $ gem install zeus
    $ zeus init
    $ zeus start

And feel the lightning speed.

.notes Remind no need to change your codebase

<!SLIDE bullets incremental>

# Drawbacks of Zeus

* Not (all) written in Ruby
* Immature

.notes 0.0.1 release in July this year
