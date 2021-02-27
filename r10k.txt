Install r10k
/opt/puppetlabs/puppet/bin/gem install r10k

/opt/puppetlabs/puppet/bin/r10k help
Setup a Control Repo and Checkout
Create your ssh keypair and add public key to your github(repo) profile
Clone puppetlabs/control-repo from https://github.com/puppetlabs/control-repo
Create
mkdir /etc/puppetlabs/r10k/
Create /etc/puppetlabs/r10k/r10k.yaml with following contents. Replace your git repo

# The location to use for storing cached Git repos
:cachedir: '/var/cache/r10k'

# A list of git repositories to create
:sources:
  # This will clone the git repository and instantiate an environment per
  # branch in /etc/puppetlabs/code/environments
  :my-org:
    remote: 'YOUR_GIT_CONTROL_REPO_HERE'
    basedir: '/etc/puppetlabs/code/environments'
Update Puppetfile eg.
file: Puppetfile

forge "http://forge.puppetlabs.com"

# Forge modules:
mod "puppetlabs/ntp"
Create branches, add/update code, commit and push.
  git checkout -b <branch>
  
  [modify]
  
  git commit -a 
  git push origin <branch> 
  
Deploy with r10k
TO deploy all environments

/opt/puppetlabs/puppet/bin/r10k deploy environment -v -p
To deploy 1 environment

/opt/puppetlabs/puppet/bin/r10k deploy environment <branch> -v -p
