# Mediawiki module for Puppet (forked by NexusIS)

## Nexus IS Fork

This fork brings the module up to date with latest dependency modules as well as adds a Type and Provider for MediaWiki Extensions.  

## Description

This module deploys and manages multiple mediawiki instances using a single mediawiki installation. This module has been designed and tested for CentOS 6, Red Hat Enterprise Linux 6, Debian Squeeze, Debian Wheezy, and Ubuntu Precise.

## Usage

First, install the mediawiki package which will be used by all wiki instances:

    class { 'mediawiki':
      server_name      => 'www.example.com',
      admin_email      => 'admin@puppetlabs.com',
      db_root_password => 'really_really_long_password',
      doc_root         => '/var/www/wikis'
      max_memory       => '1024'
    }
    
Next, create an individual wiki instance:

    mediawiki::instance { 'my_wiki1':
      db_password => 'super_long_password',
      db_name     => 'wiki1',
      db_user     => 'wiki1_user',
      port        => '80',
      ensure      => 'present'
    }

Using this module, one can create multiple independent wiki instances. To create another wiki instance, add the following puppet code:

    mediawiki::instance { 'my_wiki2':
      db_password => 'another_super_long_password',
      db_name     => 'another_wiki',
      db_user     => 'another_wiki_user'
      port        => '80',
      ensure      => 'present'
    }

## Preconditions

Since puppet cannot ensure that all parent directories exist you need to
manage these yourself. Therefore, make sure that all parent directories of
`doc_root` directory, an attribute of `mediawiki` class, exist.

## Notes On Testing

Puppet module tests reside in the `spec` directory. To run tests, execute 
`rake spec` anywhere in the module's directory. More information about module 
testing can be found here:

[The Next Generation of Puppet Module Testing](http://puppetlabs.com/blog/the-next-generation-of-puppet-module-testing)

## Reference

This module is based on puppet-mediawiki by carlasouza available at
https://github.com/carlasouza/puppet-mediawiki. Others who contributed to this
module include James Turnbull, Zach Leslie, Nan Liu, and Branan Purvine-Riley.
