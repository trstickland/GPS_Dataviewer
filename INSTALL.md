## Basics:

   perl -w Makefile.PL
   make && make test && make install
   
## Requirements

### MySQL/MariaDB

MySQL/MariaDB client and `mysql_config` are required.  On Debian or Ubuntu, try `apt-get install mariadb-server mariadb-client libmariadbclient-dev`.
Install `mysql_config` before trying to install the Perl package `DBD::mysql` (below).

### Perl modules:

   inc::Module::Install
   Catalyst::Authentication::Store::DBIx::Class
   Catalyst::Plugin::Authentication
   Catalyst::Plugin::Session::State::Cookie
   Catalyst::Plugin::Session::Store::FastMmap
   Catalyst::View::TT
   Log::Log4perl::Catalyst
   Module::Install::Catalyst
   DBD::mysql
   DBI
   File::ReadBackwards
   JSON
   Moose
   MooseX::NonMoose
   Spreadsheet::XLSX
   Term::Size::Any
   Text::CSV

## Configuration

These files must be provided with configuration for the local installation:

   ./gps_log.conf
   ./dbconnect.conf
