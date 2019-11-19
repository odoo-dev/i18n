# Test I18N server

This is a test server for the development of the downloadable languages pack.

**Use for demonstration purpose only, not for production !**

## Technical Changes

The `/i18n/` folder is not used anymore when loading translations.
The translations comes from a translation pack downloaded on a translation server (like this one).

Downloaded translations files are saved on the ir.module.module records (i.e. to refresh the packs once per day).

Add a new module `i18n_server` to allow people to easily create their own translation servers (and give an option for maintenace if/once we retire old versions).

See [odoo/odoo#30759](https://github.com/odoo/odoo/pull/30759) for the code.

### For Odoo SA Developers

- Keep only a `i18n/<module>.pot` file in developed module
*Translations are downloaded from "https://nightly.odoo.com" by default (or any `i18n.default.server` value)*

### For Integrator

- Deploy only a `i18n/<module>.pot` file in custom module
- Serve translation pack at `https://<mywebsite>/i18n/<version>/<lang>.tar.xz`
- Add `i18n_location: "https://<mywebsite>/"` inside the `<module>/__manifest__.py` file
*Translations for own modules are served from integrator server, can also set a `i18n.default.server` value to avoid odoo's nightly servers*

### For Independant Developer

- Publish all translations and `.pot` inside `i18n/` folder
- Add `"depends": ["i18n_server"]` and `i18n_locally": "True"` inside the `<module>/__manifest__.py` file
*The user's server becomes a translation server and will fetch translations locally for these modules*

## Test it

Test on the [runbot](http://runbot.odoo.com/runbot/quick_connect/54025).

This test server only contains the translations pack for the following version and languages:

- **14.0alpha1**
  - [ar](14.0alpha1/ar.tar.xz)
  - [de](14.0alpha1/de.tar.xz)
  - [fr](14.0alpha1/fr.tar.xz)
  - [nl](14.0alpha1/nl.tar.xz)
