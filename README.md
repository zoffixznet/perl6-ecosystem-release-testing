# perl6-ecosystem-release-testing

----

## Starting with a fresh Debian install:

Update Perl 5 and last stable release of Perl 6 versions below:

```bash
sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get -y install build-essential git curl
\curl -L https://install.perlbrew.pl | bash
git clone https://github.com/tadzik/rakudobrew ~/.rakudobrew
echo 'source ~/perl5/perlbrew/etc/bashrc' >> ~/.bashrc
echo 'export PATH=~/.rakudobrew/bin:~/.rakudobrew/moar-nom/install/share/perl6/site/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
perlbrew install 5.24.1 -Duseshrplib -Dusemultiplicity
perlbrew switch 5.24.1
perlbrew install-cpanm
rakudobrew build moar 2017.02
rakudobrew build zef
```

