# perl6-ecosystem-release-testing

----

## Starting with a fresh Debian install:

Update Perl 5 and last stable release of Perl 6 versions below:

```bash
sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get -y install build-essential git curl libssl-dev tree
\curl -L https://install.perlbrew.pl | bash
git clone https://github.com/tadzik/rakudobrew ~/.rakudobrew
echo 'source ~/perl5/perlbrew/etc/bashrc' >> ~/.bashrc
echo 'export PATH=~/.rakudobrew/bin:~/.rakudobrew/moar-nom/install/share/perl6/site/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
perlbrew install --notest 5.24.1 -Duseshrplib -Dusemultiplicity
perlbrew switch 5.24.1
perlbrew install-cpanm
cpanm -vn Mojolicious IO::Socket::SSL
rakudobrew build moar 2017.02
rakudobrew build zef

mkdir eco
cd eco
perl -MMojo::UserAgent -MEncode -MMojo::File -C -wlE 'Mojo::File->new("modules.txt")->spurt( encode "UTF-8", join "\n", sort map { $_->{name} } @{Mojo::UserAgent->new->get("https://modules.perl6.org/.json")->res->json->{dists}} )'
```

