## 1.0.1 - 2021.03.30
### Added
* Added `make clean` to the Makefile
* Added **Makefile Project Commands** to `README.md`
* Added `make composer xxx` - runs the `composer` command passed in, e.g. `make composer install`
* Added a `Makefile` for command aliases
* Added `make mysql` and `make postgres` for switching between databases
* Added Redactor plugin installed by default
* Add `craftcms/redactor` to the base config
* Add `craftcms/commerce` to the base config
* Added `soap` PHP extension for Commerce
* Added CP Style Guide to the plugins
* Added new DB Seeds

### Changed
* Set `useEmailAsUsername` to `false` in `config/general.php` so we can use the generic login `admin`
* Remove `errorTemplatePrefix` and remove the `errors/` templates completely, because, who cares?
* Updated seed dbs & Project Config

## 1.0.0 - 2021.02.28
### Added
* Initial release

Major thanks to [nystudio107](https://nystudio107.com/) for all the great work on this boilerplate!