# source 'http://rubygems.org'
source :rubygems
source :rubyforge
source :gemcutter

gem 'rails', '3.2.1'

gem 'dynamic_form'

# gem 'rubytree', '0.5.2', :require => 'tree'
gem 'rubytree', '0.7.0'
gem 'coderay'

gem "fastercsv", "~> 1.5.0", :platforms => [:mri_18, :jruby, :mingw_18]

# TODO rails-3.1: review the core changes to awesome_nested_set and decide on actions
gem 'awesome_nested_set'
## TODO rails-3.1: review the core changes to open_id_authentication and decide on actions
# gem 'open_id_authentication'

## TODO: cannot on Rails 3.1
# gem 'verification'

# gem 'ruby-prof', :git => 'http://github.com/wycats/ruby-prof.git'
gem 'ruby-prof'
# gem 'jquery-rails'
# gem 'prototype-rails', :git => "https://github.com/rails/prototype-rails.git"
gem 'prototype-rails'

gem 'therubyracer', :platforms => [:mri_18, :mri_19]

# Gems used only for assets and not required
# in production environments by default.
group :assets do
  gem 'sass-rails'
  gem 'coffee-rails'
  gem 'uglifier'
end

gem 'rails_autolink'

group :development do
  # gem 'thin'
  # gem 'autotest'
  # gem 'autotest-growl'
  # gem 'autotest-fsevent'
  # gem 'mynyml-redgreen'
  # gem 'rails-dev-tweaks', '~> 0.5.1'
  # gem 'rails-dev-tweaks'
end

group :production do
end

group :test do
  gem 'test-unit'
  # gem 'shoulda', :git => 'http://github.com/redox/shoulda', :branch => 'rails3'
  gem 'shoulda'
  gem 'mocha'
  ## ruby script/rails plugin install git://github.com/awebneck/object_daddy.git
  # gem 'edavis10-object_daddy', :require => 'object_daddy'
  # gem 'object_daddy', :git => 'https://github.com/awebneck/object_daddy.git'

  # cannot install on mingw due to fail installing linecache with native extensions
  platforms :mri_18 do gem 'ruby-debug' end
  platforms :mri_19 do
    # http://stackoverflow.com/questions/8251349/ruby-threadptr-data-type-error
    # gem 'ruby-debug19', :require => 'ruby-debug'
    gem 'linecache19', :git => 'git://github.com/mark-moseley/linecache'
    gem 'ruby-debug-base19x', '~> 0.11.30.pre4'
    gem 'ruby-debug19'
  end
end

group :ldap do
  gem "net-ldap"
end

group :openid do
  gem "ruby-openid", '~> 2.1.4', :require => 'openid'
end

group :rmagick do
  platforms :mri_18 do gem "rmagick", "~> 1.15.17" end

  ## You cannot specify the same gem twice with different version requirements.
  ## You specified: rmagick (~> 1.15.17) and rmagick (>= 0)
  ## https://github.com/carlhuda/bundler/issues/751
  # platforms :mri_19 do gem "rmagick" end

  platforms :jruby do gem "rmagick4j" end
end

# Use the commented pure ruby gems, if you have not the needed prerequisites on
# board to compile the native ones.  Note, that their use is discouraged, since
# their integration is propbably not that well tested and their are slower in
# orders of magnitude compared to their native counterparts. You have been
# warned.
#
platforms :mri, :mingw do
  group :mysql do
    gem "mysql"
    #   gem "ruby-mysql"
  end

  group :postgres do
    gem "pg", "~> 0.9.0"
    #   gem "postgres-pr"
  end
end

platforms :mri_18, :mingw_18 do
  group :sqlite do
    # gem "sqlite3-ruby", "< 1.3", :require => "sqlite3"
    gem "sqlite3"
  end
end

platforms :mri_19 do
  ## Add Windows support
  ## https://github.com/brianmario/mysql2/issues/8
  ## Getting mysql2 gem to work with Ruby on Rails 3.0 and Windows 7 64bit
  ## http://paul-wong-jr.blogspot.com/2011/06/getting-mysql2-gem-to-work-with-ruby-on.html
  group :mysql2 do
    gem "mysql2"
  end
end

platforms :mri_19, :mingw_19 do
  group :sqlite do
    gem "sqlite3"
  end
end

platforms :jruby do
  gem "jruby-openssl"

  group :mysql do
    gem "activerecord-jdbcmysql-adapter"
  end

  group :postgres do
    gem "activerecord-jdbcpostgresql-adapter"
  end

  group :sqlite do
    gem "activerecord-jdbcsqlite3-adapter"
  end
end

# Load a "local" Gemfile
gemfile_local = File.join(File.dirname(__FILE__), "Gemfile.local")
if File.readable?(gemfile_local)
  puts "Loading #{gemfile_local} ..." if $DEBUG
  instance_eval(File.read(gemfile_local))
end

# Load plugins Gemfiles
Dir.glob(File.join(File.dirname(__FILE__), %w(vendor plugins * Gemfile))) do |file|
  puts "Loading #{file} ..." if $DEBUG # `ruby -d` or `bundle -v`
  instance_eval File.read(file)
end
